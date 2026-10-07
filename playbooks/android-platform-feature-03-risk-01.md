## android-platform-feature-03-risk-01

### Title

Intercepting the application's network traffic

### Description

Because the Android platform provides HTTP Proxy feature, your application is at risk of an attacker intercepting the application's network traffic.

### Goal

As a result, this could lead to **_Collection_** - attackers trying to gather data of interest to their goal.

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* An emulated Google Pixel 6 running Android 12 (api level 31)
* A Windows host computer
* A Burp Suite instance running

#### 02. Launch your application

Launch your application and perform a sensitive user action, such as logging in or registering, to trigger API requests that may transmit sensitive data

#### 03. Inspect the intercepted requests and responses

Inspect the intercepted requests and responses in Burp Suite to identify any sensitive information

<img src="assets/feature3_risk1_ss1.png" width="800" alt="An intercepted HTTP request containing username and password fields">

*Screenshot shows an intercepted HTTP request containing username and password fields.*
