---
layout: post
title: "Ionic sync ios error"
date: 2021-03-05 10:41:14 +0900
categories: ionic
---


ionic sync ios를 했을 때 오류가 발생하는 경우

```
ionic capacitor sync ios --no-build
```


오류 내용
```
[!] CocoaPods could not find compatible versions for pod "OneSignal":
  In Podfile:
    CordovaPluginsStatic (from `../capacitor-cordova-ios-plugins`) was resolved to 2.1.2, which depends on
      OneSignal (= 2.14.3)
```


해결 방법 

```
pod repo update

pod install --repo-update

```


cocoapods version 오류 발생시 
```
[!] `FirebaseAnalytics` requires CocoaPods version `>= 1.10.0`, which is not satisfied by your current version, `1.9.1`.

```


cocoapods 업데이트 
```
sudo gem install cocoapods
```




