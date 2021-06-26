---
layout: page
background: '/img/ghorr_banner.png'
title: GRUB 2 USB LiveCD Multiboot
date: 2021-06-26
categories : dropdown
permalink: /linux/grub_livecd/
---

This tutorial is has been tested on an Arch Linux system.  If you are not an Arch user, it should still work for your distro; the main difference is that you will need to use your distro’s package manager instead of pacman.

____________________________________

If you currently do not have this package installed, download it

<code>pacman -S grub-bios</code>

Install grub to your USB device MBR (replace sdX, with your device, eg: sda, sdb, … etc.)

<code>grub-install --recheck /dev/sdX</code>

Then generate your grub.cfg file with this command (You may or may not need to initially create the boot folder on your USB device).

<code>grub-mkconfig -o /[path to your device]/boot/grub/grub.cfg</code>

Download your favorite LiveCD ISO (eg: Ubuntu 12.04 LTS).

Extract the ISO to a folder (e.g. name it ubuntu (inside there should be boot, casper, dists, … etc.))

Copy the ubuntu folder to the root of your flash drive (do NOT put it inside the boot folder on the USB).

<code>cp ubuntu /[path to your device]/ubuntu</code>

Navigate to /[path to your device]/boot/grub to edit your grub.cfg with a text editor.

<code>nano /[path to your device]/boot/grub/grub.cfg</code>

Modify the grub.cfg file accordingly (for Ubuntu it should look exactly like this example; feel free to generate additional enteries manually.

Code:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>set timeout=10</code><br>
<code>set default=0</code><br>
<br>
<code>#Ubuntu 12.04</code><br>
<code>menuentry “Ubuntu 12.04 LTS” {</code><br>
<code>linux /ubuntu/casper/vmlinuz file=/cdrom/ubuntu/preseed/ubuntu.seed rw ignore_uuid root=UUID=0777-0924 rootfstype=ntfs boot=casper live-media-path=/ubuntu/casper noprompt quickreboot quiet splash —</code><br>
<code>initrd /ubuntu/casper/initrd.lz</code><br>
<br>
<code>}</code><br>
</div>
</div>
