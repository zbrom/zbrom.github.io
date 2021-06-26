---
layout: page
background: '/img/ghorr_banner.png'
title: Backup with dd Command
date: 2021-06-26
categories : dropdown
permalink: /linux/backup_dd/
---

This tutorial provides an effective method for backing up your boot hard drive which contains your OS.  Backing up your system is very essential to protect against data loss; additionally if something where to go drastically wrong with your system, you could restore to a previous image.  I recommend backing up your system drive at least once every three months.  Additionally data backups should occur much more often.

____________________________________

Use fdisk or blkid to identify which drive you would like to backup or restore (e.g. /dev/sda).

<code>fdisk -l</code>

##### Backing up your system:

Use the dd command to backup your system.  (I chose to use gzip compression in order to save space, because dd will copy every sector of your hard drive.)

    Change /dev/sda to your desired drive;  make sure to include the proper path for the destination of the backup.

<code>dd if=/dev/sda | gzip > /[your desired path]/backup.gz</code>

##### Restoring your system:

Use the gzip command piped into the dd command to restore your system.

    Change /dev/sda to your desired drive;  make sure to include the proper path for the location of the backup to restore.

<code>gzip -dc /[your desired path]/backup.gz | dd of=/dev/sda</code>
