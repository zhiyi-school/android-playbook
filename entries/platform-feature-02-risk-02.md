## platform-feature-02-risk-02

### Description

Because the Android platform provides USB debugging feature, your application is at risk of an attacker capturing the application's runtime logs via Android Debug Bridge (ADB).

### Goal

As a result, this could lead to **_Collection_** - attackers gathering data of interest like session tokens, credit card numbers to their goal.

### Demonstration
#### 01. Prepare the environment

Set up the required environment with:
* An emulated Google Pixel 6 running Android 12 (api level 31)
* A Windows host computer with Android Studio & adb installed

#### 02.

Ensure the AVD is connected to your computer and detectable by Android Studio to facilitate communication via Android Debug Bridge (ADB) for log capture

``` cmd
adb devices
``` 

#### 03.

Open the Logcat window in Android Studio by navigating to View → Tool Windows → Logcat from the menu bar to view logs from the connected device in real-time

#### 04.

Perform sensitive user actions in your application (e.g.  login, profile updates, payments) to trigger logs that might expose sensitive data.

#### 05.

Filter the logs by your application’s package name, (e.g. "gov.sg.cpf.mycpf") to isolate the specific logs related to your application

#### 06.

Export the filtered logs using the Logcat’s export function to capture evidence of any sensitive data exposure in the logs