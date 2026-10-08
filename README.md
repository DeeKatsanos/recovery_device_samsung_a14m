# Android device tree for samsung SM-A145R (a14m)

### Working
* Device Boots to TWRP

### BUGS
* Anything else

### Useful links / Personal notes

According to [this source](https://gist.github.com/lopestom/685cdd9c71476e9daf95ca612066e23f), you are supposed to import the touch drivers under root/vendor/lib/modules, then explicitly call them on your board config via "TW_LOAD_VENDOR_MODULES". I tried a bunch, which took some (shamefully long enough) time to test it all. Nothing worked. 

example: [this commit](https://github.com/devhunter1/android_device_samsung_a15/commit/6618c99fbca8714cde752b146bcb461bc2102169)

ForForkSake fixed the touchscreen issue on this device (although on pre GKI Kernel) by forcing the drivers to always use recovery boot instead of normal, in [this commit](https://github.com/forforksake/android_kernel_samsung_a145p/commit/2ad60c6b7b89f6f37d1eb483696e7d121c8972bd). Patching the new GKI source this way unfortunately produces no different results.
Also, my device _probably_ uses the jadard touchscreen variant, whose source code had major changes during the gki transition. 
(probably as in: Device Info HW shows "focaltech_fpspi" as touchscreen under system tab, and "jadard-touchscreen" under input tab).

### Todo:

* Figure a way to debug twrp: an expdb dump or a last_kmsg log seem useless since LK succesfully jumps to kernel address. TWRP boots normally. The issue is that we can't connect to the device via usb and/or use logcat. If only there was a way to get verbose logs onto sd...
