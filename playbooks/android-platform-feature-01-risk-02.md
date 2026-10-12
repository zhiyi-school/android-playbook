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
* A Windows host computer with Apktool & keytool installed

#### 02. Unpack the APK

Unpack the APK using APKtool to access your application’s files

```cmd
apktool d <apk-name>
```

#### 03. Edit the AndroidManifest.xml

Edit the AndroidManifest.xml by adding debuggable="true" to the \<application> tag to allow Android Debug Bridge (ADB) debugging

*Code excerpt from the screenshot (partial):*

```xml
android:debuggable="true"
```

#### 04. Rebuild the modified APK

Rebuild the modified APK using APKtool to save the changes and create a new APK

```cmd
apktool b <decompiled_folder> -o <output_apk_name>
```

#### 05. Generate a self-signed certificate

Generate a self-signed certificate and use it to sign the APK(s) using the keytool command to allow installation on an Android device, as all apps must be signed

```cmd
keytool -alias colesmith -genkey -v -keystore release.keystore -keyalg RSA
```
```cmd
apksigner sign --ks release.keystore base.apk
```

#### 06. Install the repackaged APK

Install the repackaged APK to verify if the app is debuggable. Note that this only happen if the legitimate app is not installed on the device

```cmd
adb install <apk> or adb install-multiple <apk1> <apk2>
```

#### 07. List files in the app’s private directory

List files in the app’s private directory to confirm the repackaged app is now debuggable

```cmd
adb shell run-as <apk_name> ls -R
```

### Additional screenshot from the PDF

<img src="assets/feature1_risk2_ss1.png" width="800" alt="The device home screen with the application icons highlighted">

*Screenshot shows the device home screen with the application icons highlighted.*
