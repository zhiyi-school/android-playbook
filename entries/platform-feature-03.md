## platform-feature-03

### Description

The Android platform provides HTTP Proxy feature.

### Additional context

HTTP Proxy is a feature that allows all network traffic to be routed from an Android Virtual Device through an intermediary proxy server before it reaches the internet. Proxies are usually used for corporate network access or content filtering..

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:
* An emulated Google Pixel 6 running Android 12 (api level 31)

#### 02.

Configure Burp Suite to listen on all network interfaces of the host computer running Burp so the AVD can connect to it by launching Burp, clicking ‘Next’, selecting ‘Start Burp’, navigating to the ‘Proxy’ tab, opening ‘Proxy Settings’, selecting the existing listener at 127.0.0.1:8080, clicking ‘Edit’, changing the binding to ‘All Interfaces’, and clicking ‘OK’ to apply the changes

#### 03.

Configure Android Debug Bridge (ADB) to set the AVD’s HTTP proxy to the host computer’s IP address and Burp port so traffic from the AVD is routed through Burp by launching the AVD, opening an ADB shell (adb shell), finding the host IP using ipconfig or ifconfig, and running settings put global http_proxy <HOST_IP>:8080

#### 04.

To enable interception of HTTPS traffic: Export Burp Suite’s CA certificate in DER format to create a certificate file (ca.crt) that will be installed into the AVD’s trusted credential store

#### 05.

To enable interception of HTTPS traffic: Transfer the ca.crt file from the host computer to the AVD using ADB so that the Android system can access and install it as a trusted CA certificate

``` cmd
adb -s emulator-<id> push ca.crt /sdcard/Download/ca.crt
``` 

#### 06.

To enable interception of HTTPS traffic: Install the CA certificate on the Android Virtual Device by navigating to Settings → Security → Encryption & Credentials → Install a Certificate → CA Certificate and selecting the uploaded ca.crt file to allow Android system to trust Burp’s generated certificates and enable HTTPS traffic inspection

Because the Android platform provides HTTP Proxy feature, your app is at risk of: 
- platform-feature-03-risk-01