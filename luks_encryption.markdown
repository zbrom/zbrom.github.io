---
layout: page
background: '/img/ghorr_banner.png'
title: LUKS Drive Encryption
categories : dropdown
permalink: /security/luks_encryption/
---

This guide will provide basic insight for how one should encrypt a drive using LUKS.  Please make sure all important data is backed up, because the data that you have on drives you are about to encrypt will be completely destroyed.  There are many reasons why you may want to encrypt your drive and you must have one if you are looking here.

________________________________________________________________________________________________________________

#### List your drives

First determine your desired drive; use fdisk or blkid.

<code>fdisk -l</code>

#### Write random data for a HDD

Optional:  Lets say the drive you want to encrypt /dev/sda.  It is good practice to write random data to the drive if it is a HDD.  This will destroy all data.  Do NOT do this on an SSD!  Shred is also another option, if time is a concern with urandom.

<code>dd if=/dev/urandom of=/dev/sda bs=512</code>

(or)

<code>shred /dev/sda</code>

The block size should be equal to your physical sector size for greatest performance when running this command.  Be patient because this could potentially take hours depending on processor performance, disk size, and disk write speeds.

 

#### Zero out an SSD

Optional:  If you are using an SSD you will kill its performance by writing random data to it this way.  Instead you should zero out the drive.  Note: This could potentially expose what type of filesytem that resides in the encrypted container to an attacker. You may also use the secure erase function for your SSD, explained [here](https://wiki.archlinux.org/title/Solid_state_drive/Memory_cell_clearing){:target="_blank"}.

<code>dd if=/dev/zero of=/dev/sda bs=512</code>

 

#### Partitioning

Optional:  The next step is partitioning the disk.  Feel free to setup your partitions how you like.  If you are doing an install, ensure you have an unencrypted 256 MB boot partition; for other applications this is not of concern.  If you don’t require partitioning, you may skip this step.

<code>mkfs.ext4 /dev/sda1</code>

 

#### Encryption

Next I am going to show how to make an encrypted volume for your desired partition or disk.  Set a passphrase that is super secure.  I recommend using a short password with a yubikey static password.  You can get a yubikey [here](https://www.yubico.com/){:target="_blank"}.  For volumes greater than 2TB, use aes-xts-plain64 instead.

<code>cryptsetup -y -s 512 -c aes-xts-plain luksFormat /dev/sda1</code>

(or)

<code>cryptsetup -y -s 512 -c aes-xts-plain64 luksFormat /dev/sda1</code>

Now that you have an encrypted volume you must open this volume and give it a device mapper name.

<code>cryptsetup luksOpen /dev/sda1 encrypted</code>

 

#### Format your drive

<code>mkfs.ext4 /dev/mapper/encrypted</code>

