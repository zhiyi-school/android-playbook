## platform-feature-05-risk-02

### Description

Because the Android platform provides accessibility services feature, your application is at risk of an attacker capturing user activities within the app.

### Goal

As a result, this could lead to **_Collection_** - attackers gathering data of interest to their goal.

### Demonstration
#### 01. Prepare the environment

Set up the required environment with:
* An emulated Google Pixel 6 running Android 12 (api level 31)

#### 02.

Create a malicious application by declaring an accessibility service in the manifest with android.permission.BIND_ACCESSIBILITY_SERVICE to register the application as an accessibility service

#### 03.

Define how the accessibility service operates by (a) creating an XML configuration file in @xml/accessibility_service_config_event to specify the accessibility event types to capture (e.g., TYPE_VIEW_TEXT_CHANGED, TYPE_VIEW_FOCUSED, TYPE_VIEW_CLICKED), and (b) implementing a service class (e.g., .EventListenerAccessibilityService) that handles the captured accessibility events and persists the collected data to local storage after the user grants accessibility permission

#### 04.

Install the malicious application on the device, perform the steps listed in platform-feature-05, and then launch and use the benign application to trigger accessibility event capture
