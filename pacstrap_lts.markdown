---
layout: page
background: '/img/ghorr_banner.png'
title: Pacstrap Linux-LTS
date: 2021-06-26
categories : dropdown
permalink: /arch/pacstrap_lts/
---

This tutorial will explain how to pacstrap the linux-lts kernel without having to install the package linux from an Arch Linux Live CD.  This is recommended for users seeking less frequent kernel updates, and the potential for increased stability.

____________________________________

<code>pacman -Sy</code>

<code>pacstrap /mnt $(pacman -Sqg base | sed 's/^linux$/&-lts/')</code>
