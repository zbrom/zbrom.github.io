---
layout: page
background: '/img/ghorr_banner.png'
title: Google Authenticator
date: 2021-06-26
categories : dropdown
permalink: /arch/authenticator/
---

Google Authenticator is open source software, currently licensed under the Apache 2.0 license. It is an excellent supplement to a working RSA model for additional security measures.  It utilizes one-time passcodes (OTP) to provide authentication.

ghorr no longer recommends using the Google Authenticator Android app because the application is no longer open source. [andOTP](https://f-droid.org/en/packages/org.shadowice.flocke.andotp){:target="_blank"} is now recommended, which is Free and Open Source Software (FOSS), available on FDroid.

____________________________________

#### Setting up Google Authenticator

##### Installing Google Authenticator

You can easily install google-authenticator-libpam-hg from AUR using yaourt:

<code>yaourt -S google-authenticator-libpam-git</code>

##### Adjusting the SSHD and PAM configuration files

Open /etc/ssh/sshd_config with your favorie text editor

<code>nano /etc/ssh/sshd_config</code>

Make sure that <span style="background-color: #ff9900;">ChallengeResponseAuthentication</span> is set to <span style="background-color: #ff9900;">yes</span>.

Next you have to edit /etc/pam.d/sshd. We are only interested in the lines starting with auth.

<code>nano /etc/pam.d/sshd</code>

If you want to have to enter both your regular password and a one-time password to login, change the configuration like this:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>auth required pam_unix.so</code><br>
<code>auth required pam_google_authenticator.so</code><br>
<code>auth required pam_env.so</code><br>
</div>
</div>

<span style="background-color: #ff0000; color: #ffffff;">Warning: Every user who has not yet generated a secret file will no longer be able to login via SSH.</span>

If you want to be able to login using your regular password or a one-time password, change the configuration file like this:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>auth sufficient pam_unix.so</code><br>
<code>auth sufficient pam_google_authenticator.so</code><br>
<code>auth required pam_env.so</code><br>
</div>
</div>

#### Using Google Authenticator

Just run the command google-authenticator as the user you want to generate the secret for and follow the instructions.

<code>google-authenticator</code>

You probably want to install the [andOTP](https://f-droid.org/en/packages/org.shadowice.flocke.andotp){:target="_blank"} app for Android to generate your one-time passwords.

google-authenticator will show you a QR-code you can scan on your phone if you have installed the qrencode packge. Otherwise you have to enter the secret key manually on your phone.

If an one-time password is required for logging in, you should print out your emergency codes and store them in a safe place.

#### Removing Google Authenticator

These are the defaults for the changed parts of the configuration files:

<code>nano /etc/ssh/sshd_config</code>

Set <span style="background-color: #ff9900;">ChallengeResponseAuthentication</span> to <span style="background-color: #ff9900;">no</span>

<code>nano /etc/pam.d/sshd</code>

Code:

<div style="height: 200px; width: 675px; border: 1px solid #cccccc; font-style: normal; font-variant: normal; font-weight: normal; line-height: 26px; font-size-adjust: none; font-stretch: normal; overflow: auto;">
<div class="sites-codeblock sites-codesnippet-block">
<code>auth required pam_unix.so</code><br>
<code>auth required pam_env.so</code><br>
</div>
</div>

#### References

[https://wiki.archlinux.org/title/Google_Authenticator](https://wiki.archlinux.org/title/Google_Authenticator){:target="_blank"}
