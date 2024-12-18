---
layout: page
background: '/img/ghorr_banner.png'
title: Tear Free Video Intel
date: 2021-06-26
categories : dropdown
permalink: /arch/tearfree_intel/
---

This tutorial will allow you to enable tear free video for both videos played locally and videos played from the browser.  I have previously needed to utilize the TearFree option when configuring Linux laptops.

____________________________________

##### Xorg Configuration:

The SNA acceleration method causes tearing for some people. To fix this, enable the “TearFree” option in the driver by adding the following line to your configuration file:

<code>nano /etc/X11/xorg.conf.d/20-intel.conf</code>

Modify the configuration file appropriately, adding the TearFree Option as shown below:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>Section "Device"</code><br>
<code>Identifier  "Intel Graphics"</code><br>
<code>Driver      "intel"</code><br>
<code>Option "TearFree" "true"</code><br>
<code>EndSection</code><br>
</div>
</div>

##### Firefox Configuration (optional):

Previously, force enabling hardware acceleration in Firefox was necessary.  Only enable this if you are noticing an issue in FireFox after enabling TearFree for the Intel driver.

Type about:config into the address bar in Firefox

Search for layers.acceleration.force-enabled

Change the Value from false to true

Restart Firefox
