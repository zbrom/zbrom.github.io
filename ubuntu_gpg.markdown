---
layout: page
background: '/img/ghorr_banner.png'
title: GPG Encryption in Ubuntu
date: 2013-08-01
categories : dropdown
permalink: /misc/ubuntu_gpg/
---
<p></p>
#### Create Encrypted Files and Folders in Ubuntu

Seahorse is a front-end for GnuPG (Gnu Guard Program), a tool for secure communication and data storage. With Seahorse extension for Nautilus, you could encrypt a file or folder by right-clicking it and selecting ‘Encrypt’ on nautilus context menu. Files and folders that are encrypted cannot be accessed without the passwords used to encrypt them. It is a another way to protect your sensitive information.

##### Getting started:

To get started, go to Ubuntu Software Center.

![](../../img/misc/ubuntu_gpg_01.jpg)

Then search and install ‘Decrypt File’.

Decrypt File 

![](../../img/misc/ubuntu_gpg_02.jpg)

After installing search for Passwords and Keys with Unity search.
 
![](../../img/misc/ubuntu_gpg_03.jpg)

Next, click File –> New

![](../../img/misc/ubuntu_gpg_04.jpg)

Then select ‘PGP Key’ and continue.

![](../../img/misc/ubuntu_gpg_05.png)

Type your name and and email address, then click ‘Create’.
 
![](../../img/misc/ubuntu_gpg_06.png)

Type your password and confirm.

![](../../img/misc/ubuntu_gpg_07.png)

Log Out and Log back in.

Open Passwords and Keys again

Click My Personal Keys (your private key should appear here)

![](../../img/misc/ubuntu_gpg_08.png)

File –> Export

save the .asc file (aka: ASCII Armored file)

This saves your public key, allowing you to share it with friends so they can share files with you.

##### How to decrypt

Simply right click on a .pgp file and click decrypt
