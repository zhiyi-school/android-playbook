## android-platform-feature-01

### Title

APK acquisition

### Description

The Android platform provides APK acquisition feature.

### Additional context

APK acquisition is a feature that allows Android Package Kit (APKs) to be extracted from a device using the Android Debug Bridge (ADB) tool. It enables developers to retrieve, inspect, and transfer installed application binaries from a connected Android device to a computer.

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* A physical Samsung A34 running Android 16 (api level 36)
* A physical Huawei P50 Pro running HarmonyOS 4.2.0 (Android API level 31)

#### 02. List the AVD’s installed application packages

List the AVD’s installed application packages to identify the target application's package name (e.g. sg.ndi.sp)

```cmd
adb shell pm list packages | findstr sg
```

#### 03. Retrieve a file path

Retrieve a file path using the target’s application package name to locate where the APK is stored on the AVD

```cmd
adb shell pm path <package-name>
```

#### 04. Copy the APK

Copy the APK from the AVD to your local machine for analysis

```cmd
adb pull <path>
```

Because the Android platform provides APK acquisition feature, your app is at risk of:

- [android-platform-feature-01-risk-01](android-platform-feature-01-risk-01.md)
- [android-platform-feature-01-risk-02](android-platform-feature-01-risk-02.md)
