---
type: post
title: "Mod your Huawei p8 lite"
subtitle: "Flash Custom ROM Android 7.1.2 / 8.0 BETA to your p8 lite. If something goes wrong, you can always go back to stock EMUI 4.1"
---

# 1. Get unlock code

First, create an account here:
[https://emui.huawei.com](https://emui.huawei.com)

Log in and complete this form to get unlock code for your phone:
[https://emui.huawei.com/en/plugin/unlock/detail](https://emui.huawei.com/en/plugin/unlock/detail)

You'll get a 16 digits code, save it, we'll use it in the next step.

# 2. Unlock bootloader

Connect phone to pc, and run:
```bash
sudo adb devices
```

Reboot phone into fastboot mode:
```bash
adb reboot bootloader
```

Install fastboot on ubuntu:
```bash
sudo apt install android-tools-fastboot
```

As phone is in fastboot mode, check if device is detected:
```bash
sudo fastboot devices
```

Unlock phone's bootloader
```bash
sudo fastboot oem unlock 16_DIGIT_UNLOCK_CODE_HERE
...
OKAY [  2.359s]
finished. total time: 2.359s

```

Also see [official instructions](https://emui.huawei.com/en/plugin/unlock/step) for unlocking bootloader.

# 3. Install TWRP
Download TWRP 3.1.1-0 from [xda-developers](https://forum.xda-developers.com/p8lite/orig-development/twrp-t3583180).
Double check md5sum of the file, it should be: 29e1c65cf48803892946e858ebe950cf.

Flash the image:
```bash
sudo fastboot flash recovery recovery.img 
target reported max download size of 471859200 bytes
sending 'recovery' (25152 KB)...
OKAY [  0.628s]
writing 'recovery'...
OKAY [  0.735s]
finished. total time: 1.363s
```

Now, as mentioned [here](https://forum.xda-developers.com/showpost.php?p=71429023&postcount=73), next step is to reboot device in this way:
 * press & keep pressed volume UP button
 * run `sudo fastboot reboot`
 * unplug usb cable from phone

TWRP will now load!

Leave phone as is and got to next step.

# 2. Update phone to stock EMUI 4.1

While in TWRP mode, from Wipe screen, do a `Format Data` and then a `Factory Reset` to wipe dalvik/cache.

Download [stock EMUI 4.1 ROM](https://forum.xda-developers.com/showpost.php?p=73230358&postcount=2):
 * b895_update.zip for single sim version, md5 0868fab65e2a38bff95408c02ffa0aba
 * B896_update.zip for dual sim version, md5 2b3d6b4b0945592ce506d44874f00d73

Additionally, create an empty `b895_update.zip.md5` with:
```
0868fab65e2a38bff95408c02ffa0aba
```

OR `B896_update.zip.md5` with:
```
2b3d6b4b0945592ce506d44874f00d73
```

You will see the phone as a removable device. Copy the downloaded zip and md5 file to internal memory.

Md5 file will check for zip integrity before flashing on the phone.

From the Install menu, select zip file and then `Swipe to confirm Flash`.

Reboot phone.

If phone freezes with Huawei logo for more than 5 minutes, reboot phone by pressing power button for 10 seconds.

## Warning!
After this step, in TWRP you will see 0MB internal storage.

# 3. Install Custom ROM Android 7.1.2 / 8.0 BETA

Download one of these:
 * android 7.1.2 [https://forum.xda-developers.com/p8lite/development/rom-t3606568](https://forum.xda-developers.com/p8lite/development/rom-t3606568)
 * android 8.0 BETA [https://forum.xda-developers.com/p8lite/development/rom-t3707374](https://forum.xda-developers.com/p8lite/development/rom-t3707374)

Download [opengapps](http://opengapps.org/).
 * ARM64, android 7.1, nano 
 * ARM64, android 8.0, nano

Reboot phone into recovery. Do a `Format Data` and a `Wipe cache/dalvik`.

Copy ROM zip and opengapps zip to internal memory.

From Install screen, add ROM zip. Then choose `Add more Zips` and add opengapps zip. Then `Swipe to confirm Flash`.

Reboot system.

You should now boot in your new Custom ROM.
