## android-platform-feature-06-risk-01

### Title

Capturing on-screen content

### Description

Capture on-screen content through screen recording to gather data of interest from the application (MITRE ATT&CK: ***Collection*** - TA0035).

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* A physical Samsung A34 running Android 16 (api level 36)
* A physical Huawei P50 Pro running HarmonyOS 4.2.0 (Android API level 31)

#### 02. Start screen recording

Swipe down from the top of the device screen to open `Quick Settings`, then locate and tap `Screen record`. 

> Note: Screen recording in the application does not require any manual setup through `Quick Settings`. The app can initiate screen recording programmatically, but it becomes active only after the user grants permission via the system prompt at runtime. The `Quick Settings` steps are shown here to demonstrate how screen recording works.

<img src="assets/feature6_ss1.png" width="800" alt="The screen recording control highlighted in Quick Settings">

*Screenshot shows the screen recording control highlighted in` Quick Settings`.*

#### 03. Create a malicious application

Create a malicious application by declaring a foreground service in the manifest with `foregroundServiceType="mediaProjection"` to register the application’s screen capture capability.

```xml
<!-- Foreground service for persistent capture -->
<uses-permission android:name="android.permission.FOREGROUND_SERVICE"/>
<uses-permission android:name="android.permission.FOREGROUND_SERVICE_MEDIA_PROJECTION"/>
```

*Code block shows the foreground service permissions in AndroidManifest.xml*

> Note: Third-party apps cannot be granted `CAPTURE_VIDEO_OUTPUT` or `CAPTURE_SECURE_VIDEO_OUTPUT`. They capture the screen through `MediaProjection`, which requires the user to accept a consent prompt.

```xml
<service
    android:name=".ScreenCaptureService"
    android:enabled="true"
    android:exported="false"
    android:foregroundServiceType="mediaProjection" />
```

*Code block shows Manifest.xml with screen capture service*

#### 04. Define how the screen capture service operates

Define how the screen capture service operates by implementing a service class (e.g., `.ScreenCaptureService`) that requests explicit user permission for screen recording, captures the device screen, and persists the recorded output.

```kotlin
@ReactMethod
fun requestScreenCapturePermission(promise: Promise) {
    val activity = reactApplicationContext.currentActivity
    if (activity == null) {
        promise.reject("NO_ACTIVITY", "Activity is null")
        return
    }

    try {
        screenCapturePromise = promise
        val projectionManager = reactApplicationContext.getSystemService(Context.MEDIA_PROJECTION_SERVICE) as MediaProjectionManager
        val captureIntent = projectionManager.createScreenCaptureIntent()
        activity.startActivityForResult(captureIntent, REQUEST_CODE_SCREEN_CAPTURE)
        Log.d(TAG, "Started screen capture permission request")
    } catch (e: Exception) {
        Log.e(TAG, "Error requesting screen capture", e)
        promise.reject("ERROR", "Failed to request screen capture: ${e.message}")
        screenCapturePromise = null
    }
}
```

*Code block shows malicious code logic for screen capture*

#### 05. Record the target app

Install and launch the malicious application, start its screen capture, and accept the system prompt. Open the target app and display the information to be tested, then stop the capture and review the saved recording for sensitive information.

<img src="assets/feature6_risk1_ss1.png" width="800" alt="The system prompt requesting permission to record the screen">

*Screenshot shows the system prompt requesting permission to record the screen.*

<img src="assets/feature6_risk1_ss2.png" width="800" alt="The target application&#x27;s screen during an active recording">

*Screenshot shows the target application's screen during an active recording.*

<img src="assets/feature6_risk1_ss3.png" width="800" alt="Saved screen recordings in Device Explorer">

*Screenshot shows saved screen recordings in Device Explorer.*

Android-Platform-Feature-06-Risk-01 control measures:

- [android-platform-feature-06-risk-01-control-01](android-platform-feature-06-risk-01-control-01.md)
