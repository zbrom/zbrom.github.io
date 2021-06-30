---
layout: page
background: '/img/ghorr_banner.png'
title: Gentoo Installation
date: 2013-08-10
categories : dropdown
permalink: /linux/gentoo_install/
---

The ghorr staff completed a successful Gentoo installation on 10 August 2013 utilizing the following guide.  For further reference, check out the official [Gentoo documentation](https://wiki.gentoo.org/wiki/Handbook:AMD64/Full/Installation){:target="_blank"}.

____________________________________

![](../../img/linux/gblend-150x150.png){:style="float: left;margin-right: 7px;margin-top: 7px;"}

#### Gentoo Installation

<p></p>
##### *Prior to installation*

Go to [https://www.gentoo.org/downloads](https://www.gentoo.org/downloads){:target="_blank"} and download the latest install-amd64-minimal iso

Prepare a bootable drive for the ISO (use dd command, UNetbootin, or drivedroid for Android)

Boot the device

Select your keyboard layout (41 for US)

##### *Beginning the installation*

Check for a working network connection (e.g. ping google.com)

If you have no working network connection, try using the net-setup command to start the desired network interface

<code>net-setup eth0</code>

##### *Disk partitioning*

Determine your desired installation device using the fdisk command (e.g. /dev/sda)

<code>fdisk -l</code>

You may use cfdisk or fdisk to partition your drives; whatever your are more comfortable with is applicable. I chose to partition using cfdisk.

<code>cfdisk /dev/sda</code>

Create the desired number of partitions for your drive. If you wish to do encryption, ensure you have a separate boot and root partition.

Create filesystems for all of the partitions you just created. e.g.

<code>mkfs.ext4 /dev/sda1</code>

If you feel you need a swap, ensure you added a swap partition using cfdisk. After adding the swap partition, use the mkswap command to properly initialize the swap. e.g.

<code>mkswap /dev/sda2</code>

Start the swap

<code>swapon /dev/sda2</code>

Now we must begin mounting our partitions for the installation (first mount your root partition; then mount any other partitions you may have created).

<code>mount /dev/sda1 /mnt/gentoo</code>

Ensure it has a proper filesystem structrure; you should see a lost+found folder

<code>ls /mnt/gentoo</code>

If needed create directories for any additional partitions to be mounted using the mkdir command; then mount those partitions using the mount command as previously mentioned.

##### *Configure Date / Download tarball*

Before we start the installation, ensure the system date is set properly using the date command. UTC time is desired.

<code>date</code>

If the date were not correct, you can issue the following command to set it to a given time and date (e.g. 10 August 2013 at 21:00 would be entered as below).

<code>date 81721002013</code>

Change directory to the root partition that you just mounted

<code>cd /mnt/gentoo</code>

We will be using the Links CLI browser to download the stage 3 tarball

<code>links http://gentoo.org/main/en/mirrors.xml</code>

Select a nearby mirror (e.g. Argonne National Laboratory). Click the mirror → Click releases → Click amd64 → Click current-stage3 → Click default → Click the most current date → Select the latest stage3-amd64 tar.bz2 file to download

Exit Links with q

##### *Extract / Configure Flags*

Extract the downloaded package to your root partition (e.g. /mnt/gentoo)

<code>tar -xjpf stage3-amd64*</code>

Now we need to install the portage package manager

<code>links http://gentoo.org/main/en/mirrors.xml</code>

Select a nearby mirror (e.g. Argonne National Laboratory). Click the mirror → Click snapshots → Click amd64 → Scroll down and select the file portage-latest.tar.bz2 to download

Extract the downloaded package to your root partition (e.g. /mnt/gentoo), and copy it to the usr/ directory

<code>tar -xvjf portage-latest.tar.bz2 -C usr/</code>

Once portage is done unpacking, the next step is to set the gcc compiler flags

<code>nano /etc/portage/make.conf</code>

Visit the gentoo gcc optimization guide for more information. In this example we will use the -march=native option for CFLAGS

<code>CFLAGS="-march=native -02 -pipe"</code>

Set MAKEOPTS to one more that the number of processing cores you have (e.g. for a dual core processor)

<code>MAKEOPTS="-j3"</code>

##### *Chroot*

It is almost time to chroot into the new gentoo environment, but we first need to copy the DNS information over.

<code>cp -L /etc/resolv.conf /mnt/gentoo/etc/resolv.conf</code>

Now we need to mount some of the necessary filesystems

<code>mount -t proc none /mnt/gentoo/proc</code>

<code>mount -rbind /sys /mnt/gentoo/sys</code>

<code>mount -rbind /dev /mnt/gentoo/dev</code>

Now we can chroot into the new environment

<code>chroot . /bin/bash</code>

Run the following command:

<code>env-update</code>

Run the following command:

<code>source /etc/profile</code>

Update the PS1 so you can identify that you are in the chrooted environment

<code>export PS1=“(chroot) $PS1”</code>

Update the portage tree using the following command

<code>emerge --sync</code>

##### *Profile / Timezone*

Select the profile; the building block for a gentoo system. It has values for the USE and CFLAGS variables. You will use the following command to view all the available profiles.

<code>eselect profile list</code>

Pick your desired environment (e.g. gnome users would select 4)

<code>eselect profile set 4</code>

Make sure the desired profile was properly set

<code>eselect profile list</code>

Now lets set the USE variable in the make.conf file

<code>nano /etc/portage/make.conf</code>

For a gnome setup, set the USE variable as follows (for a full listing of the available USE flags please see the gentoo handbook here.

<code>USE=“$USE alsa dvd gnome gtk pulseaudio -kde”</code>

Now we will set the timezone; determine your desired timezone

<code>ls /usr/share/zoneinfo</code>

Copy the desired timezone file (e.g. US Central) to /etc/localtime

<code>cp /usr/share/zoneinfo/US/Central /etc/localtime</code>

Echo whatever file you selected into the /etc/timezone file

<code>echo “US/Central” > /etc/timezone</code>

##### *Kernel*

Now we need to download the kernel source code

<code>emerge gentoo-sources</code>

Next you have a couple of options to choose from, one is configuring the kernel manually, another option which is much easier and simpler is to simply emerge genkernel. I will be utilizing the later option due to time constraints.

<code>emerge genkernel</code>

Once genkernel is done installing, run the following command to compile the sources for your system.

<code>genkernel all</code>

The generated files will be in /boot after genkernel finishes compiling. You will have a kernel file and an initrd

<code>ls /boot/kernel*</code>

<code>ls /boot/initramfs*</code>

Now we need to configure the kernel modules. For this we will use the find command.  This command will need to be changed corresponding to the version of gentoo downloaded.

<code>find /lib/modules/3.5.7-gentoo/ -type f -iname '*.o' -or -iname '*.ko' | less</code>

Keep note of the ones you will need for the next step 😀

Edit the following file
<code>nano /etc/conf.d/modules</code>

Uncomment the line modules, and replace ohci1394 with whatever kernel modules you will need (e.g. iwlwifi).

The kernel is now configured!

##### *Fstab*

Create your fstab

<code>nano -w /etc/fstab</code>

Add all of the partitions you created during partitioning to the fstab (e.g. the root partition sould look like this).

<code>/dev/sda1 / ext4 noatime 0 1</code>

##### *Network*

Add a hostname for your network. e.g.

<code>nano /etc/conf.d/hostname</code>

<code>hostname=“ghorr”</code>

We also need to edit the host file

<code>nano /etc/hosts</code>

On the line containing your local loopback, put the hostname you just set before localhost. e.g.

<code>127.0.0.1 ghorr localhost</code>

Edit the net file

<code>nano /etc/conf.d/net</code>

You need to enter the following

<code>config_eth0=“dhcp”</code>

In order to activate the network at boot, we will need to create an init script for it.

Change directory to the following:

<code>cd /etc/init.d</code>

Create the following sym link for eth0

<code>ln -s net.lo net.eth0</code>

The sym link has now been created; next we must add it to the default run level

<code>rc-update add net.eth0 default</code>

In order for gentoo to automatically obtain an IP address, we need to install dhcpcd

<code>emerge dhcpcd</code>

##### *Root Password / locale*

Set the root password; issue the following command, then enter your desired password.

<code>passwd</code>

Modify the hwclock file to how your hardware clock is set. Leave it as is for UTC.

<code>nano -w /etc/conf.d/hwclock</code>

Modify the local.gen file for the languages you will be using (e.g. uncomment en_US.UTF-8 UTF-8)

Set the default language

<code>nano -w /etc/env.d/02locale</code>

Enter the following e.g.

<code>LANG=“en_US.UTF-8”</code>

<code>LC_COLLATE=“C”</code>

Generate your locales that were selected

<code>locale-gen</code>

Now do an environment update

<code>env-update && source /etc/profile</code>

Reset your chroot indicator

<code>export PS1=“(chroot) $PS1”</code>

#### *Grub*

Configure your grub bootloader

<code>emerge grub</code>

Now we have to configure the grub menu entries

<code>nano -w /boot/grub/grub.conf</code>

We need to know the location of the kernel file and the initramfs file

<code>ls /boot/*genkernel-x86* >> /boot/grub/grub.conf</code>

<code>nano -w /boot/grub/grub.conf</code>

Configure the grub entry for your particular drive, feel free to include a rescue kernel if desired. Here is an example:

<div style="height: 200px; width: 900px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>title Gentoo Linux</code><br>
<code>root (0,1)</code><br>
<code>kernel /boot/kernel-genkernel-x86_64-3.5.7-gentoo root=/dev/sda1</code><br>
<code>initrd /boot/kernel-initramfs-x86_64-3.5.7-gentoo</code><br>
<br>
<code>title Gentoo Linux (rescue)</code><br>
<code>root (0,1)</code><br>
<code>kernel /boot/kernel-genkernel-x86_64-3.5.7-gentoo root=/dev/sda1 init=/bin/bb</code><br>
<code>initrd /boot/kernel-initramfs-x86_64-3.5.7-gentoo</code><br>
</div>
</div>

*During our Gentoo install, we had some minor issues during the grub installation.  Please ensure that the lines shown above are uncommented (during our installation, we initially neglected to uncomment title).

Install grub to your MBR

<code>grep -v rootfs /proc/mounts > /etc/mtab</code>

<code>grub-install --nofloppy /dev/sda</code>

Exit the chroot environment, unmount your partitions, and reboot

<code>exit</code>

<code>unmount -l /mnt/gentoo/dev{/shm,/pts,}</code>

<code>unmount -l /mnt/gentoo/proc</code>

<code>reboot</code>

Hopefully your new Gentoo installation properly boots! Enjoy!

Feel free to create additional users, install a GUI, and remove the package files used during installation.
