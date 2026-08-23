# Privacy Policy

**Koorune QR/Barcode Scanner, Generator, and Library**

Developed by Azimos Labs, LLC

Applies to: all versions and platforms (Flutter mobile)

Last updated: August 23, 2026

---

## The Short Version

Koorune does not collect or harvest, transmit, sell, or share your personal data
with anyone, including the developer. Your app data and settings and everything in it stays on
your device unless you explicitly choose to back it up or sync it to a cloud storage
provider you already own and control.

---

## Overview

This policy describes exactly what Koorune does and does not do with your data. Where
something leaves your device, it is named specifically below, along with who it goes to and
why. Nothing in this app is sold, and there are no advertisers, analytics vendors, or trackers
anywhere in it.

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

Koorune does not collect any of the following:

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
telemetry library in this app. The developer has no
visibility into whether the app is installed, opened, or used by anyone,
anywhere.

---

## Online Data Connections

Every network connection this app makes, in one table. Detail on each one, exactly what is sent
and why, follows further down this document.

| Purpose                        | Platform | Use                      | What and Where to                                                                     |
|--------------------------------|----------|--------------------------|---------------------------------------------------------------------------------------|
| Cloud Sync                     | iOS      | optional, off by default | encrypted personal codes, to your own iCloud account (CloudKit), never to Azimos Labs |
| App Update checking            | iOS      | optional, off by default | nothing beyond what a standard browser request includes, to Azimos Labs |
| Safe Scan, redirect resolution | iOS      | Safe Scan is used | the link's own destination server(s), one HEAD request per hop, the same request opening the link yourself would make |
| Safe Scan, malware and adult content check | iOS      | Safe Scan is used | the domain name only, to Cloudflare's public DNS resolvers (1.1.1.1, 1.1.1.2, 1.1.1.3) |
| Safe Scan, certificate check               | iOS      | Safe Scan is used | a direct connection to the link's own destination server, to confirm its certificate, nothing downloaded |
| Safe Scan, domain age check                | iOS      | Safe Scan is used | the domain name only, to rdap.org and the domain's own registry |
| Safe Scan, hosting provider check          | iOS      | Safe Scan is used | the destination's IP address (already resolved for the malware check above, not a separate lookup), through Cloudflare's DNS resolver to Team Cymru |
| Safe Scan, sandboxed preview               | iOS      | optional, only if chosen | a direct, ephemeral connection to the link's own destination server, nothing saved once closed |
| Safe Scan, open the real destination       | iOS      | optional, only if chosen | hands off to Safari, the same as opening any link yourself |

---

## iCloud sync (optional, off unless you turn it on)

If you enable sync, your codes and folders are synced through your own iCloud account using
Apple's CloudKit, to your own private database, not a shared one, and not one we operate or
have access to. Content is encrypted before it ever leaves your device, so even the copy
sitting in your iCloud account is not something we, or Apple, can read. Turning this off stops
new syncing; it does not delete what has already synced to your iCloud account, that stays
under your own Apple ID's control, the same as any other iCloud data.

## Apple Watch and home screen widget (on-device only)

If you favorite a code, it becomes available on a home screen widget. Adding a code to your
Apple Watch is a separate toggle, not the same thing as favoriting it. Either way, this happens
entirely between your own devices, over WatchConnectivity and a shared App Group container, the
same mechanism any app's Watch companion uses. None of this touches the internet or us at any
point.

Worth knowing if you use App Lock: the widget shows a favorited code's actual image as soon
as your phone itself is unlocked, the same access anything else on your home screen already
has, App Lock does not add a further gate on top of that. Your Apple Watch is different: it has
its own passcode and only shows anything while unlocked on your own wrist, a real, separate
layer that already exists independent of this app. Un-favorite anything you want kept out of
the widget specifically.

## Safe Scan (checking a link before you open it)

Safe Scan runs a handful of checks on a web link before you decide whether to open it. Most of
these run entirely on your device with no network request at all: checking whether a link uses
a raw IP address instead of a name, whether it looks like a well known site with one character
changed, whether it hides a redirect trick, and similar pattern checks. Those never leave your
device.

Five parts of Safe Scan do make a network request, and here is exactly what each one sends and
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
- **Domain age check**: the domain name is looked up against RDAP, the open, standardized
  registry lookup system every domain registry is required to provide (the modern successor to
  WHOIS), to see when it was registered. This goes to whichever registry actually holds that
  domain's registration, by way of a public directory service (rdap.org) that simply points the
  request at the right one. No account, no key, the same kind of lookup anyone can already run
  from a terminal.
- **Hosting provider check**: the destination's IP address (already obtained from the Cloudflare
  DNS check above, not a separate lookup) is checked against Team Cymru's public IP-to-network
  lookup service, to identify which network or hosting provider it belongs to. This request is
  sent through Cloudflare's own lookup service, the same one already described above, so it does
  not add a new party beyond Cloudflare and Team Cymru itself.

None of these five sends your device identifier, your account information (there is no
account), your location, or anything about your other saved codes. Each one is scoped to
exactly the one link being checked, at the moment you check it.

## Report this link (entirely your choice, nothing sent automatically)

If you use "Report this link" inside Safe Scan, the app puts together a plain text write-up:
the link, what it found, and nothing else, no device information, no personal information. You
see the full text before anything happens. The app then hands that text to your device's own
share sheet, the same one used anywhere else you'd share something from your phone, and you
choose where it goes: your own Mail app, Notes, Messages, AirDrop, wherever you pick. We do not
have a server that automatically receives these; there isn't one. If you choose to email it
somewhere, that email goes exactly where you addressed it, same as any other email you send.

## Update check (optional, off by default)

If you turn this on, the app periodically checks a web address we control to see whether a
newer version is available. This is a plain request, the same kind of request as loading a web
page, with no account information, no device identifier, and nothing else about you attached to
it. Off by default; asked once at first launch, changeable any time in Settings.

## Camera and location

The camera is used only to scan codes, entirely on your device. No image or video from the
camera is ever stored beyond the moment of scanning, or sent anywhere.

Location permission is used for exactly one thing: reading the name of the Wi-Fi network you're
currently connected to, so it can be turned into a Wi-Fi QR code for you to share. iOS requires
location permission to read a Wi-Fi network's name, even though no actual location data
(coordinates, movement, or anything like it) is read, stored, or used. We do not track your
location.

## Backups

If you create an encrypted backup file, it is protected with a password you choose (Argon2id
key derivation, AES-256-GCM encryption). That file is created entirely on your device. What you
do with it afterward, where you save it or send it, is entirely your choice, the same as any
other file on your device.

---

## Children

This app is not directed at children under the age of 13. The developer does
not knowingly collect information from children or communicate with any users via Koorune.
This is a utility app and nothing more.

---

## Changes to This Policy

If this policy changes in a way that affects how currently released user data is handled,
outside of correcting a mistake in wording, the updated policy will be posted at this URL with a
revised date. Any change that reduces privacy protections will be called out explicitly in the
change notice in a table to be created below.

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
