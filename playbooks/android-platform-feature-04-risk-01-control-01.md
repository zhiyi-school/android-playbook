## android-platform-feature-04-risk-01-control-01

### Title

Prevent overlay windows from appearing over your app

### Description

Insert here

### Demonstration

#### 01. Prevent overlay windows from appearing over your app

Prevent overlay windows from appearing over your app by calling window.setHideOverlayWindows(true) in onResume()

*Code excerpt from the screenshot (partial):*

```kotlin
class MainActivity : ReactActivity() {
    override fun invokeDefaultOnBackPressed() {
        super.invokeDefaultOnBackPressed()
    }

    override fun onResume() {
        super.onResume()
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.Q) {
            window.setHideOverlayWindows(true)
        }
    }
```
