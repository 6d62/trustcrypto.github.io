---
title: Upgrading Firmware From Beta6 to Beta7
tags: [OnlyKey, Firmware, Upgrade]
keywords: OnlyKey, Firmware, Upgrade
last_updated: Oct, 31, 2018
summary: Follow this guide to upgrade firmware from Beta6 to Beta7
sidebar: mydoc_sidebar
permalink: upgradeguide.html
folder: mydoc
---

## Why Upgrade?

This release has a lot of improvements, most notably after upgrading your OnlyKey you can load future updates directly in the app without the need to backup and restore. Here is the short list of improvements in this release:

- Better touch sense on OnlyKey buttons using automatic touch sense calibration.
- Backup Passphrase support - Backup's may be securely encrypted with a passphrase.
- Two profile support - By setting two PINs you can have two profiles to store up to 24 accounts.
- Automatic firmware and app update notifications - The OnlyKey app can now let you know when there are updates available.
- Seamless firmware upgrades - Signed firmware can now be loaded directly through the app without wiping account data (thanks to our new blockchain bootloader).
- Better FIDO U2F support

## Steps to Upgrade

{% include note.html content="If you are a new OnlyKey user just complete steps 2 and 3 below as you won't have anything to backup/restore. Then head over to the [User's Guide](https://docs.crp.to/usersguide.html#set-pin) to get started." %}

1) **Backup OnlyKey** - Create a backup of your OnlyKey by going to the Backup/Restore tab in the OnlyKey app. Ensure you have a copy of your backup key ([User Guide Backup Instructions here](https://docs.crp.to/usersguide.html#secure-encrypted-backup-anywhere)).
2) **Upgrade OnlyKey firmware** - Follow instructions [here](#loading-onlykey-firmware) to upgrade firmware on the OnlyKey
3) **Upgrade OnlyKey desktop app** - Follow instructions [here](#app-desktop) to install the new OnlyKey app.
4) **Setup OnlyKey** - Follow instructions [here](#onlykey-setup) to setup OnlyKey and restore from backup
5) **Check out the new features [here](#new-features)**

### Steps to Upgrade OnlyKey firmware {#loading-onlykey-firmware}

**Before Getting Started**

{% include warning.html content="Legacy firmware loading wipes all data from OnlyKey. Be sure to have a backup of OnlyKey data and the backup key before loading firmware." %}


{% include callout.html content="**Step 1.**  Insert OnlyKey into USB port" type="default" %}
{% include callout.html content="**Step 2.**  Download and install [Teensy Loader](https://www.pjrc.com/teensy/loader.html)" type="default" %}
{% include callout.html content="**Step 3.**  Determine which version of OnlyKey you have and download firmware below" type="default" %}

{% include image.html file="image25.jpg" max-width="285" %}

<table>
  <tr>
   <td>OnlyKey Color (Has a square LED)
   </td>
   <td>OnlyKey Original (Has text "LED" visible)
   </td>
  </tr>
  <tr>
   <td>Download OnlyKey Color Standard Edition firmware <a href="https://github.com/trustcrypto/OnlyKey-Firmware/releases/download/v0.2-beta.6/OnlyKey_Beta6_STD_Color.cpp.hex">here</a>
   </td>
   <td>Download OnlyKey Original Standard Edition firmware <a href="https://github.com/trustcrypto/OnlyKey-Firmware/releases/download/v0.2-beta.6/OnlyKey_Beta6_STD_Original.cpp.hex">here</a>
   </td>
  </tr>
  <tr>
   <td>Download OnlyKey Color International Travel Edition firmware <a href="https://github.com/trustcrypto/OnlyKey-Firmware/releases/download/v0.2-beta.6/OnlyKey_Beta6_IN_TRVL_Color.cpp.hex">here</a>
   </td>
   <td>Download OnlyKey Original International Travel Edition firmware <a href="https://github.com/trustcrypto/OnlyKey-Firmware/releases/download/v0.2-beta.6/OnlyKey_Beta6_IN_TRVL_Original.cpp.hex">here</a>
   </td>
  </tr>
</table>


{% include callout.html content="**Step 4.** You can ensure the integrity of your downloaded firmware by verifying the checksum" type="default" %}

<table>
  <tr>
   <td>
File Name
   </td>
   <td>SHA 256 Checksums
   </td>
  </tr>
  <tr>
   <td>OnlyKey_Beta6_STD_Color.cpp.hex
   </td>
   <td>68f2ba7a23e6d4983cb47d4318e8eedbb86ecdf094feaf4928383ade88eb9150
   </td>
  </tr>
  <tr>
   <td>OnlyKey_Beta6_STD_Original.cpp.hex
   </td>
   <td>309da576981b0f9cf811f577467c8e214ce761bc543f7a469eed25e43c0dd811
   </td>
  </tr>
  <tr>
   <td>OnlyKey_Beta6_IN_TRVL_Color.cpp.hex
   </td>
   <td>d50ffa47c1e201fea4f77cddc3ad49e3afeb5873c537281569df65d12e27749d
   </td>
  </tr>
  <tr>
   <td>OnlyKey_Beta6_IN_TRVL_Original.cpp.hex
   </td>
   <td>018c2f3fda8f958653e9e3f0c686ca1b9f84c2d5f1dab182b6efa8d2428234e8
   </td>
  </tr>
</table>


{% include tip.html content="To do this in Windows open a command prompt and type 'certUtil -hashfile pathToFileToCheck SHA256'. To do this in Linux open a terminal and type 'sha256sum pathToFileToCheck'. Where pathToFileToCheck is replaced with the path of the file you are checking." %}

{% include callout.html content="**Step 5.**  In Teensy Loader select File -> Open HEX File. Then select the firmware you downloaded and click open." type="default" %}
{% include callout.html content="**Step 6.**  Now the firmware should appear at the bottom of the Teensy Loader application." type="default" %}

{% include image.html file="image67.png" max-width="213" %}

{% include note.html content="If a message prompts that 'HEX file is too large' ensure that your OnlyKey is plugged in." %}

{% include callout.html content="**Step 7.**  In order to enable the OnlyKey to upload the new firmware a jumper (Paperclip, aluminum foil etc) must make contact between the two small copper color circles shown while the OnlyKey is plugged into the USB port." type="default" %}

{% include tip.html content="If your OnlyKey has a case on it you can just slip the two corners out of the case without completely removing the case." %}

{% include image.html file="image16.png" %}

{% include callout.html content="**Step 8.**  With the Teensy Loader in the foreground, you should now see the Teensy Loader progress bar and then a reboot complete appear in the Teensy Loader which indicates that the firmware has loaded successfully." type="default" %}

{% include image.html file="image48.png" max-width="200" %}

{% include image.html file="image2.png" max-width="202" %}

**Under The Hood** - What actually happens when you load the firmware is that a mass erase is completed first. What this means is that all data is completely wiped, and then the new firmware is loaded.


### Install OnlyKey Desktop App {#app-desktop}

{% include callout.html content="**Step 1.** Download installer" type="default" %}

[<i class="fa fa-apple fa-2x"></i> **macOS**](https://s3.amazonaws.com/onlykey/apps/desktop/releases/latest/OnlyKey_5.0.0.dmg.zip)

[<i class="fa fa-windows fa-2x"></i> **Windows**](https://s3.amazonaws.com/onlykey/apps/desktop/releases/latest/OnlyKey_5.0.0.exe.zip)

[<i class="fa fa-linux fa-2x"></i> **Linux**](https://s3.amazonaws.com/onlykey/apps/desktop/releases/latest/OnlyKey_5.0.0.deb.gz)

{% include callout.html content="**Step 2.** Install and launch the app." type="default" %}

{% include tip.html content="You can ensure the integrity of your downloaded file by verifying the checksum. <br>macOS SHA 256 CHECKSUM: 51db9944ee234569146e053341cd57168baf84b145054cde77211c64cbbb81c7<br>Windows SHA 256 CHECKSUM: bdfb4561f506992664dbb9450033a2222160bfd8d5d7b6702512db438a110e9f<br>Linux SHA 256 CHECKSUM: 517d8d795b4a293b773676623997464b91e7756f1e2454b5e6c3c692fd467ed3<br> [ **GPG Public Key**](https://keybase.io/trustcrypto/pgp_keys.asc)" %}


### Steps to Setup OnlyKey {#onlykey-setup}

Now that the new OnlyKey app and firmware are installed its time to setup OnlyKey.

{% include callout.html content="**Step 1.**  Insert OnlyKey into USB port and select [Next] in the app." type="default" %}

Step 1 - Select [Next] to get started.
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/ite1.png)

Step 2 - Enter a PIN code, check the disclaimer box, and select [Next].
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/ite2.png)

Step 3 - Re-enter PIN code, and select [Next].

Step 4 - Enter a PIN code for second profile, check the disclaimer box, and select [Next].
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/ite4.png)

Step 5 - If you wish to set a self-destruct PIN enter a PIN code, check the disclaimer box, and select [Next].
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/ite5.png)

Step 6 - Re-enter PIN code, and select [Next].

Step 7 - Select [Use PGP Key instead of passphrase]
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/setup7.png)

Step 8 - With slot 1 selected, paste OpenPGP RSA key and enter passphrase and then select [Next].
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/setup8.png)

Step 9 - If you generated your keys as described in the [Generating Keys section](https://docs.crp.to/usersguide.html##generating-keys) select [subkey 1] and then select [Save]. If you generated a custom backup key then load the subkey used for backups to slot 1.
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/setup9.png)

Step 10 - Select [Choose File] and select your OnlyKey backup file and then select [Next] to load it onto your OnlyKey. Your device will reboot automatically when the restore is complete.
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/setup10.png)

Your device is now set up!

Check out the new app features below.

## New OnlyKey Features {#new-features}

### Backup Passphrase

Keys are great but a passphrase is an easier way to securely backup your OnlyKey. If you are already using an OpenPGP key for backup you can switch to a passphrase simply by following the instructions on the [Set Backup Passphrase or Key] page. Your OpenPGP key will remain on the OnlyKey but the passphrase will be used for future backup and restore.
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/newfeature1.png)

### Two Profile Support

You may notice now that when setting your PINs there is a primary profile and a secondary profile. The secondary profile can be either a standard profile or plausible deniability profile. This is a change as the previous OnlyKey release only had the option for the second profile to be a plausible deniability profile. The standard profile is a full featured second profile with 12 available slots and the plausible deniablity profile is a limited feature second profile that looks and acts just like a device with [International Travel Edition firmware](https://docs.crp.to/internationaledition.html).
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/ite4.png)

### In App Firmware Updates

You may notice now that there is an option in the app to load firmware when setting up a device. There is also a tab named Firmware in the app. This may be used to load the latest firmware onto OnlyKey directly through the app, no backup/restore or wiping is required. Firmware updates are securely signed using a simple blockchain and verified by on the OnlyKey.
![](https://raw.githubusercontent.com/trustcrypto/trustcrypto.github.io/master/images/newfeature2.png)

{% include links.html %}