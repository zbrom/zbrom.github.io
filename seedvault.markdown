---
layout: page
background: '/img/ghorr_banner.png'
title: Restore SeedVault Backup with ADB
date: 2021-08-22
categories : dropdown
permalink: /linux/android/seedvault/
---

SeedVault is an [open source](https://github.com/seedvault-app/seedvault){:target="_blank"} encrypted backup solution that can be used with the Android operating system.  It is an excellent alternative to using Google's cloud based online backup.  SeedVault can be used to backup your device locally or to a NextCloud server.  It allows for easy app and app data backups, without the need for root on your device.  Additionally, it will restore app data if you uninstall and reinstall apps.

This tutorial explains how to restore a backup onto a new build of Android.  If you need to wipe your device and reinstall, this will allow you to restore your previously installed apps with app data more easily.

____________________________________

First make sure you can execute the adb command on your computer.  On Arch Linux, the package [android-tools](https://archlinux.org/packages/community/x86_64/android-tools){:target="_blank"} provides adb.

Enable USB debugging on your device, under developer options.

[![](../../../img/linux/android/seedvault_sm.jpg)](../../../img/linux/android/seedvault.jpg){:target="_blank"}

Connect your device to your computer.

Run the following command to ensure the device is available to be used for ADB debugging:

<code>adb devices</code>

Execute the following command to open SeedVault to restore a backup from your recovery key:

<code>adb shell am start-activity -a com.stevesoltys.seedvault.RESTORE_BACKUP</code>
