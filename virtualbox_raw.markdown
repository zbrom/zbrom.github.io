---
layout: page
background: '/img/ghorr_banner.png'
title: Virtualbox Raw Disk Access
date: 2017-08-28
categories : dropdown
permalink: /misc/virtualbox_raw/
---

In this tutorial I am going to show you how to change the permissions of a /dev/sdx file to allow you to create a vmdk to boot a Windows installation on another HDD. In this tutorial I am going to use ferb as the user.

NOTE: I have not tried this tutorial with a processor that does not support VT-x/AMD-V. Check your bios to make sure that this is enabled.

____________________________________

<div style="text-align: center;"><span style="background-color: #ff0000; color: #ffffff;">WARNING:<br />
Raw disk access is for expert users only. Incorrect usage can lead to massive data loss. Never mount a drive that is being accessed by a virtual machine. Doing so WILL cause unrecoverable data corruption.</span></div>

As always make sure that you have done backups first.

The first step is to figure out which device contains the Windows install. Run the following command

Code:

<code>fdisk -l</code>

Output:
<div style="height: 200px; width: 900px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto; text-align: left;">
<code>Disk /dev/sda: 60.0 GB, 60022480896 bytes, 117231408 sectors</code><br>
<br>
<code>Units = sectors of 1 * 512 = 512 bytes</code><br>
<br>
<code>Sector size (logical/physical): 512 bytes / 512 bytes</code><br>
<br>
<code>I/O size (minimum/optimal): 512 bytes / 512 bytes</code><br>
<br>
<code>Disk identifier: 0x0009bad8</code><br>
<br>
<code>   Device Boot      Start         End      Blocks   Id  System</code><br>
<br>
<code>/dev/sda1            2048      526335      262144   83  Linux</code><br>
<br>
<code>/dev/sda2          526336    42469375    20971520   83  Linux</code><br>
<br>
<code>/dev/sda3        42469376   117229567    37380096   83  Linux</code><br>
<br>
<code>Disk /dev/sdb: 3000.6 GB, 3000592982016 bytes, 5860533168 sectors</code><br>
<br>
<code>Units = sectors of 1 * 512 = 512 bytes</code><br>
<br>
<code>Sector size (logical/physical): 512 bytes / 4096 bytes</code><br>
<br>
<code>I/O size (minimum/optimal): 4096 bytes / 4096 bytes</code><br>
<br>
<code>Disk /dev/sdc: 60.0 GB, 60022480896 bytes, 117231408 sectors</code><br>
<br>
<code>Units = sectors of 1 * 512 = 512 bytes</code><br>
<br>
<code>Sector size (logical/physical): 512 bytes / 512 bytes</code><br>
<br>
<code>I/O size (minimum/optimal): 512 bytes / 512 bytes</code><br>
<br>
<code>Disk identifier: 0xd4c0c6cf</code><br>
<br>
<code>   Device Boot      Start         End      Blocks   Id  System</code><br>
<br>
<code>/dev/sdc1            2048      206847      102400    7  HPFS/NTFS/exFAT</code><br>
<br>
<code>/dev/sdc2   *      206848   117229567    58511360    7  HPFS/NTFS/exFAT</code><br>
</div>

My Windows install is located at /dev/sdc. The next thing we need to do is to give your user read/write access to this file. Use the following code to see the current permissions of the file.

Code:

<code>ls -l /dev/sdc</code

Output:

<code>brw-rw---- 1 root disk 8, 32 Nov  9 03:06 /dev/sdc</code>

We can see here that the user root has ownership of the file and the group is disk. Both users have rw permissions on the file. So in order to give your user rw permissions to the file you must add your user to the group disk. Use the following code.

Code:

<code>usermod -a -G disk ferb</code>

In order for this to take work you must either reboot or log out after running the above command.

Now that your user has the correct permissions we can continue with the real tutorial. In order to make the vmdk we must use the tool VBoxManage. Run the following command.

Code:

<code>VBoxManage internalcommands createrawvmdk -filename /home/ferb/windows_vm/windows.vmdk -rawdisk /dev/sdc</code>

Now that we have a vmdk file for a rawdisk we need to set up the virtual machine. This is much more user friendly because it has a GUI.

Launch Virtual Box. You should see this:

![](../../img/misc/virtualbox_raw_01.png)

Now click on the icon that says new. You should see this:

![](../../img/misc/virtualbox_raw_02.png)

Now name your virtual machine and select the type and version:

![](../../img/misc/virtualbox_raw_03.png)

Click the next button and set the memory. I used 8GB becasue I have 16GB of ram. You will want to set it somewhere in the green space:

![](../../img/misc/virtualbox_raw_04.png)

Click the next button and browse to your vmdk file:

![](../../img/misc/virtualbox_raw_05.png)

Click create and you should see something like this:

![](../../img/misc/virtualbox_raw_06.png)

Click on settings:

![](../../img/misc/virtualbox_raw_07.png)

Click on System:

![](../../img/misc/virtualbox_raw_08.png)

Click on acceleration and make sure the following are checked:

![](../../img/misc/virtualbox_raw_09.png)

To change the number of processors click on processor:

![](../../img/misc/virtualbox_raw_10.png)

If your Windows is installed on an SSD click on storage:

![](../../img/misc/virtualbox_raw_11.png)

Next click on your vmdk and select the use as SSD box:

![](../../img/misc/virtualbox_raw_12.png)

Then click ok and click on start. My Windows is encrypted with both AES and twofish so I see this screen. (I’ll post a tutorial on Windows full system encryption at a later time):

![](../../img/misc/virtualbox_raw_13.png)

Windows booting:

![](../../img/misc/virtualbox_raw_14.png)

Windows booted:

![](../../img/misc/virtualbox_raw_15.png)

As you can see the virtual machine has the amount of ram and processors that you specified in the settings. The virtual machine however does not have Aero running. You must install guest additions to use Aero.

Click on Devices at the top of the virtualbox window and click on install guest additions. If it asks you to download the image say yes. Once it has finished downloading click mount. It should come up in Autoplay:

![](../../img/misc/virtualbox_raw_16.png)

Click on run:

![](../../img/misc/virtualbox_raw_17.png)

Click next and check the direct3D box:

![](../../img/misc/virtualbox_raw_18.png)

Click NO:

![](../../img/misc/virtualbox_raw_19.png)

Then click OK then click install. When you see the following image check the box and click install:

![](../../img/misc/virtualbox_raw_20.png)

Now it should start installing:

![](../../img/misc/virtualbox_raw_21.png)

When you see the following screen click finish:

![](../../img/misc/virtualbox_raw_22.png)

After rebooting you should be able to enable Aero.
