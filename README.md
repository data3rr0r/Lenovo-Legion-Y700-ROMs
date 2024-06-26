# Lenovo Legion Y700 (TB9707F) ROMs
Repo with all the info about the ROMs available for the Lenovo Legion Y700 2022 model

Korean users, please move to [this page.](README-KR.md)

**For Y700(2023) with model number TB320FU, please move to [this page.](2023/README.md)**
  
> [!WARNING]  
> Do this at your own risk. This process may brick your devices. You can unbrick using [this method](https://www.youtube.com/watch?v=VaCjtUDoqXA), but I am not responsible for any dagame caused to your device.

</br>

# 📚 Index

[Unlocking bootloader](#blu)

ROMs: 
* ⚡ [How to flash Official CN Stock ROM (ZUI 14 Android 12 or ZUI 15 Android 13)](#stock-rom) -> Unbrick device
* ⚡ [How to sideload the Unofficial ZUI 15 OTA with Android 13](#unofficial-ota)
* ⚡ [How to flash a GSI ROM](#flash-gsi)
* ℹ️ [GSI ROMs working in the Lenovo Legion Y700 2022](#info)
* ℹ️ [GSI fixes](#gsifix)
  
<br>

Utilities: 
* 🦄 [How to install Magisk (Root tablet)](#magisk)
* 🛠️ Magisk fixes: To Be Done
* 🚀 [Acknowledgements](#acknowledgements)

---
<br>

## Unlocking Bootloader: <a name=blu></a>
Enable Developer settings by clicking ZUI Version in "About Tablet"
Enable OEM unlocking and USB debugging
Connect your Tablet to PC, and allow USB debugging.

Now check your PC recognizes Y700.
```
adb devices
```
If your device is detected, your serial number will appear. 

Restart your tablet with this command:
```
adb reboot bootloader
```

The device will now boot into bootloader. 
Now check your PC recognizes your device **IN BOOTLOADER MODE** with:
```
fastboot devices
```
> [!IMPORTANT]  
> In case your device is not recognised in fasboot mode (device does not appear when you run the above command): [How to install bootloader interface drivers](https://droidwin.com/install-google-android-bootloader-interface-drivers/)

After your device gets detected, unlock bootloader with:
```
fastboot flashing unlock
```

A warning message will appear. Use volume buttons and select "UNLOCK THE BOOTLOADER" with power button.
Your data will be wiped and system will reboot automatically.

Congratulations. You now have unlocked bootloader.

---
<br>

## ⚡ How to flash Official CN Stock ROM (ZUI 14 Android 12 or ZUI 15 Android 13): <a name=stock-rom></a>

> [!WARNING]  
> You need to have your bootloader unlocked to follow the process. Check this post in case you don't have it unlocked:  [XDA post](https://xdaforums.com/t/guide-unbrick-lenovo-y700-tablet.4509297/)
* ZUI 14, Android 12: You can check the process in this [video](https://www.youtube.com/watch?v=VaCjtUDoqXA) or in the [XDA post](https://xdaforums.com/t/guide-unbrick-lenovo-y700-tablet.4509297/)
* ZUI 15, Android 13: You can check the process in this [video](https://www.youtube.com/watch?v=aEHFUM-yLt0)

Links: 
* [Download ADB from the offical source](https://developer.android.com/studio/releases/platform-tools?hl=es-419)
* [QFIL - Direct Link](https://qpsttool.com/qpst-tool-v2-7-496)
* [ZUI 14 Stock CN ROM](https://drive.google.com/file/d/1P-8sFTtID0StfhNnf1kkROhzv0wHovun/view?usp=sharing)
* [ZUI 15 Stock CN ROM](https://drive.google.com/file/d/16PRQV0eE2F2GTm9eaFuoZoqGZgWcSTL_/view?usp=sharing)
* [Stock Rom Collections](https://reindex-ot.github.io/lenovo/) Note: Link for QFIL ROM 14.0.255 is dead. Use ZUI 14 Stock CN ROM link above instead. If you are using Fastboot ROM, Use [FastbootEnhance](https://github.com/libxzr/FastbootEnhance)

Other alternatives: 
* [All the above filles needed in 1 zip file - MEGA](https://mega.nz/file/8XU1kLgT#GVKDjBmvmJgXYfxIUEHSxsxSqLjMDmjixbV-W9GYM9w)
* [Other place with OTAs and stock ROMs - Sourceforge](https://sourceforge.net/projects/lenovo-y700/files/TB9707F/) thanks to [terajima-alc](https://terajima-alc.dev/)

---
<br>

## ⚡ How to sideload the Unofficial ZUI 15 OTA (ZUI 15 Android 13): <a name=unofficial-ota></a>
You can check the process in this [video](https://www.youtube.com/watch?v=ZN-D9tlXCTM)

* Prerequisites:  
  * [Download ADB from the offical source](https://developer.android.com/studio/releases/platform-tools?hl=es-419)
  * Having the CN stock ROM already installed on your device, explained here: ⚡ [How to flash CN Stock ROM](#stock-rom)
  * The OTA zip file (in the video description you have the links too):
    * [OTA LINK OPTION 1 - MEGA](https://mega.nz/file/lOUxnIYT#EzAg7reYfJ8oy_82OzCtQFi8XbMdhb_2YYjvVIf1P90)
    * [OTA LINK OPTION 2 - Official Lenovo page](https://mobile-ota-cdn.lenovo.com/firmware/2023111110434825-3726.zip&v=ZN-D9tlXCTM)

### Commands: 
1. Check that your PC recognize the device: 
```
adb devices
```
2. Restart the tablet in recovery mode
```
adb reboot recovery
```
3. In the recovery mode select "Apply update from ADB"
4. Start sideloading the OTA update
```
adb sideload OTA_FILENAME.zip
```
5. Select "Reboot system now" in the recovery mode and the tablet will reboot with the new version of ZUI and Android

---
<br>

## ℹ️ GSI ROMs working in the Lenovo Legion Y700 2022: <a name=info></a>
Here you can find a [list with all the GSI ROMs](https://github.com/phhusson/treble_experimentations/wiki/Generic-System-Image-%28GSI%29-list). Below I document the ones that I or someone else has already tested and we know they work fine, but if you have used any other ROM that is not in this list but works, please let me know (open an issue on Github, leave a comment on Youtube or send me a Telegram message). 

Click on any of the ROMs listed here to see how they look and possible issues
* [CRDROID](/roms/crdroid.md)
* [EvolutionX](/roms/evolution.md)
* [Voltage OS](/roms/voltageos.md)
* [Google AOSP](/roms/google_aosp.md)
* [LeOS U](/roms/leosu.md)
* [Elixir Project](/roms/elixir.md)


--- 
<br>

## ℹ️ GSI Fixes: <a name=gsifix></a>
Here you can find some issues with GSI roms and how to fix them.
This section is currently WIP. Your problem may not be listed here.

### Audio jack (3.5mm) not working
<br>
Go Settings->Phh Treble Settings->Qualcomm features->Enable `Use alternate audio policy`
<br>
Go Settings->Phh Treble Settings->Misc features->Enable `Use alternate way to detect headsets`

### Utilising slide switch / Auto brightness fix / Face Unlock Fix (Magisk Module)
<br>

Install [this module](https://github.com/reindex-ot/LegionY700-GSI-Fix_MOD). Magisk Required.

---
<br>

## ⚡ How to flash a GSI ROM: <a name=flash-gsi></a>

> [!TIP]  
> I have recorded the whole process on this [video](https://www.youtube.com/watch?v=zQ0Guo1v9LA). I recommend you to take a look at it before flashing the ROMs.

* Prerequisites:  
  * [Download ADB from the offical source](https://developer.android.com/studio/releases/platform-tools?hl=es-419)
  * You will need the vbmeta.img file from the stock ROM (I have a link to it in [this video](https://www.youtube.com/watch?v=VaCjtUDoqXA&t=0s))
  * A GSI ROM, in this example we will use [CRDROID](/roms/crdroid.md)


### Commands: 
1. Check that your PC recognize the device: 
```
adb devices
```

2. Reboot to booloader
```
adb reboot bootloader
```

3. Check that your PC recognize the device in fastboot mode
```
fastboot devices
```
> [!IMPORTANT]  
> In case your device is not recognised in fasboot mode (device does not appear when you run the above command): [How to install bootloader interface drivers](https://droidwin.com/install-google-android-bootloader-interface-drivers/)

4. Flash the vbmeta.img file (from the stock ROM or you can get it [here](https://xdaforums.com/t/how-to-install-gsi-with-google-services-on-legion-y700-netflix-problem-solved-games-payment-issue-solved.4651090/) too)
```
fastboot --disable-verification flash vbmeta vbmeta.img
```

5. Reboot on fastboot mode
```
fastboot reboot fastboot
```
And select "Enter fasboot" in the menu

6. Check you are using a user space
```
fastboot getvar is-userspace
```

6. Erase system
```
fastboot erase system
```

7. Delete logical partition B
```
fastboot delete-logical-partition product_b
```

8. Flash the GSI ROM, for this example we are using [CRDROID](/roms/crdroid.md)
```
fastboot flash system crDroid-10.0-arm64_bgN-Unofficial.img
```

9. Reboot into recovery
```
fastboot reboot recovery
```

10. Select "Wipe Data / Factory Reset" and confirm
11. Select "Reboot System now"

--- 
<br>

## 🦄 How to install Magisk (Root tablet): <a name=magisk></a>

### Long method: 
Patch your own boot.img. The steps are desribed in the following [post](https://xdaforums.com/t/gsi-rom-install-magisk-with-no-root-on-gsi-rom-dsu-method.4651428/)

### Easy method: 
[Guide in Video](https://www.youtube.com/watch?v=eVR1i7yASXA)

* Download patched img and magisk from [here](https://drive.google.com/drive/folders/1E5BsgLwW4Yc_2-ajOklnAVocDODDGs2M)
* Follow the commands below

#### Commands easy method: 
1. Check that your device is detected in ADB
```
adb devices
```
2. Install Magisk apk (you can do it by sending the apk to the device or by using the command below)
```
adb install Magisk.apk
```
3. Reboot to bootloader
```
adb reboot bootloader
```
4. Check that your device is detected in fastboot mode
```
fastboot devices
```
5. Flash the patched boot.img
```
fastboot flash boot magiskPatchedBootB.img
```
6. Restart to recovery selecting "Restart recovery" (move up/down with vol+/- and confirm with the lock button)
7. Select "Restar system now"
8. Go to Magisk and reboot the device from there
9. Check that the installation has been carried out correctly
![](/images/magisk/magisk.png)

---  
<br>

## 🚀 Acknowledgements <a name=acknowledgements></a>
Thanks to vicenteMartinezY700 for [this post](https://xdaforums.com/t/how-to-install-gsi-with-google-services-on-legion-y700-netflix-problem-solved-games-payment-issue-solved.4651090/) in XDA about the GSI ROMs and his help testing everything in this tablet. 
---  

