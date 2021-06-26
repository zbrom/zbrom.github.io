---
layout: page
background: '/img/ghorr_banner.png'
title: Fonts
date: 2013-08-01
categories : dropdown
permalink: /arch/fonts/
---

Arch Linux only comes with the bare minimum essential fonts.  I had not realized it was necessary to install additional fonts until after libreoffice was installed.  This guide will provide the user with some useful fonts for a typical Arch install.  For additional fonts please visit the [Arch Wiki](https://wiki.archlinux.org/index.php/Fonts){:target="_blank"}.

____________________________________

##### Font Installation:

For compatibility with office documents, I recommend installing Microsoft Fonts and the Liberation Fonts.

<code>pacman -S ttf-liberation && yaourt -S ttf-ms-fonts</code>

I frequently use Chinese, Korean, Japanese characters in filenames; the following asian fonts are optional if you desire the compatibility.

<code>pacman -S ttf-hannom ttf-baekmuk && yaourt -S ttf-vlgothic</code>

##### Xorg Configuration:

After installing desired fonts, the font paths must be added to the xorg file.

Go to /usr/share/fonts/ to display all installed fonts.

![](../../img/arch/fonts.png)

Edit your xorg config file with your favorite text editor:

<code>nano /etc/X11/xorg.conf</code>

Here is a sample xorg configuration, you must modify it to match the fonts installed in your fonts folder; then add it to xorg.conf.

Code:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code># Let X.Org know about the custom font directories</code><br>
<code>Section "Files"</code><br>
<code>FontPath "/usr/share/fonts/75dpi"</code><br>
<code>FontPath "/usr/share/fonts/100dpi"</code><br>
<code>FontPath "/usr/share/fonts/cyrillic"</code><br>
<code>FontPath "/usr/share/fonts/encodings"</code><br>
<code>FontPath "/usr/share/fonts/kanjistrokeorders"</code><br>
<code>FontPath "/usr/share/fonts/misc"</code><br>
<code>FontPath "/usr/share/fonts/TTF"</code><br>
<code>FontPath "/usr/share/fonts/util"</code><br>
<code>EndSection</code>
</div>
</div>

All your fonts should now be recognized; a reboot may be required.

##### References:

[https://wiki.archlinux.org/index.php/Fonts](https://wiki.archlinux.org/index.php/Fonts){:target="_blank"}
