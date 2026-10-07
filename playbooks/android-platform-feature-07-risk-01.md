## android-platform-feature-07-risk-01

### Title

Accessing the application’s private data directory

### Description

Because the Android platform provides rooting feature, your application is at risk of an attacker accessing the application’s private data directory.

### Goal

As a result, this could lead to **_Collection_** - attackers gathering data of interest to their goal.

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* An emulated Google Pixel 6 running Android 12 (api level 31)

#### 02. Identify potentially sensitive files

Identify potentially sensitive files stored by the application using superuser privileges. Use the ls command to enumerate files within the application's private data directory and locate files that may contain sensitive information. Once identified, use the cat command to read the contents of the file directly from the directory

```cmd
adb shell "su -c 'ls /data/data/com.demo.victimapp/files/'"
```

```cmd
adb shell "su -c 'cat /data/data/com.demo.victimapp/files/pii.json'"
```
