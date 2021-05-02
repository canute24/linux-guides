# GRUB2 Complete: Install, Setup, Troubleshooting and Rescue:
###### Source: Interwebz

**IMPORTANT: Ensure all file are backed up before editing and file related to the OS**

GRUB Legacy fix:
```shell
find /boot/grub/stage1 (optional)
root (hdX,Y)
setup (hd0)
quit
```
GRUB2 Update Config: (1.0<GRUB<=1.99)
`update-grub / update-grub2` has been replaced with replaced with `grub-mkconfig / grub2-mkconfig`
```shell
grub2-mkconfig --root-directory= changed to --boot-directory=
```
GRUB2 Fix:
```shell
mount /dev/sda1 /mnt/
grub-install --boot-directory=/mnt /dev/sda
```
GRUB commandline: (Press "C" in GRUB Menu to load grub commandline. Has paging and command completion)
```shell
(get info)
grub> set pager=1
grub> ls
grub> ls (hd0,1)/
grub> cat (hd0,1)/etc/issue

(set options)
grub> set root=(hd0,1)
grub> linux /boot/vmlinuz-3.13.0-29-generic root=/dev/sda1
grub> initrd /boot/initrd.img-3.13.0-29-generic
grub> boot
```
Other commands from grub rescue:
```shell
grub rescue> set prefix=(hd0,1)/boot/grub
grub rescue> set root=(hd0,1)
grub rescue> insmod normal
grub rescue> normal
grub rescue> insmod linux
grub rescue> linux /boot/vmlinuz-3.13.0-29-generic root=/dev/sda1
grub rescue> initrd /boot/initrd.img-3.13.0-29-generic
grub rescue> boot
```
GRUB2 Install:
```shell
grub-install --target=i386-pc /dev/sda #--boot-directory=/boot/ is default in which /grub is created
/boot/grub/grub.cfg #do not edit this file or attribs, you can loot at it for additional options

#On error the following file is created to be edited and re-run grub-install
/boot/grub/device.map
```
GRUB2 Config Paths:
```shell
/etc/default/grub
/etc/grub.d/
```
Change boot order by changing numbers:
```shell
cp 40_custom 50_custom
chmod -x 40_custom
chmod +x 50_custom
chmod -x 10_linux (optional generic kernel hide)
chmod -x 20_memtest86+
```
GRUB Setup:
```shell
cp /boot/grub/grub.cfg ~/home/grub.cfg.bkp.date # Backup first

#os-prober if installed will detect other mounted partition OSs. ntfs-3g kernel driver required.
grub-mkconfig | less # Output file to terminal
grub-mkconfig -o /boot/grub/grub.cfg # If GRUB Legacy is installed then use grub2-mkconfig

grub2-mkrescue --output=<name>.iso /boot/grub
configfile /grub.cfg # On another pc booted from this iso should show the menu when this command is entered
```
GRUB2 CONFIG FILE EXAMPLES:
Grub config files are located at /etc/grub.d/. See 10_linux for additional options
To add a new listing make a new file with XX_NAME where XX is a number which is processed in ascending order e.g /etc/grub.d/50_custom_option1
##### Source: https://dareneiri.github.io/Configuring-Grub-2-on-CentOS-7/
```shell
menuentry "Windows 7" {
         set root=(hd0,1)
         chainloader +1
         }
```
##### Source: https://www.dedoimedo.com/computers/grub-2.html
```bash
#!/bin/sh -e
echo "Adding my custom Linux to GRUB 2 ..."
cat << EOF
menuentry "My custom Linux" {
        set root=(hd0,2)
        linux /boot/vmlinuz
        initrd /boot/initrd.img
        }
EOF
```
```bash
#!/bin/sh -e
echo "Adding Windows 7 to GRUB 2 menu ... "
cat << EOF
menuentry "Windows 7" {
set root=(hd0,1)
chainloader (hd0,1)+1
}
EOF
```
To get UUID of disks:
`ls -l /dev/disk/by-uuid for UUID`

##### Source: https://unix.stackexchange.com/questions/436112/how-to-install-grub-on-windows-10-dual-boot-with-centos
##### and https://askubuntu.com/questions/135272/how-to-boot-into-windows-7-when-grub-is-installed-in-the-windows-partition
```shell
menuentry "Windows 7 (loader) (on /dev/sda1)" {
        insmod ntfs
        insmod ntldr
        insmod part_msdos
        insmod search_fs_uuid
	set root='(hd0,msdos1)'
        search --fs-uuid --no-floppy --set=root <WINDOWS DISK UUID>
        ntldr /bootmgr
}
````
Difference between GRUB and GRUB2 in drive naming: (hd0,0) is now (hd0,msdos1) when msdos is specified for windows and 1 is the first partition \
GRUB2 on USB:
```shell
grub-install --no-floppy --force --boot-directory=/media/LINUXUSB /dev/sdg1 (? –boot-directory=/mnt/boot /dev/sdb)
```
GRUB2 boot from iso file on disk:
##### Source: https://www.linuxjournal.com/content/grub-boot-iso and http://pendrivelinux.com/downloads/grub.cfg
```shell
set timeout=10 set default=0

menuentry "Run Fedora" {
    loopback loop /Fedora13.iso
    linux (loop)/isolinux/vmlinuz0 boot=isolinux iso-scan/filename=/Fedora13.iso splash --
    initrd (loop)/isolinux/initrd0.img
}

menuentry "Run Ubuntu" {
    loopback loop /ubuntu-10.04-netbook-i386.iso 
    linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=/ubuntu-10.04-netbook-i386.iso splash --
    initrd (loop)/casper/initrd.lz
}

menuentry "Run Clonezilla" {
    loopback loop /clonezilla.iso
    linux (loop)/live/vmlinuz boot=live iso-scan/filename=/clonezilla.iso splash --
    initrd (loop)/live/initrd.img }
```
##### Source: https://www.pcsuggest.com/create-a-multiboot-usb-drive-with-grub-in-linux/
```shell
sudo mkfs.vfat -F 32 -n your_drive_name /dev/sdc1
grub-install --target=i386-pc --boot-directory=/mnt/boot --force /dev/sdc
```
`cfdisk` to set bootable flag on USB and copy isos to boot folder (some other paths could be better here)


### Multiboot USB drive GRUB configuration file
##### Source: https://www.pcsuggest.com
##### File: /boot/grub/grub.cfg
```bash
set timeout=10
set default=0
insmod loopback

menuentry "lubuntu 14.04.1 32 bit" {
loopback loop /boot/lubuntu-14.04.1-desktop-i386.iso
set gfxpayload=keep
linux (loop)/casper/vmlinuz boot=casper iso-scan/filename=/boot/lubuntu-14.04.1-desktop-i386.iso noeject noprompt --
initrd (loop)/casper/initrd.lz
}

menuentry "kali linux 1.0.3 live" {
set iso_file=/boot/kali-linux-1.0.3-amd64.iso
loopback loop $iso_file
linux (loop)/live/vmlinuz boot=live noconfig=sudo username=root hostname=kali noswap noautomount
initrd (loop)/live/initrd.img
}

menuentry "TinyCore Pure64 6.2" {
set iso_file=/boot/TinyCorePure64-6.2.iso
loopback loop $iso_file
linux (loop)/boot/vmlinuz64 loglevel=3 cde vga=normal
initrd (loop)/boot/corepure64.gz
}
```
### Further reading:
Write your own GRUB menu entry:
- mount the Linux installer ISO file of your choic.
- find the path and name of kernel
- find the path and name of initrd
- find the boot time kernel parameters, usually find in the syslinux.cfg or grub.cfg file
- write down them in the ~/multiboot/boot/grub/grub.cfg file

An example grub menu entry:
```shell
menuentry "My Distro Name" {
        set iso_file=/path/to/your_iso_file.iso
        loopback loop $iso_file
        linux (loop)/path/to/your_kernel your_distro_spacific_boot_time_kernel_parameters
        initrd (loop)/path/to/your_initrd_file
}
```