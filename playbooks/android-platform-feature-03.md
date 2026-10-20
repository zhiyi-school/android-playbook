## android-platform-feature-03

### Title

HTTP Proxy

### Description

HTTP Proxy is a feature that allows all network traffic to be routed from an Android device through an intermediary proxy server before it reaches the internet. Proxies are usually used for corporate network access or content filtering.
### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* A physical Samsung A34 running Android 16 (api level 36)
* A physical Huawei P50 Pro running HarmonyOS 4.2.0 (Android API level 31)

#### 02. Configure Burp Suite

Configure Burp Suite to accept connections from the test device. Launch Burp, open the `Proxy` tab, and select `Proxy settings`. Under `Proxy listeners`, click `Add`, set `Bind to port` to `8081`, set `Bind to address` to `All interfaces`, and click `OK`.

<img src="assets/feature3_ss3.png" width="800" alt="The Proxy tab highlighted in Burp Suite">

*Screenshot shows the `Proxy` tab highlighted in Burp Suite.*

<img src="assets/feature3_ss4.png" width="800" alt="The Proxy settings button highlighted in Burp Suite">

*Screenshot shows the `Proxy settings` button highlighted in Burp Suite.*

<img src="assets/feature3_ss5.png" width="800" alt="The proxy listener settings and edit option">

*Screenshot shows the proxy listener settings with Add option highlighted.*

<img src="assets/feature3_ss6.png" width="800" alt="The listener binding set to All interfaces">

*Screenshot shows the adding a listener with bind to port set to `8081` and binding set to `All interfaces`.*

#### 03. Route the device's traffic through Burp

On the host computer, find its IP address by running `ipconfig` (Windows) or `ifconfig` (macOS/Linux). Then set the test device's global HTTP proxy to that address and the Burp listener port:

```cmd
adb shell settings put global http_proxy <HOST_IP>:8081
```

When testing is finished, remove the proxy setting:

```cmd
adb shell settings put global http_proxy :0
```

#### 04. Export Burp Suite’s CA certificate

To enable interception of HTTPS traffic: Export Burp Suite’s CA certificate in DER format to create a certificate file (`ca.crt`) that will be installed into the test device’s trusted credential store.

<img src="assets/feature3_ss7.png" width="800" alt="The certificate export dialog with the DER format selected">

*Screenshot shows the certificate export dialog with the DER format selected.*

#### 05. Transfer the `ca.crt` file

To enable interception of HTTPS traffic: Transfer the ca.crt file from the host computer to the test device using ADB so that the Android system can access and install it as a trusted CA certificate.

```cmd
adb push ca.crt /sdcard/Download/ca.crt
```

#### 06. Install the CA certificate

To enable interception of HTTPS traffic: open `Settings`, search for `CA certificate`, select the option to install a CA certificate, and choose the transferred `ca.crt` file. 

<img src="assets/feature3_ss8.png" width="800" alt="The Android settings screens for installing a CA certificate">

*Screenshot shows the Android settings screens for installing a CA certificate.*

> Note: Since Android 7 (API level 24), apps trust user-installed CA certificates only if their network security configuration allows it. Most apps do not, so their HTTPS connections fail through Burp whether or not they use certificate pinning. A failed connection at this point does not show that the app pins certificates. To test the app's own behaviour, use one of the following:
>
> - A debug build of the app whose network security configuration trusts user certificates in `<debug-overrides>`
> - A rooted test device, such as the Corellium device in [android-platform-feature-07](android-platform-feature-07.md), with Burp's CA installed as a system certificate. On Android 14 and later, the system store is under `/apex/com.android.conscrypt/cacerts`.

```xml
<network-security-config>
    <debug-overrides>
        <trust-anchors>
            <certificates src="user" />
        </trust-anchors>
    </debug-overrides>
</network-security-config>
```

*Code block shows a network security configuration that trusts user certificates in debug builds only*

Because the Android platform provides HTTP Proxy feature, your app is at risk of:

- [android-platform-feature-03-risk-01](android-platform-feature-03-risk-01.md)
