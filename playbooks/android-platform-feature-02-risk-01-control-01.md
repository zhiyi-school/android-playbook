## android-platform-feature-02-risk-01-control-01

### Title

Prevent access to private data directory information

### Description

Prevent access to private data directory information by encrypting sensitive data at rest using AES-256 encryption with a SecretKey stored in the Android Keystore.

### Demonstration

#### 01. Prevent access to private data directory information

Prevent access to private data directory information by encrypting sensitive data at rest using AES-256 encryption with a SecretKey stored in the Android Keystore.

```java
public String encrypt(String plaintext) throws Exception {
    if (plaintext == null || plaintext.isEmpty()) {
        return "";
    }

    Cipher cipher = Cipher.getInstance(TRANSFORMATION);
    cipher.init(Cipher.ENCRYPT_MODE, getOrCreateKey());

    // Encrypt the data
    byte[] encryptedBytes = cipher.doFinal(plaintext.getBytes(StandardCharsets.UTF_8));

    // Get the IV (Initialization Vector)
    byte[] iv = cipher.getIV();

    // Combine IV and encrypted data
    // Format: Base64(IV) + SEPARATOR + Base64(Ciphertext)
    String ivString = Base64.encodeToString(iv, Base64.DEFAULT);
    String encryptedString = Base64.encodeToString(encryptedBytes, Base64.DEFAULT);
```

*Code block shows implementation of AES-256 encryption*

```java
private SecretKey getOrCreateKey() throws Exception {
    KeyStore keyStore = KeyStore.getInstance(ANDROID_KEYSTORE);
    keyStore.load(null);

    // Reuse the key if it was created on an earlier run.
    SecretKey existing = (SecretKey) keyStore.getKey(KEY_ALIAS, null);
    if (existing != null) {
        return existing;
    }

    // Otherwise create a 256-bit AES key inside the Android Keystore.
    KeyGenParameterSpec spec = new KeyGenParameterSpec.Builder(
            KEY_ALIAS,
            KeyProperties.PURPOSE_ENCRYPT | KeyProperties.PURPOSE_DECRYPT)
            .setBlockModes(KeyProperties.BLOCK_MODE_GCM)
            .setEncryptionPaddings(KeyProperties.ENCRYPTION_PADDING_NONE)
            .setKeySize(256)
            .build();

    KeyGenerator keyGenerator = KeyGenerator.getInstance(KeyProperties.KEY_ALGORITHM_AES, ANDROID_KEYSTORE);
    keyGenerator.init(spec);
    return keyGenerator.generateKey();
}
```

*Code block shows retrieving the AES key from the Android Keystore, or creating it on first use*

<img src="assets/feature2_risk1_control1_ss1.png" width="800" alt="The application&#x27;s stored files in Device Explorer">

*Screenshot shows the application's stored files in Device Explorer.*

<img src="assets/feature2_risk1_control1_ss2.png" width="800" alt="Encrypted data in the stored preferences file">

*Screenshot shows encrypted data in the stored preferences file.*

The source code with the implemented control can be found [here](control-examples/android-platform-feature-02-risk-01-control-01.zip).
