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

Disk partitioning

Determine your desired installation device using the fdisk command (e.g. /dev/sda)
fdisk -l

You may use cfdisk or fdisk to partition your drives; whatever your are more comfortable with is applicable. I chose to partition using cfdisk.
cfdisk /dev/sda

Create the desired number of partitions for your drive. If you wish to do encryption, ensure you have a separate boot and root partition.

Create filesystems for all of the partitions you just created. e.g.
mkfs.ext4 /dev/sda1

If you feel you need a swap, ensure you added a swap partition using cfdisk. After adding the swap partition, use the mkswap command to properly initialize the swap. e.g.
mkswap /dev/sda2

Start the swap
swapon /dev/sda2

Now we must begin mounting our partitions for the installation (first mount your root partition; then mount any other partitions you may have created).
mount /dev/sda1 /mnt/gentoo

Ensure it has a proper filesystem structrure; you should see a lost+found folder
ls /mnt/gentoo

If needed create directories for any additional partitions to be mounted using the mkdir command; then mount those partitions using the mount command as previously mentioned.

 

Configure Date / Download tarball

Before we start the installation, ensure the system date is set properly using the date command. UTC time is desired.
date

If the date were not correct, you can issue the following command to set it to a given time and date (e.g. 10 August 2013 at 21:00 would be entered as below).
date 81721002013

Change directory to the root partition that you just mounted
cd /mnt/gentoo

We will be using the Links CLI browser to download the stage 3 tarball
links http://gentoo.org/main/en/mirrors.xml

Select a nearby mirror (e.g. Argonne National Laboratory). Click the mirror → Click releases → Click amd64 → Click current-stage3 → Click default → Click the most current date → Select the latest stage3-amd64 tar.bz2 file to download

Exit Links with q

 

Extract / Configure Flags

Extract the downloaded package to your root partition (e.g. /mnt/gentoo)
tar -xjpf stage3-amd64*

Now we need to install the portage package manager
links http://gentoo.org/main/en/mirrors.xml

Select a nearby mirror (e.g. Argonne National Laboratory). Click the mirror → Click snapshots → Click amd64 → Scroll down and select the file portage-latest.tar.bz2 to download

Extract the downloaded package to your root partition (e.g. /mnt/gentoo), and copy it to the usr/ directory
tar -xvjf portage-latest.tar.bz2 -C usr/

Once portage is done unpacking, the next step is to set the gcc compiler flags
nano /etc/portage/make.conf

Visit the gentoo gcc optimization guide for more information. In this example we will use the -march=native option for CFLAGS
CFLAGS="-march=native -02 -pipe"

Set MAKEOPTS to one more that the number of processing cores you have (e.g. for a dual core processor)
MAKEOPTS="-j3"

 

Chroot

It is almost time to chroot into the new gentoo environment, but we first need to copy the DNS information over.
cp -L /etc/resolv.conf /mnt/gentoo/etc/resolv.conf

Now we need to mount some of the necessary filesystems
mount -t proc none /mnt/gentoo/proc
mount -rbind /sys /mnt/gentoo/sys
mount -rbind /dev /mnt/gentoo/dev

Now we can chroot into the new environment
chroot . /bin/bash

Run the command env-update

Run source /etc/profile

Update the PS1 so you can identify that you are in the chrooted environment
export PS1=“(chroot) $PS1”

Update the portage tree using the following command
emerge --sync

 

Profile / Timezone

Select the profile; the building block for a gentoo system. It has values for the USE and CFLAGS variables. You will use the following command to view all the available profiles.
eselect profile list

Pick your desired environment (e.g. gnome users would select 4)
eselect profile set 4

Make sure the desired profile was properly set
eselect profile list

Now lets set the USE variable in the make.conf file
nano /etc/portage/make.conf

For a gnome setup, set the USE variable as follows (for a full listing of the available USE flags please see the gentoo handbook here.
USE=“$USE alsa dvd gnome gtk pulseaudio -kde”

Now we will set the timezone; determine your desired timezone
ls /usr/share/zoneinfo

Copy the desired timezone file (e.g. US Central) to /etc/localtime
cp /usr/share/zoneinfo/US/Central /etc/localtime

Echo whatever file you selected into the /etc/timezone file
echo “US/Central” > /etc/timezone


Kernel

Now we need to download the kernel source code
emerge gentoo-sources

Next you have a couple of options to choose from, one is configuring the kernel manually, another option which is much easier and simpler is to simply emerge genkernel. I will be utilizing the later option due to time constraints.
emerge genkernel

Once genkernel is done installing, run the following command to compile the sources for your system.
genkernel all

The generated files will be in /boot after genkernel finishes compiling. You will have a kernel file and an initrd
ls /boot/kernel*
ls /boot/initramfs*

Now we need to configure the kernel modules. For this we will use the find command.  This command will need to be changed corresponding to the version of gentoo downloaded.
find /lib/modules/3.5.7-gentoo/ -type f -iname '*.o' -or -iname '*.ko' | less

Keep note of the ones you will need for the next step :smiley:
