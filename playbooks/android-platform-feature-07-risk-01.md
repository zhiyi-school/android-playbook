## android-platform-feature-07-risk-01

### Title

Accessing the application’s private data directory

### Description

Access the application's private data directory on a rooted device to gather data of interest (MITRE ATT&CK: ***Collection*** - TA0035).

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* A physical Samsung A34 running Android 16 (api level 36)
* A physical Huawei P50 Pro running HarmonyOS 4.2.0 (Android API level 31)

#### 02. Identify potentially sensitive files

Identify potentially sensitive files stored by the application using superuser privileges. Use the ls command to enumerate files within the application's private data directory and locate files that may contain sensitive information. Once identified, use the cat command to read the contents of the file directly from the directory

```cmd
adb shell "su -c 'ls /data/data/com.demo.victimapp/files/'"
```

```cmd
adb shell "su -c 'cat /data/data/com.demo.victimapp/files/pii.json'"
```
