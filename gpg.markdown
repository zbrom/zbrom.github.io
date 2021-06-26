---
layout: page
background: '/img/ghorr_banner.png'
title: GPG Encryption
date: 2021-06-25
categories : dropdown
permalink: /arch/gpg/
---

GnuPG is a complete and free implementation of the OpenPGP standard as defined by RFC4880. Here is a basic guide how to setup GPG encryption on Arch.

________________________________________________________________________________________________________________

##### Generating a New Key:

Install gnupg:

<code>pacman -S gnupg</code>

Create a key pair:

<code>gpg --full-gen-key</code>

##### Exporting Public Key:

Export your public key to share it with others.

<code>gpg --export --armor --output publickey.asc user-id</code>

##### Importing Public or Private Keys:

This command can be utilized to import a public or private key.

<code>gpg --import key.asc</code>

##### Backup Private Key:

<code>gpg --export-secret-keys --armor --output privkey.asc user-id</code>

##### Additional Information:

GNOME Keyring can be managed with Seahorse. Package: seahorse

##### References:

[https://wiki.archlinux.org/index.php/GnuPG#Export_your_public_key](https://wiki.archlinux.org/index.php/GnuPG#Export_your_public_key){:target="_blank"}
