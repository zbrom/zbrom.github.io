---
layout: page
background: '/img/ghorr_banner.png'
title: Easter Eggs
date: 2013-08-01
categories : dropdown
permalink: /arch/easter_eggs/
---

Here you will find some tutorials for some fun Arch hidden features, otherwise known as easter eggs.

____________________________________

Show an ASCII pacman during package management:

Open pacman.conf with your favorite text editor.

    nano /etc/pacman.conf

Add the following to line 38 of your pacman config

    ILoveCandy

Sample pacman.conf:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
#<br>
# /etc/pacman.conf<br>
#<br>
# See the pacman.conf(5) manpage for option and repository directives<br>
<br>
#<br>
# GENERAL OPTIONS<br>
#<br>
[options]<br>
# The following paths are commented out with their default values listed.<br>
# If you wish to use different paths, uncomment and update the paths.<br>
#RootDir     = /<br>
#DBPath      = /var/lib/pacman/<br>
#CacheDir    = /var/cache/pacman/pkg/<br>
#LogFile     = /var/log/pacman.log<br>
#GPGDir      = /etc/pacman.d/gnupg/<br>
#HookDir     = /etc/pacman.d/hooks/<br>
HoldPkg     = pacman glibc<br>
#XferCommand = /usr/bin/curl -L -C - -f -o %o %u<br>
#XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u<br>
#CleanMethod = KeepInstalled<br>
Architecture = auto<br>
<br>
# Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup<br>
#IgnorePkg   =<br>
#IgnoreGroup =<br>
<br>
#NoUpgrade   =<br>
#NoExtract   =<br>
<br>
# Misc options<br>
#UseSyslog<br>
#Color<br>
#TotalDownload<br>
CheckSpace<br>
#VerbosePkgLists<br>
ILoveCandy<br>
# By default, pacman accepts packages signed by keys that its local keyring<br>
# trusts (see pacman-key and its man page), as well as unsigned packages.<br>
SigLevel    = Required DatabaseOptional<br>
LocalFileSigLevel = Optional<br>
#RemoteFileSigLevel = Required<br>
</div>
</div>

Working example:

![](../../img/arch/pacman.png)

What is the meaning of life?
Using vim (vi improved), you can find out the meaning of life…or death?
Open vim: vim
Then type :help 42
Vim will then reference The Hitchhiker’s Guide to the Galaxy, answering the question many of us have asked.
What is the meaning of life?



