---
layout: page
background: '/img/ghorr_banner.png'
title: Add a LiveCD to GRUB
date: 2021-06-28
categories : dropdown
permalink: /misc/livecd_grub/
---

This tutorial explains how to add a LiveCD as an entry for your GRUB menu. This is especially useful for backing up your boot drive, or when you may need to troubleshoot an installation. I have provided an example using Ubuntu LTS; these entries should be similar for other Debian based distributions.

____________________________________

First edit the grub.cfg file, and modify (hd1,2) according to your drive and partition number.

<code>nano /boot/grub/grub.cfg</code>

Code:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>#Ubuntu LiveCD</code><br>
<code>menuentry "Ubuntu 12.04.1 LTS" {</code><br>
<code>set root=(hd1,2)</code><br>
<code>linux /livecd/ubuntu-12.04.1-desktop-amd64/casper/vmlinuz file=/cdrom/livecd/ubuntu-12.04.1-desktop-amd64/preseed/mint.seed rw ignore_uuid root=UUID=0777-0924 rootfstype=ntfs boot=casp$</code><br>
<code>initrd /livecd/ubuntu-12.04.1-desktop-amd64/casper/initrd.lz</code><br>
<code>}</code><br>
</div>
</div>
