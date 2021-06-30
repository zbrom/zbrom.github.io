---
layout: page
background: '/img/ghorr_banner.png'
title: Windows 10 MBR (BIOS) to GPT (UEFI)
date: 2017-08-28
categories : dropdown
permalink: /misc/windows_mbr_gpt/
---

These commands may be carried out from a running Windows 10 installation or from a PE environment.

____________________________________

From a running Windows 10 installation, launch Disk Management from the start menu and determine your Disk number for your MBR Windows 10 installation.

![](../../img/misc/windows_mbr_gpt_01.png)

Launch powershell as administrator from the start menu and run the following command (replace 0 with your Disk number):

<code>mbr2gpt /convert /disk:0 /allowfullOS</code>

![](../../img/misc/windows_mbr_gpt_02.png)

This will convert the drive to GPT and make an EFI partition on the drive as well.

From a PE environment, you can use the following command:

<code>mbr2gpt /convert /disk:0</code>

If you need to add your Windows 10 EFI Boot Manager to Grub, check out this [page](../windows_grub){:target="_blank"}.

#### References:

[https://docs.microsoft.com/en-us/windows/deployment/mbr-to-gpt](https://docs.microsoft.com/en-us/windows/deployment/mbr-to-gpt){:target="_blank"}

[https://www.partitionwizard.com/partitionmagic/mbr2gpt.html](https://www.partitionwizard.com/partitionmagic/mbr2gpt.html){:target="_blank"}
