# Android risk-test sample sources

Source coverage reviewed on 2026-10-22. Binary paths in [inventory.json](inventory.json) are relative to the automation backend repository, `mobile_playbook_automation`. The inventory records package identifiers and reference binary/archive SHA-256 checksums.

## Available source archives

| Archive | Package | Purpose |
| --- | --- | --- |
| [android-platform-feature-04-risk-01-overlay-attacker-source.zip](android-platform-feature-04-risk-01-overlay-attacker-source.zip) | `com.mobileplaybook.overlay` | Native focusable sign-in overlay with local canary capture; replaces `F4_Attacker.apk` for automated testing. |
| [android-platform-feature-05-risk-01-accessibility-attacker-source.zip](android-platform-feature-05-risk-01-accessibility-attacker-source.zip) | `com.mobileplaybook.accessibility` | Accessibility service with the playbook's logout-clicking logic, an optional target-package filter and JSON attack output; replaces `F5R1_Attacker.apk` for automated testing. |
| [android-platform-feature-06-risk-01-screen-capture-helper-source.zip](android-platform-feature-06-risk-01-screen-capture-helper-source.zip) | `com.mobileplaybook.screencapture` | MediaProjection helper used by the automated screen-capture risk; distinct from `F6_Attacker.apk`. |
| [android-demo-bank-source.zip](android-demo-bank-source.zip) | `com.playbook.demobank` | Deliberately insecure victim for runtime-log and accessibility-logout manual tests. This APK is stored with the manual tests, not in intake. |

Each archive includes original source/build files, `ARCHIVE.md` with standalone build notes, and `SOURCE.json` with source checksums and the reference APK checksum. All available source archives were built successfully from fresh extractions. Generated binaries, build caches, private signing keys and local IDE state are excluded. A new test signing key is generated when rebuilding, so the signed APK will not be byte-identical to the reference.

## Recovered code from APKs

The user confirmed that the original source locations for the five attacker APKs are unavailable. The following archives contain code recovered from those exact intake binaries using JADX 1.5.6. They are inspection artifacts, not original or validated buildable projects.

| Archive | Intake APK | Package |
| --- | --- | --- |
| [android-platform-feature-04-risk-01-overlay-attacker.zip](android-platform-feature-04-risk-01-overlay-attacker.zip) | `F4_Attacker.apk` | `com.overlayonly` |
| [android-platform-feature-05-risk-01-accessibility-attacker.zip](android-platform-feature-05-risk-01-accessibility-attacker.zip) | `F5R1_Attacker.apk` | `com.malicious.accessibilityattacker` |
| [android-platform-feature-05-risk-02-event-spy.zip](android-platform-feature-05-risk-02-event-spy.zip) | `F5R2_Attacker.apk` | `com.malicious.eventspy` |
| [android-platform-feature-05-risk-03-text-scraper.zip](android-platform-feature-05-risk-03-text-scraper.zip) | `F5R3_Attacker.apk` | `com.malicious.textscraper` |
| [android-platform-feature-06-risk-01-screen-capture-attacker.zip](android-platform-feature-06-risk-01-screen-capture-attacker.zip) | `F6_Attacker.apk` | `com.capturingeg` |

Each recovered archive includes app-owned decompiled Java, the decoded manifest and resources, diagnostics, and `RECOVERY.json` with input/output checksums and recovery limitations. Original build scripts, dependency versions and author source are unavailable; decompiler warnings are preserved. Event Spy and Text Scraper also include instruction-level fallbacks for incomplete MainActivity methods. The overlay and screen-capture attacker archives preserve their compiled Hermes bundles, not original JavaScript source. No recovered archive was rebuilt or runtime-tested.

The native overlay test app (`F4_Overlay_Attacker.apk`, `com.mobileplaybook.overlay`) replaces the recovered `F4_Attacker.apk` (`com.overlayonly`) for automated testing. The recovered APK and archive remain unchanged for inspection.

Likewise, the native accessibility test app (`F5R1_Accessibility_Attacker.apk`, `com.mobileplaybook.accessibility`) replaces the recovered `F5R1_Attacker.apk` (`com.malicious.accessibilityattacker`). Its logout patterns are exactly the playbook's, whereas the recovered app omits `log_out` and adds `reset`. It has not yet been runtime-tested on a device.

The buildable screen-capture helper is a separate implementation from `F6_Attacker.apk`; the two are listed separately in the inventory.

ZIP files remain local sample artifacts under the repository's existing ignore rule. Third-party production APKs are outside this inventory.
