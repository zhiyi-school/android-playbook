## platform-feature-06-risk-01

### Description

Because the Android platform provides screen recording feature, your application is at risk of an attacker capturing on-screen content.

### Goal

As a result, this could lead to **_Collection_** - attackers gathering data of interest to their goal.

### Demonstration
#### 01. Prepare the environment

Set up the required environment with:
* An emulated Google Pixel 6 running Android 12 (api level 31)

#### 02.

Create a malicious application by declaring a foreground service in the manifest with foregroundServiceType="mediaProjection" to register the application’s screen capture capability

#### 03.

Define how the screen capture service operates by implementing a service class (e.g., .ScreenCaptureService) that requests explicit user permission for screen recording, captures the device screen, and persists the recorded output

