---
layout: page
background: '/img/ghorr_banner.png'
title: Laptop Brightness Fix
date: 2021-06-28
categories : dropdown
permalink: /misc/laptop_brightness/
---

This tutorial provides a fix for the inability of adjusting brightness on Linux laptops.  The following tutorial has been confirmed as a solution for fixing the brightness controls on an Acer Aspire 5741.  The tutorial is carried out by modifying GRUB.

____________________________________

Edit GRUB with your favorite text editor

<code>nano /etc/default/grub</code>

Add the following entries to these specific lines (do NOT delete any arguments you currently have, e.g. encryption).

Code:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi_backlight=vendor"</code><br>
<code>GRUB_CMDLINE_LINUX="acpi_osi=Linux"</code><br>
</div>
</div>

Update GRUB (e.g for Arch Linux)

<code>grub-mkconfig -o /boot/grub/grub.cfg</code>

*Note, if you are dual booting with Windows, make sure you re-add your Windows entry to /boot/grub/grub.cfg  A tutorial for that may be found [here](../windows_grub){:target="_blank"}.
