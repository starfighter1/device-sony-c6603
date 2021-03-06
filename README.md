Copyright (C) Sony Mobile Communication 2013
============================================

This is the Android device configuration for Xperia Z

To setup a tree and build images for the device do the following:

repo init as described by Google over at:
http://source.android.com/source/downloading.html

Put the following snippet in .repo/local_manifests/c6603.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
<remote  name="sony" fetch="git://github.com/sonyxperiadev/" />
<remote  name="pabx" fetch="git://github.com/adrian-bl-yuga/" />
<remote  name="github" fetch="git://github.com/" />

<remove-project name="platform/hardware/qcom/display" />
<remove-project name="platform/hardware/qcom/keymaster" />
<remove-project name="platform/hardware/qcom/media" />
<remove-project name="platform/hardware/qcom/msm8960" />
<remove-project name="platform/hardware/qcom/power" />
<remove-project name="platform/hardware/qcom/sensors" />
<remove-project name="platform/hardware/invensense" />
<!-- changed repos //-->
<remove-project name="platform/hardware/libhardware" />
<remove-project name="platform/frameworks/native" />
<remove-project name="platform/hardware/qcom/audio" />
<remove-project name="platform/packages/apps/Settings" />
<remove-project name="platform/frameworks/base" />
<remove-project name="platform/hardware/ril" />
<remove-project name="platform/system/core" />
<remove-project name="platform/packages/apps/Gallery2" />
<remove-project name="platform/frameworks/opt/telephony" />
<remove-project name="platform/packages/apps/VoiceDialer" />
<remove-project name="platform/system/vold" />




<project path="frameworks/opt/telephony"    name="android_frameworks_opt_telephony" remote="pabx" revision="jb43" />
<project path="hardware/libhardware"        name="android_hardware_libhardware"   remote="pabx" revision="jb43" />
<project path="hardware/ril"                name="android_hardware_ril"           remote="pabx" revision="jb43" />
<project path="frameworks/native"           name="android_frameworks_native"      remote="pabx" revision="jb43" />
<project path="frameworks/base"             name="android_frameworks_base"        remote="pabx" revision="jb43" />
<project path="system/core"                 name="android_system_core"            remote="pabx" revision="jb43" />
<project path="system/vold"                 name="android_system_vold"            remote="pabx" revision="jb43" />
<project path="packages/apps/Settings"      name="android_packages_apps_Settings" remote="pabx" revision="jb43" />
<project path="packages/apps/Gallery2"      name="android_packages_apps_Gallery2" remote="pabx" revision="jb43" />
<project path="packages/apps/VoiceDialer"   name="android_packages_apps_VoiceDialer" remote="pabx" revision="jb43" />
<project path="hardware/qcom/audio"         name="android_hardware_qcom_audio"    remote="pabx" revision="jb43" />
<project path="vendor/sony/yuga_blobs"      name="yuga-blobs-a806"                remote="pabx" revision="master" />
<project path="kernel/sony/k_a806"          name="kernel_a806"                    remote="pabx" revision="jb42" />
<project path="external/yuga-tools"         name="yuga-tools"                     remote="pabx" revision="master" />

<project path="device/sony/lagan"           name="device-sony-lagan" groups="device" remote="pabx" revision="jb43" />
<project path="device/sony/c6603"           name="device-sony-c6603" groups="device" remote="pabx" revision="jb43" />

<project path="vendor/sony/dash"            name="DASH"              groups="device" remote="pabx" revision="jb43" />
<project path="external/busybox"            name="CyanogenMod/android_external_busybox" remote="github" revision="cm-10.2" />

<!-- google and qcom went closed-source with this in 4.3, well: the 4.2 release is good enough for us //-->
<project path="hardware/qcom/gps"           name="platform/hardware/qcom/gps" revision="refs/tags/android-4.2.2_r1.2" />

</manifest>
```

Download the zip file with vendor binaries from:
http://developer.sonymobile.com/downloads/tool/software-binaries-for-xperia-z-and-xperia-tablet-z/

In the root of your Android code tree unzip the SW_binaries_for_Xperia_Z_Xperia_Tablet_Z_v3.zip.
you should now have a directory named vendor/sony/lagan and vendor/sony/c6603 in your tree.

* repo sync
* lunch full_c6603-userdebug
* cd kernel/sony/k253 && ./_build.sh && cd -
* make

To flash the images produced make sure your device is unlocked, as described on
http://unlockbootloader.sonymobile.com/

Enter fastboot mode on the device by pressing volume up while inserting the USB
cable or execute adb reboot bootloader.

* fastboot flash userdata out/target/product/c6603/userdata.img
* fastboot flashall

Reflashing userdata is not necessary every time, but incompatibilities with
previous content might result in a device that doesn't boot. If this happens
try to reflash just the userdata again.
