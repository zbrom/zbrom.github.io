---
layout: page
background: '/img/ghorr_banner.png'
title: Encrypted Dropbox w/ EncFS
categories : dropdown
permalink: /arch/encrypted_dropbox/
---

This tutorial will allow you to make an encrypted EncFS filesystem within your Dropbox account, or other file sharing service.  Please close Dropbox or disconnect your internet prior to following this tutorial.

____________________________________

Make sure you have a bin folder in your home directory; feel free to set an Environment Variable for it if desired:

<code>mkdir ~/bin</code>

Install encfs from the official repository:

<code>pacman -S encfs</code>

Change the directory to just outside the folder you wish to setup the EncFS filesystem:

<code>cd ~/</code>

Run the encfs command to create the encrypted and decrypted filesystem.  You must use full paths.  ghorr recommends using the highest AES algorithm and the highest block size:

<code>encfs /home/ghorr/Dropbox/.encrypted /home/ghorr/Dropbox-decrypted</code>

Change directory into your encrypted encfs filesystem:

<code>cd ~/Dropbox/.encrypted</code>

Move the .encfs6.xml into a different location, so it will not get uploaded to Dropbox:

<code>mkdir ~/bin/dropbox && mv .encfs6.xml ~/bin/dropbox</code>

Create a new file in ~/bin/dropbox to store your EncFS password to automatically unlock the filesystem:

<code>nano ~/bin/dropbox/encfs-dropbox.pass</code>

Enter your password into the file and save it.

Create the following script in your home bin folder:

<code>nano encfs-dropboxmount</code>

Add the following, using full paths for everything:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
#!/bin/sh<br>
<br>
export ENCFS6_CONFIG="/home/ghorr/bin/dropbox/.encfs6.xml"  encfs  "/home/ghorr/Dropbox/.encrypted/" /home/ghorr/Dropbox-decrypted/<br>
<br>
encfs --public --extpass="cat /home/ghorr/bin/dropbox/encfs-dropbox.pass" $*
</div>
</div>

To automount the encrypted filesystem on boot, edit your fstab:

<code>nano /etc/fstab</code>

Add the following line to your fstab file:

<code>/home/ghorr/bin/dropbox/encfs-dropboxmount#/home/ghorr/Dropbox/.encrypted /home/ghorr/Dropbox-decrypted/ fuse rw,user,auto 0 0</code>

The encrypted filesystem should now start on boot.
