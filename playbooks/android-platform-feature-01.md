## android-platform-feature-01

### Title

APK acquisition

### Description

APK acquisition is a feature that allows Android Package Kit (APKs) to be extracted from a device using the Android Debug Bridge (ADB) tool. It enables developers to retrieve, inspect, and transfer installed application binaries from a connected Android device to a computer.

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* A physical Samsung A34 running Android 16 (api level 36)
* A physical Huawei P50 Pro running HarmonyOS 4.2.0 (Android API level 31)
* A host computer with Android Debug Bridge (ADB) installed
* A target app installed on the selected test device

Connect the selected test device to the host computer with USB debugging enabled and approve the debugging prompt on the device. Confirm that it is connected:

```shell
adb devices
```

Use one connected test device at a time. If multiple devices are listed, use `adb -s <device-serial>` instead of `adb` for the commands below.

#### 02. List the device's installed application packages

List the device's installed application packages to identify the target application's package name (e.g. `sg.ndi.sp`). Replace `<package-filter>` with part of the package name, such as `sg`.

```shell
adb shell pm list packages <package-filter>
```

#### 03. Retrieve the APK paths

Retrieve the APK paths using the target application's package name to locate its installed APK files on the device.

```shell
adb shell pm path <package-name>
```

#### 04. Copy the APK

On the host computer, open a terminal in your local analysis folder and copy the APK from the device using a path returned in the previous step. Replace `<path>` with the APK path without the `package:` prefix. The APK is saved in the terminal's current directory.

```shell
adb pull <path>
```

If multiple APK paths are returned, copy each APK into the same analysis folder and retain its filename. Application content may be distributed across the base APK and split APKs.

Because the Android platform provides APK acquisition feature, your app is at risk of:

- [android-platform-feature-01-risk-01](android-platform-feature-01-risk-01.md)
- [android-platform-feature-01-risk-02](android-platform-feature-01-risk-02.md)
