---
layout: page
background: '/img/ghorr_banner.png'
title: HP Printer Rules
date: 2021-06-29
categories : dropdown
permalink: /misc/hp_printer/
---

When I initially installed Arch Linux, I had some difficulty configuring my HP USB printer to properly work.  Everyone said it would be easier to simply use it as a network printer, but I was persistent and eventually got it working.  One of the final steps needed for the printer to be detected was to modify the 50-udev-default.rules file to give the printer permission to access the USB bus.  Much of this tutorial may be outdated, therefore I am including it under the Misc category. 

____________________________________

Make sure you first have the hplip package installed, which provides the appropriate drivers for HP printers.

<code>pacman -S hplip</code>

Modify /lib/udev/rules.d/50-udev-default.rules to comment out the line
with MODE=”0664″ and make it MODE=”0666″ for the libusb section.

<code>nano /lib/udev/rules.d/50-udev-default.rules</code>

This suppresses most of the messages that looked like this when running xsane:

<code>libusb couldn't open USB device /dev/bus/usb/001/001: Permission denied.</code>

libusb requires write access to USB device nodes.

After applying this mod, a reboot is typically required; your 50-udev-default.rules files should look like this:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>#libusb device nodes</code><br>
<br>
<code>#SUBSYSTEM==”usb”, ENV{DEVTYPE}==”usb_device”, NAME=”bus/usb/$env{BUSNUM}/$env{DEVNUM}”, MODE=”0664″</code><br>
<br>
<code>SUBSYSTEM==”usb”, ENV{DEVTYPE}==”usb_device”, NAME=”bus/usb/$env{BUSNUM}/$env{DEVNUM}”, MODE=”0666″</code><br>
</div>
</div>

Additionally, make your user a member of the lp group.
