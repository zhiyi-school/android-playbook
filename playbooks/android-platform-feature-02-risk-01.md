## android-platform-feature-02-risk-01

### Title

Accessing the application’s private data directory

### Description

Access the application's private data directory through USB debugging to obtain stored usernames and passwords (MITRE ATT&CK: ***Credential Access*** - TA0031).

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* A physical Samsung A34 running Android 16 (api level 36)
* A physical Huawei P50 Pro running HarmonyOS 4.2.0 (Android API level 31)
* A Windows host computer with Android Studio, Android Debug Bridge (ADB), Apktool, apksigner & keytool installed

#### 02. Enable developer mode 

On the AVD, go to `Settings > About Device > Build Number`. Then, click on the “`Build Number`” setting 7 times to enable developer mode.

* Samsung A34: Go to `Settings > About phone > Software information` and tap `Build number` seven times.
* Huawei P50 Pro: Go to `Settings > About phone` and tap `HarmonyOS version` seven times.

<img src="assets/feature2_ss1.png" width="800" alt="The Build number setting highlighted on the device">

*Screenshot shows the `Build number` setting highlighted on the device.*

Enter the device's lock-screen PIN if prompted. Open `Developer options` and enable `USB debugging`.

#### 03. Toggle the USB Debugging option

Toggle the USB Debugging option to enable USB Debugging.

<img src="assets/feature2_ss2.png" width="800" alt="The USB debugging toggle enabled in Developer options">

*Screenshot shows the `USB debugging` toggle enabled in Developer options.*

Connect the selected test device to the host computer and approve the debugging prompt on the device. Confirm that it is connected:

```shell
adb devices
```

Use one connected test device at a time. If multiple devices are listed, use `adb -s <device-serial>` instead of `adb` for the commands below.

#### 04. Check the installed app

Check whether the app installed from the store is debuggable or allows backups. If it is, its existing data can be read without repackaging.

```cmd
adb shell dumpsys package <package-name> | findstr pkgFlags
adb shell run-as <package-name> ls
```

*Command shows the app's package flags and attempts to list its private directory*

If `pkgFlags` includes `DEBUGGABLE`, or `run-as` lists files, the installed app is debuggable: continue from the Android Studio steps below without repackaging. If `pkgFlags` includes `ALLOW_BACKUP`, try `adb backup -f app.ab <package-name>`. On Android 12 and later, a backup only includes app data for apps that target API level 30 or lower.

#### 05. Prepare a debuggable APK

> Note: Use this step only if the installed app is not debuggable. The original app must be uninstalled before the repackaged APK can be installed, which deletes its data. This step therefore shows what the app stores after you sign in to the repackaged copy, not data already stored by the original installation.

Disassemble your APK using Apktool:

```cmd
apktool d <apk-name>
```

Add `debuggable="true"` to `AndroidManifest.xml` to enable application debugging, then rebuild the modified APK:

```cmd
apktool b --debug <directory>
```

Generate a self-signed certificate, align the rebuilt APK, and then sign it. Android only installs signed apps, and the APK must be aligned before signing because aligning afterwards invalidates the signature.

```cmd
keytool -genkeypair -v -keystore test.keystore -alias test -keyalg RSA -keysize 2048 -validity 365

zipalign -p -f 4 <output_apk_name> aligned.apk
apksigner sign --ks test.keystore --ks-key-alias test --out signed.apk aligned.apk
```

Install your repackaged APK and verify that it is debuggable.

```cmd
adb install <apk>
```

#### 06. Open Android Studio

Open Android Studio and go to `View → Tool Windows → Device File Explorer` to view device files.

<img src="assets/feature2_risk1_ss1.png" width="800" alt="The Device Explorer option in Android Studio">

*Screenshot shows the Device Explorer option in Android Studio.*

#### 07. Access your application’s private data directory

Navigate to `/data/data/package_name/` to access your application’s private data directory.

> Note: The package name will vary between applications.

<img src="assets/feature2_risk1_ss2.png" width="800" alt="Application files and their contents in Android Studio&#x27;s Device Explorer">

*Screenshot shows application files and their contents in Android Studio's Device Explorer.*

Android-Platform-Feature-02-Risk-01 control measures:

- [android-platform-feature-02-risk-01-control-01](android-platform-feature-02-risk-01-control-01.md)
