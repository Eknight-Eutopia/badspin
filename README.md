# badspin (adjusted for arm emulator)
[original readme](./README_origin.md)

## Environment
- Mac ARM
- Android Studio
- emulator(arm64)
- Pixel 6 avd(Android 12, api 31)
- Android kernel version: 5.10.110 (branch: android12-5.10.110_r01)

## Emulation
start compiled kernel:
```shell
#!/bin/bash

SYS_DIR=/Users/fish/Library/Android/sdk/system-images/android-31/default/arm64-v8a/
DATA_DIR=/Users/fish/.android/avd/Pixel_6_API_31_ARM64_AOSP.avd/

export ANDROID_PRODUCT_OUT=$SYS_DIR
export ANDROID_BUILD_TOP=$SYS_DIR

~/Library/Android/sdk/emulator/emulator \
  -avd Pixel_6_API_31_ARM64_AOSP \
  -show-kernel \
  -no-snapshot-save -no-snapshot-load -no-snapstorage -no-snapshot \
  -system $SYS_DIR/system.img \
  -ramdisk $SYS_DIR/ramdisk.img \
  -cache $DATA_DIR/cache.img \
  -sysdir $SYS_DIR \
  -vendor $SYS_DIR/vendor.img \
  -writable-system \
  -no-window \
  -no-audio \
  -no-cache \
  -wipe-data \
  -accel on -netdelay none -no-sim \
  -verbose \
  -qemu -m 8192 -smp 8 -append "nokaslr" -s -no-reboot
```

use `adb shell` and run `uname -ar` and you can find:
```shell
Linux localhost 5.10.110-android12-9 #1 SMP PREEMPT Wed Apr 20 14:10:20 UTC 2022 aarch64
```

then you can try to exploit this kernel using modified exp.
