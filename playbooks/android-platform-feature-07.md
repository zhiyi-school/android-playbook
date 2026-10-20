## android-platform-feature-07

### Title

Rooting

### Description

Rooting is a feature that gives full control over an Android device. It grants superuser access, allowing system files to be modified and Android restrictions to be bypassed via advanced tools that run with elevated privileges.

This playbook demonstrates rooting on a Corellium Android virtual device instead of a physical rooted phone. Corellium Android virtual devices provide root access by default, so no rooting tool such as Magisk needs to be installed.

> Note: A physical rooted Android device is currently not available for testing, so this playbook is demonstrated only on a Corellium virtual device.
### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* A Corellium account with a project that can create Android virtual devices
* A Corellium Android virtual device running Android 14 (API level 34)
* A host machine with Android Platform Tools (`adb`) installed
* Network access from the host machine to the Corellium device through the Corellium VPN profile
* The target app APK available for installation

#### 02. Create and boot the device

In the Corellium project, create a new device, select `Android`, choose Android 14, and start the device. Corellium boots the virtual device with root access available, providing a controlled Android environment with the elevated privileges used during testing.

<img src="assets/feature7_ss2.png" width="800" alt="Corellium device creation with Android 14 selected">

*Screenshot shows creating an Android 14 virtual device in the Corellium project.*

#### 03. Connect to the device over ADB

Open the device's `Connect` tab in Corellium, download and connect the VPN profile, then run the `adb connect` command shown in the tab using the device's IP address.

```cmd
adb connect <device-ip>:5001
```

*Command shows connecting ADB to the Corellium device*

```cmd
adb devices
```

*Command shows confirming the Corellium device is listed as connected*

#### 04. Install the target app

Install the target app on the Corellium device over ADB.

```cmd
adb install victimapp.apk
```

*Command shows installing the target app on the Corellium device*

#### 05. Confirm root access

Run `id` through `su` and confirm the output shows `uid=0(root)`. Confirming root access establishes that the device is ready for the risks that follow.

```cmd
adb shell "su -c 'id'"
```

*Command shows confirming that commands run with superuser privileges*

Because the Android platform provides rooting feature, your app is at risk of:

- [android-platform-feature-07-risk-01](android-platform-feature-07-risk-01.md)
