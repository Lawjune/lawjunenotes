# Linux Essentials for Ethical Hackers 

## Useful keyboard Shortcuts

* **CTRL + ALT + T** => open the terminal
* **SUPER + Arrow Keys**
* **CTRL + SHIFT & +** => increase the font-size 
* **CTRL + -** => reduce the font-size
* **CTRL + C** => end the process
* **CTRL + Z** => suspend the process
* **CTRL + L** => clear the terminal window
* **CTRL + SHIFT + W** => close the window

## File Management & Manipulation

* pwd
* ls 
	* ls -l => list the files in the format of *list*
	* ls -a => list *all* of the files
	* ls -la
	* ls -lrt => list the files *ranking by time*
	* ls -lart
	* ls -lR Documents/ => listing *Recursive*
* cd
	cd ..
	cd ${ABSOLUTE_PATH}

```sh
cd Desktop/ 
``` 
=> To quickly create a file

```sh
whatis touch
```

```sh 
touch test.txt
echo "Jun Luo is not cool" > test.txt
cat test.txt
```
=> `Jun Luo is not cool`

```sh
cat /etc/passwd > pass.txt
```

* mkdir ${DIRECTORY_NAME} => *make directory"
* cp => *copy*
* rm
	* rm -R 
* mv => move (to implement `rename`)


## File & Directory Permissions

```sh
touch test.sh
cat /etc/passwd > test.sh
mkdir Test
ls -lh
`=>
total 16K
drwxrwxr-x  2 lawjune lawjune 4.0K 9月  16 20:28 Test
-rw-rw-r--  1 lawjune lawjune 2.7K 9月  16 20:28 test.sh
```

* d -> direcotry
* r -> read
* w -> write
* x -> executable

d<owner><group><allOtherUser>

### chmod symbolic Mode Format
```sh
cat /dev/null > test.sh 
cat test.sh 
echo "echo \"Hello World\"" > test.sh
./test.sh
`=>
bash: ./test.sh: Permission denied
```

```sh
chmod u=rwx test.sh 
ls -lh
`=>
total 16K

drwxrwxr-x  2 lawjune lawjune 4.0K 9月  16 20:28 Test
-rwxrw-r--  1 lawjune lawjune   13 9月  16 20:37 test.sh
```
```sh
./test.sh 
`=>
Hello World
```
```sh
chmod a=rwx test.sh
ls -lh
`=>
total 16K
drwxrwxr-x  2 lawjune lawjune 4.0K 9月  16 20:28 Test
-rwxrwxrwx  1 lawjune lawjune   19 9月  16 20:42 test.sh
```

* a -> all
* u -> user
* g -> group
* o -> other

*How to remove the permision?*

```sh
chmod go-wx test.sh 
ls -lh
`=>
total 16K
drwxrwxr-x  2 lawjune lawjune 4.0K 9月  16 20:28 Test
-rwxr--r--  1 lawjune lawjune   19 9月  16 20:42 test.sh
```

### chmod Octal/Binary Mode Format

```sh
chmod 777 test.sh 
ls -lh
`=>
total 16K
drwxrwxr-x  2 lawjune lawjune 4.0K 9月  16 20:28 Test
-rwxrwxrwx  1 lawjune lawjune   19 9月  16 20:42 test.sh
```

```sh
chmod 666 test.sh 
ls -lh
`=>
total 16K
drwxrwxr-x  2 lawjune lawjune 4.0K 9月  16 20:28 Test
-rw-rw-rw-  1 lawjune lawjune   19 9月  16 20:42 test.sh
```

```sh
chmod 444 test.sh 
ls -lh
`=>total 16K
drwxrwxr-x  2 lawjune lawjune 4.0K 9月  16 20:28 Test
-r--r--r--  1 lawjune lawjune   19 9月  16 20:42 test.sh
```

```sh
chmod 744 test.sh 
ls -lh
`=>
total 16K
drwxrwxr-x  2 lawjune lawjune 4.0K 9月  16 20:28 Test
-rwxr--r--  1 lawjune lawjune   19 9月  16 20:42 test.sh
```

### chmod for directory

```sh
ls -lh
`=>
total 8.0K
drwxrwxr-x 2 lawjune lawjune 4.0K 9月  16 20:28 Test
-rwxr--r-- 1 lawjune lawjune   19 9月  16 20:42 test.s
```

```sh
chmod ugo=rwx Test/
ls -lh
`=>
total 8.0K
drwxrwxrwx 2 lawjune lawjune 4.0K 9月  16 20:28 Test
-rwxr--r-- 1 lawjune lawjune   19 9月  16 20:42 test.sh
```

```sh
chmod 644 Test/
ls -lh
`=>
total 8.0K
drw-r--r-- 2 lawjune lawjune 4.0K 9月  16 20:28 Test
-rwxr--r-- 1 lawjune lawjune   19 9月  16 20:42 test.sh
```

```sh
  -R, --recursive 
  `=> change files and directories recursively
```

```sh
chmod 755 test.sh
chmod 755 Test/
mv test.sh Test/
ls -lh Test/
`=>
total 4.0K
-rwxr-xr-x 1 lawjune lawjune 19 9月  16 20:42 test.sh
```
```sh
chmod -R 777 Test/
ls -lh Test/
`=>
total 4.0K
-rwxrwxrwx 1 lawjune lawjune 19 9月  16 20:42 test.sh
```

## File & Directory Ownership

```sh
sudo bash
`=>
root@lawjune-ThinkPad-T530:/home/lawjune/Desktop#
```

```sh
whatis chown
`=>
chown (1)            - change file owner and group
chown (2)            - change ownership of a file
```

```sh
cd Test/
chown root test.sh 
ls -lh
`=>
total 4.0K
-rwxrwxrwx 1 root lawjune 19 9月  16 20:42 test.sh
```

```sh
whatis chgrp
`=>
chgrp (1)            - change group ownership
```

```sh
groups root
`=>
root : root
```

```sh
groups lawjune
`=>
lawjune : lawjune adm cdrom sudo dip plugdev lpadmin lxd sambashare
```

```sh
chgrp root test.sh 
ls -lh
`=>
total 4.0K
-rwxrwxrwx 1 root root 19 9月  16 20:42 test.sh
```

```sh
exit
cd Test/
sudo chgrp $(whoami) test.sh
sudo chown $(whoami) test.sh
ls -lh
`=>total 4.0K
-rwxrwxrwx 1 lawjune lawjune 19 9月  16 20:42 test.sh
```

## grep & piping

```sh
grep "Manager" /etc/passwd
`=>
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
nm-openvpn:x:118:124:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
gdm:x:125:130:Gnome Display Manager:/var/lib/gdm3:/bin/false
```

```sh
cat /etc/passwd | grep Manager
`=>
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
nm-openvpn:x:118:124:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
gdm:x:125:130:Gnome Display Manager:/var/lib/gdm3:/bin/false
```

```sh
ps -ef | grep sublime
`=>
lawjune    39437    1276  0 9月15 ?       00:02:11 /opt/sublime_text/sublime_text
lawjune    39460   39437  0 9月15 ?       00:00:04 /opt/sublime_text/plugin_host 39437 --auto-shell-env
lawjune    83530   43997  0 21:41 pts/0    00:00:00 grep --color=auto sublime
```

```sh
ps aux | grep -i apt
`=>
root         628  0.0  0.1 129344  9788 ?        Ssl  9月15   0:00 /usr/sbin/thermald --systemd --dbus-enable --adaptive
root       76589  0.0  0.0  15176  5080 ?        S    21:27   0:00 sudo apt-get install virtualbox
root       76610  0.3  0.8  85704 70380 ?        S    21:27   0:03 apt-get install virtualbox
lawjune    84550  0.0  0.0  12112  2988 pts/0    S+   21:43   0:00 grep --color=auto -i apt
```

```sh
ifconfig | grep inet
`=>
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        inet 192.168.0.102  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::f609:928a:5f38:8ec6  prefixlen 64  scopeid 0x20<link>
```

## Finding Files With Locate

```sh
locate /etc --all passwd
`=>
/etc/passwd
/etc/passwd-
/etc/pam.d/chpasswd
/etc/pam.d/passwd
/etc/security/opasswd
/snap/core/11606/etc/passwd
/snap/core/11606/etc/cron.daily/passwd
/snap/core/11606/etc/init/passwd.conf
/snap/core/11606/etc/pam.d/chpasswd
/snap/core/11606/etc/pam.d/passwd
/snap/core/11606/etc/security/opasswd
/snap/core18/1880/etc/passwd
/snap/core18/1880/etc/pam.d/chpasswd
/snap/core18/1880/etc/pam.d/passwd
/snap/core18/1880/etc/security/opasswd
/snap/core18/2128/etc/passwd
/snap/core18/2128/etc/pam.d/chpasswd
/snap/core18/2128/etc/pam.d/passwd
/snap/core18/2128/etc/security/opasswd
```

```sh
locate passwd | grep /etc/
`=>
/etc/passwd
/etc/passwd-
/etc/pam.d/chpasswd
/etc/pam.d/passwd
/etc/security/opasswd
/snap/core/11606/etc/passwd
/snap/core/11606/etc/cron.daily/passwd
/snap/core/11606/etc/init/passwd.conf
/snap/core/11606/etc/pam.d/chpasswd
/snap/core/11606/etc/pam.d/passwd
/snap/core/11606/etc/security/opasswd
/snap/core18/1880/etc/passwd
/snap/core18/1880/etc/pam.d/chpasswd
/snap/core18/1880/etc/pam.d/passwd
/snap/core18/1880/etc/security/opasswd
/snap/core18/2128/etc/passwd
/snap/core18/2128/etc/pam.d/chpasswd
/snap/core18/2128/etc/pam.d/passwd
/snap/core18/2128/etc/security/opasswd
```

```sh
locate --all *.conf | grep resolve
`=>
/etc/systemd/resolved.conf
/snap/core/11606/etc/dbus-1/system.d/org.freedesktop.resolve1.conf
/snap/core/11606/etc/systemd/resolved.conf
/snap/core/11606/lib/systemd/system/systemd-resolved.service.d/resolvconf.conf
/snap/core18/1880/etc/systemd/resolved.conf
/snap/core18/1880/run/systemd/resolve/stub-resolv.conf
/snap/core18/1880/usr/share/dbus-1/system.d/org.freedesktop.resolve1.conf
/snap/core18/2128/etc/systemd/resolved.conf
/snap/core18/2128/usr/share/dbus-1/system.d/org.freedesktop.resolve1.conf
/usr/lib/NetworkManager/conf.d/10-dns-resolved.conf
/usr/share/dbus-1/system.d/org.freedesktop.resolve1.conf
```

```sh
locate --all -c *.conf
`=>
2511
```

```sh
locate -i proxychain
```

## Enumerating Distribution & Kernel Information

```sh
whoami
`=>
lawjune
```
```sh
hostname
`=>
lawjune-ThinkPad-T530
```
```sh
sudo vim /etc/hostname
```
```sh
id
uid=1000(lawjune) gid=1000(lawjune) groups=1000(lawjune),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),120(lpadmin),131(lxd),132(sambashare)
```

```sh
lsb_release -a
`=>
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 20.04.3 LTS
Release:	20.04
Codename:	focal
```

```sh
cat /etc/issue
`=>
Ubuntu 20.04.3 LTS \n \l
```

```sh
cat /etc/*release
`=>
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.3 LTS"
NAME="Ubuntu"
VERSION="20.04.3 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.3 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
```

```sh
cat /etc/redhat-release
```

```sh
lscpu
`=>
Architecture:                    x86_64
CPU op-mode(s):                  32-bit, 64-bit
Byte Order:                      Little Endian
Address sizes:                   36 bits physical, 48 bits virtual
CPU(s):                          8
On-line CPU(s) list:             0-7
Thread(s) per core:              2
Core(s) per socket:              4
Socket(s):                       1
NUMA node(s):                    1
Vendor ID:                       GenuineIntel
CPU family:                      6
Model:                           58
Model name:                      Intel(R) Core(TM) i7-3610QM CPU @ 2.30GHz
Stepping:                        9
CPU MHz:                         1400.000
CPU max MHz:                     3300.0000
CPU min MHz:                     1200.0000
BogoMIPS:                        4589.40
Virtualization:                  VT-x
L1d cache:                       128 KiB
L1i cache:                       128 KiB
L2 cache:                        1 MiB
L3 cache:                        6 MiB
NUMA node0 CPU(s):               0-7
Vulnerability Itlb multihit:     KVM: Mitigation: VMX disabled
Vulnerability L1tf:              Mitigation; PTE Inversion; VMX conditional cach
                                 e flushes, SMT vulnerable
Vulnerability Mds:               Mitigation; Clear CPU buffers; SMT vulnerable
Vulnerability Meltdown:          Mitigation; PTI
Vulnerability Spec store bypass: Mitigation; Speculative Store Bypass disabled v
                                 ia prctl and seccomp
Vulnerability Spectre v1:        Mitigation; usercopy/swapgs barriers and __user
                                  pointer sanitization
Vulnerability Spectre v2:        Mitigation; Full generic retpoline, IBPB condit
                                 ional, IBRS_FW, STIBP conditional, RSB filling
Vulnerability Srbds:             Vulnerable: No microcode
Vulnerability Tsx async abort:   Not affected
Flags:                           fpu vme de pse tsc msr pae mce cx8 apic sep mtr
                                 r pge mca cmov pat pse36 clflush dts acpi mmx f
                                 xsr sse sse2 ss ht tm pbe syscall nx rdtscp lm 
                                 constant_tsc arch_perfmon pebs bts rep_good nop
                                 l xtopology nonstop_tsc cpuid aperfmperf pni pc
                                 lmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3
                                  cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic popcn
                                 t tsc_deadline_timer aes xsave avx f16c rdrand 
                                 lahf_lm cpuid_fault epb pti ssbd ibrs ibpb stib
                                 p tpr_shadow vnmi flexpriority ept vpid fsgsbas
                                 e smep erms xsaveopt dtherm ida arat pln pts md
                                 _clear flush_l1d
```

```sh
whatis uname
`=>
uname (1)            - print system information
uname (2)            - get name and information about current kernel
```

```sh
uname -a
`=>
Linux lawjune-ThinkPad-T530 5.11.0-34-generic #36~20.04.1-Ubuntu SMP Fri Aug 27 08:06:32 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux
```

## Find + OverTheWire Bandit Challenge

```sh
whatis find
`=>
find (1)  - search for files in a directory hierarchy
```

Find the files
```sh
sudo find / -type f -name "lawjune"
```

Find the directories
```sh
sudo find / -type d -name "lawjune"
```

Ignore the upper/lower case
```sh
sudo find / -type f -iname Lawjune
`=>
/var/lib/AccountsService/users/lawjune
find: ‘/tmp/.mount_PigchaRFmcDA’: Permission denied
find: ‘/run/user/1000/doc’: Permission denied
find: ‘/run/user/1000/gvfs’: Permission denied
/run/sudo/ts/lawjune
```

```sh
sudo find /etc -type f -name *.conf | grep net
`=>
/etc/modprobe.d/blacklist-rare-network.conf
/etc/bluetooth/network.conf
/etc/sysctl.d/10-network-security.conf
/etc/systemd/networkd.conf
/etc/sane.d/dell1600n_net.conf
/etc/sane.d/net.conf
/etc/dbus-1/system.d/net.hadess.SwitcherooControl.conf
/etc/dbus-1/system.d/net.hadess.SensorProxy.conf
```

```sh
chmod 400 test.sh
find /home -type f -perm 400
`=>
/home/lawjune/Desktop/Test/test.sh
```

***https://overthewire.org/wargames/bandit/***


## Shells & Bash Configuration

```sh
echo $SHELL
`=>
/bin/bash
```

```sh
cat /etc/shells 
`=>
# /etc/shells: valid login shells
/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/bin/dash
/usr/bin/dash
```

### Change Default Login Shell

```sh
cat /etc/passwd | grep lawjune
`=>
lawjune:x:1000:1000:Lawjune,,,:/home/lawjune:/bin/bash
```

```sh
whatis chsh
`=>
chsh (1)             - change login shell
```

```sh
chsh
`=>
Password: 
Changing the login shell for lawjune
Enter the new value, or press ENTER for the default
	Login Shell [/bin/bash]: usr/bin/dash
```

```sh
cat /etc/passwd | grep lawjune
`=>
lawjune:x:1000:1000:Lawjune,,,:/home/lawjune:/usr/bin/dash

```
### Clear Bash History

```sh
ls -alps | grep .bash
`=>
 0 -rw-------  1 lawjune lawjune     0 9月  18 08:17 .bash_history
 4 -rw-r--r--  1 lawjune lawjune   220 9月  15 19:03 .bash_logout
 8 -rw-r--r--  1 lawjune lawjune  4254 9月  15 21:30 .bashrc
```

```sh
cat /dev/null > .bash_history
```

### Bash Aliases 

```sh
touch .bash_aliases
vim .bash_aliases
`<=
alias update='sudo apt-get update'
alias upgrade='sudo apt-get upgrade'
```

```sh
source .bash_aliases
update
`=>
......
```

## Disk Usage

### du

```sh
whatis du
`=>
du (1)               - estimate file space usage
```

* -s -> summary
* -h -> human readable
```sh
du -sh *
`=>
6.0G	anaconda3
7.7G	Android
25M	AndroidStudioProjects
12K	Desktop
4.6M	Documents
772M	Downloads
3.8G	Kali
4.0K	Music
4.0K	Pictures
4.0K	Public
9.5M	PycharmProjects
9.9M	snap
4.0K	Templates
4.0K	Videos
4.0K	VirtualBox VMs
```

```sh
du -sh * | grep G
`=>
6.0G	anaconda3
7.7G	Android
3.8G	Kali
```

```sh
cd /
sudo du -sh *
`=>
0	bin
145M	boot
4.0K	cdrom
0	dev
12M	etc
23G	home
0	lib
0	lib32
0	lib64
0	libx32
16K	lost+found
8.0K	media
4.0K	mnt
282M	opt
du: cannot access 'proc/25016/task/25016/fd/4': No such file or directory
du: cannot access 'proc/25016/task/25016/fdinfo/4': No such file or directory
du: cannot access 'proc/25016/fd/3': No such file or directory
du: cannot access 'proc/25016/fdinfo/3': No such file or directory
0	proc
84K	root
du: cannot access 'run/user/1000/doc': Permission denied
du: cannot access 'run/user/1000/gvfs': Permission denied
1.9M	run
0	sbin
8.2G	snap
4.0K	srv
2.1G	swapfile
0	sys
du: cannot access 'tmp/.mount_PigchaSvYroS': Permission denied
156K	tmp
5.5G	usr
4.0G	var
```

* -c -> total -> produce a grand total
```sh
cd ~
du -shc *
6.0G	anaconda3
7.7G	Android
25M	AndroidStudioProjects
12K	Desktop
4.6M	Documents
772M	Downloads
3.8G	Kali
4.0K	Music
4.0K	Pictures
4.0K	Public
9.5M	PycharmProjects
9.9M	snap
4.0K	Templates
4.0K	Videos
4.0K	VirtualBox VMs
19G	total
```

### df

```sh
whatis df
df (1)               - report file system disk space usage
```

```sh
df -h
`=>
Filesystem      Size  Used Avail Use% Mounted on
udev            3.8G     0  3.8G   0% /dev
tmpfs           778M  1.9M  776M   1% /run
/dev/sda2       468G   35G  410G   8% /
tmpfs           3.8G   31M  3.8G   1% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           3.8G     0  3.8G   0% /sys/fs/cgroup
/dev/loop2       56M   56M     0 100% /snap/core18/2128
/dev/loop0      100M  100M     0 100% /snap/core/11606
/dev/loop3      256M  256M     0 100% /snap/gnome-3-34-1804/36
/dev/loop5      219M  219M     0 100% /snap/gnome-3-34-1804/72
/dev/loop4       62M   62M     0 100% /snap/core20/1081
/dev/loop1      965M  965M     0 100% /snap/android-studio/114
/dev/loop8       55M   55M     0 100% /snap/core18/1880
/dev/loop6       66M   66M     0 100% /snap/gtk-common-themes/1515
/dev/loop7      427M  427M     0 100% /snap/pycharm-community/252
/dev/loop9       63M   63M     0 100% /snap/gtk-common-themes/1506
/dev/loop10      30M   30M     0 100% /snap/snapd/8542
/dev/loop11      51M   51M     0 100% /snap/snap-store/547
/dev/loop12      50M   50M     0 100% /snap/snap-store/467
/dev/loop13      33M   33M     0 100% /snap/snapd/12883
/dev/loop14     723M  723M     0 100% /snap/intellij-idea-community/323
/dev/sda1       511M  5.3M  506M   2% /boot/efi
tmpfs           778M   40K  778M   1% /run/user/1000
```

```sh
df -h | grep sd
`=>
/dev/sda2       468G   35G  410G   8% /
/dev/sda1       511M  5.3M  506M   2% /boot/efi
```

* -t -> type
```sh
df -ht ext4
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2       468G   35G  410G   8% /
```


## File Compression & Archiving With tar

### tar

```sh
whatis tar
`=>
tar (1)              - an archiving utility
```

```sh
ls -alps
`=>
total 12
4 drwxr-xr-x  3 lawjune lawjune 4096 9月  16 21:03 ./
4 drwxr-xr-x 30 lawjune lawjune 4096 9月  18 08:28 ../
4 drwxrwxrwx  2 lawjune lawjune 4096 9月  16 21:03 Test/
```

```sh
tar -cf test.tar Test/
ls -alps
`=>
total 24
 4 drwxr-xr-x  3 lawjune lawjune  4096 9月  18 09:55 ./
 4 drwxr-xr-x 30 lawjune lawjune  4096 9月  18 08:28 ../
 4 drwxrwxrwx  2 lawjune lawjune  4096 9月  16 21:03 Test/
12 -rw-rw-r--  1 lawjune lawjune 10240 9月  18 09:55 test.tar
```

```sh
file test.tar 
`=>
test.tar: POSIX tar archive (GNU)
```

```sh
rm test.tar
tar -cvf test.tar Test/
`=>
Test/
Test/test.sh
```

```sh
rm -rf Test/
tar -xvf test.tar
ls -alps
`=>
total 24
 4 drwxr-xr-x  3 lawjune lawjune  4096 9月  18 09:59 ./
 4 drwxr-xr-x 30 lawjune lawjune  4096 9月  18 08:28 ../
 4 drwxrwxr-x  2 lawjune lawjune  4096 9月  16 21:03 Test/
12 -rw-rw-r--  1 lawjune lawjune 10240 9月  18 09:57 test.tar
```

### gzip

```sh
whatis gzip
`=>
gzip (1)             - compress or expand files
```

```sh
rm test.tar
tar -czf test.tar.gz Test/
ls -alps
`=>
total 16
4 drwxr-xr-x  3 lawjune lawjune 4096 9月  18 10:03 ./
4 drwxr-xr-x 30 lawjune lawjune 4096 9月  18 08:28 ../
4 drwxrwxr-x  2 lawjune lawjune 4096 9月  16 21:03 Test/
4 -rw-rw-r--  1 lawjune lawjune  181 9月  18 10:03 test.tar.gz
```

```sh
file test.tar.gz 
`=>
test.tar.gz: gzip compressed data, from Unix, original size modulo 2^32 10240
```

```sh
rm -rf Test/
tar -xzf test.tar.gz
`=>
ls -alps
total 16
4 drwxr-xr-x  3 lawjune lawjune 4096 9月  18 10:05 ./
4 drwxr-xr-x 30 lawjune lawjune 4096 9月  18 08:28 ../
4 drwxrwxr-x  2 lawjune lawjune 4096 9月  16 21:03 Test/
4 -rw-rw-r--  1 lawjune lawjune  181 9月  18 10:03 test.tar.gz
```

### bzip2


## Users And Groups & Permissions With Visudo

### Users 

```sh
sudo su
cd ~
visudo
```

```sh
sudo useradd cheryl
sudo groups cheryl
`=>
cheryl : cheryl
```

```sh
cat /etc/passwd | grep cheryl
`=>
cheryl:x:1001:1001::/home/cheryl:/bin/sh
```

```sh
sudo userdel -r cheryl 
`=>
userdel: cheryl mail spool (/var/mail/cheryl) not found
userdel: cheryl home directory (/home/cheryl) not found
```

```sh
-m, --create-home
   Create the user's home directory if it does not exist. The files
   defined with the -k option) will be copied to the home directory.
   enabled, no home directories are created.

-c, --comment COMMENT
   Any text string. It is generally a short description of the login,
   and is currently used as the field for the user's full name.
   The new user will be created using HOME_DIR as the value for the
   user's login directory. The default is to append the LOGIN name to
   BASE_DIR and use that as the login directory name. The directory
   HOME_DIR does not have to exist but will not be created if it is
   See below, the subsection "Changing the default values".
   The date on which the user account will be disabled. The date is
   specified in the format YYYY-MM-DD.

-s, --shell SHELL
   The name of the user's login shell. The default is to leave this
   field blank, which causes the system to select the default login
   shell specified by the SHELL variable in /etc/default/useradd, or
   an empty string by default.
   The numerical value of the user's ID. This value must be unique,
   unless the -o option is used. The value must be non-negative. The
   default is to use the smallest ID value greater than or equal to
   UID_MIN and greater than every other user.
   See also the -r option and the UID_MAX description.
```

```sh
sudo useradd -m -c "cheryl" -s /bin/bash cheryl
sudo passwd cheryl
`=> <=
New password: 
Retype new password: 
passwd: password updated successfully
```

```sh
su cheryl
sudo apt update
`=>
[sudo] password for cheryl: 
cheryl is not in the sudoers file.  This incident will be reported.
```

```sh
su lawjune
sudo visudo
```

```sh
# User privilege specification
root    ALL=(ALL:ALL) ALL
# Add this line
cheryl  ALL=(ALL) /usr/bin/apt-get
```

```sh
su cheryl
sudo apt-get update
....`=> working
```

```sh
sudo vim /etc/ssh/ssh_config
`=>
[sudo] password for cheryl: 
Sorry, user cheryl is not allowed to execute '/usr/bin/vim /etc/ssh/ssh_config' as root on lawjune-ThinkPad-T530.
```

```sh
su lawjune
sudo visudo
```

*sudo group**
```sh
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```

### Groups

```sh
groups cheryl
`=>
cheryl : cheryl
```

```sh
sudo groupadd hackers
```

Listing all of the groups
```sh
cat /etc/group
```
```sh
cat /etc/group | grep hackers
`=>
hackers:x:1002:
```

Add user
```sh
-g, --gid GROUP
   The group name or number of the user's new initial login group. The group must exist.
   primary group of the user will be owned by this new group.
   The group ownership of files outside of the user's home directory
-G, --groups GROUP1[,GROUP2,...[,GROUPN]]]
   A list of supplementary groups which the user is also a member of.
   Each group is separated from the next by a comma, with no
   intervening whitespace. The groups are subject to the same
   restrictions as the group given with the -g option.
   If the user is currently a member of a group which is not listed,
   the user will be removed from the group. This behaviour can be
   changed via the -a option, which appends the user to the current
   supplementary group list.
```

```sh
sudo usermod -aG hackers cheryl
groups cheryl
`=>
cheryl : cheryl hackers
```

```sh
sudo visudo
`<=
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# Add this line
# Hackers group
# ALL=(USER/GROUP)
%hackers ALL=(ALL:ALL) /usr/bin/apt /usr/bin/apt-get
```
```sh
su cheryl
sudo apt update
`=>...working
```
```sh
sudo cat /etc/shadow
`=>
[sudo] password for cheryl: 
Sorry, user cheryl is not allowed to execute '/usr/bin/cat /etc/shadow' as root on lawjune-ThinkPad-T530.
```

```sh
exit
sudo cat /etc/shadow
`=>
root:!:18885:0:99999:7:::
daemon:*:18474:0:99999:7:::
bin:*:18474:0:99999:7:::
......
lawjune:$6$OctGMQjTTTh5MKsf$4dJGy2LMXRH9zwiB0O9IM49.1bxQKJ29811p2OTXiYwKfmF3rogx6msq4wV7JGFscYSvzm54CPcZRirq.wi9o.:18885:0:99999:7:::
systemd-coredump:!!:18885::::::
cheryl:$6$6m9di4gj8bkInqJn$BSGu4Buwi/WAYFCilfPws8t.LDlubKmgu/6.yz.olM0raz3hjOJiSHXBU9pw626VFoghxYmFRl5BYuhu9nYJF0:18888:0:99999:7:::

`---comments
mark:$6$.n.:17736:0:99999:7:::
[--] [----] [---] - [---] ----
|      |      |   |   |   |||+-----------> 9. Unused
|      |      |   |   |   ||+------------> 8. Expiration date
|      |      |   |   |   |+-------------> 7. Inactivity period
|      |      |   |   |   +--------------> 6. Warning period
|      |      |   |   +------------------> 5. Maximum password age
|      |      |   +----------------------> 4. Minimum password age
|      |      +--------------------------> 3. Last password change
|      +---------------------------------> 2. Encrypted Password
+----------------------------------------> 1. Username

`=>
2. Encrypted Password. The password is using the $type$salt$hashed format. $type is the method cryptographic hash algorithm and can have the following values:

$1$ – MD5
$2a$ – Blowfish
$2y$ – Eksblowfish
$5$ – SHA-256
$6$ – SHA-512
```

## Networking (ifconfig, netstat & netdiscover)

### ip & ifconfig

```sh
whatis ip
`=>
ip (8)               - show / manipulate routing, network devices, interfaces...
ip (7)               - Linux IPv4 protocol implementation
```

```sh
ip route show
`=>
default via 172.20.10.1 dev enx16d00deaa81b proto dhcp metric 100 
169.254.0.0/16 dev enx16d00deaa81b scope link metric 1000 
172.20.10.0/28 dev enx16d00deaa81b proto kernel scope link src 172.20.10.13 metric 100 
```

```sh
man ip | grep route
`=>
       OBJECT := { link | address | addrlabel | route | rule | neigh | ntable
               | tunnel | tuntap | maddress | mroute | mrule | monitor | xfrm
       mroute - multicast routing cache entry.
       route  - routing table entry.
       ip route
           Show table routes.
       ip-monitor(8), ip-mroute(8), ip-neighbour(8), ip-netns(8), ip-
       ntable(8), ip-route(8), ip-rule(8), ip-tcp_metrics(8), ip-token(8), ip-
iproute2                          20 Dec 2011                            IP(8)
```

```sh
ip addr
`=>
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp0s25: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 3c:97:0e:8b:93:ab brd ff:ff:ff:ff:ff:ff
3: wlp3s0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000
    link/ether 6c:88:14:02:68:78 brd ff:ff:ff:ff:ff:ff
6: enx16d00deaa81b: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 16:d0:0d:ea:a8:1b brd ff:ff:ff:ff:ff:ff
    inet 172.20.10.13/28 brd 172.20.10.15 scope global dynamic noprefixroute enx16d00deaa81b
       valid_lft 80286sec preferred_lft 80286sec
    inet6 2408:840c:845f:e9ab:bb5d:cd90:debc:dae6/64 scope global temporary dynamic 
       valid_lft 599551sec preferred_lft 80599sec
    inet6 2408:840c:845f:e9ab:11b5:ecb2:f09a:b93b/64 scope global mngtmpaddr noprefixroute 
       valid_lft forever preferred_lft forever
    inet6 2408:840c:861f:a456:db63:5a64:a54b:5e56/64 scope global temporary dynamic 
       valid_lft 599428sec preferred_lft 80476sec
    inet6 2408:840c:861f:a456:504c:23b2:9bdf:9bfa/64 scope global mngtmpaddr noprefixroute 
       valid_lft forever preferred_lft forever
    inet6 fe80::ea89:67bb:77db:65ed/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

```sh
`=>
ifconfig | grep inet
        inet 172.20.10.13  netmask 255.255.255.240  broadcast 172.20.10.15
        inet6 2408:840c:861f:a456:db63:5a64:a54b:5e56  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::ea89:67bb:77db:65ed  prefixlen 64  scopeid 0x20<link>
        inet6 2408:840c:861f:a456:504c:23b2:9bdf:9bfa  prefixlen 64  scopeid 0x0<global>
        inet6 2408:840c:845f:e9ab:bb5d:cd90:debc:dae6  prefixlen 64  scopeid 0x0<global>
        inet6 2408:840c:845f:e9ab:11b5:ecb2:f09a:b93b  prefixlen 64  scopeid 0x0<global>
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
```

### dhclient

```sh
whatis dhclient
`=>
dhclient (8)         - Dynamic Host Configuration Protocol Client
```

```sh
sudo systemctl restart network-manager.service 
```

### netstat

```sh
whatis netstat
netstat (8)          - Print network connections, routing tables, interface s...
```

```sh
netstat -ie
`=>
Kernel Interface table
enp0s25: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 3c:97:0e:8b:93:ab  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 20  memory 0xf2500000-f2520000  

enx16d00deaa81b: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.20.10.13  netmask 255.255.255.240  broadcast 172.20.10.15
        inet6 fe80::ea89:67bb:77db:65ed  prefixlen 64  scopeid 0x20<link>
        inet6 2408:840c:845f:e9ab:ab2d:c7d1:bb03:b662  prefixlen 64  scopeid 0x0<global>
        inet6 2408:840c:845f:e9ab:11b5:ecb2:f09a:b93b  prefixlen 64  scopeid 0x0<global>
        ether 16:d0:0d:ea:a8:1b  txqueuelen 1000  (Ethernet)
        RX packets 110281  bytes 140157653 (140.1 MB)
        RX errors 0  dropped 1  overruns 0  frame 0
        TX packets 307715  bytes 17330076 (17.3 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 181482  bytes 397773683 (397.7 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 181482  bytes 397773683 (397.7 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlp3s0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 6c:88:14:02:68:78  txqueuelen 1000  (Ethernet)
        RX packets 6335  bytes 5827814 (5.8 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 945  bytes 165641 (165.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

```sh
netstat -r
`=>
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
default         localhost       0.0.0.0         UG        0 0          0 enx16d00deaa81b
link-local      0.0.0.0         255.255.0.0     U         0 0          0 enx16d00deaa81b
172.20.10.0     0.0.0.0         255.255.255.240 U         0 0          0 enx16d00deaa81b
```

List all of the active connections
```sh
netstat -a | grep http
`=>
tcp        0      0 lawjune-ThinkPad-:52484 no-rdns.kddi.peeri:http ESTABLISHED
tcp        0      0 lawjune-ThinkPad-:52522 no-rdns.kddi.peeri:http ESTABLISHED
tcp        0      0 lawjune-ThinkPad-:33406 45.55.41.223:http       CLOSE_WAIT 
tcp        0      0 lawjune-ThinkPad-:52496 no-rdns.kddi.peeri:http ESTABLISHED
tcp        0      0 lawjune-ThinkPad-:52402 no-rdns.kddi.peeri:http ESTABLISHED
tcp        0      0 lawjune-ThinkPad-:52440 no-rdns.kddi.peeri:http ESTABLISHED
tcp        0      0 lawjune-ThinkPad-:52504 no-rdns.kddi.peeri:http ESTABLISHED
tcp        0      0 lawjune-ThinkPad-:52390 no-rdns.kddi.peeri:http ESTABLISHED
tcp        0      0 lawjune-ThinkPad-:52366 no-rdns.kddi.peeri:http ESTABLISHED
```

```sh
[--tcp|-t]  [--udp|-u] 

--interfaces, -i
   Display a table of all network interfaces.
   Display a list of masqueraded connections.
--statistics, -s
   Display summary statistics for each protocol.
   Tell  the user what is going on by being verbose. Especially print some
   useful information about unconfigured address families.
   Do not truncate IP addresses by using output as wide as needed. This is
   optional for now to not break existing scripts.
   Show  numerical addresses instead of trying to determine symbolic host,
   port or user names.

-l, --listening
   Show only listening sockets.  (These are omitted by default.)

-p, --program
   Show the PID and name of the program to which each socket belongs.
   option, show interfaces that are not up
   The protocol (tcp, udp, udpl, raw) used by the socket.
   Established:  The  count  of  bytes not copied by the user program con‐
   Address  and  port  number  of the local end of the socket.  Unless the
   --numeric (-n) option is specified, the socket address is  resolved  to
   its  canonical host name (FQDN), and the port number is translated into
   the corresponding service name.
   Address and port number of the remote end of the socket.  Analogous  to
          The socket is actively attempting to establish a connection.
          The socket is waiting after close to handle packets still in the
          are  not included in the output unless you specify the --listen‐
          ing (-l) or --all (-a) option.
   Slash-separated  pair  of  the process id (PID) and process name of the
   process that owns the socket.  --program causes this column to  be  in‐
   cluded.   You  will also need superuser privileges to see this informa‐
   The protocol (usually unix) used by the socket.
   The reference count (i.e. attached processes via this socket).
```

```sh
netstat -t
`=>
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 localhost:58404         localhost:15733         TIME_WAIT  
tcp        0      0 localhost:58430         localhost:15733         TIME_WAIT  
tcp        0      0 localhost:58436         localhost:15733         TIME_WAIT  
tcp        0      0 localhost:40176         localhost:15732         ESTABLISHED
tcp        0      0 localhost:40146         localhost:15732         ESTABLISHED
tcp        1      0 localhost:59446         localhost:15732         CLOSE_WAIT 
tcp        0      0 localhost:58382         localhost:15733         ESTABLISHED
tcp        0      0 localhost:40184         localhost:15732         ESTABLISHED
tcp        0      1 lawjune-ThinkPad-:56280 5.180.77.219:http       LAST_ACK   
tcp        0      1 lawjune-ThinkPad-:56254 5.180.77.219:http       LAST_ACK   
tcp        0      0 localhost:40086         localhost:15732         ESTABLISHED
tcp        0      0 localhost:40208         localhost:15732         ESTABLISHED
tcp        0      0 lawjune-ThinkPad-:56304 5.180.77.219:http       ESTABLISHED
tcp        0      0 localhost:58412         localhost:15733         ESTABLISHED
tcp        0      0 lawjune-ThinkPad-:56334 5.180.77.219:http       ESTABLISHED
tcp        0      0 localhost:58418         localhost:15733         ESTABLISHED
tcp        0      0 localhost:58442         localhost:15733         ESTABLISHED
tcp        0      1 lawjune-ThinkPad-:56364 5.180.77.219:http       SYN_SENT   
tcp        0      0 localhost:58320         localhost:15733         ESTABLISHED
tcp        0      0 localhost:58424         localhost:15733         TIME_WAIT  
tcp        0      0 lawjune-ThinkPad-:56242 5.180.77.219:http       ESTABLISHED
tcp        0      0 lawjune-ThinkPad-:56340 5.180.77.219:http       ESTABLISHED
tcp6       0      0 127.0.0.1:15733         127.0.0.1:58412         ESTABLISHED
tcp6       0      0 127.0.0.1:15733         127.0.0.1:58320         ESTABLISHED
tcp6       0      0 127.0.0.1:15733         127.0.0.1:58418         ESTABLISHED
tcp6       0      0 127.0.0.1:15732         127.0.0.1:40086         ESTABLISHED
tcp6       0      0 127.0.0.1:15732         127.0.0.1:40176         ESTABLISHED
tcp6       0      0 127.0.0.1:15732         127.0.0.1:40196         TIME_WAIT  
tcp6       0      0 127.0.0.1:15732         127.0.0.1:40184         ESTABLISHED
tcp6       0      0 127.0.0.1:15732         127.0.0.1:40208         TIME_WAIT  
tcp6       0      0 127.0.0.1:15732         127.0.0.1:40146         ESTABLISHED
tcp6       0      0 127.0.0.1:15732         127.0.0.1:40214         ESTABLISHED
tcp6       0      0 127.0.0.1:15733         127.0.0.1:58448         ESTABLISHED
tcp6       0      0 127.0.0.1:15732         127.0.0.1:40190         TIME_WAIT  
tcp6       0      0 127.0.0.1:15733         127.0.0.1:58382         ESTABLISHED
tcp6       0      0 127.0.0.1:15732         127.0.0.1:40202         TIME_WAIT
```

```sh
netstat -lt
`=>
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 localhost:15731         0.0.0.0:*               LISTEN     
tcp        0      0 localhost:domain        0.0.0.0:*               LISTEN     
tcp        0      0 localhost:ipp           0.0.0.0:*               LISTEN     
tcp6       0      0 [::]:15732              [::]:*                  LISTEN     
tcp6       0      0 [::]:15733              [::]:*                  LISTEN     
tcp6       0      0 ip6-localhost:ipp       [::]:*                  LISTEN 
```

```sh
netstat -lu
`=>
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
udp        0      0 localhost:domain        0.0.0.0:*                          
udp        0      0 0.0.0.0:631             0.0.0.0:*                          
udp        0      0 0.0.0.0:50285           0.0.0.0:*                          
udp        0      0 224.0.0.251:mdns        0.0.0.0:*                          
udp        0      0 0.0.0.0:mdns            0.0.0.0:*                          
udp6       0      0 [::]:55371              [::]:*                             
udp6       0      0 fe80::ea8:dhcpv6-client [::]:*                             
udp6       0      0 [::]:mdns               [::]:*     
```

```sh
netstat -atp
`=>
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 localhost:ipp           0.0.0.0:*               LISTEN      -                   
tcp        0      0 localhost:15731         0.0.0.0:*               LISTEN      9113/PigchaProxy    
tcp        0      0 localhost:domain        0.0.0.0:*               LISTEN      -                   
tcp        0      0 lawjune-ThinkPad-:52538 no-rdns.kddi.peeri:http ESTABLISHED 9113/PigchaProxy    
tcp        0      0 localhost:54664         localhost:15733         ESTABLISHED 9113/PigchaProxy    
tcp        0      0 localhost:54772         localhost:15733         ESTABLISHED 9113/PigchaProxy    
tcp        0      0 lawjune-ThinkPad-:33406 45.55.41.223:http       CLOSE_WAIT  9394/plugin_host    
tcp        0      0 localhost:54806         localhost:15733         ESTABLISHED 9113/PigchaProxy    
tcp        0      0 lawjune-ThinkPad-:52402 no-rdns.kddi.peeri:http ESTABLISHED 9113/PigchaProxy    
tcp        0      0 localhost:33530         localhost:15732         ESTABLISHED 8869/chrome --type= 
tcp        0      0 localhost:54812         localhost:15733         ESTABLISHED 9113/PigchaProxy    
tcp        0      0 lawjune-ThinkPad-:52504 no-rdns.kddi.peeri:http ESTABLISHED 9113/PigchaProxy    
tcp        0      0 lawjune-ThinkPad-:52544 no-rdns.kddi.peeri:http ESTABLISHED 9113/PigchaProxy    
tcp        0      0 localhost:33566         localhost:15732         ESTABLISHED 8869/chrome --type= 
tcp        0      0 localhost:33424         localhost:15732         ESTABLISHED 8869/chrome --type= 
tcp        0      0 localhost:33572         localhost:15732         ESTABLISHED 8869/chrome --type= 
tcp6       0      0 ip6-localhost:ipp       [::]:*                  LISTEN      -                   
tcp6       0      0 [::]:15732              [::]:*                  LISTEN      9113/PigchaProxy    
tcp6       0      0 [::]:15733              [::]:*                  LISTEN      9113/PigchaProxy    
tcp6       0      0 127.0.0.1:15732         127.0.0.1:33566         ESTABLISHED 9113/PigchaProxy    
tcp6       0      0 127.0.0.1:15732         127.0.0.1:33572         ESTABLISHED 9113/PigchaProxy    
tcp6       0      0 127.0.0.1:15733         127.0.0.1:54812         ESTABLISHED 9113/PigchaProxy    
tcp6       0      0 127.0.0.1:15733         127.0.0.1:54772         ESTABLISHED 9113/PigchaProxy    
tcp6       0      0 127.0.0.1:15732         127.0.0.1:33530         ESTABLISHED 9113/PigchaProxy    
tcp6       0      0 127.0.0.1:15733         127.0.0.1:54806         ESTABLISHED 9113/PigchaProxy    
tcp6       0      0 127.0.0.1:15732         127.0.0.1:33424         ESTABLISHED 9113/PigchaProxy    
tcp6       0      0 127.0.0.1:15733         127.0.0.1:54664         ESTABLISHED 9113/PigchaProxy   
```

```sh
netstat -tnlp
`=>
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      -                   
tcp        0      0 127.0.0.1:15731         0.0.0.0:*               LISTEN      9113/PigchaProxy    
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -                   
tcp6       0      0 ::1:631                 :::*                    LISTEN      -                   
tcp6       0      0 :::15732                :::*                    LISTEN      9113/PigchaProxy    
tcp6       0      0 :::15733                :::*                    LISTEN      9113/PigchaProxy  
```

```sh
netstat -nlp | grep :15731
`=>
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
tcp        0      0 127.0.0.1:15731         0.0.0.0:*               LISTEN      9113/PigchaProxy    
```

### netdiscover

```sh
whatis  netdiscover
`=>
netdiscover (8)      - active/passive ARP reconnaissance tool
```

```sh
`=>
-i device
      The  network interface to sniff and inject packets. If no inter‐
      face is specified, first available will be used.

-r range
      Scan a given range instead of auto scan. Valid range values area
      for  example:  192.168.0.0/24,  192.168.0.0/16 or 192.168.0.0/8.
      Currently, acceptable ranges are /8, /16 and /24 only.
```


```sh
sudo netdiscover -i enx16d00deaa81b -r 172.20.10.0/16
`=>
1 Captured ARP Req/Rep packets, from 1 hosts.   Total size: 42                
 _____________________________________________________________________________
   IP            At MAC Address     Count     Len  MAC Vendor / Hostname      
 -----------------------------------------------------------------------------
 172.20.10.1     16:d0:0d:ae:91:64      1      42  Unknown vendor     
 ```

### DNS Server Setting

```sh
sudo vim /etc/resolv.conf 
systemd-resolve --status
`=>
Global
       LLMNR setting: no                  
MulticastDNS setting: no                  
  DNSOverTLS setting: no                  
      DNSSEC setting: no                  
    DNSSEC supported: no                  
          DNSSEC NTA: 10.in-addr.arpa     
                      16.172.in-addr.arpa 
                      168.192.in-addr.arpa
                      17.172.in-addr.arpa 
                      18.172.in-addr.arpa 
                      19.172.in-addr.arpa 
                      20.172.in-addr.arpa 
                      21.172.in-addr.arpa 
                      22.172.in-addr.arpa 
                      23.172.in-addr.arpa 
                      24.172.in-addr.arpa 
                      25.172.in-addr.arpa 
                      26.172.in-addr.arpa 
                      27.172.in-addr.arpa 
                      28.172.in-addr.arpa 
                      29.172.in-addr.arpa 
                      30.172.in-addr.arpa 
                      31.172.in-addr.arpa 
                      corp                
                      d.f.ip6.arpa        
                      home                
                      internal            
                      intranet            
                      lan                 
                      local               
                      private             
                      test                

Link 7 (enx16d00deaa81b)
      Current Scopes: DNS                     
DefaultRoute setting: yes                     
       LLMNR setting: yes                     
MulticastDNS setting: no                      
  DNSOverTLS setting: no                      
      DNSSEC setting: no                      
    DNSSEC supported: no                      
  Current DNS Server: 172.20.10.1             
         DNS Servers: 172.20.10.1             
                      fe80::c4f:4431:880b:18ca
          DNS Domain: ~.                      

Link 3 (wlp3s0)
      Current Scopes: none                   
DefaultRoute setting: no                     
       LLMNR setting: yes                    
MulticastDNS setting: no                     
  DNSOverTLS setting: no                     
      DNSSEC setting: no                     
    DNSSEC supported: no                     
  Current DNS Server: fe80::ca5:6eed:9dc4:afa
         DNS Servers: fe80::ca5:6eed:9dc4:afa
          DNS Domain: ~.                     

Link 2 (enp0s25)
      Current Scopes: none
DefaultRoute setting: no  
       LLMNR setting: yes 
MulticastDNS setting: no  
  DNSOverTLS setting: no  
      DNSSEC setting: no  
    DNSSEC supported: no  
lines 45-67/67 (END)
```

```sh
sudo vim /etc/hosts
```
```sh
sudo systemctl restart network-manager.service 
```


## TOR & Proxychains

### TOR

```sh
sudo apt-get install tor
whatis tor
tor (1)              - The second-generation onion router
tor (5)              - The second-generation onion router
```

```sh
systemctl status tor
`=>
● tor.service - Anonymizing overlay network for TCP (multi-instance-master)
     Loaded: loaded (/lib/systemd/system/tor.service; enabled; vendor preset:>
     Active: active (exited) since Sat 2021-09-18 16:09:22 CST; 2min 42s ago
   Main PID: 22607 (code=exited, status=0/SUCCESS)
      Tasks: 0 (limit: 9262)
     Memory: 0B
     CGroup: /system.slice/tor.service

9月 18 16:09:22 lawjune-ThinkPad-T530 systemd[1]: Starting Anonymizing overla>
9月 18 16:09:22 lawjune-ThinkPad-T530 systemd[1]: Finished Anonymizing overla>
lines 1-10/10 (END)
```

*port 9050 opened by tor*
```sh
netstat -lt | grep :9050
`=>
tcp        0      0 localhost:9050          0.0.0.0:*               LISTEN    
```

### Proxychains

```sh
sudo apt-get install proxychains
sudo vim /etc/proxychains.conf
`<=
# defaults set to "tor"
socks4 	127.0.0.1 9050
socks5  127.0.0.1 9050
```

```sh
proxychains firefox dnsleaktest.com
```

## Service And Process Management (HTOP & systemctl)

### HTOP

```sh
whatis top
`=>
top (1)              - display Linux processes
```

```sh
sudo apt-get install htop
```

```sh
whatis htop
`=>
htop (1)             - interactive process viewer
```

```sh
whatis free
`=>
free (1)             - Display amount of free and used memory in the system
free (3)             - allocate and free dynamic memory
```

```sh
free -h
`=>
              total        used        free      shared  buff/cache   available
Mem:          7.6Gi       3.2Gi       1.7Gi       329Mi       2.7Gi       3.8Gi
Swap:         2.0Gi          0B       2.0Gi
```

### PROCESS - ps

**ps - report a snapshot of the current processes.**

```sh
ps aux | grep sublime
`=>
lawjune     9380  0.6  2.4 1363192 196076 ?      Ssl  15:25   0:25 /opt/sublime_text/sublime_text
lawjune     9394  0.0  0.5 234580 41148 ?        Sl   15:25   0:01 /opt/sublime_text/plugin_host 9380 --auto-shell-env
lawjune    41219  0.0  0.0  12116  2768 pts/0    S+   16:36   0:00 grep --color=auto sublime
```

```sh
ps -ef | grep sublime
lawjune     9380    3345  0 15:25 ?        00:00:26 /opt/sublime_text/sublime_text
lawjune     9394    9380  0 15:25 ?        00:00:01 /opt/sublime_text/plugin_host 9380 --auto-shell-env
lawjune    41416    7847  0 16:37 pts/0    00:00:00 grep --c
```

```sh
ps aux | grep tor
`=>
debian-+   43386 10.6  0.2  28172 22944 ?        Ss   16:44   0:00 /usr/bin/tor --defaults-torrc /usr/share/tor/tor-service-defaults-torrc -f /etc/tor/torrc --RunAsDaemon 0
```

```sh
sudo kill -9 43386
```
*Once we killed this process, the service will restart automatically.*

```sh
ps aux | grep tor
`=>
debian-+   43797  5.9  0.3  32984 28956 ?        Ss   16:45   0:00 /usr/bin/tor --defaults-torrc /usr/share/tor/tor-service-defaults-torrc -f /etc/tor/torrc --RunAsDaemon 0
```

### Service Management - systemd

```sh
whatis systemctl
`=>
systemctl (1)        - Control the systemd system and service manager
```

```sh
udo systemctl status ssh
`=>
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor pre>
     Active: active (running) since Sat 2021-09-18 16:50:41 CST; 1min 7s >
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 45738 (sshd)
      Tasks: 1 (limit: 9262)
     Memory: 1.0M
     CGroup: /system.slice/ssh.service
             └─45738 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 start>

9月 18 16:50:41 lawjune-ThinkPad-T530 systemd[1]: Starting OpenBSD Secure>
9月 18 16:50:41 lawjune-ThinkPad-T530 sshd[45738]: Server listening on 0.>
9月 18 16:50:41 lawjune-ThinkPad-T530 sshd[45738]: Server listening on ::>
9月 18 16:50:41 lawjune-ThinkPad-T530 systemd[1]: Started OpenBSD Secure >
lines 1-15/15 (END)
```

```sh
sudo systemctl is-enabled ssh
`=>
enabled
```

```sh
sudo systemctl enable ssh.service
`=>
Synchronizing state of ssh.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable ssh
```

```sh
sudo systemctl disable ssh.service
`=>
Synchronizing state of ssh.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install disable ssh
Removed /etc/systemd/system/sshd.service.
Removed /etc/systemd/system/multi-user.target.wants/ssh.service.
```

```sh
sudo systemctl daemon-reload
```

```sh
service $(SERVICE_NAME) start/stop/restart/status
```

## SSH And SSH Security

### SSH apt-get

* openssh-client
* openssh-client-ssh1
* openssh-known-hosts
* openssh-server
* openssh-sftp-server

### Basic Concepts

**What is SSH?
* Secure Shell
* Communication Protocl (Like http, https, ftp, etc)
* Do just about anything on the remote computer
* Traffic is encrypted
* Used mostly in the terminal/command line
**

**Client/Server Communicaiton
* SSH is the client
* SSHD is the server (Open SSH Daemon)
* The server must have sshd installed and running or you will not be able to connect using SSH
**

**Authentication Methods
* > ssh lawjune@192.168.1.67
* Password
* Public / Private Key Pair
* Host Based
**

**Generating Keys
* > ssh-keygen
* ~/.ssh/id_rsa(Private Key)
* ~/.ssh/id_rsa.pub (Public Key)
* Public key goes into server "authorized_keys" file
**

**What About Windows?
* Windows 10 now supports native SSH
* Putty is used older versions of Windows
* Git Bash & other terminal programs include the ssh command & other Unix tools
**



```sh
ls /etc/ssh/
`=>
moduli        sshd_config.d           ssh_host_ed25519_key.pub
ssh_config    ssh_host_ecdsa_key      ssh_host_rsa_key
ssh_config.d  ssh_host_ecdsa_key.pub  ssh_host_rsa_key.pub
sshd_config   ssh_host_ed25519_key    ssh_known_hosts
```

```sh
cat /etc/ssh/ssh_config
`=>
# This is the ssh client system-wide configuration file.  See
# ssh_config(5) for more information.  This file provides defaults for
# users, and the values can be changed in per-user configuration files
# or on the command line.

# Configuration data is parsed as follows:
#  1. command line options
#  2. user-specific file
#  3. system-wide file
# Any configuration value is only changed the first time it is set.
# Thus, host-specific definitions should be at the beginning of the
# configuration file, and defaults at the end.

# Site-wide defaults for some commonly used options.  For a comprehensive
# list of available options, their meanings and defaults, please see the
# ssh_config(5) man page.

Include /etc/ssh/ssh_config.d/*.conf

Host *
#   ForwardAgent no
#   ForwardX11 no
#   ForwardX11Trusted yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   IdentityFile ~/.ssh/id_ecdsa
#   IdentityFile ~/.ssh/id_ed25519
#   Port 22
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
#   RekeyLimit 1G 1h
#   UserKnownHostsFile ~/.ssh/known_hosts.d/%k
    SendEnv LANG LC_*
    HashKnownHosts yes
    GSSAPIAuthentication yes
```

*If we modify the ssh_config, then we need to:*
```sh
sudo systemctl restart sshd.service
```

```sh
sudo passwd -S root
`=>
root L 09/15/2021 0 99999 7 -1
```

```sh
sudo vim /etc/ssh/sshd_config
cat /etc/ssh/sshd_config
`=>
#	$OpenBSD: sshd_config,v 1.103 2018/04/09 20:41:22 tj Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.

Include /etc/ssh/sshd_config.d/*.conf

#Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::

#HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_ecdsa_key
#HostKey /etc/ssh/ssh_host_ed25519_key

# Ciphers and keying
#RekeyLimit default none

# Logging
#SyslogFacility AUTH
#LogLevel INFO

# Authentication:

#LoginGraceTime 2m
#PermitRootLogin no
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 3

#PubkeyAuthentication yes

# Expect .ssh/authorized_keys2 to be disregarded by default in future.
#AuthorizedKeysFile	.ssh/authorized_keys .ssh/authorized_keys2

#AuthorizedPrincipalsFile none

#AuthorizedKeysCommand none
#AuthorizedKeysCommandUser nobody

# For this to work you will also need host keys in /etc/ssh/ssh_known_hosts
#HostbasedAuthentication no
# Change to yes if you don't trust ~/.ssh/known_hosts for
# HostbasedAuthentication
#IgnoreUserKnownHosts no
# Don't read the user's ~/.rhosts and ~/.shosts files
#IgnoreRhosts yes

# To disable tunneled clear text passwords, change to no here!
#PasswordAuthentication yes
#PermitEmptyPasswords no

# Change to yes to enable challenge-response passwords (beware issues with
# some PAM modules and threads)
ChallengeResponseAuthentication no

# Kerberos options
#KerberosAuthentication no
#KerberosOrLocalPasswd yes
#KerberosTicketCleanup yes
#KerberosGetAFSToken no

# GSSAPI options
#GSSAPIAuthentication no
#GSSAPICleanupCredentials yes
#GSSAPIStrictAcceptorCheck yes
#GSSAPIKeyExchange no

# Set this to 'yes' to enable PAM authentication, account processing,
# and session processing. If this is enabled, PAM authentication will
# be allowed through the ChallengeResponseAuthentication and
# PasswordAuthentication.  Depending on your PAM configuration,
# PAM authentication via ChallengeResponseAuthentication may bypass
# the setting of "PermitRootLogin without-password".
# If you just want the PAM account and session checks to run without
# PAM authentication, then enable this but set PasswordAuthentication
# and ChallengeResponseAuthentication to 'no'.
UsePAM yes

#AllowAgentForwarding yes
#AllowTcpForwarding yes
#GatewayPorts no
X11Forwarding yes
#X11DisplayOffset 10
#X11UseLocalhost yes
#PermitTTY yes
PrintMotd no
#PrintLastLog yes
#TCPKeepAlive yes
#PermitUserEnvironment no
#Compression delayed
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS no
#PidFile /var/run/sshd.pid
#MaxStartups 10:30:100
#PermitTunnel no
#ChrootDirectory none
#VersionAddendum none

# no default banner path
#Banner none

# Allow client to pass locale environment variables
AcceptEnv LANG LC_*

# override default of no subsystems
Subsystem	sftp	/usr/lib/openssh/sftp-server

# Example of overriding settings on a per-user basis
#Match User anoncvs
#	X11Forwarding no
#	AllowTcpForwarding no
#	PermitTTY no
#	ForceCommand cvs server
```

**To avoid `sudo su` after logining with admin account**

To generate the ssh keys to **ONLY** allow admin user to login as *root*.

```sh
ssh-keygen -t rsa
`=>
Generating public/private rsa key pair.
Enter file in which to save the key (/home/lawjune/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/lawjune/.ssh/id_rsa
Your public key has been saved in /home/lawjune/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:ESPdRCxM0f/A2vK9M6OBfL4PQAsYgocwhjUnNsnY8Ww lawjune@lawjune-ThinkPad-T530
The key's randomart image is:
+---[RSA 3072]----+
|+BB=o o+=Bo      |
|+o*B.. ++o+      |
|   .E . o..o     |
|   .     + .+    |
|        S oo o   |
|         .oo. .  |
|          oo+.   |
|           o.o=  |
|            ++o= |
+----[SHA256]-----+
```

To copy the public key to the ssh server.

```sh
cd .ssh
ls
`=>
config  id_rsa  id_rsa.pub  known_hosts
```

*The most common means of authentication is via SSH asymmetric key pairs. The server uses the public key to encrypt a message and send it to the client. If the client has the correct private key, they can decrypt the message and send it back to the server for verification.*

```sh
ssh-copy-id lawjune@172.20.10.13
`=>
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
lawjune@172.20.10.13's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'lawjune@172.20.10.13'"
and check to make sure that only the key(s) you wanted were added.
```

### SSH Login

```sh
ssh lawjune@172.20.10.13
`=>
lawjune@172.20.10.13's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.11.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

894 updates can be applied immediately.
To see these additional updates run: apt list --upgradable

Your Hardware Enablement Stack (HWE) is supported until April 2025.
Last login: Wed Sep 22 09:14:37 2021 from 172.20.10.13
```

To install the apache server
```sh
sudo apt install apache2 -y
```

### Create SSH Key

https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-2

```sh
exit
ssh-keygen
`=>
Generating public/private rsa key pair.
Enter file in which to save the key (/home/cheryl/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/cheryl/.ssh/id_rsa
Your public key has been saved in /home/cheryl/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:LUxYah9ZuncuwKvK1JNf3rH/5NiCMj2PLvwusctcyZw cheryl@lawjune-ThinkPad-T530
The key's randomart image is:
+---[RSA 3072]----+
|        . .      |
|       + +       |
|      + =        |
|     . = +       |
|        S o .    |
|     . . =.= o   |
|    . + ..o+E.  .|
|   o   + =B+++.= |
|    o.. . =XB++o+|
+----[SHA256]-----+
```

```sh
ls .ssh/
`=>
id_rsa  id_rsa.pub  known_hosts
```

### Get the Public Key into the Server

```sh
cd .ssh/
ssh-copy-id lawjune@172.20.10.13
`=>
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/cheryl/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
lawjune@172.20.10.13's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'lawjune@172.20.10.13'"
and check to make sure that only the key(s) you wanted were added.
```

*Next time been able to login `ssh lawjune@172.20.10.13` without password.*

In the server:
```sh
cat .ssh/authorized_keys 
`=>
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDfZ/dm3RarWau9vk+edl2jQBeSIjOgFdeQsQdMhABfGyy8incYwx/TvMq3gnlN/d5SKMKJVkWV3kX/YyFRw5Kar+SqF7lfR2t7EW4u89hHO2jjz5BGxb1OrUW12pEthYgeOXHmN24iWgxt1pVbg/fYnrt6b/eui3xFBmuPhkLlsQw9vbSF6iNT8Mz3RRdA15dC8rlZbLEofXcGCZSBY5QSFM/6CcIjwF9nUJU+Dte4ct2g2EKrAXBcMU+nSKSkjt1Jhf1TTOF/ZAI06AyFt/76xrQKkqPNflK7lHPUWBUViFym/zvF2c2uOdxsj25JZQIV8OhNam2xvWQb3wpS3fyp11WKxINoVp/vry7aMV4jrX5jUx53pgbaQRR0K6MvZNeCaVhVPjYObXf6QaryAuKlY/Ut+Q8aQGl/Mgz0JrFtcsbnmkGSNKzxRd5a6B/7eSn6X11SddbPGvEVwWu3ZMML+drjOxTmZQ5bGr8hBJdQlk5+kW6xerm18HVmAXJI5GE= lawjune@lawjune-ThinkPad-T530
```

In the client as the same:
```sh
cat .ssh/id_rsa.pub
`=>
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDeo3tdswKgP3IOByGDDm37LlDi8odi2lgsx4oLTtPk0GYV3NGAdxg4iuZZ3oRwJaMvliSXfhM8VqRerLJq4J6CMhLZn9VTVIhfBXxMeN46ER5ReMfuKLAJW6S06hfSkqtN3uAoISZp7B3he4YwXjy9GPy/7orTzA3m8ZVrFHRVybmTcIS5pFnmizrceswoA0CnLaynoXBGCE6olDtkRrpsmhVs9Z2CPvDfFQyW+du8wZR0E3hyZ7XdgxudDnlmkIQAj5UJyfeSaa5bLOsICK/njfONbSqpxl+HSLLSWwh1RXfJPFbrmQNGDLveqIPCjYJJXkaV14OoSKqrztduq/GcDeVpmUJ0SIJ8pEE+AJyxcRHSJcx4S7pFucysENhsOLwQl1d1iiccJMrF/oHeac+eShFVUX5eNXL6QUS5SomfiJkPqrVOqkshTS+06KJdX14lAGY7YqqVHi8V9cphn5WJmUVWZZ1H9nZBcdWZ4RK4eep5FryMDWh3U2VnTAqpZZs= cheryl@lawjune-ThinkPad-T530
```

### Command `scp`

## Login Cloud Server

### Add the SSH Key into the Cloud Server

***Remember to use `ssh-add` to add the new particular server key in your lobtop.***


### Add a New User

### Disable Root Login


# Curl Fundamentals

*curl is a command line tool to transfer data to or from a server, using any of the supported protocols (HTTP, FTP, IMAP, POP3, SCP, SFTP, SMTP, TFTP, TELNET, LDAP or FILE). curl is powered by Libcurl. This tool is preferred for automation, since it is designed to work without user interaction. curl can transfer multiple file at once.*

## Download the Content

```sh
man curl | grep o
`=>
-o, --output <file>
              Write output to <file> instead of stdout. If you are using {} or
              [] to fetch multiple documents, you should quote the URL and you
              can use '#' followed by a number in the <file>  specifier.  That
              variable  will  be  replaced with the current string for the URL
               curl "http://{one,two}.example.com" -o "file_#1.txt"
```

```sh
curl -o /home/lawjune/Desktop/geeks.html https://www.geeksforgeeks.org
`=>
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  112k    0  112k    0     0   164k      0 --:--:-- --:--:-- --:--:--  164k
```

## Redirect

```sh
man curl | grep L
`=>
      -L, --location
              to  a different location (indicated with a Location: header and
              as "Friends" or "London-Office".  (Added in 7.34.0)
              When  -L, --location is used, is used to prevent curl from fol‐
              To use a Metalink file in the local file system, use FILE  pro‐
              Please  note that if FILE protocol is disabled, there is no way
              Tells  curl  to  use a separate operation for the following URL
              and associated options. This allows you to send several URL re‐
              (HTTPS) Disable the ALPN TLS extension. ALPN is enabled by  de‐
              fault  if  libcurl  was built with an SSL library that supports
              ALPN. ALPN is used by a libcurl that supports HTTP/2 to negoti‐
              derlying libcurl was built to support TLS.
```

```sh
curl http://www.geeksforgeeks.org 
`=> Not working
```

```sh
curl -L http://www.geeksforgeeks.org 
`=> Working
```

## Analyze Response

```sh
curl -I https://www.geeksforgeeks.org
`=>
HTTP/1.0 200 Connection established

HTTP/1.1 200 OK
Server: nginx
Content-Type: text/html; charset=UTF-8
X-Frame-Options: DENY
Cache-Control: max-age=18492
Date: Wed, 22 Sep 2021 05:16:19 GMT
Connection: keep-alive
```

## View the TLS Handshake

```sh
curl -v https://www.geeksforgeeks.org | grep TLS
`=>
* Uses proxy env variable no_proxy == 'localhost,127.0.0.0/8,::1'
* Uses proxy env variable https_proxy == 'http://127.0.0.1:15732/'
*   Trying 127.0.0.1:15732...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0* Connected to 127.0.0.1 (127.0.0.1) port 15732 (#0)
* allocate connect buffer!
* Establish HTTP proxy tunnel to www.geeksforgeeks.org:443
> CONNECT www.geeksforgeeks.org:443 HTTP/1.1
> Host: www.geeksforgeeks.org:443
> User-Agent: curl/7.71.1
> Proxy-Connection: Keep-Alive
> 
< HTTP/1.0 200 Connection established
< 
* Proxy replied 200 to CONNECT request
* CONNECT phase completed!
* ALPN, offering http/1.1
* successfully set certificate verify locations:
*   CAfile: /home/lawjune/anaconda3/ssl/cacert.pem
  CApath: none
} [5 bytes data]
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
} [512 bytes data]
* CONNECT phase completed!
* CONNECT phase completed!
{ [5 bytes data]
* TLSv1.3 (IN), TLS handshake, Server hello (2):
{ [122 bytes data]
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
{ [35 bytes data]
* TLSv1.3 (IN), TLS handshake, Certificate (11):
{ [4321 bytes data]
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
{ [264 bytes data]
* TLSv1.3 (IN), TLS handshake, Finished (20):
{ [52 bytes data]
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
} [1 bytes data]
* TLSv1.3 (OUT), TLS handshake, Finished (20):
} [52 bytes data]
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
* ALPN, server accepted to use http/1.1
* Server certificate:
*  subject: CN=www.geeksforgeeks.org
*  start date: Aug  9 12:27:32 2021 GMT
*  expire date: Nov  7 12:27:30 2021 GMT
*  subjectAltName: host "www.geeksforgeeks.org" matched cert's "www.geeksforgeeks.org"
*  issuer: C=US; O=Let's Encrypt; CN=R3
*  SSL certificate verify ok.
} [5 bytes data]
> GET / HTTP/1.1
> Host: www.geeksforgeeks.org
> User-Agent: curl/7.71.1
> Accept: */*
> 
{ [5 bytes data]
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
{ [265 bytes data]
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
{ [265 bytes data]
* old SSL session ID is stale, removing
{ [5 bytes data]
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Server: nginx
< Content-Type: text/html; charset=UTF-8
< X-Frame-Options: DENY
< X-Akamai-Transformed: 9 - 0 pmb=mRUM,2
< Cache-Control: max-age=21416
< Date: Wed, 22 Sep 2021 05:18:31 GMT
< Transfer-Encoding:  chunked
< Connection: keep-alive
< Connection: Transfer-Encoding
< Server-Timing: cdn-cache; desc=HIT
< Server-Timing: edge; dur=1
< 
{ [16032 bytes data]
100  112k    0  112k    0     0   167k      0 --:--:-- --:--:-- --:--:--  167k
* Connection #0 to host 127.0.0.1 left intact
```

### Test the Credential

```sh
curl --data "log=admin&pwd=password" https://wordpress.com/wp-login.php
```


# UFW - Uncomplicated Firewall

*(UFW) is a program for managing a netfilter firewall designed to be easy to use. It uses a command-line interface consisting of a small number of simple commands, and uses iptables for configuration.*

```sh
sudo apt-get install ufw
```

```sh
sudo ufw status
`=>
Status: inactive
```

```sh
sudo ufw enable
`=>
Firewall is active and enabled on system startup
```

```sh
sudo ufw disable
`=>
Firewall stopped and disabled on system startup
```

***BE CAUTION TO USE `RESET` COMMAND for UFW***

```sh
sudo ufw default deny incoming
`=>
Default incoming policy changed to 'deny'
(be sure to update your rules accordingly)
```

```sh
sudo ufw default allow incoming
`=>
Default incoming policy changed to 'allow'
(be sure to update your rules accordingly)
```

```sh
sudo ufw allow ssh
`=>
Rules updated
Rules updated (v6)
```

```sh
sudo ufw allow 22
`=>
Rules updated
Rules updated (v6)
```

```sh
sudo ufw deny ssh
```

```sh
sudo ufw allow proto tcp from any to any port 80,443
```

```sh
sudo ufw allow from 192.168.1.1
```

```sh
sudo ufw allow from 192.168.1.1 to any port 22
```

```sh
sudo ufw allow from 192.168.1.1/24 to any port 22
```

```sh
sudo ufw enable
sudo ufw status
Status: active
`=>
To                         Action      From
--                         ------      ----
22/tcp                     DENY        Anywhere                  
22                         ALLOW       Anywhere                  
80,443/tcp                 ALLOW       Anywhere                  
22                         ALLOW       192.168.1.0/24            
22/tcp (v6)                DENY        Anywhere (v6)             
22 (v6)                    ALLOW       Anywhere (v6)             
80,443/tcp (v6)            ALLOW       Anywhere (v6)  
```

```sh
sudo ufw status verbose
`=>
Status: active
Logging: on (low)
Default: allow (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     DENY IN     Anywhere                  
22                         ALLOW IN    Anywhere                  
80,443/tcp                 ALLOW IN    Anywhere                  
22                         ALLOW IN    192.168.1.0/24            
22/tcp (v6)                DENY IN     Anywhere (v6)             
22 (v6)                    ALLOW IN    Anywhere (v6)             
80,443/tcp (v6)            ALLOW IN    Anywhere (v6)        
```

```sh
sudo ufw status numbered
Status: active
`=>
     To                         Action      From
     --                         ------      ----
[ 1] 22/tcp                     DENY IN     Anywhere                  
[ 2] 22                         ALLOW IN    Anywhere                  
[ 3] 80,443/tcp                 ALLOW IN    Anywhere                  
[ 4] 22                         ALLOW IN    192.168.1.0/24            
[ 5] 22/tcp (v6)                DENY IN     Anywhere (v6)             
[ 6] 22 (v6)                    ALLOW IN    Anywhere (v6)             
[ 7] 80,443/tcp (v6)            ALLOW IN    Anywhere (v6)  
```

```sh
sudo ufw delete 1
`=>
Deleting:
 deny 22/tcp
Proceed with operation (y|n)? y
Rule deleted
```


