---
layout: page
background: '/img/ghorr_banner.png'
title: F-Droid Privileged Extension
date: 2021-07-12
categories : dropdown
permalink: /linux/android/f-droid_priv/
---

This guide will explain how to install F-Droid as a privileged app on a deGoogled phone.  This will allow you to still receive automatic updates for your apps after deGoogling.  Similar functionality is built into the [LineageOS for microG](https://lineage.microg.org){:target="_blank"} ROM, but this tutorial will allow you to setup something similar for those not interested in running microG.  In order to install the F-Droid Privileged Extension on a non-rooted phone, you will need to enter a Root ADB shell on your device.  This can easily by completed using [TWRP Recovery](https://twrp.me){:target="_blank"}.

____________________________________

##### Download Extension

You first need to download [F-Droid Privileged Extension OTA](https://f-droid.org/en/packages/org.fdroid.fdroid.privileged.ota){:target="_blank"} from the F-Droid website.  Supposedly, you should be able to directly flash this within TWRP Recovery, however, this did not work for me on the latest LineageOS 18.1.  So manual intervention was required.

Extract the zip file:

<code>unzip org.fdroid.fdroid.privileged* -d ./f-droid</code>

Change directory into the folder:

<code>cd f-droid</code>

##### Boot TWRP and Mount System Partition

Attain a Root ADB shell on your device (e.g., boot into TWRP recovery):

Select <span style="background-color: #ff9900;">mount</span>

[![](../../../img/linux/android/f-droid_priv_01_sm.jpg)](../../../img/linux/android/f-droid_priv_01.jpg){:target="_blank"}

Check <span style="background-color: #ff9900;">System</span>

[![](../../../img/linux/android/f-droid_priv_02_sm.jpg)](../../../img/linux/android/f-droid_priv_02.jpg){:target="_blank"}

Hit the back button

##### ADB Root Shell

Connect your phone to your computer and run the following commands in adb.

List connected adb devices:

<code>adb devices</code>

Ensure you have root:

<code>adb root</code>

Remount your partitions:

<code>adb remount</code>

Install F-Droid and F-Droid Privileged Extension.

<code>adb push F-DroidPrivilegedExtension.apk /system/priv-app/</code>

<code>adb push permissions_org.fdroid.fdroid.privileged.xml /system/etc/permissions/</code>

<code>adb push F-Droid.apk /system/app/</code>

<code>adb push 80-fdroid.sh /system/addon.d/</code>

Reboot your phone and launch F-Droid.  Enable "Automatically install updates" under settings.

[![](../../../img/linux/android/f-droid_priv_03_sm.jpg)](../../../img/linux/android/f-droid_priv_03.jpg){:target="_blank"}

Your phone should now receive automatic updates from F-Droid for all of your installed apps.

***Optional***: Installing the [F-Droid Privileged Extension](https://f-droid.org/en/packages/org.fdroid.fdroid.privileged){:target="_blank"} from F-Droid, after completing these steps, should in theory keep the F-Droid Privileged Extension up to date (untested).

##### References

[https://www.reddit.com/r/fdroid/comments/jdz7ij/install_fdroid_as_system_app_using_nanodroidfdroid](https://www.reddit.com/r/fdroid/comments/jdz7ij/install_fdroid_as_system_app_using_nanodroidfdroid){:target="_blank"}
