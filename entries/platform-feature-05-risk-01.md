## platform-feature-05-risk-01

### Description

Because the Android platform provides accessibility services feature, your application is at risk of an attacker performing operations programmatically on its user interface.

### Goal

As a result, this could lead to **_Impact_** - attackers manipulating your application.

### Demonstration
#### 01. Prepare the environment

Set up the required environment with:
* An emulated Google Pixel 6 running Android 12 (api level 31)

#### 02.

Create a malicious application by declaring an accessibility service in the manifest with android.permission.BIND_ACCESSIBILITY_SERVICE to register the application as an accessibility service

#### 03.

Define how the accessibility service operates by (a) creating an XML configuration file in @xml/accessibility_config to specify the event types and service capabilities requested, and (b) implementing a service class (e.g., .EventListenerAccessibilityService) that listens for TYPE_WINDOW_STATE_CHANGED events to detect activity changes and automatically locate and click logout UI elements after the user grants accessibility permission

#### 04.

Install the malicious application on the device, perform the steps listed in platform-feature-05, and then launch the application
