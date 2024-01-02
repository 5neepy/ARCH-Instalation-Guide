# ARCH Instalation Guide by 5neepy

## Checking the internet on the system - Arch Instalation Guide

ping gnu.org

timedatectl set-ntp true

## Check the disk name (sda, sdb etc...) - Arch Instalation Guide

lsblk

cfdisk /dev/your_disk_name // put your disk name on your_disk_name

## 1.Label type
***!!! IF YOU WILL USE EFI CHOOSE GPT***  
gpt - disk > 2TB  
dos - disk < 2TB

## 2.Partitioning

### Boot loader
size: 128M  
press the "B" key to set boot

### Root
size: everything-left

**Write the changes and quit**


## Format your drive - Arch Instalation Guide
``` bash
mkfs.fat -F 32 /dev/sda1 	
mkfs.ext4 /dev/root_partition_name
```
***put your root partition name on root_partition_name, like sda2,*** ^  
**From now on I'll use sda1 for boot and sda2 for root!**

## Mount your partitions

``` bash
mount /dev/sda2 /mnt
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
```

*check if everything is ok*

``` bash
lsblk
```

## Install your base - Arch Instalation Guide
``` bash
pacstrap /mnt base base-devel linux linux-firmware vim
```
**DISCLAMER: This is the longest part**  

## Generate your fstab - Arch Instalation Guide

``` bash
genfstab -U /mnt >> /mnt/etc/fstab
```

## Go in your arch system - Arch Instalation Guide
```bash
arch-chroot /mnt /bin/bash
```
## Enable Wi-Fi on boot and set up GRUB - Arch Instalation Guide
```bash
pacman -S networkmanager grub

systemctl enable NetworkManager

grub-install /dev/sda (or sdb or etc...)

grub-mkconfig -o /boot/grub/grub.cfg
```

## Set your password - Arch Instalation Guide

```bash
passwd
```

## Set your locale.gen - Arch Instalation Guide
```bash
vim /etc/locale.gen
```
**Uncoment the lenguige that you will use**
```bash
:wq
```
**! PRO TIP: This is how you exit vim ^**

```bash
locale-gen
```

```bash
vim /etc/locale.conf
```
```bash
LANG=en_US.UTF-8
```
Or whatever languige you've selected. 
```bash
:wq
```

## Set your hostname - Arch Instalation Guide

```bash
vim /etc/hostname
arch
:wq
```

## Set your time zone

```bash
ln -sf /usr/share/zoneinfo/Europe/... // 
```
**Type your city ^**  

## Exit the chroot

```bash
exit
```

## Unmount the partition - Arch Instalation Guide

```bash
umount -R /mnt
```
## Reboot

```bash
reboot
```
## GG - Arch Instalation Guide
You now can be that guy that uses arch btw :p

*If you want a tutorial for the graphic environment, message me and I will make it.*
