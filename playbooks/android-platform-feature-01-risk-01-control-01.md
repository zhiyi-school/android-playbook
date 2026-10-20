## android-platform-feature-01-risk-01-control-01

### Title

Prevent reverse engineering

### Description

Prevent reverse engineering by enabling `R8`/`Proguard` in `app/build.gradle` to rename classes, methods and variables into short, meaningless words.

### Demonstration

#### 01. Prevent reverse engineering

Prevent reverse engineering by enabling `R8/Proguard` in `app/build.gradle` to rename classes, methods and variables into short, meaningless words.

```groovy
buildTypes {
    release {
        minifyEnabled true
        shrinkResources true
        proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        signingConfig signingConfigs.release
    }
}
```

*Code block shows R8 code shrinking, obfuscation and resource shrinking enabled for release builds*

> Note: Do not sign debug builds with the release key. A debuggable build signed with the release key can be installed over the production app as an update, and `run-as` then gives access to the production app's data.

<img src="assets/feature1_risk1_control1_ss1.png" width="800" alt="Obfuscated class and method names in the application output">

*Screenshot shows obfuscated class and method names in the application output.*

#### 02. Hide hardcoded values from simple string searches

Hide hardcoded values from simple string searches by storing them as XOR-obfuscated byte arrays. This stops the value appearing in MobSF's hardcoded-secrets report. 

```java
public static String getApiKey() {
    // Encrypted bytes of "sk_live_1234567890abcdef"
    byte[] encrypted = {
        0x29, 0x50, 0x17, 0x79, 0x23, 0x47, 0x05, 0x60,
        0x3B, 0x08, 0x4D, 0x21, 0x7A, 0x16, 0x58, 0x6F,
        0x3B, 0x0A, 0x4F, 0x28, 0x73, 0x1C, 0x05, 0x6D
    };
    return decrypt(encrypted);
}
```

*Code block shows the API key stored as an XOR-obfuscated byte array and decoded at runtime*

```java
/**
 * XOR decryption - reverses the encryption
 */
private static String decrypt(byte[] encrypted) {
    byte[] decrypted = new byte[encrypted.length];
    for (int i = 0; i < encrypted.length; i++) {
        decrypted[i] = (byte) (encrypted[i] ^ KEY[i % KEY.length]);
    }
    return new String(decrypted);
}
```

*Code block shows the XOR routine that recovers the original value using a key stored in the app*

However, it is obfuscation, not encryption: the key is in the same APK, so the value can be recovered with a decompiler or by hooking `getApiKey()` at runtime.

> Note: Secret keys, such as payment `sk_live_` keys, must not be shipped in the app in any form. Keep them on the server and have the app call the server instead.

The source code with the implemented control can be found [here](control-examples/android-platform-feature-01-risk-01-control-01.zip).
