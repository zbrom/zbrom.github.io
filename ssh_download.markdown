---
layout: page
background: '/img/ghorr_banner.png'
title: SSH Download Script
date: 2013-08-01
categories : dropdown
permalink: /code/ssh_download/
---

This script allows you to download a file from a remote SSH server and verify the md5sum to ensure no corruption during transfer.  Feel free to use it as is or modify it to your liking.

____________________________________

Copy the code into your favorite text editor.

Code:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>#! /bin/bash<br></code>
<code># www.ghorr.org - 2013<br></code>
<br>
<code>#ssh server to download from (e.g., server=user@127.0.0.1)<br></code>
<code>#path on remote host<br></code>
<code>echo ""<br></code>
<code>echo "Input the path you wish to download from."<br></code>
<code>read "path1"<br></code>
<code>#listing files in above path and choosing the file to download<br></code>
<code>ssh $server ls $path1<br></code>
<br>
<code>echo ""<br></code>
<code>echo "Choose the file you wish to download."<br></code>
<code>read "file"<br></code>
<br>
<code>#path on local host<br></code>
<code>echo ""<br></code>
<code>echo "Input the destination directory."<br></code>
<code>read "path2"<br></code>
<br>
<code>scp $server:/$path1/$file $path2/<br></code>
<br>
<code>#md5sum<br></code>
<code>echo ""<br></code>
<code>echo "Would you like to run an md5sum? (Y/n)"<br></code>
<code>read "run"<br></code>
<br>
<code>if [ "$run" = "Y" ]<br></code>
<code>then<br></code>
<code>#collecting the md5sums for the downloaded file<br></code>
<code>cd $HOME<br></code>
<code>md5sumfile1=$(ssh $server md5sum $path1/$file | cut -c -32)<br></code>
<code>cd $HOME<br></code>
<code>cd $path2<br></code>
<code>md5sumfile2=$(md5sum $file | cut -c -32)<br></code>
<br>
<code>#displaying the two md5sums<br></code>
<code>echo ""<br></code>
<code>cd $HOME<br></code>
<code>echo $(ssh $server md5sum $path1/$file)<br></code>
<code>echo ""<br></code>
<code>cd $HOME<br></code>
<code>cd $path2<br></code>
<code>echo $(md5sum $file)<br></code>
<br>
<code>#determining if the two md5sums match<br></code>
<code>if [ "$md5sumfile1" = "$md5sumfile2" ]<br></code>
<code>then<br></code>
<code>echo "SUCCESS, md5sums match"<br></code>
<code>else<br></code>
<code>echo "md5sums do NOT match"<br></code>
<code>fi<br></code>
<br>
<code>else<br></code>
<code>exit<br></code>
<code>fi</code><br>
</div>
</div>

You first need to define the server you wish to use, modify the server variable to your liking.

<code>server=user@127.0.0.1)</code>

Save your file and place it in a directory that is easily accessible. I currently have mine placed in the bin folder in my home directory.  You can also place it in the /usr/bin directory if you like.  Ensure you save the script with UTF-8 encoding.

Make the script executable by running the following command in terminal, with the correct path to the script.

<code>chmod +x [path to file]</code>
