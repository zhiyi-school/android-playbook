## platform-feature-02

### Description

The Android platform provides USB debugging feature.

### Additional context

USB debugging is a feature that allows communication between an Android device and a computer via Android Debug Bridge (ADB). It enables developers to install apps, run commands, access logs, and debug applications. 

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:
* An emulated Google Pixel 6 running Android 12 (api level 31)

#### 02.

On the AVD, go to “Settings > About Device > Build Number”. Then, click on the “Build Number” setting 7 times to enable developer mode

#### 03.

Toggle the USB Debugging option to enable USB Debugging

Because the Android platform provides APK acquisition feature, your app is at risk of: 
- platform-feature-02-risk-01
- platform-feature-02-risk-02