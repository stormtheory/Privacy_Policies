# Privacy Policy

**Eldrfur Data Vault**
Developed by Azimos Labs, LLC
Applies to: all versions and platforms (Java desktop, Flutter mobile/desktop)
Last updated: June 21, 2026

---

## The Short Version

Eldrfur Data Vault does not collect or harvest, transmit, sell, or share your personal data
with anyone, including the developer. Your vault and everything in it stays on
your device unless you explicitly choose to back it up or sync it to your cloud storage
provider you already own and control.

---

## Versions Covered by This Policy

This policy covers all releases of Eldrfur Data Vault:

| Version                  | Platforms               | Status          |
|--------------------------|-------------------------|-----------------|
| Java desktop             | Windows, Linux (JDK 25) | Current release |
| Flutter mobile/desktop   | iOS, macOS, Android     | Current Release |

Both versions use the same vault file format, the same encryption scheme
(AES-256-GCM + Argon2id), and the same SQLite database schema. This policy
applies equally to both.

---

## What Eldrfur Data Vault Does

Eldrfur Data Vault is a local or decentralized, user-centric, privacy-first, encrypted password and secrets manager. 
**All valuable vault database fields is encrypted on your device before being stored or transmitted anywhere.
Encryption uses AES-256-GCM with a key derived from your Master Password using
Argon2id (Single-User) or the Master Password unlocks the Encryption Key (Multi-User). 
The developer cannot decrypt your vault under any circumstances. End-user is responsible 
for storage of their vault(s) and their Master Password and Recovery.

**The only data that is not encrypted is for proper operation of the sqlite database and it's framework, along with some of 
the metadata not needing to be encrypted to protect your privacy. The metadata includes things like the type of vault (single or multi-user).

---

## What the Developer Does NOT Collect

All versions of Eldrfur Data Vault does NOT collect any of the following:

- Analytics or usage data of any kind
- Crash reports or diagnostic data sent anywhere
- Advertising identifiers or advertising data
- Device identifiers or hardware fingerprints
- Contact information
- Location data
- Browsing history
- In-app purchase history
- User content
- Telemetry of any kind

There is no analytics SDK, crash reporting framework, advertising network, or
telemetry library in either version of this app. The developer has no
visibility into whether the app is installed, opened, or used by anyone,
anywhere.

---

> [!NOTE] 
> References: Here and in follows there is terms and locations that vary 
> and to keep on the same page here is a list of terms:
>
> `vault.db` - Vault names vary from system to system and user to user. 
> We will refer to the databases that are the physical encrypted data at rest as vault.db.

---

## Data Stored On Your Device(s)

The following is stored locally on your device only unless otherwise chosen and is never sent to the
developer or any third party by the app it's self:

### Vault database (`vault.db`)

This is a standard sqlite database framework file.
Your encrypted entries includes but not limited to: labels, usernames, passwords, notes, SSH keys, VPN
keys, passkeys, binary keys, and any other secrets you store. All credential
fields are encrypted with AES-256-GCM before being written to disk. The
database is a standard SQLite file. Database is read and decrypted into RAM on your device.

### Vault location configuration

Stored in app preferences on your device: which cloud storage provider you have configured
(if any), your auto-sync preferences, and the local path to your vault file.
Contains no credentials or secrets with exception of when using rclone and your configuration is encrypted.
Eldrfur will encrypt your rclone's password with your masterpassword and store the secret 
in it's config file locally.

### PIN unlock data (Flutter version, if you enable PIN unlock)

Stored in your device's hardware-backed secure storage (iOS Keychain, macOS
Keychain, or Android Keystore):

- An AES-256-GCM encrypted copy of your Master Password, wrapped with a key
  derived from your PIN using Argon2id
- The Argon2id salt and IV used for that wrapping
- A failed attempt counter (resets on success, wipes PIN data at 5 failures)
- Flags for whether PIN and biometric unlock are enabled
- A flag recording that you accepted the biometric legal disclaimer

Your Master Password is never stored in plaintext anywhere. Only the encrypted
wrapper is kept, and only in hardware-backed storage that does not synchronize
to iCloud Keychain or any other cloud service.

The Java desktop version does not implement PIN unlock. It relies on your
operating system's session security (Windows login, Linux session lock).

---

## Biometric Data (Flutter version only)(iOS/macOS)

Eldrfur Data Vault does not access, store, or transmit biometric data. When
biometric unlock is enabled, the app requests the operating system to
authenticate you. The OS returns only a pass or fail. Your biometric data
(fingerprint, face geometry, iris scan) should never leaves the device's secure
hardware and is never accessible to this app.

The Java desktop version does not use biometric authentication.

---

## Cloud Storage (Optional, User-Controlled)

Cloud backup is entirely optional and disabled by default. If enabled, you
select from providers you already have accounts with. The developer operates
no server, has no account on your behalf with any provider, and receives
nothing from any of these flows.

**What is sent to the cloud:** Only the `vault.db` file. Because all credential
fields are encrypted before leaving your device, the provider receives an
opaque binary file and cannot read its contents. They just see the framework of 
an sql database and some metadata.

> [!NOTE]
> We can't list every possible cloud provider combination or connection method you could use. That choice is yours, since it's your data.
> A few examples are given below, but our role stays largely the same regardless of which cloud provider you choose.
> Eldrfur encrypts/decrypts your data and provide user controlled options.
> Cloud providers only ever see a database file with encrypted data fields. 
> Ultimately, it's the end user's responsibility to use trusted devices and staying current with their chosen service provider's policies.

### iCloud Drive (Flutter version: iOS and macOS only)

Your vault.db is stored in an app-specific iCloud container
(`iCloud.com.stormtheory.dataVault`) under your Apple ID. This container is
not visible to other apps. Authentication is handled entirely by the OS using
your existing Apple ID. No iCloud capability exists in the Java desktop
version. This is all governed by 
[Apple's Privacy Policy](https://www.apple.com/legal/privacy/).

### Google Drive (Flutter version: Android version only)

Your vault.db is stored in the app's private `appDataFolder`, a hidden
app-specific folder not visible in your main Google Drive view and not
accessible to any other app or service. Authentication uses OAuth 2.0 via your
existing Google account. The app requests only the
`drive.appdata` scope, which is the narrowest scope available and limits access
to this single hidden folder. Governed by
[Google's Privacy Policy](https://policies.google.com/privacy).

### Nextcloud (both versions)

If you connect to a Nextcloud server, your vault.db is stored in a folder you
choose (default `EldrfurVault`) on the Nextcloud server you specify. The app
talks directly to your server over WebDAV (HTTPS) using your username and a
Nextcloud app password that you create and can revoke at any time from your
Nextcloud security settings. The app password is recommended over your account
password precisely because it is scoped and revocable.
Your Nextcloud server URL, username, and app password are stored encrypted in
your vault (AES-256-GCM, the same scheme as every other provider) under your
control; they are never sent to the developer. Because the vault file is already
encrypted on your device before upload, your Nextcloud server (whether self-
hosted or provider-hosted) only ever receives an opaque encrypted file. The app
communicates only with the server address you enter; no third-party server is
involved. Governed by the privacy policy of whoever operates your Nextcloud
instance (for self-hosted servers, that is you).
[Nextcloud "All about privacy"](https://nextcloud.com/compliance/).

### Proton Drive (All platforms)

Your vault.db is stored in by default the `EldrfurVault` folder on your Proton Drive. 
The app authenticates from your device to Proton's servers directly using your existing Proton
account information, performing the login on-device via Proton's SRP protocol (your
password is never sent to Proton; SRP proves knowledge of it without
transmitting it). If Proton challenges the login with a human-verification
(CAPTCHA) step, that challenge is presented in-app and solved by you; the app
forwards only the resulting verification token. Two-factor authentication, if
enabled on your account, is handled the same way.

Once authenticated, Proton's own end-to-end encryption applies on top of the vault's
AES-256-GCM encryption, so on Proton Drive the file is encrypted twice before
storage. Your Proton session tokens are held on device and never shared with the developer.
Proton Drive is governed by [Proton's Privacy Policy](https://proton.me/legal/privacy).

Note: native Proton Drive sync is currently available in the Flutter iOS and macOS
versions. The Java desktop version's Proton support is with rclone on Linux 
or Proton's Drive Client on Windows. The app communicates directly with Proton's 
official API endpoints over HTTPS; no third-party server is involved.

---

## PDF Viewing (both versions)

If you store a PDF file in the vault and open it for viewing, the file is
decrypted in memory on your device and displayed locally. No PDF content is
transmitted anywhere. The Java version uses Apache PDFBox; the Flutter version
uses the pdfx package. Both operate entirely offline.

---

## AutoFill (Flutter iOS version only)

The iOS version includes an optional AutoFill Credential Provider extension. If
you enable Eldrfur as an AutoFill provider in iOS Settings, the system may ask
the extension to supply a saved login when you are signing in to an app or
website. When this happens, the extension reads credentials from your local
vault on-device, after you authenticate, and hands the chosen credential to the
requesting app through the operating system.

AutoFill operates entirely on-device. Credentials are never transmitted to the
developer or any third party; they are passed only to the app you are signing
in to, through Apple's AuthenticationServices framework, and only when you
select an entry. The extension accesses the same local, encrypted vault as the
main app via a shared app group; it cannot decrypt anything without your
authentication. AutoFill is disabled until you explicitly enable it in iOS
Settings. The Java desktop version has no AutoFill feature.

---

## Fonts (Flutter version)

In debug builds and on first launch on a new device, the Flutter app uses the
Google Fonts package to download the Cinzel and Source Serif 4 typefaces from
Google's font servers (`fonts.googleapis.com`, `fonts.gstatic.com`). These
requests contain no personal data, no vault data, and no user identifiers.
Fonts are cached locally after the first download and no further font requests
are made. Governed by [Google's Privacy Policy](https://policies.google.com/privacy).

The Java desktop version does not use Google Fonts.

---

## Third-Party Libraries

Both versions use third-party open source libraries for cryptography, database
access, and platform integration. These libraries operate locally on your
device and do not transmit data independently. The main libraries are:

**Java version:** BouncyCastle (AES-256-GCM), argon2-jvm (Argon2id),
sqlite-jdbc (SQLite), Apache PDFBox (PDF rendering), and platform-specific
OAuth libraries for cloud providers when enabled.

**Flutter version:** pointycastle (AES-256-GCM), an embedded pure-Dart
Argon2id implementation (ported from BouncyCastle, Apache 2.0; no third-party
Argon2 package), sqlite3 (SQLite), flutter_secure_storage (hardware keychain),
local_auth (biometric), icloud_storage (iCloud), http (Proton Drive API over
HTTPS), pdfx (PDF rendering), file_selector and file_picker (local file
selection), google_fonts (typography). Native Proton Drive support on iOS uses
a small bundled Go-based bridge that talks to Proton's official API over HTTPS;
it runs in-process and transmits nothing to the developer.

---

## Data Not Shared With Third Parties

The developer does not share any data with any third party because the
developer does not collect any data. The app contains no advertising networks,
data brokers, analytics providers, or data-sharing integrations of any kind other. 

Only time third parties are invloved is when the user allows for storage of their own 
information with their own account with another other provider, then their own policies 
will then apply.

---

## Data Security

All vault credentials are encrypted with AES-256-GCM, a standard authenticated
encryption algorithm, before being stored. The encryption key is derived from
your Master Password using Argon2id, a memory-hard algorithm designed to resist
brute-force attacks. The Master Password is never stored in the vault database
or anywhere on the device in plaintext.

The Flutter version's PIN unlock feature wraps the Master Password with a
second Argon2id-derived key before storing it in hardware-backed secure
storage. The PIN itself is never stored anywhere. A self detructive Pin after so many fails.
With an option of using biometrics for a more of a "two factor" approach.

User is solely responsible for choosing a strong Master Password and keeping it
secure. If user loses their Master Password, the user's vault data cannot be recovered
by the developer or by anyone else without possible years of brute force. Users are also solely 
responsible for choosing trusted devices and staying current with their chosen service provider's own policies.

---

## Children

This app is not directed at children under the age of 13. The developer does
not knowingly collect information from children or commuicate with any users via the Eldrfur Data Vault.
This is an utility app and nothing more.

---

## Changes to This Policy

If this policy changes in a way that affects how currently released user data is handled, 
outside of correcting a mistake in wording, the updated policy will be posted at this URL with a revised date. 
Any change that reduces privacy protections will be called out explicitly in the change notice in a table to be created below.

---

## Contact

Questions about this privacy policy or the app's data practices:

stormtheory@azimoslabs.com

---

## App Store and Google Play Privacy Nutrition Label Reference

The following summarizes this policy in the format used by Apple App Store
and Google Play Store privacy disclosure screens.

**Data collected by this app:** None.

**Data linked to you:** None.

**Data used to track you:** None.

**Data not linked to you:** None.

All data created in this app stays on the user's device or in cloud storage
the user controls under their own account. The developer collects nothing,
stores nothing server-side, and has no access to any user data.
