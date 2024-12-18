---
layout: page
background: '/img/ghorr_banner.png'
title: Encrypted LVM/Root
date: 2021-06-25
categories : dropdown
permalink: /arch/encrypted_lvm/
---

So there are many reasons why you may want to encrypt your root partition and you must have one if you are looking here.

There are a million different ways you could set up your partition scheme. I’m just going to show you one way here. I’m going to assume you have a decent amount of experience with Linux because encryption and Arch Linux are not for n00bs.

____________________________________

<div style="text-align: center;"><span style="background-color: #ff0000; color: #ffffff;">WARNING!<br>
FOLLOWING THIS TUTORIAL COULD RESULT IN MASSIVE LOSE OF DATA. ALWAYS BACKUP FIRST.</span></div>

As stated above you should always backup up data. Data that you have on drives that you are about to encrypt will be completely destroyed.First you want to find the drive you want to install to so run.

Code: 

<code>fdisk -l</code>

This is the output on my system.

Code:

<div style="height: 200px; width: 900px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<p><code>Disk /dev/sda: 60.0 GB, 60022480896 bytes, 117231408 sectors</code><code>Units = sectors of 1 * 512 = 512 bytes</code><code>Sector size (logical/physical): 512 bytes / 512 bytes</code><code>I/O size (minimum/optimal): 512 bytes / 512 bytes</code><code>Disk identifier: 0x0009bad8</code></p>
<p><code>   Device Boot      Start         End      Blocks   Id  System</code></p>
<p><code>/dev/sda1            2048      526335      262144   83  Linux</code></p>
<p><code>/dev/sda2          526336    42469375    20971520   83  Linux</code></p>
<p><code>/dev/sda3        42469376   117229567    37380096   83  Linux</code></p>
<p><code>Disk /dev/sdb: 3000.6 GB, 3000592982016 bytes, 5860533168 sectors</code></p>
<p><code>Units = sectors of 1 * 512 = 512 bytes</code></p>
<p><code>Sector size (logical/physical): 512 bytes / 4096 bytes</code></p>
<p><code>I/O size (minimum/optimal): 4096 bytes / 4096 bytes</code></p>
<p><code>Disk /dev/mapper/root: 21.5 GB, 21472739328 bytes, 41938944 sectors</code></p>
<p><code>Units = sectors of 1 * 512 = 512 bytes</code></p>
<p><code>Sector size (logical/physical): 512 bytes / 512 bytes</code></p>
<p><code>I/O size (minimum/optimal): 512 bytes / 512 bytes</code></p>
<p><code>Disk /dev/mapper/data: 3000.6 GB, 3000590884864 bytes, 5860529072 sectors</code></p>
<p><code>Units = sectors of 1 * 512 = 512 bytes</code></p>
<p><code>Sector size (logical/physical): 512 bytes / 4096 bytes</code></p>
<p><code>I/O size (minimum/optimal): 4096 bytes / 4096 bytes</code></p>
<p><code>Disk /dev/mapper/home: 38.3 GB, 38275121152 bytes, 74756096 sectors</code></p>
<p><code>Units = sectors of 1 * 512 = 512 bytes</code></p>
<p><code>Sector size (logical/physical): 512 bytes / 512 bytes</code></p>
<p><code>I/O size (minimum/optimal): 512 bytes / 512 bytes</code></p>
<p><code>Disk /dev/mapper/datadrive-data: 3000.6 GB, 3000588304384 bytes, 5860524032 sectors</code></p>
<p><code>Units = sectors of 1 * 512 = 512 bytes</code></p>
<p><code>Sector size (logical/physical): 512 bytes / 4096 bytes</code></p>
<p><code>I/O size (minimum/optimal): 4096 bytes / 4096 bytes</code></p>
</div>
</div>

Lets say the drive you want to install to is /dev/sda. You would want to write random data to this drive if it is a HDD. This will destroy all data.

Code:

<code>dd if=/dev/urandom of=/dev/sda bs=512</code>

The block size should be equal to your physical sector size for greatest performance when running this command. Be patient because this could potentially take hours depending on processor performance, disk size, and disk write speeds.

If you are using an SSD you will kill its performance by writing random data to it this way. Instead you should zero out the drive.

<div style="text-align: center;"><span style="background-color: #ff0000; color: #ffffff;">Note: This could potentially expose what type of filesytem that resides in the encrypted container to an attacker.</span></div>

Code:

<code>dd if=/dev/zero of=/dev/sda bs=512</code>

The next step is to partition the disk. There are many programs that you use to do this. I assume you know how so I won’t go into great detail here. Create two primary partitions on the drive. Make the first one 256 MB. The second one will take the rest of the drive up.

You should now have two partitions on the drive. Format the 256 MB partition. This partition will be made for /boot.

Code:

<code>mkfs.ext4 /dev/sda1</code>

Next I am going to show how to make an encrypted volume. Set a passphrase that is super secure. I recommend using a short password with a yubikey static password. You can get a yubikey [here](https://www.yubico.com/){:target="_blank"}.

Code:

<code>cryptsetup -y -s 512 -c aes-xts-plain luksFormat /dev/sda2</code>

For drives larger than 2 TB you should use aes-xts-plain64.

Now that you have an encrypted volume you must open this volume and give it a device mapper name.

Code:

<code>cryptsetup luksOpen /dev/sda2 encrypted</code>

If you want to be able to create more than one partition inside of your encrypted volume you will want to create an LVM. I will show how to create a partition for a 20GB root and the rest for /home. I will also show you how to format the new logical volumes.

Code:

<code>pvcreate /dev/mapper/encrypted</code>

<code>vgcreate vg_name /dev/mapper/encrypted</code>

<code>lvcreate -n root -L 20G vg_name</code>

<code>lvcreate -n home -l 100%FREE vg_name</code>

<code>vgchange -ay<code>

<code>mkfs.ext4 /dev/mapper/vg_name-root</code>

<code>mkfs.ext4 /dev/mapper/vg_name-home</code>

From this point you would go about the Arch install, following the [Arch Installation Guide](https://wiki.archlinux.org/title/Installation_guide){:target="_blank"}, with a few modifications that I will show. It is import that we tell the kernel where the root partition is and what parititon must be unlocked.

Code:

<code>blkid /dev/sda2</code>

The output should be something like the following. I have highlighted the important part.

Code:

<code>/dev/sda2: UUID="<span style="background-color: #ff9900;">99ed413f-a4d1-48e5-bdcb-63a5ed351787</span>" TYPE="crypto_LUKS"</code>

Next you need to modify the file /etc/default/grub. Change the line that says GRUB_CMDLINE_LINUX=”” to the following if you are using a HDD.

Code:

<code>GRUB_CMDLINE_LINUX="cryptdevice=/dev/disk/by-uuid/99ed413f-a4d1-48e5-bdcb-63a5ed351787:encrypted root=/dev/mapper/vg_name-root ro"</code>

Also make sure that the line GRUB_DISABLE_LINUX_UUID=true is commeted out.

If you are using an SSD you need to change GRUB_CMDLINE_LINUX=”” to the following line in order for trim to work properly.

Code:

<code>GRUB_CMDLINE_LINUX="cryptdevice=/dev/disk/by-uuid/99ed413f-a4d1-48e5-bdcb-63a5ed351787:encrypted:allow-discards
root=/dev/mapper/vg_name-root ro"</code>

Also make sure that the line GRUB_DISABLE_LINUX_UUID=true is commeted out.

Next you need to modify your /etc/mkinitcpio.conf file. Change the HOOKS array to look like the following.

Code:

<code>HOOKS="base udev autodetect pata scsi sata encrypt lvm2 filesystems usbinput fsck"</code>

Then create an initramfs with the following command.

Code:

<code>mkinitcpio -p linux</code>

Then generate your grub.cfg file with this command.

Code:

<code>grub-mkconfig -o /boot/grub/grub.cfg</code>

Lastly make sure that your /etc/fstab is correct. It should look something like this if you have a HDD.

Code:

<div style="height: 200px; width: 900px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto; text-align: left;">
<div class="sites-codeblock sites-codesnippet-block">
<p><code># /etc/fstab: static file system information</code><code>#</code><code># &lt;file system&gt; &lt;dir&gt;   &lt;type&gt;  &lt;options&gt;       &lt;dump&gt;  &lt;pass&gt;</code><code>tmpfs           /tmp    tmpfs   nodev,nosuid    0       0</code><code>/dev/mapper/vg_name-root        /               ext4            rw,data=ordered 0 0</code></p>
<p><code># UUID=2bac00da-6283-45ab-8ba4-bed8d943218b</code></p>
<p><code>/dev/mapper/vg_name-home        /home           ext4            rw,data=ordered 0 0</code></p>
<p><code># UUID=61386444-0a37-4453-82db-64c803306b7e /dev/sda1</code></p>
<p><code>/dev/disk/by-uuid/61386444-0a37-4453-82db-64c803306b7e                  /boot           ext4            rw,data=ordered       0 0</code></p>
</div>
</div>

If you have a SSD it should look like this.

<div style="height: 200px; width: 900px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto; text-align: left;">
<div class="sites-codeblock sites-codesnippet-block">
<p><code># /etc/fstab: static file system information</code><code>#</code><code># &lt;file system&gt; &lt;dir&gt;   &lt;type&gt;  &lt;options&gt;       &lt;dump&gt;  &lt;pass&gt;</code><code>tmpfs           /tmp    tmpfs   nodev,nosuid    0       0</code><code>/dev/mapper/vg_name-root        /               ext4            rw,noatime,discard,data=ordered 0 0</code></p>
<p><code># UUID=2bac00da-6283-45ab-8ba4-bed8d943218b</code></p>
<p><code>/dev/mapper/vg_name-home        /home           ext4            rw,</code><code><code>noatime,discard,</code>data=ordered 0 0</code></p>
<p><code># UUID=61386444-0a37-4453-82db-64c803306b7e /dev/sda1</code></p>
<p><code>/dev/disk/by-uuid/61386444-0a37-4453-82db-64c803306b7e                  /boot           ext4            rw,noatime,discard,data=ordered       0 0</code></p>
</div>
</div>

If everything has gone correctly you should be able to reboot and will be prompted for your passphrase to unlock your encrypted drive.
