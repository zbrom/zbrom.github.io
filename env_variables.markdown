---
layout: page
background: '/img/ghorr_banner.png'
title: Environment Variables
date: 2021-06-25
categories : dropdown
permalink: /arch/env_variables/
---

This tutorial will help you set environment variables for a particular user.  An excellent example of this is mapping your /home/$user/bin to the $PATH variable, allowing the user to execute scripts from the /home/$user/bin from any terminal.  Using the /home/$user/bin method is more convenient during development rather than soley copying files over to the /usr/bin folder.  Whenever $user is specified in this tutorial, feel free to replace it with your username.

____________________________________

<div style="text-align: center;"><span style="background-color: #ff0000; color: #ffffff;">First, ensure you have created a bin folder inside of your home folder.</span></div>

Edit the .bashrc file in your home folder; open a terminal and type the following.

<code>nano .bashrc</code>

Add the following line of code to your .bashrc file; this will map your ~/bin folder to the $PATH variable.

<code>export PATH=$HOME/bin:$PATH

Sample output of mine:

<div style="height: 200px; width: 900px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>## ~/.bashrc## If not running interactively, don't do anything[[ $- != *i* ]] && return</code><br>
<br>
<code>alias ls='ls --color=auto'</code><br>
<br>
<code>PS1='[\u@\h \W]\$ '</code><br>
<br>
<code>export PATH=$HOME/bin:$PATH</code><br>
</div>
</div>

You can now execute scripts inside of your /home/$user/bin folder from any terminal.

____________________________________

It is also possible to set environment variables for a particular session, by entering the following into a terminal:

<code>export PATH="${PATH}:/home/$user/tmp/usr/bin"</code>

This method will only remain valid until you logoff.

For additional information, please visit the Arch Wiki:  [https://wiki.archlinux.org/index.php/Environment_Variables](https://wiki.archlinux.org/index.php/Environment_Variables){:target="_blank"}

Check out the code section of the site for useful scripts.
