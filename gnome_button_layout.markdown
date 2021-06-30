---
layout: page
background: '/img/ghorr_banner.png'
title: Move Close, Maximize, & Minimize to the Left
date: 2014-10-20
categories : dropdown
permalink: /linux/gnome/gnome_button_layout
---

In the latest GNOME update to GNOME 3.14, there is a different method required to move the window buttons in GNOME. This tutorial will outline an easy customization scheme.

____________________________________

If not already installed, install gnome-tweak-tool

Open gnome-tweak-tool

<code>gnome-tweak-tool</code>

Click on Windows, and ensure that Maximize and Minimize are turned on.

![](../../../img/linux/gnome_button_layout_01.png)

Open dconf-editor using terminal or alt-F2

<code>dconf-editor</code>

Navigate to the following:

<code>org.gnome.desktop.wm.preferences</code>

Adjust the button-layout to read:

<code>close,maximize,minimize</code>

![](../../../img/linux/gnome_button_layout_02.png)
