## android-platform-feature-01-risk-01

### Title

Analysing the application's APK file

### Description

Because the Android platform provides APK acquisition feature, your application is at risk of an attacker analysing the application's APK file.

### Goal

As a result, this could lead to **_Discovery_** -  attackers figuring out the APK’s vulnerabilities.

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* An emulated Google Pixel 6 running Android 12 (api level 31)
* A MobSF instance running and accessible through a web browser

#### 02. Set up a mobile application analyser

Set up a mobile application analyser like Mobile Security Framework (MobSF) to perform analysis on APKs

#### 03. Upload a target APK

Upload a target APK to initiate the analysis

<img src="assets/feature1_risk1_ss1.png" width="800" alt="The APK upload interface in MobSF">

*Screenshot shows the APK upload interface in MobSF.*

<img src="assets/feature1_risk1_ss2.png" width="800" alt="Findings in the MobSF network security report">

*Screenshot shows findings in the MobSF network security report.*
