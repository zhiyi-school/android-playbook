## android-platform-feature-01-risk-02-control-01

### Title

Detect modifications to your application

### Description

Insert here

### Demonstration

#### 01. Detect modifications to your application

Detect modifications to your application by calculating the SHA-256 signature hash at runtime and comparing it to a hardcoded expected value

*Code excerpt from the screenshot (partial):*

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // CONTROL FX02-C01: Signature verification MUST be first thing in onCreate()
        // This runs before any other initialization to prevent tampered apps from executing
        if (!SignatureVerification.verifySignature(this)) {
            // Signature mismatch detected - app has been repackaged/tampered
            SignatureVerification.showTamperDialog(this);
            // Dialog will terminate app when user clicks "Exit"
            return; // Stop further initialization
        }

        // If we reach here, signature is valid - continue normal app flow
        initializeApp();
    }

    /**
     * Normal app initialization after signature verification passes.
     */
    private void initializeApp() {
        TextView statusText = findViewById(R.id.statusText);
        statusText.setText("✓ Signature verification passed!\n\nThis app is authentic and has not been modified.");
```

```java
private static boolean verifySignatureHash(Signature signature) {
    try {
        // Get the raw certificate bytes
        byte[] signatureBytes = signature.toByteArray();

        // Calculate SHA-256 hash
        MessageDigest digest = MessageDigest.getInstance("SHA-256");
        byte[] hashBytes = digest.digest(signatureBytes);

        // Convert hash bytes to hexadecimal string
        String actualHash = bytesToHex(hashBytes);

        // Log for debugging (remove in production or obfuscate)
        System.out.println("====================================");
        System.out.println("CERTIFICATE SIGNATURE VERIFICATION");
        System.out.println("====================================");
        System.out.println("Actual SHA-256: " + actualHash);
        System.out.println("Expected SHA-256: " + EXPECTED_SIGNATURE_HASH);

        // Compare with expected hash
        boolean isValid = actualHash.equalsIgnoreCase(EXPECTED_SIGNATURE_HASH);
        System.out.println("Signature Valid: " + isValid);
        System.out.println("====================================");

        return isValid;

    } catch (Exception e) {
        e.printStackTrace();
        return false;
    }
}
```

<img src="assets/feature1_risk2_control1_ss1.png" width="800" alt="The actual and expected SHA-256 hashes in the application logs">

*Screenshot shows the actual and expected SHA-256 hashes in the application logs.*

#### 02. Prevent your application from executing when modifications to your application are detected

Prevent your application from executing when modifications to your application are detected by displaying a non-cancellable dialog

<img src="assets/feature1_risk2_control1_ss2.png" width="800" alt="An integrity verification warning displayed by the application">

*Screenshot shows an integrity verification warning displayed by the application.*
