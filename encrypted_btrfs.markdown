---
layout: page
background: '/img/ghorr_banner.png'
title: Encrypted BTRFS Root with EFI
categories : dropdown
permalink: /arch/encrypted_btrfs/
---

So there are many reasons why you may want to encrypt your root partition and you must have one if you are looking here.

There are a million different ways you could set up your partition scheme. I’m just going to show you one way here. I’m going to assume you have a decent amount of experience with Linux because encryption and Arch Linux are not for n00bs.

First, boot the Arch Linux Live CD off a UEFI Flash Drive.

____________________________________

Preliminary:

Update repos:

<code>pacman -Syy</code>

OPTIONAL AMAZING STEP – Configure your system from a remote terminal:

systemctl start sshd
Preparing your Drive:

If installing to an SSD, make sure to Secure Erase your drive; if installing to an HDD, make sure to write random data to your drive before proceeding.
Create GPT Partitions:

gdisk /dev/sda

press o – to create a new empty GUID partition table (GPT)

————–

CREATE 1st PARTITION FOR BOOT:

press n – to create new partition

First Sector – just leave defaults so hit enter

Last Sector – just put “256M” without quotes and hit enter, this makes a 256M partition

Hex code: type “ef00” and hit enter – this is necessary for EFI

It should now take you back to main menu

OUTPUT SHOULD LOOK LIKE THIS FOR 1st PARTITION:

Command (? for help): n

Partition number (1-128, default 1):

First sector (34-500118158, default = 2048) or {+-}size{KMGTP}:

Last sector (2048-500118158, default = 500118158) or {+-}size{KMGTP}: 256M

Current type is ‘Linux filesystem’

Hex code or GUID (L to show codes, Enter = 8300): ef00

Changed type of partition to ‘EFI System’

————–

CREATE 2nd PARTITION FOR ROOT/DATA:

press n – to create new partition

First Sector – just leave defaults so hit enter

Last Sector – just leave default so hit enter – this will select the remaining space for data

Hex code: type “8300” and hit enter (or just hit enter as 8300 is the default) – this is for data

OUTPUT SHOULD LOOK LIKE THIS FOR 3rd PARTITION:

Partition number (2-128, default 2):

First sector (34-500118158, default = 16779264) or {+-}size{KMGTP}:

Last sector (16779264-500118158, default = 500118158) or {+-}size{KMGTP}:

Current type is ‘Linux filesystem’

Hex code or GUID (L to show codes, Enter = 8300):

Changed type of partition to ‘Linux filesystem’

————–

CONFIRM

Confirm you have 2 partitions with about the same settings as this (if your swap or data are different sizes that’s cool)

After creating the 2nd partition it should of brought you to main menu, at the main menu press “p” to see the current pending partition table (its not written to disk just yet)

OUTPUT SHOULD LOOK LIKE THIS:

Command (? for help): p

Disk /dev/sda: 500118192 sectors, 238.5 GiB

Logical sector size: 512 bytes

Disk identifier (GUID): 8E8C0F70-22D8-4FE6-A5AB-E20A0483C2F5

Partition table holds up to 128 entries

First usable sector is 34, last usable sector is 500118158

Partitions will be aligned on 2048-sector boundaries

Total free space is 6108 sectors (3.0 MiB)

Number Start (sector) End (sector) Size Code Name

1 2048 614400 256.0 MiB EF00 EFI System

3 616448 500118158 230.5 GiB 8300 Linux filesystem

SAVE

Save everything after confirmation

Press w to write to disk

Press Y to confirm

————–

Make the FAT 32 system for EFI boot:

mkfs.vfat -F32 /dev/sda1

————–
Setting up the Encrypted Filesystem:

Next I am going to show how to make an encrypted volume. Set a passphrase that is super secure. I recommend using a short password with a yubikey static password. You can get a yubikey here.

Code:

cryptsetup -y -s 512 -c aes-xts-plain64 luksFormat /dev/sda2

Now that you have an encrypted volume you must open this volume and give it a device mapper name.

Code:

cryptsetup luksOpen /dev/sda2 encrypted

Now we will format /dev/mapper/encrypted to btrfs:

mkfs.btrfs /dev/mapper/encrypted

————–
Subvolume Configuration:

We will now make our ROOT subvolume, this will be a folder called ROOT located at the root of /dev/mapper/encrypted. The way we will design this is that when the system boots we will not see /ROOT, we will be inside ROOT. Inside ROOT you will have all of your etc, sys, proc, etc.

mount /dev/mapper/encrypted /mnt

cd /mnt

btrfs subvolume create /mnt/ROOT

This should show you your ROOT

btrfs subvolume list -a /mnt

Something like this: ID 256 gen 5 top level 5 path ROOT

cd /

umount /dev/mapper/encrypted

Now we will mount the ROOT subvolume as /mnt and we will dump the arch system into there with pacman. We will also enable compress to utilize btrfs compress feature.

mount -o defaults,compress,subvol=ROOT /dev/mapper/encrypted /mnt

cd /mnt

mkdir /mnt/boot

mount /dev/sda1 /mnt/boot
Install the Base System:

Pacstrap the Arch Linux base:

pacstrap -i /mnt base base-devel

Note it might ask confirmation steps requiring either to press “enter” to accept all selections or Y and enter. Just select whichever option downloads everything.

genfstab -U -p /mnt >> /mnt/etc/fstab

————–

By default fstab for vfat thats generated by genfstab picks a value that makes the filesystem check too often for vfat, in fact we need to change it to never doing a filesystem check because vfat (or else it will complain later, so in there we change the value from 2 to 0, meaning never doing filesystem check)

nano /mnt/etc/fstab

Change this:

# /dev/sda1

UUID=C218-8694 /boot vfat rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0 2

To this:

# /dev/sda1

UUID=C218-8694 /boot vfat rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0 0

————–

Finally make sure in that fstab file you see: “defaults,compress,subvol=ROOT” on /mnt.

Lets chroot into the /mnt folder:

arch-chroot /mnt

From this point you would go about the Arch install the same way you would using the wiki found here. With a few modifications that I will show. It is import that we tell the kernel where the root partition is and what parititon must be unlocked.

Code:

blkid /dev/sda2

The output should be something like the following.

Code:

/dev/sda2: UUID="99ed413f-a4d1-48e5-bdcb-63a5ed351787" TYPE="crypto_LUKS"

Next you need to modify the file /etc/default/grub. Change the line that says GRUB_CMDLINE_LINUX=”” to the following; if you are using an SSD, allow-discards is necessary for trim to work properly.

Code:

GRUB_CMDLINE_LINUX="rootflags=subvol=ROOT cryptdevice=/dev/disk/by-uuid/99ed413f-a4d1-48e5-bdcb-63a5ed351787:encrypted:allow-discards root=/dev/mapper/encrypted"

Also make sure that the line GRUB_DISABLE_LINUX_UUID=true is commeted out.

Next you need to modify your /etc/mkinitcpio.conf file. Change the HOOKS array to look like the following.

Code:

HOOKS="base udev autodetect encrypt modconf block filesystems keyboard btrfs"

Then create an initramfs with the following command.

Code:

mkinitcpio -p linux
Setting up the EFI Bootloader with GRUB 2:

Grub exists for BIOS mbr and gpt boots, but also for EFI. Efi supports many more bootloaders, infact it supports no bootloader (and it will load your OS) that’s called EFISTUB.

mount -t efivarfs efivarfs /sys/firmware/efi/efivars

pacman -S grub efibootmgr

grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=Arch_GRUB --recheck

grub-mkconfig -o /boot/grub/grub.cfg

We are hoping for output like this from the grub-install command:

Installation finished. No error reported.

Exit from the chroot environment:

exit

Since the partitions are mounted under /mnt, we use the following command to unmount them:

We mounted a few things into mnt, lets unmount all of them recursively:

umount -R /mnt

Lets reboot, in my case it comes right up 🙂

reboot
References:

http://www.kossboss.com/linux—arch-installation-with-btrfs-root-and-efi-grub-boot

https://wiki.archlinux.org/index.php/Installation_guide
