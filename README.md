# How to root Evolveo H4

on the device:
* enable developer options
	- Settings - About - keep clicking on Build number
* allow USB Debugging
	- Settings - Developer options - Debugging - Allow USB Debugging
* download SuperSU for recovery
	- from now on I will refer to its location as `/path/to/supersu.zip`, but it will likely be `/sdcard/Download/SuperSU-v2.82-201705271822.zip`
	- tested with SuperSU v2.82 https://s3-us-west-2.amazonaws.com/supersu/download/zip/SuperSU-v2.82-201705271822.zip
	
on PC:
* connect through wifi ADB (how to obtain and use adb: http://www.makeuseof.com/tag/use-adb-fastboot-android/)
	- `adb connect IP:PORT`
	- install Wifi ADB on your device from Play Store if you are not sure about the IP and PORT
* `adb shell`

now in adb shell:
```su
 mount -o remount,rw /system
 mount -o remount,rw /
 mkdir /tmp
 mkdir /dev/block/by-name
 ln -s /dev/block/boot /dev/block/by-name/boot
 ln -s /system/xbin/unzip /sbin/unzip
 unzip /path/to/supersu.zip META-INF/com/google/android/* -d /tmp
 sh /tmp/META-INF/com/google/android/update-binary dummy 1 /path/to/supersu.zip
```


## Install Xposed
I don't think there is a way to flash custom recovery (like TWRP), but there is another way, now that we have a root.

On the device:
* download Flashfire from https://flashfire.chainfire.eu/
* download Xposed zip for arm from here http://dl-xda.xposed.info/framework/sdk23/arm/
* flash the zip using Flashfire
* install Xposed installer from https://forum.xda-developers.com/showthread.php?t=3034811

## Fake Wifi
Some apps don't cope well with connection over ethernet. They either don't see it or don't accept it as valid connection.
Install [the Fake Wifi](https://play.google.com/store/apps/details?id=eu.chylek.adam.fakewifi) Xposed module to deceive those apps.
After you install the app, activate it in Xposed and reboot (there's an option for that in the notification when the app is installed). 
Now simply open the app, choose from the list apps that should be deceived and you are all set. They should now think the are on WiFi.
