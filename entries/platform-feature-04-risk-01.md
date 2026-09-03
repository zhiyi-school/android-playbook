## platform-feature-04-risk-01

### Description

Because the Android platform provides overlay feature, your application is at risk of an attacker drawing over its user interface with a malicious application.

### Goal

As a result, this could lead to **_Credential access_** - attackers stealing usernames & passwords.

### Demonstration
#### 01. Prepare the environment

Set up the required environment with:
* An emulated Google Pixel 6 running Android 12 (api level 31)

#### 02.

Create a malicious application by adding the android.permission.SYSTEM_ALERT_WINDOW permission to the manifest and implementing logic to invoke windowManager.addView() (e.g., within showOverlay()) to display an overlay when the malicious application runs in the background

#### 03.

Install the malicious application on the device, perform the steps listed in platform-feature-04, and then launch the application