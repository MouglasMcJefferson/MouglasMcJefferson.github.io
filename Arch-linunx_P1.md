# Arch Install 
Used this installization guide https://wiki.archlinux.org/title/Installation_guide

## Pre-Installation
Downloaded from second mit.edu from 2022.10.01

Booted straight to iso so no need for a medium

Did not have key so started unlicensed workstation pro 17

Boot kept timing out so reinstalled and verified signature and this fixed problem 

- Selected file location
- Selected operating system as linux kernel 64-bit
- Changed disk size from 8 to 20 GB in size
- customized hardware to give 2 GB of ram
- Went to vmx file and added firmware=”efi” to line 2 of file
- booted in efi mode
## Once Booted

Used to verify boot mode

    ls /sys/firmware/efi/efivars

Used this command to test for internet

	ip link


had problem with ethernet so did not show up first time, tested with google
	
    ping google.com
Updated the system clock

	timedatectl


## Partitioning/Formating Disks
Set up partioning

	fdisk -l
	fdisk /dev/sda, 
Then for partition 1 I entered:
    
    m, p, n, p, enter, enter, +500MB, p
For partition 2 I used:
    
    n, 2, enter, enter, enter, p, w

	mkfs.ext4 /dev/sda2

    mkfs.fat -F 32 /dev/sda1
Used this command to format partitioned drives

mkfs.ext4/dev/sda2 did not have a space so i used this command to bypass problem (spelling error)
    
    sudo mkfs -t ext4 /dev/sda2

Followed this walkthrough for errors that occured throught the installization process and to double check my steps along the way: https://www.youtube.com/watch?v=sgWAj0Vhhd4&ab_channel=DebugDomain
    
Then needed to mount the Drives and make sure they were there

	mount /dev/sda2 /mnt
	mount --mkdir /dev/sda1 /mnt/boot
	ls /mnt 
	
## Install Essential Packages
	pacstrap -K /mnt base linux linux-firmware
	
Install failed so restarted back from booting up the enviorment till I reached this point again

same issue occured so I reinstalled and that fixed the problem
## SyStem Configuration
Mount location and used to show mnts but did not show anything
	genfstab -U /mnt >> /mnt/etc/fstab
	nano mnt/etc/fstab


mnt wasn't doing anything

spent ~40 min trying to fix so went and reinstalled a 2nd time back form begining

    nano /mnt/etc/fstab

realized problem was used mnt/ instead of /mnt/ after second reinstall     

Saw they were triple mounted due to typo issue so unmounted twice
    "umount -R /mnt"



Changed root into new system

	arch-chroot /mnt

Set up time and place

	ln -sf /usr/share/zoneinfo/
	ln -sf /usr/share/zoneinfo/America
	ln -sf /usr/share/zoneinfo/America/Ohio /etc/localtime
	hwclock --systohc
	pacman -S nano


nano download keeps corrupting, tried with vim and same thing

Used > to write to file instead of editing

	en_US.UTF-8 UTF-8 > /etc/locale.gen
	Lang=en_us.UTF-8 > /etc/locale.config
	D-man > /etc/hostname
	
## Users and Passwords
Set uop root password

	psasswd
	Douglas1 

(nice and secure)

created user Codi and Douglas with set passwords

    user add -m Codi
    user add -m Douglas
    passwd codi
    GraceHopper1906
    passwd Douglas
    Password123


pacman -s sudo  (still corrupt, did not work)

Now installed bootloader

	grub-instgall--target=x86_64-efi --efi-directory=boot --bootloader-id=grub_uefi
This install worked...

Now unmount and reboot

    grub-mkconfig -o /boot/grub/grub.cfg
    umount -R /mnt
	reboot
## After Reboot into System
Logged into D-man@root, D-man@Codi, and D-man@Douglas

could not use any commands except nano

COULD NOT FIX SO 4TH RESTART FROM 1.1

same issue at post install so kept 4th one and just made a 5th one

will add more when progress is made

No progress made
