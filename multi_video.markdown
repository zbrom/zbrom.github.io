---
layout: page
background: '/img/ghorr_banner.png'
title: Multi-Monitor Video Script
date: 2013-08-01
categories : dropdown
permalink: /code/multi_video/
---

Here is a simple script that allows you to play video synced on two screens using mplayer.  The script allows the user to select the video they would like to play from a specific folder.

Ensure you have mplayer installed; it should be readily available from your package manager.

____________________________________

Copy the code into your favorite text editor.

Code:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>#! /bin/bash</code><br>
<code># www.ghorr.org - 2012</code><br>
<br>
<code>#find out who the user is</code><br>
<code>user=$(whoami)</code><br>
<br>
<code>#USER CONFIG: change this to match your path to videos</code><br>
<code>path="/home/$user/Videos/"</code><br>
<br>
<code>echo ""</code><br>
<br>
<code>#display list of videos</code><br>
<code>ls $path</code><br>
<code>echo ""</code><br>
<br>
<code>echo "Enter the name of the video you would like to play, include extension."</code><br>
<code>echo ""</code><br>
<code>read "video"</code><br>
<br>
<code>#launching the video with multimonitor support. Define one monitor as -xineramascreen 0 and the other as -xineramascreen 1; -nosound indicates the second video will be muted to avoid distortion.</code><br>
<code>mplayer -xineramascreen 0 -fs -framedrop "$path""$video" & mplayer -xineramascreen 1 -fs -framedrop -nosound "$path""$video"</code><br>

</div>
</div>

You first need to define the path to your video directory, by editing this line in the code:

<code>path="/home/$user/Videos/"</code>

Save your file and place it in a directory that is easily accessible.  I currently have mine placed in the bin folder in my home directory.  You can also place it in the /usr/bin directory if you like.

Make the script executable by running the following command in terminal, with the correct path to the script.

<code>chmod +x [path to file]</code>

Example:

![](../../img/code/2multi.png)
