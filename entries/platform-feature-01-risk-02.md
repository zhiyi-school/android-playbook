## platform-feature-01-risk-02

### Description

Because the Android platform provides APK acquisition feature, your application is at risk of an attacker repackaging the application's APK file.

### Goal

As a result, this could lead to **_Defense evasion_** -  attackers avoid being detected.

### Demonstration
#### 01. Prepare the environment

Set up the required environment with:
* An emulated Google Pixel 6 running Android 12 (api level 31)
* A Windows host computer with Apktool & keytool installed

#### 02.

Unpack the APK using APKtool to access your application’s files

``` cmd
apktool d <apk-name>
``` 

#### 03.

Edit the AndroidManifest.xml by adding debuggable="true" to the <application> tag to allow Android Debug Bridge (ADB) debugging 

#### 04.

Rebuild the modified APK using APKtool to save the changes and create a new APK

``` cmd
apktool b <decompiled_folder> -o <output_apk_name>
``` 

#### 05.

Generate a self-signed certificate and use it to sign the APK(s) using the keytool command to allow installation on an Android device, as all apps must be signed

``` cmd
keytool -alias colesmith -genkey -v -keystore release.keystore -keyalg RSA
``` 
``` cmd
apksigner sign --ks release.keystore base.apk
```

#### 06.

Install the repackaged APK to verify if the app is debuggable. Note that this only happen if the legitimate app is not installed on the device

``` cmd
adb install <apk> or adb install-multiple <apk1> <apk2>
```

#### 07.

List files in the app’s private directory to confirm the repackaged app is now debuggable

``` cmd
adb shell run-as <apk_name> ls -R
```
