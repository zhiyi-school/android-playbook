## android-platform-feature-01-risk-02

### Title

Repackaging the application's APK file

### Description

Repackage the application's APK to modify the application and avoid being detected (MITRE ATT&CK: ***Defense Evasion*** - TA0030).

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* A physical Samsung A34 running Android 16 (api level 36)
* A physical Huawei P50 Pro running HarmonyOS 4.2.0 (Android API level 31)
* A Windows host computer with Android Debug Bridge (ADB), Apktool & keytool installed
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

#### 05. Unpack the APK

Unpack the APK using APKtool to access your application’s files.

```cmd
apktool d <apk-name>
```

#### 06. Edit the AndroidManifest.xml

Edit the AndroidManifest.xml by adding debuggable="true" to the \<application> tag to allow Android Debug Bridge (ADB) debugging.

```xml
android:debuggable="true"
```

*Code block shows setting debuggable to true*

#### 07. Rebuild the modified APK

Rebuild the modified APK using APKtool to save the changes and create a new APK.

```cmd
apktool b <decompiled_folder> -o <output_apk_name>
```

#### 08. Generate a self-signed certificate

Generate a self-signed certificate, align the rebuilt APK, and then sign it. Android only installs signed apps, and the APK must be aligned before signing because aligning afterwards invalidates the signature.

```cmd
keytool -genkeypair -v -keystore test.keystore -alias test -keyalg RSA -keysize 2048 -validity 365

zipalign -p -f 4 <output_apk_name> aligned.apk
apksigner sign --ks test.keystore --ks-key-alias test --out signed.apk aligned.apk
```

#### 09. Install the repackaged APK

Uninstall the original app. Android refuses to install an app over one signed with a different key, and uninstalling deletes the original app's data.

```cmd
adb uninstall <package-name>
adb install signed.apk
```

Install the repackaged APK to verify if the app is debuggable. 

```cmd
adb install <apk> or adb install-multiple <apk1> <apk2>
```

For split APKs, install them together with `adb install-multiple <apk1> <apk2>`.

#### 10. List files in the app’s private directory

List files in the app’s private directory to confirm the repackaged app is now debuggable.

```cmd
adb shell run-as <package-name> ls -R
```

Android-Platform-Feature-01-Risk-02 control measures:

- [android-platform-feature-01-risk-02-control-01](android-platform-feature-01-risk-02-control-01.md)
