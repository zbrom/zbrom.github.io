---
layout: page
background: '/img/ghorr_banner.png'
title: Reduce Titlebar Height
date: 2021-06-30
categories : dropdown
permalink: /linux/gnome/gnome_titlebar
---

Open a terminal and run the following command with root privileges.

<code>sed -i "/title_vertical_pad/s/value=\"[0-9]\{1,2\}\"/value=\"0\"/g" /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml</code>

Adjust value=\”0\ to your liking; I chose 7.

e.g.

<code>sed -i "/title_vertical_pad/s/value=\"[0-9]\{1,2\}\"/value=\"7\"/g" /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml</code>
