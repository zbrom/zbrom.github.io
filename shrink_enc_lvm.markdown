---
layout: page
background: '/img/ghorr_banner.png'
title: Shrink an Encrypted LVM
date: 2021-06-27
categories : dropdown
permalink: /linux/shrink_enc_lvm/
---

Recently while preparing a persistent USB Linux OS, I found difficulty in removing an encrypted swap and shrinking the size of the encrypted LVM.  This guide should provide some clarification.

____________________________________
<p></p>
#### Remove Swap

If you previously had a swap partition, ensure it is turned off

<code>sudo swapoff -a</code>

Remove your particular cryptswap partition.

<code>sudo cryptsetup remove /dev/mapper/cryptswap1</code>

Remove your logical volume.

<code>lvremove /dev/VolGroup00/LogVol01</code>

#### Resize Volumes

Display the size of your logical volume(s)

<code>lvdisplay | grep Size</code>

If desired, feel free to resize a logical volume (choose your desired size e.g. 50G)

<code>lvresize /dev/VolGroup/LogVol00 --size 50G</code>

Resize your physical volume to match the logical volume (choose your desired size e.g. 50G)

<code>pvresize /dev/sda2 --setphysicalvolumesize 50G</code>

#### Display Volume Sizes

Display the size of your logical volume(s)

<code>lvdisplay | grep Size</code>

Display the PV sizes in SECTORS and take note of the smaller PSize:

<code>lvm pvs --units s</code>

Display the partition Size in SECTORS using parted and take note of the Start sector and partition Number of the partition with “lvm” in the Flags column (I recommend you save the full output of the following command):

<code>parted /dev/sda unit s print</code>

<div style="text-align: center;">
<p><strong><span style="background-color: #ff0000; color: #ffffff;">POINT OF NO RETURN – HAVE BACKUPS</span></strong></p>
</div>

Now we need to nuke the old, large partition from the partition table, and immediately recreate it with the exact same Start sector, but with a newer, shorter End sector. To calculate the new End sector, ADD the partition Start sector to the PV PSize, and then add a safety margin of around 131072 sectors (64MB) to that.  When I attempted this, it required my to do five times this amount (655360 sectors).  The number 2 should correspond to your particular lvm partition.  Again, make sure your data is backed up.

parted /dev/sda rm 2

Recreate it smaller + safety margin (as explained above). NOTE: remember to append the letter “s” to your values to qualify them as sectors. (e.g. “131072s”)

parted /dev/sda mkpart primary 401625s 105390297s
parted /dev/sda set 2 lvm on
parted /dev/sda print
fdisk -l /dev/sda

Hopefully this offers some clarification of how to accomplish this cumbersome task.  For further information, check out these references.

#### References:

[https://centoshelp.org/resources/post-install-options/shrink-a-default-install-lvm-pv-to-create-another-partition/](https://centoshelp.org/resources/post-install-options/shrink-a-default-install-lvm-pv-to-create-another-partition/)

[https://www.logilab.org/blogentry/29155](https://www.logilab.org/blogentry/29155){:target="_blank"}
