---
layout: post
title: "AOSP build"
date: 2021-03-05 10:41:14 +0900
categories: android
---


pixel 3 기준

```
lunch aosp_blueline-userdebug
m -j4
```


다 되면 
```
adb reboot bootloader 

fastboot flash boot out/target/product/blueline/boot.img
fastboot flash system out/target/product/blueline/system.img
fastboot flash vendor out/target/product/blueline/vendor.img
fastboot flash userdata out/target/product/blueline/userdata.img

//없네..
fastboot flash recovery out/target/product/blueline/recovery.img


fastboot flashall -w


```




https://go-madhat.github.io/AOSP/
