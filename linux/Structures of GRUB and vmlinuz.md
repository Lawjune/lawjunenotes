# 1 Global Boot and Start Process

**Two phases:**
- Boot
- Start

PowerUp->BIOS->GRUG1->GRUB1.5->GRUB2->Linux Kernel(Environment Hard Disk Boot, MBR Segment)

## 1.1 Boot: From BIOS to GRUB

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

### 1.1.4 GRUB2 Phase

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

### 1.1.5 vmlinuz 

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


## 1.2 Start

### 1.2.1 From `_start` of setup.bin

**Review how to build *vmlinuz file* -> *bzImage format***
1. Build *bzImage format*
1.1 head_64.S + other source files => compiled => vmlinux(A)
1.2 objcopy tool to copy (meanwhile removing the ".comment", sign table and reindirect table) => vmlinux.bin(A)
1.3 gzib to compress => vmlinux.bin.gz
1.4 piggy to pack, combine decompressed data => piggy.o => link other .o files => vmlinux(B)
1.5 objcopy tool to copy (meanwhile removing the ".comment", sign table and reindirect table) => vmlinux.bin(B)
1.6 head.S + main.c + other files => setup.bin
1.7 setup.bin + vmlinux.bin(B) => bzImage converter => bzImage

2. GRUB to load bzImage file
2.1 To load bzImage[setup.bin] to the memory at the address of [0x90000]
2.2 To load vmlinuz[vmlinux.bin] to the memory at the address of 1MB


```sh (asm)

#linux/arch/x86/boot/head.S
  .code16
  .section ".bstext", "ax"
  .global bootsect_start
bootsect_start:
  ljmp  $BOOTSEG, $start2
start2:
#……
#这里的512字段bootsector对于硬盘启动是用不到的
#……
  .globl  _start
_start:
    .byte  0xeb    # short (2-byte) jump
    .byte  start_of_setup-1f #这指令是用.byte定义出来的，跳转start_of_setup-1f
#……
#这里是一个庞大的数据结构，没展示出来，与linux/arch/x86/include/uapi/asm/bootparam.h文件中的struct setup_header一一对应。这个数据结构定义了启动时所需的默认参数
#……
start_of_setup:
  movw  %ds, %ax
  movw  %ax, %es   #ds = es
  cld               #主要指定si、di寄存器的自增方向，即si++ di++

  movw  %ss, %dx
  cmpw  %ax, %dx  # ds 是否等于 ss
  movw  %sp, %dx     
  je  2f    
  # 如果ss为空则建立新栈
  movw  $_end, %dx
  testb  $CAN_USE_HEAP, loadflags
  jz  1f
  movw  heap_end_ptr, %dx
1:  addw  $STACK_SIZE, %dx
  jnc  2f
  xorw  %dx, %dx  
2:
  andw  $~3, %dx
  jnz  3f
  movw  $0xfffc, %dx  
3:  movw  %ax, %ss
  movzwl  %dx, %esp  
  sti      # 栈已经初始化好，开中断
  pushw  %ds
  pushw  $6f
  lretw      # cs=ds ip=6：跳转到标号6处
6:
  cmpl  $0x5a5aaa55, setup_sig #检查setup标记
  jne  setup_bad
  movw  $__bss_start, %di
  movw  $_end+3, %cx
  xorl  %eax, %eax
  subw  %di, %cx
  shrw  $2, %cx
  rep; stosl          #清空setup程序的bss段
  calll  main  #调用C语言main函数 
```

### 1.2.2 setup_header struct

```c

struct setup_header {    
__u8    setup_sects;        //setup大小
__u16   root_flags;         //根标志   
__u32   syssize;            //系统文件大小
__u16   ram_size;           //内存大小
__u16   vid_mode;    
__u16   root_dev;           //根设备号
__u16   boot_flag;          //引导标志
//……
__u32   realmode_swtch;     //切换回实模式的函数地址     
__u16   start_sys_seg;    
__u16   kernel_version;     //内核版本    
__u8    type_of_loader;     //引导器类型 我们这里是GRUB
__u8    loadflags;          //加载内核的标志 
__u16   setup_move_size;    //移动setup的大小
__u32   code32_start;       //将要跳转到32位模式下的地址 
__u32   ramdisk_image;      //初始化内存盘映像地址，里面有内核驱动模块 
__u32   ramdisk_size;       //初始化内存盘映像大小
//……
} __attribute__((packed));
```
***Continue***

3. **GRUB** continues to execute ***setup.bin*** codes with the entry at header.S(arch/x86/boot/header.S)
- **GRUB** will fil a **setup_header struct** in Linux kernel by writing the start-needed information into the correspondng positions of kernel.
- ***Header.S*** starts with **start_of_setup** which is exactly a **setup_header struct**.
- ***bootparam.h*** will copy the structure data from ***Header.S*** into itself definition.

4. **GRUB** will jump to [0x90200] and start to run --- skipped the 512 bytes bootsector, which is exactly the positon of ***head.S***.

5. At end of ***head.S***(*linux/arch/x86/boot/head.S*), it calls the main function.

### 1.2.3 16 bits main function

*linux/arch/x86/boot/main.c*
```c

//定义boot_params变量
struct boot_params boot_params __attribute__((aligned(16)));
char *HEAP = _end;
char *heap_end = _end; 
//……
void main(void){
    //把先前setup_header结构复制到boot_params结构中的hdr变量中，在linux/arch/x86/include/uapi/asm/bootparam.h文件中你会发现boot_params结构中的hdr的类型正是setup_header结构  
    copy_boot_params();
    //初始化早期引导所用的console    
    console_init();    
    //初始化堆 
    init_heap();
    //检查CPU是否支持运行Linux    
    if (validate_cpu()) {        
        puts("Unable to boot - please use a kernel appropriate "             "for your CPU.\n");        
        die();    
    }
    //告诉BIOS我们打算在什么CPU模式下运行它
    set_bios_mode();
    //查看物理内存空间布局    
    detect_memory();
    //初始化键盘
    keyboard_init();
    //查询Intel的(IST)信息。    
    query_ist();
    /*查询APM BIOS电源管理信息。*/
    #if defined(CONFIG_APM) || defined(CONFIG_APM_MODULE)   
    query_apm_bios();
    #endif
    //查询EDD BIOS扩展数据区域的信息
    #if defined(CONFIG_EDD) || defined(CONFIG_EDD_MODULE) 
    query_edd();
    #endif
    //设置显卡的图形模式    
    set_video();
    //进入CPU保护模式，不会返回了       
    go_to_protected_mode();
}
```

*linux/arch/x86/boot/pm.c*
```c

//linux/arch/x86/boot/pm.c
void go_to_protected_mode(void){    
    //安装切换实模式的函数
    realmode_switch_hook();
    //开启a20地址线，是为了能访问1MB以上的内存空间
    if (enable_a20()) {        
        puts("A20 gate not responding, unable to boot...\n");
        die();    
    }
    //重置协处理器，早期x86上的浮点运算单元是以协处理器的方式存在的    
    reset_coprocessor();
    //屏蔽8259所示的中断源   
    mask_all_interrupts();
    //安装中断描述符表和全局描述符表，    
    setup_idt();    
    setup_gdt();
    //保护模式下长跳转到boot_params.hdr.code32_start
    protected_mode_jump(boot_params.hdr.code32_start,                (u32)&boot_params + (ds() << 4));
}
```

**protected_mode_jump**, jump to the address of **boot_params.hdr.code32_start**(long protected mode, jump to [0x100000])
```c
code32_start:
long  0x100000
```

**Note: GRUB has put vmlinuz[vmlinux.bin] at the 1MB started if memory, this jump will effectively enter vmlinux.bin.**

### 1.2.4 startup_32 function

*arch/x86/boot/compressed/head64.S*

- Load sector descriptor
- Calculate the ***vmlinux.bin*** complied address and load the offset of this address
- Reset kernel stack
- Check whether CPU support long-mode
- Calculate the offset of ***vmlinux.bin*** loading address to locate the ***vmlinux.bin.gz*** decompressed address

```sh (asm)
  .code32
SYM_FUNC_START(startup_32)
  cld
  cli
  leal  (BP_scratch+4)(%esi), %esp
  call  1f
1:  popl  %ebp
  subl  $ rva(1b), %ebp
    #重新加载全局段描述符表
  leal  rva(gdt)(%ebp), %eax
  movl  %eax, 2(%eax)
  lgdt  (%eax)
    #……篇幅所限未全部展示代码
    #重新设置栈
  leal  rva(boot_stack_end)(%ebp), %esp
    #检测CPU是否支持长模式
  call  verify_cpu
  testl  %eax, %eax
  jnz  .Lno_longmode
    #……计算偏移的代码略过
    #开启PAE
    movl  %cr4, %eax
  orl  $X86_CR4_PAE, %eax
  movl  %eax, %cr4
    #……建立MMU页表的代码略过
    #开启长模式
    movl  $MSR_EFER, %ecx
  rdmsr
  btsl  $_EFER_LME, %eax
    #获取startup_64的地址
    leal  rva(startup_64)(%ebp), %eax
    #……篇幅所限未全部展示代码
    #内核代码段描述符索和startup_64的地址引压入栈
    pushl  $__KERNEL_CS
  pushl  %eax
    #开启分页和保护模式
  movl  $(X86_CR0_PG | X86_CR0_PE), %eax 
  movl  %eax, %cr0
    #弹出刚刚栈中压入的内核代码段描述符和startup_64的地址到CS和RIP中，实现跳转，真正进入长模式。
  lret
SYM_FUNC_END(startup_32）
```

### 1.2.5 startup_64 function

*arch/x86/boot/compressed/head64.S*
- Init registers
- Init stack
- Set MMU level
- Compress kernel to the end of **Buffer**
- Call ***.Lrelocated***

```sh (asm)

  .code64
  .org 0x200
SYM_CODE_START(startup_64)
  cld
  cli
  #初始化长模式下数据段寄存器
  xorl  %eax, %eax
  movl  %eax, %ds
  movl  %eax, %es
  movl  %eax, %ss
  movl  %eax, %fs
  movl  %eax, %gs
    #……重新确定内核映像加载地址的代码略过
    #重新初始化64位长模式下的栈
    leaq  rva(boot_stack_end)(%rbx), %rsp
    #……建立最新5级MMU页表的代码略过
    #确定最终解压缩地址，然后拷贝压缩vmlinux.bin到该地址
    pushq  %rsi
  leaq  (_bss-8)(%rip), %rsi
  leaq  rva(_bss-8)(%rbx), %rdi
  movl  $(_bss - startup_32), %ecx
  shrl  $3, %ecx
  std
  rep  movsq
  cld
  popq  %rsi
    #跳转到重定位的Lrelocated处
    leaq  rva(.Lrelocated)(%rbx), %rax
  jmp  *%rax
SYM_CODE_END(startup_64)

  .text
SYM_FUNC_START_LOCAL_NOALIGN(.Lrelocated)
    #清理程序文件中需要的BSS段
  xorl  %eax, %eax
  leaq    _bss(%rip), %rdi
  leaq    _ebss(%rip), %rcx
  subq  %rdi, %rcx
  shrq  $3, %rcx
  rep  stosq
    #……省略无关代码
  pushq  %rsi      
  movq  %rsi, %rdi    
  leaq  boot_heap(%rip), %rsi
    #准备参数：被解压数据的开始地址   
  leaq  input_data(%rip), %rdx
    #准备参数：被解压数据的长度   
  movl  input_len(%rip), %ecx
    #准备参数：解压数据后的开始地址     
  movq  %rbp, %r8
    #准备参数：解压数据后的长度
  movl  output_len(%rip), %r9d
    #调用解压函数解压vmlinux.bin.gz，返回入口地址
    call  extract_kernel
  popq  %rsi
    #跳转到内核入口地址 
  jmp  *%rax
SYM_FUNC_END(.Lrelocated)
```

***.Lrelocated***
- Apply memory
- Start address of decompressed source data
- Length of decompressed source data
- Start address of decompressed ouput data
- Length of decompressed output data
- Call **extract_kernel** to decompress kernel

### 1.2.6 extract_kernel function

*arch/x86/boot/compressed/misc.c*
```c

asmlinkage __visible void *extract_kernel(
                                void *rmode, memptr heap,
                                unsigned char *input_data,
                                unsigned long input_len,
                                unsigned char *output,
                                unsigned long output_len
                                ){    
    const unsigned long kernel_total_size = VO__end - VO__text;
    unsigned long virt_addr = LOAD_PHYSICAL_ADDR;    
    unsigned long needed_size;
    //省略了无关性代码
    debug_putstr("\nDecompressing Linux... ");    
    //调用具体的解压缩算法解压
    __decompress(input_data, input_len, NULL, NULL, output, output_len,            NULL, error);
    //解压出的vmlinux是elf格式，所以要解析出里面的指令数据段和常规数据段
    //返回vmlinux的入口点即Linux内核程序的开始地址  
    parse_elf(output); 
    handle_relocations(output, output_len, virt_addr);    debug_putstr("done.\nBooting the kernel.\n");
    return output;
}
```

- Save **boot_params**
- Decompress kernel
- Parse **ELF**
- **handle_relocations** = put the instruction section, data section, BSS and data in elf of **vmlinux** into the particular memory
- Reurn the kernel address and save it to ***%rax*** 
- Back to ***.Lrelocated*** and continue to execute
Note: the last instruction: `jmp *rax` => `rax` is the return `output` of **extract_kernel**, which is the entry of Linux kernel

### 1.2.7 startup_64 of Linux Kernel

*Note: This **startup_64** is NOT the one in previous.*

*linux/arch/x86/kernel/head_64.S*
```sh (asm)

#linux/arch/x86/kernel/head_64.S  
    .code64
SYM_CODE_START_NOALIGN(startup_64)
  #切换栈
    leaq  (__end_init_task - SIZEOF_PTREGS)(%rip), %rsp
  #跳转到.Lon_kernel_cs:
    pushq  $__KERNEL_CS
  leaq  .Lon_kernel_cs(%rip), %rax
  pushq  %rax
  lretq
.Lon_kernel_cs:
    #对于第一个CPU，则会跳转secondary_startup_64函数中1标号处
  jmp 1f
SYM_CODE_END(startup_64)
```

=> **secondary_startup_64**
```sh (asm)

SYM_CODE_START(secondary_startup_64)
    #省略了大量无关性代码
1:
  movl  $(X86_CR4_PAE | X86_CR4_PGE), %ecx
#ifdef CONFIG_X86_5LEVEL
  testl  $1, __pgtable_l5_enabled(%rip)
  jz  1f
  orl  $X86_CR4_LA57, %ecx
1:
#endif
    #省略了大量无关性代码
.Ljump_to_C_code:
  pushq  $.Lafter_lret  
  xorl  %ebp, %ebp
    #获取x86_64_start_kernel函数地址赋给rax  
  movq  initial_code(%rip), %rax
  pushq  $__KERNEL_CS  
    #将x86_64_start_kernel函数地址压入栈中
  pushq  %rax
    #弹出__KERNEL_CS  和x86_64_start_kernel函数地址到CS：RIP完成调用  
    lretq
.Lafter_lret:
SYM_CODE_END(secondary_startup_64)
#保存了x86_64_start_kernel函数地址
SYM_DATA(initial_code,  .quad x86_64_start_kernel)
```

### 1.2.8 The first C function of Linux Kernel

*linux/arch/x86/kernel/head64.c*

```c

asmlinkage __visible void __init x86_64_start_kernel(char * real_mode_data){    
    //重新设置早期页表
    reset_early_page_tables();
    //清理BSS段
    clear_bss();
    //清理之前的顶层页目录
    clear_page(init_top_pgt);
    //复制引导信息
    copy_bootdata(__va(real_mode_data));
    //加载BSP CPU的微码
    load_ucode_bsp();
    //让顶层页目录指向重新设置早期页表
    init_top_pgt[511] = early_top_pgt[511];
    x86_64_start_reservations(real_mode_data);
}
void __init x86_64_start_reservations(char *real_mode_data){  
   //略过无关的代码
    start_kernel();
}
```

### 1.2.9 start_kernel

*/linux/init/main.c*
```c

void start_kernel(void){    
    char *command_line;    
    char *after_dashes;
    //CPU组早期初始化
    cgroup_init_early();
    //关中断
    local_irq_disable();
    //ARCH层初始化
    setup_arch(&command_line);
    //日志初始化      
    setup_log_buf(0);    
    sort_main_extable();
    //陷阱门初始化    
    trap_init();
    //内存初始化    
    mm_init();
    ftrace_init();
    //调度器初始化
    sched_init();
    //工作队列初始化
    workqueue_init_early();
    //RCU锁初始化
    rcu_init();
    //IRQ 中断请求初始化
    early_irq_init();    
    init_IRQ();    
    tick_init();    
    rcu_init_nohz();
    //定时器初始化 
    init_timers();    
    hrtimers_init();
    //软中断初始化    
    softirq_init();    
    timekeeping_init();
    mem_encrypt_init();
    //每个cpu页面集初始化
    setup_per_cpu_pageset();    
    //fork初始化建立进程的 
    fork_init();    
    proc_caches_init();    
    uts_ns_init();
    //内核缓冲区初始化    
    buffer_init();    
    key_init();    
    //安全相关的初始化
    security_init();  
    //VFS数据结构内存池初始化  
    vfs_caches_init();
    //页缓存初始化    
    pagecache_init();
    //进程信号初始化    
    signals_init();    
    //运行第一个进程 
    arch_call_rest_init();
}
```

```c
void __init __weak arch_call_rest_init(void){    
    rest_init();
}
```

**rest_init()** to create two Linux Kernel processes
```c
noinline void __ref rest_init(void){    struct task_struct *tsk;
    int pid;
    //建立kernel_init线程
    pid = kernel_thread(kernel_init, NULL, CLONE_FS);   
    //建立khreadd线程 
    pid = kernel_thread(kthreadd, NULL, CLONE_FS | CLONE_FILES);
}
```

### 1.2.10 The First Linux User Process

Created in **kernel_init** process.
```c
static int __ref kernel_init(void *unused){   
     int ret;
     if (ramdisk_execute_command) {       
         ret = run_init_process(ramdisk_execute_command);        
         if (!ret)            
             return 0;        
         pr_err("Failed to execute %s (error %d)\n",ramdisk_execute_command, ret);    
     }
     if (execute_command) {        
         ret = run_init_process(execute_command);        
         if (!ret)            
         return 0;        
         panic("Requested init %s failed (error %d).",              execute_command, ret);    
     }
    if (!try_to_run_init_process("/sbin/init") ||                    !try_to_run_init_process("/etc/init") ||        !try_to_run_init_process("/bin/init") ||        !try_to_run_init_process("/bin/sh"))        
    return 0;
panic("No working init found.  Try passing init= option to kernel. "          "See Linux Documentation/admin-guide/init.rst for guidance.");
}
```

**ramdisk_execute_command** and **execute_command** are configure in **GRUB**