# Privacy Policy

**Eldrfur Data Vault**

Developed by Azimos Labs, LLC

Applies to: all versions and platforms (Java desktop, Flutter mobile/desktop)

Last updated: August 13, 2026

---

## The Short Version

Eldrfur Data Vault does not collect or harvest, transmit, sell, or share your personal data
with anyone, including the developer. Your vault and everything in it stays on
your device unless you explicitly choose to back it up or sync it to your cloud storage
provider you already own and control.

---

## Versions Covered by This Policy

This policy covers all releases of Eldrfur Data Vault:

| Version                  | Platforms               | Status                                   |
|--------------------------|-------------------------|------------------------------------------|
| Java desktop             | Windows, Linux (JDK 25) | Still supported; updated less frequently |
| Flutter mobile/desktop   | iOS, macOS, Android     | Current release                          |

The Java desktop version remains available and continues to receive updates,
just on a slower cadence than the Flutter version. It is not discontinued or
deprecated - it still uses the same vault file format, the same encryption
scheme (AES-256-GCM + Argon2id), and the same SQLite database schema as the
Flutter version, and this policy applies equally to both.

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

## Online Data Connections

All versions of Eldrfur Data Vault use one or more of the following connections:

| Purpose            |Platform | Use                      | What and Where to                                                                                      |
|--------------------|---------|--------------------------|--------------------------------------------------------------------------------------------------------|
| Cloud Sync         | All     | optional, off by default | encrypted personal data, to personal cloud service providers                                           |
| App Update checking| iOS/Mac | optional, off by default | https encrypted file read connection to check what builds are available from Azimos Lab's web servers  |
| App Update checking| Android | optional, off by default | communicates directly with Google Play to check for and download app updates                           |

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

## AutoFill (Flutter iOS and macOS versions)

The iOS and macOS versions include an optional AutoFill Credential Provider
extension. If you enable Eldrfur as an AutoFill provider in iOS or macOS
Settings, the system may ask the extension to supply a saved login when you
are signing in to an app or website. When this happens, the extension reads
credentials from your local vault on-device, after you authenticate, and
hands the chosen credential to the requesting app through the operating
system.

AutoFill operates entirely on-device. Credentials are never transmitted to the
developer or any third party; they are passed only to the app you are signing
in to, through Apple's AuthenticationServices framework, and only when you
select an entry. The extension accesses the same local, encrypted vault as the
main app via a shared app group; it cannot decrypt anything without your
authentication. AutoFill is disabled until you explicitly enable it in iOS or
macOS Settings. The Java desktop version has no AutoFill feature.

**AutoFill is single-vault at a time.** If you have more than one vault, only
one can be the active AutoFill vault at once - this is a deliberate design
choice, not a limitation on what data is protected. The AutoFill
configuration screen (Settings > Passwords > AutoFill Passwords, tapping
this app) shows a plain-text, non-secret label naming which vault is
currently configured, stored device-only in the same shared, access-
controlled keychain group as the rest of AutoFill's material - it is never
transmitted anywhere and contains nothing about the vault's contents, only
the display name you gave it.

**AutoFill setup hand-off.** Both versions register a private, app-only URL
scheme (`eldrfurvault://`) used solely to let the AutoFill configuration
screen open the main app directly to its AutoFill setup screen when you tap
"Open Eldrfur to Set Up AutoFill." This is an on-device hand-off between the
extension and the app only; it carries no vault data, credentials, or
identifiers of any kind, and nothing about it is ever sent anywhere.

**Optional AutoFill diagnostic log.** For troubleshooting, you can turn on a
local diagnostic log for the AutoFill extension (off by default) from PIN /
AutoFill settings. When enabled, it records operational detail about what
the extension is doing - which steps ran, timing, and non-secret identifiers
like which website requested a fill - to a size-capped file inside the
shared app group container on your device. It never records your Master
Password, PIN, vault entries, or decrypted credentials. You can view or
clear this log at any time from the same settings screen, and turning the
toggle off deletes the existing log file. Nothing in this log is ever
transmitted anywhere; it exists only for you (or, if you choose to share it
yourself, whoever you send it to) to read on-device.

---

## Fonts (Flutter version)

Every typeface the app uses (Cinzel, Cinzel Decorative, Source Serif 4,
Source Code Pro) is a font file bundled directly inside the app at build
time. They load from disk, the same as any other app asset - never from a
network request, on any platform, on any build (debug or release), on first
launch or any later launch. The app makes no request of any kind to Google,
or to any other font provider, for any reason.

CORRECTION (this policy previously said otherwise): an earlier version of
this document described a Google Fonts network fetch that does not reflect
this app's actual behavior - the fonts have been fully bundled as local
assets this entire time, and the one remaining unused reference to the
`google_fonts` package (kept only for a network-disabling settings flag it
never needed) has been removed outright. That earlier wording was a
documentation error, not a description of something the app ever did in
this codebase; it is corrected here so this document matches the code
exactly, not just in intent.

The Java desktop version does not use Google Fonts.

---

## App Update Checks

**iOS and macOS:** once every 24 hours, after you unlock your vault, the
app automatically checks a small remote file over HTTPS to see if a newer
version is available. You can also trigger this check yourself anytime
via Settings > Check for Updates > Check Now, which does the same thing
on demand rather than waiting for the 24-hour cycle. Either way, the
request sends no personal data, no vault data, and no user identifier -
it is a plain, unauthenticated request for a static file listing the
current version number (a timestamp is added to the request only to
prevent an intermediate cache from serving a stale answer; it identifies
nothing about you or your device). If a newer version is found, you
decide what happens next: dismiss it, tell the app not to remind you
again for that specific version, or open the update link yourself.
Nothing downloads or installs automatically. This check is OFF by default
and must be turned on in Settings > Check for Updates.

**Android:** uses Google Play's own official In-App Updates feature
instead of the check described above - genuinely different infrastructure,
not this app's own server. This means Google Play itself (which you are
already connected to as the source the app was installed from) is asked
whether a newer version exists, using Google's own SDK built for this
exact purpose. If you accept, Google Play downloads the update directly
in the background; the app never has its own copy of that file or any
part of the process, and never sees anything beyond whether an update is
available. Same behavior otherwise: off by default, on-demand "Check Now"
available, and nothing installs without you choosing to restart and
finish it.

The Java desktop version does not perform update checks.

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

**Android only, worth calling out separately:** Google Play's own In-App
Updates library (Play Core) is the one exception to "these libraries
operate locally and do not transmit data independently" above - by
design, it communicates directly with Google Play to check for and
download app updates (see "App Update Checks" above). This is the same
relationship you already have with Google Play as the source the app was
installed from, not a new third party this app introduces on its own -
but unlike every other library in this list, it genuinely does talk to an
external server, so it is listed separately rather than folded into the
"local only" description above it.

---

## Data Not Shared With Third Parties

The developer does not share any data with any third party because the
developer does not collect any data. The app contains no advertising networks,
data brokers, analytics providers, or data-sharing integrations of any kind.

Two narrow exceptions, both described in full above and both optional:
when the update check is turned on (off by default), a version-number
request goes to either the developer's own server (iOS/macOS) or Google
Play (Android) - see "App Update Checks" for exactly what that does and
does not send. Otherwise, third parties are only ever involved when you
choose to store your own vault data with your own account on another
provider (Proton, Nextcloud, iCloud, or a folder you pick), at which
point that provider's own policies apply to what you have chosen to store
with them.

---

## Data Security

All vault credentials are encrypted with AES-256-GCM, a standard authenticated
encryption algorithm, before being stored. The encryption key is derived from
your Master Password using Argon2id, a memory-hard algorithm designed to resist
brute-force attacks. The Master Password is never stored in the vault database
or anywhere on the device in plaintext.

The Flutter version's PIN unlock feature wraps the Master Password with a
second Argon2id-derived key before storing it in hardware-backed secure
storage. The PIN itself is never stored anywhere. A self destructive Pin after so many fails.
With an option of using biometrics for a more of a "two factor" approach.

User is solely responsible for choosing a strong Master Password and keeping it
secure. If user loses their Master Password, the user's vault data cannot be recovered
by the developer or by anyone else without possible years of brute force. Users are also solely 
responsible for choosing trusted devices and staying current with their chosen service provider's own policies.

---

## Children

This app is not directed at children under the age of 13. The developer does
not knowingly collect information from children or communicate with any users via the Eldrfur Data Vault.
This is an utility app and nothing more.

---

## Changes to This Policy

If this policy changes in a way that affects how currently released user data is handled, 
outside of correcting a mistake in wording, the updated policy will be posted at this URL with a revised date. 
Any change that reduces privacy protections will be called out explicitly in the change notice in a table to be created below.

---

## Contact

Questions about this privacy policy or the app's data practices:

software_feedback_report@azimoslabs.com

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

**Android-specific note for Google Play's own Data Safety form:** the
"None" answers above describe what this app itself collects, which is
still accurate on Android. Separately, Google Play's own In-App Updates
SDK (used only if the optional update check is turned on - see "App
Update Checks" above) is a Google-operated feature governed by Google
Play's own privacy policy, not something this document can speak for -
worth listing as a used SDK on Google Play's own disclosure form, even
though it does not change what this app collects.


## Change Log
| Date            | Build | Changes                                                                                |
|-----------------|-------|----------------------------------------------------------------------------------------|
| June 21, 2026   |Beta   | Initial privacy policy (Pre-Release - Beta Version)                                    |
| August 02, 2026 |1      | Build 1 Release - Added change log table, no major changes to the privacy of the apps. |
| August 13, 2026 |2      | Build 2 - <br> Disclosed three new on-device-only items introduced this build: <br>• (1) a non-secret vault display name stored in the shared AutoFill keychain group so the AutoFill setup screen can show which vault is configured, <br>• (2) the private `eldrfurvault://` URL scheme used only for an on-device hand-off from that screen into the app, <br>• (3) the existing opt-in AutoFill diagnostic log, described here for the first time even though the toggle itself predates this build. None of these transmit anything off-device; no protections were reduced. <br>• (4) Added a new "App Update Checks" section: once every 24 hours after unlock, the app requests a small static file over HTTPS to check for a newer version. No personal data, vault data, or user identifier is sent; OFF by default, toggleable in Settings. Nutrition-label answers unchanged - this is the same category of request as the existing Fonts section (a static-resource fetch with no data collected), not a new "data collected" item. |
| - | - | <br>• (5) Privacy Policy corrected for fonts from google, the app does not reach out to google, the fonts are downloaded in the app assembly/building stage during development. <br>• (6) Added the Online Data Connections table near the top.|
| August 15, 2026 | 3     | "App Update Checks" split into iOS/macOS (the existing hosted-manifest check, now also describing the on-demand "Check Now" option and the cache-busting timestamp added to each request) and Android (genuinely different mechanism: Google Play's own official In-App Updates SDK, not this app's own server). Added Play Core to the Third-Party Libraries list with an explicit callout that, unlike every other library listed there, it does communicate with an external server by design. Added a narrow, explicit exception to "Data Not Shared With Third Parties" covering both update-check paths. Added an Android-specific note to the Nutrition Label section for Google Play's own separate Data Safety form. Nutrition-label answers themselves unchanged (still None/None/None/None) - nothing above changes what this app itself collects, only what is now disclosed about Play's own SDK. Also corrected pre-existing typos in "Data Not Shared With Third Parties" unrelated to this change. |
| -               | 3     | "PDF Viewing" retitled "PDF Viewing & Document/Key Export" and updated for a new explicit Share/Export action (document viewer + "Binary Keys" entries), using the device's own native share sheet - entirely on-device, one item at a time, only on explicit tap, temp copy zeroed and deleted immediately after regardless of outcome. Nutrition-label answers unchanged (still None/None/None/None) - this is an on-device action the person themselves initiates and directs, not new data collection or a new developer-facing transmission. Also corrected the Third-Party Libraries list, found stale while making this update: it still named google_fonts (removed entirely in an earlier Build 3 change - this list was never updated to match at the time) and file_picker (never actually a dependency - iOS uses a small custom native channel instead, specifically because that third-party package repeatedly broke the iOS build); added share_plus for the new export feature. |
