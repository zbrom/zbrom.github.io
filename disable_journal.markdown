---
layout: page
background: '/img/ghorr_banner.png'
title: Disable Journaling
date: 2021-06-26
categories : dropdown
permalink: /linux/disable_journal/
---

This guide allows you to disable journaling on a particular volume. This can be useful for flash drives or SD cards if desired.

____________________________________

Run the following command from a terminal.

<code>tune2fs -O ^has_journal /dev/sdX</code>
