---
layout: page
background: '/img/ghorr_banner.png'
title: Cloud Storage
date: 2021-07-10
categories : dropdown
permalink: /degoogle/cloud_storage/
---

While Google Drive claims to be secure with encryption, all of your uploaded files are stored on their servers with Google Drive's server side encryption.  Google still has access to your data and maintains control of your encryption keys.  Companies such as Dropbox, Google Drive, Microsoft OneDrive and Apple iCloud all have permission to access your data.  This guide will help those looking for private, secure, and encrypted alternatives.  For additional security, it is recommended to encrypt files using [EncFS](https://wiki.archlinux.org/title/EncFS){:target="_blank"}, [eCryptfs](https://wiki.archlinux.org/title/ECryptfs){:target="_blank"}, or [VeraCrypt](https://veracrypt.fr/en/Home.html){:target="_blank"} prior to uploading to the cloud.  For best security, consider self-hosting your data.

________________________________________________________________________________________________________________

##### Encrypted Cloud Storage (Free & Paid Options):

* **[Mega](https://mega.nz){:target="_blank"}** – Privides zero-knowledge, end-to-end encryption with AES-128 and TLS and supports 2FA, necessary to protect against spying by powerful government agencies.  Based in New Zealand, originally founded by [Kim Dotcom](https://en.wikipedia.org/wiki/Kim_Dotcom){:target="_blank"}.  Data is stored in New Zealand and Europe, GDPR compliant.  Uploaded files are client-side encrypted.  Free and paid plans are available.  Free plans have 20 GB storage.  They have sync clients available for Android, Mac, Linux, and Windows.  Browser extensions are available for Chrome, Firefox, and Opera.  They are partially [open source](https://github.com/meganz){:target="_blank"}.  They provide annual transparency reports.  They also provide an encrypted chat, voice, and video calling service.  Accepts crypto for payments.

* **[Internxt](https://internxt.com){:target="_blank"}** – Privides zero-knowledge, end-to-end encryption, on a decentralized cloud architecture.  Uploaded files are client-side encrypted, then fragmented into small pieces, where only the user holds the decryption key.  The company is based in Valencia, Spain.  Free and paid plans are available.  Free plans have 10 GB storage.  They have a desktop app, web app, Android app, and iOS app.  They have their own cryptocurrency token called INXT.  They are [open Source](https://github.com/internxt){:target="_blank"}.  Accepts crypto for payments, including INXT.

* **[Icedrive](https://icedrive.net){:target="_blank"}** – Privides zero-knowledge, end-to-end encryption with Twofish and TLS and supports 2FA.  Based in Wales, UK.  Data is stored in Europe and the US.  
Uploaded files are client-side encrypted.  Free and paid plans are available.  Free plans have 10 GB storage.  They have apps available for Android, Mac, Linux, and Windows.  They are not open source.  They accept crypto for payments on lifetime plans.

* **[Tresorit](https://tresorit.com){:target="_blank"}** – Privides zero-knowledge, end-to-end encryption with AES-256 and TLS and supports 2FA.  Based in Switzerland, GDPR compliant.  By default, your files are stored on data centers in Ireland.  Business and enterprise customers can opt to store their data in the US, UK, Canada, Ireland, Germany, France, Switzerland, Netherlands, Singapore, and Dubai.  Free and paid plans are available.  Free plans have 3 GB storage.  They have sync clients available for Android, Mac, Linux, and Windows.  Browser extensions are available for Chrome, Firefox, and Opera.  They are not open source.  They do not accepts crypto for payments.

##### Encrypted Cloud Storage (Self-hosted Options):

* **[Nextcloud](https://nextcloud.com){:target="_blank"}** – Excellent cloud storage suite, alowing for integration with over a hundred third party apps.  [100% Free and Open Source Software (FOSS).](https://github.com/nextcloud){:target="_blank"}.  Supports end-to-end encryption on your self-hosted server, along with 2FA.  Transmitted data can be secured with TLS.  Files can be setup with end-to-end encryption using AES-128-GCM, along with optional at rest encryption using AES-256.  Supports file versioning, collaboration, and media streaming.  Clients run on Android, iOS, Linux, Mac, and in the web browser.  They additionally provide syncing for calendar, contacts, notes, and tasks.

* **[Syncthing](https://syncthing.net){:target="_blank"}** – Excellent self-hosted option for file synchronization.  [100% Free and Open Source Software (FOSS).](https://github.com/syncthing){:target="_blank"}  Transmitted data is secured with TLS.  Supports end-to-end encryption for syncing with [untrusted devices (beta)](https://docs.syncthing.net/users/untrusted.html){:target="_blank"}.  File synchronization occurs over P2P, which does not require a server even.  You can sync your desktop computer to a mobile device, or opt to keep a server running in order to always be in full synchronization.  Sync clients run on Android, BSD, Linux, Mac, Solaris, and Windows.
