---
layout: page
background: '/img/ghorr_banner.png'
title: Map Windows Key to KMenu
date: 2021-06-30
categories : dropdown
permalink: /misc/windows_kmenu/
---

This tutorial explains how to map the Windows key to open KMenu in KDE

____________________________________

Open a Konsole window

Find the key to which Super_L (the Windows key comes up as Super_L) is mapped by running xev (it will open a small window that waits for your keyboard input and displays it in the console window where xev was started. Closing the window will cause xev to terminate.

Code:

xev | grep Super_L

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>state 0x0, keycode 133 (keysym 0xffeb, Super_L), same_screen YES,</code><br>
<code>state 0x40, keycode 133 (keysym 0xffeb, Super_L), same_screen YES,</code><br>
</div>
</div>

The keycode above came from my keyboard. Please run xev to determine what your keycode is.

Create a file under ~/.kde/Autostart to remap the above discovered keycode to F13. I called my file win-key.sh as per the doc at Mepis (also Mepis mentioned mapping the keycode to the string Menu, but that did not work for me).

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>#!/bin/bash</code><br>
<code>xmodmap -e 'keycode 133 = F13'</code><br>
</div>
</div>

Make the script you created in Step 3 executable:

<code>chmod +x ~/.kde/Autostart/win-key.sh</code>

Execute the script manually (it will be executed every time you restart)

<code>~/.kde/Autostart/win-key.sh</code>

Confirm the keycode has been mapped to F13

Code:

<code>xev | grep F13</code>

Output:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>state 0x0, keycode 133 (keysym 0xffca, F13), same_screen YES,</code><br>
<code> state 0x40, keycode 133 (keysym 0xffca, F13), same_screen YES,</code><br>
</div>
</div>

KMenu –> Search: Global Keyboard Shortcuts –> KDE Component: Plasma Desktop Shell –> Activate Application Launcher Widget –> Custom (Click None)

    Press the Windows Key and None should change to F13
    
Click OK.

The Windows key should now activate the KMenu. Remember, if you have programs using the Windows key as the Meta key then your programs will now be broken (I lied when I said I would only warn you once).

##### References:

[https://cvalcarcel.wordpress.com/2012/01/07/kubuntu-11-10-mapping-the-windows-key-to-activate-kmenu/](https://cvalcarcel.wordpress.com/2012/01/07/kubuntu-11-10-mapping-the-windows-key-to-activate-kmenu/){:target="_blank"}
