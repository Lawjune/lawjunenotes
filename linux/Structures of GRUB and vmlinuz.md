# 1 Global Start Process

**Two phases:**
- Boot
- Startup

PowerUp->BIOS->GRUG1->GRUB1.5->GRUB2->Linux Kernel(Environment Hard Disk Boot, MBR Segment)

## 1.1 From BIOS to GRUB

*CPU only runs the programs stored in memory, but not in the hard disk or U driver.*

**Hardware Design:** 
- Power Up
	=> CS Register -> 0xF000
	=> IP Register -> 0xFFF0
		=> [CS:IP] -> 0xFFFF0 
		=> Physically *[0xFFFF0]* links to a small ROM.
		=> BOIS program is firmed in this ROM.

### 1.1.1 BIOS startup

- Init CPU

- Check and init memory

- Copy BIOS program to memory

- Jump to memory and run the BIOS program

- Enumerate local devices
	- Init
	- Check (whether damage)
	- By running the firmwares (such Display, Network, etc)

- Build **Interrup Table** and **Interrup Service Program** in memory
	- *The most important job of Linux*
	- **Interrup Table** 
		- Memory size: 1KB
		- Memory address: *[0x00000 ~ 0x003FF]*
		- 256 vectors
		- Each vector has 4 bytes
		- 2 bytes for the value of CS Register
		- 2 bytes for the value of IP Register
	- **BIOS DATA SEGMENT**
		- Memory size: 256KB
		- Memory address: *[0x00400 ~ 0x00fFF]*
	- **Interrup Service Program** 
		- Memory address: Start at *[0x0e05b]* inside **BIOS DATA SEGMENT**
		- Memory size: 8kb 
		- Corresponding to **Interrup Table**

- Search boot-up device for running the progran in external devices
	- Search order: CMOS settings
		- Heads: 8 bits
		- Cylinder: 10 bits
		- Sector: 6 bits
	- CD driver, Hard disk, network interface and USB driver, etc.
	- Usually boot up from hard disk
	- MBR(Master Boot Record) the first section (512 bytes per section) in hard disk 
	- *A master boot record (MBR) is a **special type of boot sector at** the very beginning of partitioned computer mass storage devices like fixed disks or removable drives intended for use with IBM PC-compatible systems and beyond.*

- Load **MBR** to memory at *[0x7c00]*
	- **BIOS** triggers interrup ***INT 19H*** while detected **Boot-Up-Flag**
	- **MBR** contains **GRUB** start program (**GRUB1 Phase**) and **Sector Table**
	- **BIOS** has handed over the control to **GRUB1**
	- **MBR Sector** has 512 bytes, ended with 66 bytes (64 bytes DPT + 2 bytes boot-up-flag) => **GRUB1** maximum size: 446 bytes

### 1.1.2 GRUB startup

*The whole GRUB program can not run in only 446 bytes memory!*

*Where is **GRUB1.5***
[sector0->MBR][sector1][sector2]......[sector63]: 62 free sectors => 31 KB


```sh
ls /boot/grub/i386-pc *.img
`=>
boot.img core.img
```

- **GRUB1**->***boot.img*** runs in **MBR**
- ***boot.img*** => Load **GRUB1.5**->***core.img***

The responsibilities of ***core.img***:
- Load file system driver
- Mount file system
- Bit loading 
- Run **GRUB2** program

***core.img*** contains:
- ***diskboot.img***: **GRUB1.5** boot-up program, in the first section of **MBR GAP**
	- If drive by CD => ***cdboot.img***
- ***lzma_decompress.img***: decompress the program
- ***kernel.img***: grub core codes which are compressed to store
- Other modules:
	- ***biosdisk.mod***: Disk driver
	- ***Part_msdos.mod***: MBR partitions support
	- ***Ext2.mod***: EXT file systems driver which are commpressed to store

***diskboot.img*** recursively loads the files in ***core.img***
	- The locations of ***core.img*** are stored in ***diskboot.img*** as *file block table*.
	- ***diskboot.img*** reads the ***core.img***  files via **BIOS INT** sector by sector.
1. Loads ***lzma_decompress.img***.
2. Loads ***kernel.img***.
	- `grub_main()` in ***kernel.img*** will call `grub_load_modules()` to load each ***mod***.
	- **GRUB** starts to support file system after loading all of ***mod***.


### 1.1.3 UEFI Boot Process (vs BIOS)

https://uefi.org/learning_center/presentationsandvideos

PowerUp->UEFI->GRUB->Linux

**UEFI Starts**
- Detect hardware and init
- Select Boot-up Mode: Legacy => CSM supports MBR
- Read, search and mount the hard disk sector table to ESP(EFI System Partition, vfat format)
	- GPT section GUID: C12A7328-F81F-11D2-BA4B-00A0C93EC93B
	- MBR section flag: 0xEF
- OS bootloader program are stored in /boot/efi/
	- *Manipulating files is much easier than sectors*
	- Such as Ubuntu, /boot/efi/ubuntu/grubx64.efi
```sh
sudo ls /boot/efi/EFI/ubuntu
`=>
BOOTX64.CSV  grub.cfg  grubx64.efi  mmx64.efi  shimx64.efi
```

*efi on the EFI System Partition (ESP) is the GRUB binary, and EFI/ubuntu/shimx64. efi is the binary for shim. The latter is a relatively simple program that provides a way to boot on a computer with Secure Boot active.*

*Typically, EFI/ubuntu/grubx64.efi on the EFI System Partition (ESP) is the GRUB binary, and EFI/ubuntu/shimx64.efi is the binary for shim. The latter is a relatively simple program that provides a way to boot on a computer with Secure Boot active. On such a computer, an unsigned version of GRUB won't launch, and signing GRUB with Microsoft's keys is impossible, so shim bridges the gap and adds its own security tools that parallel those of Secure Boot. In practice, shim registers itself with the firmware and then launches a program called grubx64.efi in the directory from which it was launched, so on a computer without Secure Boot (such as a Mac), launching shimx64.efi is just like launching grubx64.efi. On a computer with Secure Boot active, launching shimx64.efi should result in GRUB starting up, whereas launching grubx64.efi directly probably won't work.*

*Note that there's some ambiguity possible. In particular, if you want to use a boot manager or boot loader other than GRUB in a Secure Boot environment with shim, you must call that program grubx64.efi, even though it's not GRUB. Thus, if you were to install rEFInd on a Secure Boot-enabled computer, grubx64.efi could be the rEFInd binary. This binary would probably not reside in EFI/ubuntu, though; both it and a shim binary would probably go in EFI/refind. Also, as you've got a Mac (which doesn't support Secure Boot), there's no need to install rEFInd in this way; it makes much more sense to install rEFInd as EFI/refind/refind_x64.efi (its default location and name).*

### 1.1.3 GRUB2 Phase

- ***kernel.img*** calls `grub_load_normal_mode()` to load **normal module**
- **normal module** reads ***grub.cfg***

```sh
sudo cat /boot/efi/EFI/ubuntu/grub.cfg
`=>
search.fs_uuid 023f132d-385c-4c9c-adfa-865f25a6058f root hd0,gpt2 
set prefix=($root)'/boot/grub'
configfile $prefix/grub.cfg

```
=>
```sh
cat /boot/grub/grub.cfg
`=>
#
# DO NOT EDIT THIS FILE
#
# It is automatically generated by grub-mkconfig using templates
# from /etc/grub.d and settings from /etc/default/grub
#

### BEGIN /etc/grub.d/00_header ###
if [ -s $prefix/grubenv ]; then
  set have_grubenv=true
  load_env
fi
if [ "${initrdfail}" = 2 ]; then
   set initrdfail=
elif [ "${initrdfail}" = 1 ]; then
   set next_entry="${prev_entry}"
   set prev_entry=
   save_env prev_entry
   if [ "${next_entry}" ]; then
      set initrdfail=2
   fi
fi
if [ "${next_entry}" ] ; then
   set default="${next_entry}"
   set next_entry=
   save_env next_entry
   set boot_once=true
else
   set default="0"
fi

if [ x"${feature_menuentry_id}" = xy ]; then
  menuentry_id_option="--id"
else
  menuentry_id_option=""
fi

export menuentry_id_option

if [ "${prev_saved_entry}" ]; then
  set saved_entry="${prev_saved_entry}"
  save_env saved_entry
  set prev_saved_entry=
  save_env prev_saved_entry
  set boot_once=true
fi

function savedefault {
  if [ -z "${boot_once}" ]; then
    saved_entry="${chosen}"
    save_env saved_entry
  fi
}
function initrdfail {
    if [ -n "${have_grubenv}" ]; then if [ -n "${partuuid}" ]; then
      if [ -z "${initrdfail}" ]; then
        set initrdfail=1
        if [ -n "${boot_once}" ]; then
          set prev_entry="${default}"
          save_env prev_entry
        fi
      fi
      save_env initrdfail
    fi; fi
}
function recordfail {
  set recordfail=1
  if [ -n "${have_grubenv}" ]; then if [ -z "${boot_once}" ]; then save_env recordfail; fi; fi
}
function load_video {
  if [ x$feature_all_video_module = xy ]; then
    insmod all_video
  else
    insmod efi_gop
    insmod efi_uga
    insmod ieee1275_fb
    insmod vbe
    insmod vga
    insmod video_bochs
    insmod video_cirrus
  fi
}

if [ x$feature_default_font_path = xy ] ; then
   font=unicode
else
insmod part_gpt
insmod ext2
set root='hd0,gpt2'
if [ x$feature_platform_search_hint = xy ]; then
  search --no-floppy --fs-uuid --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2  023f132d-385c-4c9c-adfa-865f25a6058f
else
  search --no-floppy --fs-uuid --set=root 023f132d-385c-4c9c-adfa-865f25a6058f
fi
    font="/usr/share/grub/unicode.pf2"
fi

if loadfont $font ; then
  set gfxmode=auto
  load_video
  insmod gfxterm
  set locale_dir=$prefix/locale
  set lang=en_US
  insmod gettext
fi
terminal_output gfxterm
if [ "${recordfail}" = 1 ] ; then
  set timeout=30
else
  if [ x$feature_timeout_style = xy ] ; then
    set timeout_style=hidden
    set timeout=0
  # Fallback hidden-timeout code in case the timeout_style feature is
  # unavailable.
  elif sleep --interruptible 0 ; then
    set timeout=0
  fi
fi
### END /etc/grub.d/00_header ###

### BEGIN /etc/grub.d/05_debian_theme ###
set menu_color_normal=white/black
set menu_color_highlight=black/light-gray
### END /etc/grub.d/05_debian_theme ###

### BEGIN /etc/grub.d/10_linux ###
function gfxmode {
	set gfxpayload="${1}"
	if [ "${1}" = "keep" ]; then
		set vt_handoff=vt.handoff=7
	else
		set vt_handoff=
	fi
}
if [ "${recordfail}" != 1 ]; then
  if [ -e ${prefix}/gfxblacklist.txt ]; then
    if hwmatch ${prefix}/gfxblacklist.txt 3; then
      if [ ${match} = 0 ]; then
        set linux_gfx_mode=keep
      else
        set linux_gfx_mode=text
      fi
    else
      set linux_gfx_mode=text
    fi
  else
    set linux_gfx_mode=keep
  fi
else
  set linux_gfx_mode=text
fi
export linux_gfx_mode
menuentry 'Ubuntu' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-simple-023f132d-385c-4c9c-adfa-865f25a6058f' {
	recordfail
	load_video
	gfxmode $linux_gfx_mode
	insmod gzio
	if [ x$grub_platform = xxen ]; then insmod xzio; insmod lzopio; fi
	insmod part_gpt
	insmod ext2
	set root='hd0,gpt2'
	if [ x$feature_platform_search_hint = xy ]; then
	  search --no-floppy --fs-uuid --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2  023f132d-385c-4c9c-adfa-865f25a6058f
	else
	  search --no-floppy --fs-uuid --set=root 023f132d-385c-4c9c-adfa-865f25a6058f
	fi
	linux	/boot/vmlinuz-5.11.0-43-generic root=UUID=023f132d-385c-4c9c-adfa-865f25a6058f ro  quiet splash $vt_handoff
	initrd	/boot/initrd.img-5.11.0-43-generic
}
submenu 'Advanced options for Ubuntu' $menuentry_id_option 'gnulinux-advanced-023f132d-385c-4c9c-adfa-865f25a6058f' {
	menuentry 'Ubuntu, with Linux 5.11.0-43-generic' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-5.11.0-43-generic-advanced-023f132d-385c-4c9c-adfa-865f25a6058f' {
		recordfail
		load_video
		gfxmode $linux_gfx_mode
		insmod gzio
		if [ x$grub_platform = xxen ]; then insmod xzio; insmod lzopio; fi
		insmod part_gpt
		insmod ext2
		set root='hd0,gpt2'
		if [ x$feature_platform_search_hint = xy ]; then
		  search --no-floppy --fs-uuid --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2  023f132d-385c-4c9c-adfa-865f25a6058f
		else
		  search --no-floppy --fs-uuid --set=root 023f132d-385c-4c9c-adfa-865f25a6058f
		fi
		echo	'Loading Linux 5.11.0-43-generic ...'
		linux	/boot/vmlinuz-5.11.0-43-generic root=UUID=023f132d-385c-4c9c-adfa-865f25a6058f ro  quiet splash $vt_handoff
		echo	'Loading initial ramdisk ...'
		initrd	/boot/initrd.img-5.11.0-43-generic
	}
	menuentry 'Ubuntu, with Linux 5.11.0-43-generic (recovery mode)' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-5.11.0-43-generic-recovery-023f132d-385c-4c9c-adfa-865f25a6058f' {
		recordfail
		load_video
		insmod gzio
		if [ x$grub_platform = xxen ]; then insmod xzio; insmod lzopio; fi
		insmod part_gpt
		insmod ext2
		set root='hd0,gpt2'
		if [ x$feature_platform_search_hint = xy ]; then
		  search --no-floppy --fs-uuid --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2  023f132d-385c-4c9c-adfa-865f25a6058f
		else
		  search --no-floppy --fs-uuid --set=root 023f132d-385c-4c9c-adfa-865f25a6058f
		fi
		echo	'Loading Linux 5.11.0-43-generic ...'
		linux	/boot/vmlinuz-5.11.0-43-generic root=UUID=023f132d-385c-4c9c-adfa-865f25a6058f ro recovery nomodeset dis_ucode_ldr 
		echo	'Loading initial ramdisk ...'
		initrd	/boot/initrd.img-5.11.0-43-generic
	}
	menuentry 'Ubuntu, with Linux 5.11.0-41-generic' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-5.11.0-41-generic-advanced-023f132d-385c-4c9c-adfa-865f25a6058f' {
		recordfail
		load_video
		gfxmode $linux_gfx_mode
		insmod gzio
		if [ x$grub_platform = xxen ]; then insmod xzio; insmod lzopio; fi
		insmod part_gpt
		insmod ext2
		set root='hd0,gpt2'
		if [ x$feature_platform_search_hint = xy ]; then
		  search --no-floppy --fs-uuid --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2  023f132d-385c-4c9c-adfa-865f25a6058f
		else
		  search --no-floppy --fs-uuid --set=root 023f132d-385c-4c9c-adfa-865f25a6058f
		fi
		echo	'Loading Linux 5.11.0-41-generic ...'
		linux	/boot/vmlinuz-5.11.0-41-generic root=UUID=023f132d-385c-4c9c-adfa-865f25a6058f ro  quiet splash $vt_handoff
		echo	'Loading initial ramdisk ...'
		initrd	/boot/initrd.img-5.11.0-41-generic
	}
	menuentry 'Ubuntu, with Linux 5.11.0-41-generic (recovery mode)' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-5.11.0-41-generic-recovery-023f132d-385c-4c9c-adfa-865f25a6058f' {
		recordfail
		load_video
		insmod gzio
		if [ x$grub_platform = xxen ]; then insmod xzio; insmod lzopio; fi
		insmod part_gpt
		insmod ext2
		set root='hd0,gpt2'
		if [ x$feature_platform_search_hint = xy ]; then
		  search --no-floppy --fs-uuid --set=root --hint-bios=hd0,gpt2 --hint-efi=hd0,gpt2 --hint-baremetal=ahci0,gpt2  023f132d-385c-4c9c-adfa-865f25a6058f
		else
		  search --no-floppy --fs-uuid --set=root 023f132d-385c-4c9c-adfa-865f25a6058f
		fi
		echo	'Loading Linux 5.11.0-41-generic ...'
		linux	/boot/vmlinuz-5.11.0-41-generic root=UUID=023f132d-385c-4c9c-adfa-865f25a6058f ro recovery nomodeset dis_ucode_ldr 
		echo	'Loading initial ramdisk ...'
		initrd	/boot/initrd.img-5.11.0-41-generic
	}
}

### END /etc/grub.d/10_linux ###

### BEGIN /etc/grub.d/10_linux_zfs ###
### END /etc/grub.d/10_linux_zfs ###

### BEGIN /etc/grub.d/20_linux_xen ###

### END /etc/grub.d/20_linux_xen ###

### BEGIN /etc/grub.d/20_memtest86+ ###
### END /etc/grub.d/20_memtest86+ ###

### BEGIN /etc/grub.d/30_os-prober ###
### END /etc/grub.d/30_os-prober ###

### BEGIN /etc/grub.d/30_uefi-firmware ###
menuentry 'UEFI Firmware Settings' $menuentry_id_option 'uefi-firmware' {
	fwsetup
}
### END /etc/grub.d/30_uefi-firmware ###

### BEGIN /etc/grub.d/40_custom ###
# This file provides an easy way to add custom menu entries.  Simply type the
# menu entries you want to add after this comment.  Be careful not to change
# the 'exec tail' line above.
### END /etc/grub.d/40_custom ###

### BEGIN /etc/grub.d/41_custom ###
if [ -f  ${config_directory}/custom.cfg ]; then
  source ${config_directory}/custom.cfg
elif [ -z "${config_directory}" -a -f  $prefix/custom.cfg ]; then
  source $prefix/custom.cfg;
fi
### END /etc/grub.d/41_custom ###
```

=> loacate and load Linux.

### 1.1.4 vmlinuz 

***vmlinuz is the name of the Linux kernel executable.***

```sh
ls /boot/
`=>
config-5.11.0-41-generic      memtest86+.elf
config-5.11.0-43-generic      memtest86+_multiboot.bin
efi                           System.map-5.11.0-41-generic
grub                          System.map-5.11.0-43-generic
initrd.img                    vmlinuz
initrd.img-5.11.0-41-generic  vmlinuz-5.11.0-41-generic
initrd.img-5.11.0-43-generic  vmlinuz-5.11.0-43-generic
initrd.img.old                vmlinuz.old
memtest86+.bin

```

*Complied bzImage and copied it as vmlinuz*
```sh
#linux/arch/x86/boot/Makefile
install:    sh $(srctree)/$(src)/install.sh $(KERNELRELEASE) $(obj)/bzImage \        System.map "$(INSTALL_PATH)"
```

```sh

#linux/arch/x86/boot/Makefile
$(obj)/bzImage: $(obj)/setup.bin $(obj)/vmlinux.bin $(obj)/tools/build FORCE    $(call if_changed,image)    @$(kecho) 'Kernel: $@ is ready' ' (#'`cat .version`')'
```

***bzImage*** depends on:
	- ***setup.bin***
	- ***vmlinux.bin***
	- ***/tools/build***


***//tools/build/***/ is an application proram running in Host OS to combine ***setup.bin*** and ***vmlinux.bin*** into a new file ***bzImage***.


How to build ***setup.bin***?
```sh

#这些目标文件正是由/arch/x86/boot/目录下对应的程序源代码文件编译产生
setup-y     += a20.o bioscall.o cmdline.o copy.o cpu.o cpuflags.o cpucheck.o
setup-y     += early_serial_console.o edd.o header.o main.o memory.o
setup-y     += pm.o pmjump.o printf.o regs.o string.o tty.o video.o
setup-y     += video-mode.o version.o

#……
SETUP_OBJS = $(addprefix $(obj)/,$(setup-y))
#……
LDFLAGS_setup.elf   := -m elf_i386 -T$(obj)/setup.elf: $(src)/setup.ld $(SETUP_OBJS) FORCE    $(call if_changed,ld)
#……
OBJCOPYFLAGS_setup.bin  := -O binary$(obj)/setup.bin: $(obj)/setup.elf FORCE    $(call if_changed,objcopy)
```

How to build ***vmlinux.bin***?
```sh

#linux/arch/x86/boot/Makefile
OBJCOPYFLAGS_vmlinux.bin := -O binary -R .note -R .comment -S$(obj)/vmlinux.bin: $(obj)/compressed/vmlinux FORCE    $(call if_changed,objcopy)
```

***vmlinux.bin*** depends on the vmlinux target on $(obj)/compressed/

```sh

#linux/arch/x86/boot/compressed/Makefile
#……
#这些目标文件正是由/arch/x86/boot/compressed/目录下对应的程序源代码文件编译产生$(BITS)取值32或者64
vmlinux-objs-y := $(obj)/vmlinux.lds $(obj)/kernel_info.o $(obj)/head_$(BITS).o \    $(obj)/misc.o $(obj)/string.o $(obj)/cmdline.o $(obj)/error.o \    $(obj)/piggy.o $(obj)/cpuflags.o
vmlinux-objs-$(CONFIG_EARLY_PRINTK) += $(obj)/early_serial_console.o
vmlinux-objs-$(CONFIG_RANDOMIZE_BASE) += $(obj)/kaslr.o
ifdef CONFIG_X86_64    
vmlinux-objs-y += $(obj)/ident_map_64.o    
vmlinux-objs-y += $(obj)/idt_64.o $(obj)/idt_handlers_64.o    vmlinux-objs-y += $(obj)/mem_encrypt.o    
vmlinux-objs-y += $(obj)/pgtable_64.o    
vmlinux-objs-$(CONFIG_AMD_MEM_ENCRYPT) += $(obj)/sev-es.o
endif
#……
$(obj)/vmlinux: $(vmlinux-objs-y) $(efi-obj-y) FORCE  
$(call if_changed,ld)
```
We can find all of above the source file in Linux Kernel source code except ***piggy.S***.

How to build ***piggy.S*** showed in above sricpts.
```sh

#linux/arch/x86/boot/compressed/Makefile
#……
quiet_cmd_mkpiggy = MKPIGGY $@      
cmd_mkpiggy = $(obj)/mkpiggy $< > $@

targets += piggy.S
$(obj)/piggy.S: $(obj)/vmlinux.bin.$(suffix-y) $(obj)/mkpiggy FORCE    $(call if_changed,mkpiggy)
```

Again how to build ***vmlinux.bin***?
```sh

#linux/arch/x86/boot/compressed/Makefile
#……
OBJCOPYFLAGS_vmlinux.bin :=  -R .comment -S
$(obj)/vmlinux.bin: vmlinux FORCE 
$(call if_changed,objcopy)
```

Actually ***vmlinux*** file is compiled by the whole Linux Kernel srouce code.
- **vm** = *Virtual Memory*
- **linu** = *Linux*
- **z** = *Compress*

***piggy.S*** running in the Host OS to compress ***vmlinux.bin.gz***  using assembly instructor `incbin`.

*mkpiggy.c*
```c

int main(int argc, char *argv[]){ 
    uint32_t olen;    
    long ilen;    
    FILE *f = NULL;    
    int retval = 1;
    f = fopen(argv[1], "r");    
    if (!f) {        
        perror(argv[1]);        
        goto bail;    
    }
    //……为节约篇幅略去部分代码
    printf(".section \".rodata..compressed\",\"a\",@progbits\n");
    printf(".globl z_input_len\n");    
    printf("z_input_len = %lu\n", ilen);    
    printf(".globl z_output_len\n");    
    printf("z_output_len = %lu\n", (unsigned long)olen);
    printf(".globl input_data, input_data_end\n");
    printf("input_data:\n");    
    printf(".incbin \"%s\"\n", argv[1]);    
    printf("input_data_end:\n");
    printf(".section \".rodata\",\"a\",@progbits\n");
    printf(".globl input_len\n");    
    printf("input_len:\n\t.long %lu\n", ilen);    
    printf(".globl output_len\n");    
    printf("output_len:\n\t.long %lu\n", (unsigned long)olen);
    retval = 0;
bail:    
    if (f)        
        fclose(f);    
    return retval;
}
//由上mkpiggy程序“写的”一个汇编程序piggy.S。
.section ".rodata..compressed","a",@progbits 
.globl z_input_len
 z_input_len = 1921557 
.globl z_output_len 
z_output_len = 3421472 
.globl input_data,input_data_end
.incbin "arch/x86/boot/compressed/vmlinux.bin.gz" 
input_data_end:
.section ".rodata","a",@progbits
.globl input_len
input_len:4421472
.globl output_len
output_len:4424772
```

**The reason of using mkpiggy.c to build piggy.S, open-srouce developer can set different parameters in `.incbin "arch/x86/boot/compressed/vmlinux.bin.gz"` for differentiation.**