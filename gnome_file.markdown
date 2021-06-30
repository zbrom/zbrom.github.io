---
layout: page
background: '/img/ghorr_banner.png'
title: File Associations
date: 2021-06-30
categories : dropdown
permalink: /linux/gnome/gnome_file
---

This tutorial deals with changing the default file associations in GNOME 3.  For some cases, an application may not appear when you right click on the file –> Choose Open With –> Choose Other Applications.  This will correct the association and allow you to choose default applications with ease.

____________________________________

First locate the application (.desktop file) in /usr/share/applications.

Edit the desired file with your favorite text editor

<code>nano /usr/share/applications/[your application].desktop</code>

Modify the Exec line to look like

<code>Exec=yourprogram %U</code>

The application should now appear in your application list.
