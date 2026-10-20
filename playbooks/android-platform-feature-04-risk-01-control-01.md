## android-platform-feature-04-risk-01-control-01

### Title

Prevent overlay windows from appearing over your app

### Description

Prevent overlay windows from appearing over your app by calling window.setHideOverlayWindows(true) in onResume().

### Demonstration

#### 01. Prevent overlay windows from appearing over your app

Declare the permission in `AndroidManifest.xml`. `setHideOverlayWindows()` is available from Android 12 (API level 31).

```xml
<uses-permission android:name="android.permission.HIDE_OVERLAY_WINDOWS" />
```

*Code block shows adding `setHideOverlayWindows()` permission in `AndroidManifest.xml`.*

Prevent overlay windows from appearing over your app by calling `window.setHideOverlayWindows(true)` in `onResume()`.

```kotlin
class MainActivity : ReactActivity() {
    override fun invokeDefaultOnBackPressed() {
        super.invokeDefaultOnBackPressed()
    }

    override fun onResume() {
        super.onResume()
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.S) {
            window.setHideOverlayWindows(true)
        }
    }
```

*Code block shows implementation of `window.setHideOverlayWindows(true)`*
