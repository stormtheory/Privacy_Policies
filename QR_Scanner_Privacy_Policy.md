# Privacy Policy

**Koorune QR/Barcode Scanner,Generator, and Library**

Developed by Azimos Labs, LLC

Applies to: all versions and platforms (Flutter mobile)

Last updated: August 23, 2026

---

## The Short Version
Koorune does not collect or harvest, transmit, sell, or share your personal data
with anyone, including the developer. Your app data and settings and everything in it stays on
your device unless you explicitly choose to back it up or sync it to your cloud storage
provider you already own and control.

---

This policy describes exactly what Koorune does and does not do with your data. Where
something leaves your device, it is named specifically below, along with who it goes to and
why. Nothing in this app is sold, and there are no advertisers, analytics vendors, or trackers
anywhere in it.

---

## The short version

- Everything you create or scan stays on your device, encrypted, unless you turn on iCloud
  sync yourself, in which case it goes to your own iCloud account, not to us.
- We do not run any servers that store your codes, your scans, or your identity. There is no
  account to create, no sign-in, no user database.
- A small number of features make network requests to check whether a link is safe. Exactly
  what those requests contain, and who they go to, is listed below, item by item.
- The camera never sends anything anywhere. Scanning happens entirely on your device.

---

## What is stored on your device

- **Your saved codes**: their name, contents, and which folder they're in, encrypted at rest
  (AES-GCM). The encryption key lives in the device's own secure hardware store (the Keychain
  on iOS), never in a plain file.
- **Folder names**, encrypted the same way.
- **Scan history**, if you have it enabled: what you scanned and when, stored locally the same
  way as your saved codes.
- **App settings**: things like light/dark mode, whether Details Mode is on, whether the update
  check is on, and whether you've completed the first-run setup. These are low sensitivity
  preferences, not encrypted the way your codes are, since there is nothing sensitive in "dark
  mode is on."
- **App Lock**, if you turn it on: uses Face ID or Touch ID through Apple's own
  LocalAuthentication system. We never see, store, or have access to any biometric data at
  all, that is handled entirely by iOS itself, on your device.

None of the above is ever transmitted to us. We could not read it if we wanted to, we don't
have a server it could be sent to.

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

## iCloud sync (optional, off unless you turn it on)

If you enable sync, your codes and folders are synced through your own iCloud account using
Apple's CloudKit, to your own private database, not a shared one, and not one we operate or
have access to. Content is encrypted before it ever leaves your device, so even the copy
sitting in your iCloud account is not something we, or Apple, can read. Turning this off stops
new syncing; it does not delete what has already synced to your iCloud account, that stays
under your own Apple ID's control, the same as any other iCloud data.

## Apple Watch and home screen widget (on-device only)

If you favourite a code, it becomes available on a paired Apple Watch and on a home screen
widget. This happens entirely between your own devices, over WatchConnectivity and a shared
App Group container, the same mechanism any app's Watch companion uses. None of this touches
the internet or us at any point.

## Safe Scan (checking a link before you open it)

Safe Scan runs a handful of checks on a web link before you decide whether to open it. Most of
these run entirely on your device with no network request at all: checking whether a link uses
a raw IP address instead of a name, whether it looks like a well known site with one character
changed, whether it hides a redirect trick, and similar pattern checks. Those never leave your
device.

Three parts of Safe Scan do make a network request, and here is exactly what each one sends and
to whom:

- **Redirect resolution**: to find out where a link actually leads, the app sends a request
  (specifically, a HEAD request, which asks a server "what's here" without downloading the
  page itself) to the link's own destination server, and to each server in its redirect chain.
  This is the same basic request your browser would make if you tapped the link yourself, it is
  inherent to checking where any link goes. The destination server sees this the same way it
  would see any visitor.
- **Cloudflare DNS check**: the domain name (not the full link, not any part of your identity)
  is looked up against Cloudflare's public DNS resolvers, to check whether that domain is on
  Cloudflare's own malware or adult content lists. Cloudflare is a real, named third party here;
  this is the same public service behind the addresses 1.1.1.1, 1.1.1.2, and 1.1.1.3. Cloudflare
  sees the domain being looked up and your IP address, the same as any DNS lookup your device
  already makes constantly just to browse the internet.
- **Certificate check**: the app connects directly to the destination server to confirm it
  presents a valid security certificate. This is a direct connection to that server, no third
  party involved, the same connection a browser makes as the first step of loading any secure
  site.

None of these three sends your device identifier, your account information (there is no
account), your location, or anything about your other saved codes. Each one is scoped to
exactly the one link being checked, at the moment you check it.

---

## Report this link (entirely your choice, nothing sent automatically)

If you use "Report this link" inside Safe Scan, the app puts together a plain text write-up:
the link, what it found, and nothing else, no device information, no personal information. You
see the full text before anything happens. The app then hands that text to your device's own
share sheet, the same one used anywhere else you'd share something from your phone, and you
choose where it goes: your own Mail app, Notes, Messages, AirDrop, wherever you pick. We do not
have a server that automatically receives these; there isn't one. If you choose to email it
somewhere, that email goes exactly where you addressed it, same as any other email you send.

---

## Update check (optional, off by default)

If you turn this on, the app periodically checks a web address we control to see whether a
newer version is available. This is a plain request, the same kind of request as loading a web
page, with no account information, no device identifier, and nothing else about you attached to
it. Off by default; asked once at first launch, changeable any time in Settings.

---

## Camera and location

The camera is used only to scan codes, entirely on your device. No image or video from the
camera is ever stored beyond the moment of scanning, or sent anywhere.

Location permission is used for exactly one thing: reading the name of the Wi-Fi network you're
currently connected to, so it can be turned into a Wi-Fi QR code for you to share. iOS requires
location permission to read a Wi-Fi network's name, even though no actual location data
(coordinates, movement, or anything like it) is read, stored, or used. We do not track your
location.

---

## Backups

If you create an encrypted backup file, it is protected with a password you choose (Argon2id
key derivation, AES-256-GCM encryption). That file is created entirely on your device. What you
do with it afterward, where you save it or send it, is entirely your choice, the same as any
other file on your device.

---

## Children

This app is not directed at children under the age of 13. The developer does
not knowingly collect information from children or communicate with any users via the Koorune.
This is an utility app and nothing more.

---

## Changes to This Policy

If this policy changes in a way that affects how currently released user data is handled, 
outside of correcting a mistake in wording, the updated policy will be posted at this URL with a revised date. 
Any change that reduces privacy protections will be called out explicitly in the change notice in a table to be created below.

---

## Contact

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
