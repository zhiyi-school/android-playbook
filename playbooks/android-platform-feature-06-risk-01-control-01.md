## android-platform-feature-06-risk-01-control-01

### Title

Prevent on-screen content from being captured in screen recordings

### Description

Prevent on-screen content from being captured in screen recordings by setting `FLAG_SECURE` in `onCreate()`. This flag instructs the system to block the content of the window from being recorded or displayed on non-secure displays, protecting sensitive information from being captured by screen recording or screenshots.

### Demonstration

#### 01. Prevent on-screen content from being captured in screen recordings

Prevent on-screen content from being captured in screen recordings by setting `FLAG_SECURE` in `onCreate()`. This flag instructs the system to block the content of the window from being recorded or displayed on non-secure displays, protecting sensitive information from being captured by screen recording or screenshots.

```kotlin
class MainActivity : ReactActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        window.setFlags(
            WindowManager.LayoutParams.FLAG_SECURE,
            WindowManager.LayoutParams.FLAG_SECURE
        )
        // Set the theme to AppTheme BEFORE onCreate to support
        // coloring the background, status bar, and navigation bar.
        // This is required for expo-splash-screen.
        setTheme(R.style.AppTheme);
        super.onCreate(null)
    }
```

*Code block shows implementation of `FLAG_SECURE`*

> Note: `FLAG_SECURE` applies only to the window it is set on. Dialogs, popup windows, bottom sheets, and React Native `<Modal>` content open in separate windows that do not inherit it, so set the flag on those windows too and include them when verifying the control.