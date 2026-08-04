# Privacy Policy — Veteran Education Homeport (VetEduHP)

**Effective date:** August 4, 2026
**Last updated:** August 4, 2026
**App name:** Veteran Education Homeport (VetEduHP)
**Platform:** iOS and macOS (Apple App Store) · Android (Google Play Store)
**Developer:** Azimos Labs, LLC — https://azimoslabs.com
**Contact:** software_feedback_report@azimoslabs.com

---

## Overview

Veteran Education Homeport (VetEduHP) is a free utility application built for student veterans, active duty servicemembers, military-connected students, and their dependents at any supported university. It helps students track semester checklist tasks, estimate VA housing benefits, navigate their school with an interactive map and find veteran resources.

This privacy policy describes how the app handles user information. The short version: **we collect two pieces of information, we store nothing on any server, and we share nothing with anyone.**

---

## 1. Data We Collect and How We Use It

### 1.1 Information entered during onboarding

When a student first opens the app, they are asked to provide:

| Field                      | Purpose                                      | Stored?                                   |
|----------------------------|----------------------------------------------|-------------------------------------------|
| School email address       | Determines which school's content to show    | **No — see 1.2, only the domain is kept** |
| First name                 | Personalizes the greeting on the home screen | Yes — encrypted on device only            |

The app does not collect a student ID number, a password, or any other identifier. No account is created and no login is required.

### 1.2 How the email address is handled

The student's full email address is used only once, during onboarding, to determine which school they attend. Immediately after that:

- The email address itself is **discarded and never stored**.
- Only the **domain** — the portion after the `@` symbol (for example, `university.edu`) — is saved on the device.

The domain identifies which school's content to display (its checklist tasks, campus contacts, and BAH rates, where available). A domain identifies an institution, not an individual, and is not personally identifiable information. We have no way to determine who a specific user is from the domain alone.

If a student's school domain isn't yet recognized by the app, the student still has full access to every feature that doesn't depend on school-specific information — the BAH calculator, national VA resources, and the Veterans Crisis Line all remain available.

### 1.3 User-generated checklist data

Students may mark checklist tasks complete or add their own personal tasks. This data is stored locally on the device and is never transmitted anywhere.

### 1.4 App preferences

Theme selection (light, dark, or system default) is stored locally on the device.

### 1.5 Data we do not collect

The app does not collect, access, or process any of the following:

- Student ID numbers or any other institutional identifier
- Full email addresses (only the domain is retained, per 1.2)
- Location data
- Contact list or address book
- Camera or microphone
- Photos or media library
- Browsing history
- Device advertising identifiers (IDFA, IDFV, Android Advertising ID)
- Crash logs, analytics, or usage telemetry
- Biometric data
- Payment or financial information
- Social network credentials

---

## 2. How Data Is Stored

All data entered by the user is stored **exclusively on the user's device** using the platform's native encrypted storage:

- **iOS, iPadOS, and macOS:** Keychain (`kSecClassGenericPassword`) via `flutter_secure_storage`. Configured with `synchronizable: false` — data is explicitly prevented from syncing to iCloud or any Apple server.
- **Android:** Android Keystore system backed by `EncryptedSharedPreferences`. Hardware-backed encryption where the device supports it.

No backend server, database, cloud storage, or third-party data processor receives any data from this app.

---

## 3. Data Transmission

The app makes outbound network connections only in the following circumstances, all of which are initiated explicitly by the user:

| Action | Destination | What is sent |
|-------------------------------------------------------------|---------------------------|---------------------------------------------------------|
| Tapping an external link (VA.gov, a school's website, etc.) | The linked website        | Nothing beyond what a standard browser request includes |
| Tapping "Directions"                                        | Apple Maps or Google Maps | The destination address or GPS coordinates of the selected campus building, where a campus map is available |
| Tapping "Call"                                              | The device's phone dialer | The phone number                                        |
| Tapping "Email" or "Report an issue"                        | The device's mail app     | A pre-composed email draft opened for the user to review and send manually |
| Loading the interactive campus map, where available         | OpenStreetMap tile servers (openstreetmap.org) | Tile coordinates only — no user identity or location data |

The app does not make any background network requests. No data is transmitted without a direct user action.

---

## 4. Data Sharing and Disclosure

We do not sell, rent, license, or share any user data with any third party, including advertisers, data brokers, analytics providers, or any other entity. There are no third-party SDKs, advertising networks, or tracking frameworks integrated into this app.

---

## 5. How This App Is Funded

VetEduHP is free to students and free to download. To support the schools and content within the app, Azimos Labs, LLC may charge a participating university's veterans office an annual fee to have that school added and maintained in the app — its own checklist, campus contacts, campus map, BAH rates, calender events and other content.

This is an institutional licensing fee, paid by a school, for content and integration work. **It is not, and never involves, the sale, rental, licensing, or exchange of any student's personal data.** No information about any individual student is ever provided to a school, to Azimos Labs' other customers, or to any third party as part of this arrangement. A school pays to be represented accurately in the app — nothing more, and nothing involving what any specific student does with it.

---

## 6. Children's Privacy

This app is intended for use by enrolled college and university students and is not directed at children under the age of 13 (United States) or under the age of 16 (where applicable under GDPR or similar regulations). We do not knowingly collect any information from minors. If a minor has installed the app, they should uninstall it. Contact software_feedback_report@azimoslabs.com if you have concerns.

---

## 7. Education Records and FERPA

Where a student's school is subject to the Family Educational Rights and Privacy Act (FERPA), 20 U.S.C. § 1232g, our data practices are consistent with FERPA's intent:

- The app does not have access to, store, or transmit student education records to any external party.
- No student ID number or other institutional identifier is ever collected.
- Name is stored only on the student's own device and is not accessible to any school, the app developer, or any third party by design.

---

## 8. User Control and Data Deletion

Students have full control over all data stored by the app.

**To delete personal data without resetting the full app:**
Settings → Reset personal data

This deletes the stored name and checklist progress from the device's secure storage.

**To delete all app data, including the saved school domain:**
Settings → Full app reset

This deletes everything the app has stored on the device, equivalent to uninstalling the app.

**To delete all data permanently:** Uninstall the app. Because no data is stored on any server, uninstalling the app removes all associated data completely and irreversibly. There is no account to deactivate and no server-side deletion request is necessary or possible.

---

## 9. Security

Data stored by this app is protected by the device's native encrypted storage mechanisms (iOS/iPadOS/macOS Keychain, Android Keystore). These systems use AES-256 encryption and, on modern hardware, are backed by a secure enclave or trusted execution environment. The app does not implement its own encryption layer — it relies entirely on the platform's built-in, audited security infrastructure.

The app does not require a login, does not issue session tokens, and does not maintain any authenticated session with any server.

---

## 10. Accuracy of Benefit and Rate Information

Checklist tasks, deadlines, and BAH/MHA rate estimates shown in the app are provided as a reference tool and are updated periodically by the developer and participating schools. They are not sourced live from the VA or any school's systems. Students should always verify current deadlines, requirements, and payment amounts directly with the VA and their school's veterans office before relying on them for financial or academic decisions.

---

## 11. Changes to This Policy

If this policy changes materially, the updated version will be posted at the same location this policy is currently hosted, and the effective date above will be updated. Continued use of the app after a change constitutes acceptance of the revised policy.

---

## 12. Contact

Questions about this privacy policy or the app's data practices:

**Azimos Labs, LLC**
https://azimoslabs.com
software_feedback_report@azimoslabs.com

---

*This app does not monetize student data in any way. Azimos Labs, LLC generates revenue through annual licensing fees paid by participating universities — never through the sale or use of any individual student's information.*
