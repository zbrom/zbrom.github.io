---
layout: page
background: '/img/ghorr_banner.png'
title: Windows Entry for GRUB
date: 2021-06-27
categories : dropdown
permalink: /linux/windows_grub/
---

This tutorial explains how to add Windows to GRUB if you are dual booting.  This tutorial accounts for whether you are on an UEFI system or BIOS system.

____________________________________
<p></p>
#### BIOS Systems:

First edit the grub.cfg file, and modify (hd1,1) according to your drive and partition number.

<code>nano /boot/grub/grub.cfg</code>

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>#Windows</code><br>
<code>menuentry "Windows" {</code><br>
<code>set root=(hd1,1)</code><br>
<code>chainloader +1</code><br>
<code>}</code><br>
</div>
</div>

<p></p>
#### UEFI Systems:

Determine the UUID for your EFI boot partition on your drive.  Replace /dev/sdb3 with your EFI partition number.

<code>blkid /dev/sdb3</code>

Edit the grub.cfg file, and enter your UUID for the EFI partition from above.

<code>nano /boot/grub/grub.cfg</code>

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>menuentry "Windows 10" {</code><br>
<code>insmod part_gpt</code><br>
<code>insmod fat</code><br>
<code>insmod search_fs_uuid</code><br>
<code>insmod chain</code><br>
<code>search --fs-uuid --no-floppy --set=root [Enter your UUID here]</code><br>
<code>chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi</code><br>
<code>}</code><br>
</div>
</div>

This technique may also be used to add LiveCD entries to your GRUB menu with the following tutorial [here](../../misc/livecd_grub){:target="_blank"}.
