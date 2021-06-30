---
layout: page
background: '/img/ghorr_banner.png'
title: Enable Outdated Extensions
date: 2013-04-23
categories : dropdown
permalink: /linux/gnome/gnome_outdated
---

This tutorial deals with enabling extensions that currently are outdated.  While this is not recommended due to lack of testing, some extensions will still maintain functionality on the latest GNOME build.  I have currently enabled Workspace Grid with GNOME 3.8.1 and the extension seems to be working fine.

____________________________________

Launch the gnome debugger tool called looking glass by running the following:

ALT+F2 –> lg

With the console open, click on extensions, then click on View Source for the extension you wish to enable.

![](../../../img/linux/gnome_outdated.png)

Locate the metadata.json file for the given extension, and open it with your favorite text editor

<code>nano metadata.json</code>

Locate shell version and change it to your current build of GNOME (eg: GNOME 3.14).

Restart GNOME

Alt+F2
