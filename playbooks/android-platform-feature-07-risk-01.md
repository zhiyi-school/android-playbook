## android-platform-feature-07-risk-01

### Title

Accessing the application’s private data directory

### Description

Access the application's private data directory on a rooted device to gather data of interest (MITRE ATT&CK: ***Collection*** - TA0035).

### Demonstration

#### 01. Prepare the environment

Set up the required environment with:

* A Corellium Android virtual device running Android 14 (API level 34), which provides root access by default
* A host machine with Android Platform Tools (`adb`) installed
* An ADB connection to the Corellium device through the Corellium VPN profile, as shown in [android-platform-feature-07](android-platform-feature-07.md)
* The target app installed on the Corellium device

#### 02. Identify potentially sensitive files

Identify potentially sensitive files stored by the application using superuser privileges. Use the `ls` command to enumerate files within the application's private data directory and locate files that may contain sensitive information. Once identified, use the `cat` command to read the contents of the file directly from the directory.

```cmd
adb shell "su -c 'ls /data/data/com.demo.victimapp/files/'"
```

*Command shows using root user to list file directories*

```cmd
adb shell "su -c 'cat /data/data/com.demo.victimapp/files/pii.json'"
```

*Command shows using root user to view contents of a file*

Android-Platform-Feature-07-Risk-01 control measures:

- [android-platform-feature-07-risk-01-control-01](android-platform-feature-07-risk-01-control-01.md)
