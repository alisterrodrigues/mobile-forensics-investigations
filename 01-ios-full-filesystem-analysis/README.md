# iOS Full Filesystem Analysis — Apple iPhone 8

<p align="center">
  <img src="https://img.shields.io/badge/Device-Apple_iPhone_8-lightgrey?style=for-the-badge&logo=apple&logoColor=white" />
  <img src="https://img.shields.io/badge/Format-UFDR_(Cellebrite)-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Tool-Cellebrite_Reader_7.48.1.3-informational?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Tool-DB_Browser_for_SQLite-orange?style=for-the-badge" />
</p>

---

## Case Summary

| Field | Detail |
|---|---|
| **Case Reference** | UFDR_CASE_001 |
| **Evidence File** | Apple iOS Full File system_2021-10-01_Report.ufdr |
| **SHA-256** | `d4ee0bedb24e07653d11ba1eb14f68cd4cb7862e69004a974c2819fce071b523` |
| **Device** | Apple iPhone 8 (Model D20AP) |
| **Serial / IMEI** | FFMWR1NRC6F / 35670108761405 |
| **Device Name** | Berg's iPhone |
| **Time Zone** | UTC−05:00 America/New York |
| **Examination Window** | September 11 – October 1, 2021 |
| **Examiner** | Alister A. Rodrigues |

---

## What This Examination Covers

A full iOS filesystem extraction examined using Cellebrite Reader and direct SQLite database querying. The UFDR file was hash-verified against both Windows CertUtil and Cellebrite's internal validator before any analysis began, ensuring evidence integrity throughout.

---

## Methodology

**Acquisition:** UFDR file received as a verified working copy; original maintained as read-only. SHA-256 hash confirmed via `certutil -hashfile` on Windows and independently by Cellebrite Reader.

**Environment:** Cellebrite Reader 7.48.1.3 on Windows 11 Home (ARM) in VMware Fusion on macOS. DB Browser for SQLite 3.12.2 for direct database querying of iOS system databases.

**Time Zone:** Device time zone detected as UTC−05:00 (America/New York) and applied to all timestamps at examination start.

**Scope:** Device metadata and ownership → communications → network and connectivity → geolocation → application activity → summary of findings.

---

## Key Findings

### Device & Ownership
- iPhone 8 (D20AP) registered to Apple ID `bergcybersectesting@gmail.com`
- 13 user account records parsed from `Accounts3.sqlite`, all linked to the same Apple ID across iTunes Store, iCloud, Find My Friends, Game Center, and Messages
- iCloud sync active; last cloud backup: 2021-09-22 20:47:10 UTC

### Communications
- Gmail account (`bergcybersectesting@gmail.com`) — 134 total messages: 131 inbound, 3 outbound
- 3 outbound messages to `alexongkowijoyo91@ymail.com` on September 18–19, 2021 — confirmed via authenticated SMTP activity
- Inbound verification emails from Facebook, Google, Apple, WomanEze, and ProtonVPN — confirming active service registration and login activity
- No SMS, iMessage, or third-party chat data recoverable from the filesystem — documented with forensic explanation (likely device restoration or encrypted cloud-only retention prior to acquisition)

### Network & Connectivity
- **3,609 Wi-Fi BSSID entries** with geolocation coordinates and timestamps
- Multiple access points logged within the same timeframe clustered around approximately (40.739°, −73.878°), suggesting stationary or confined-area device use
- **180 Bluetooth connectivity records** with randomized MAC addresses (consistent with iOS privacy protocols)
- Wi-Fi connect/disconnect events correlated with screen-on and device-unlock events — confirming active use periods

### Geolocation
- **5,790 total location records** extracted from Core Location and Wi-Fi location caching databases
- **1,860 deleted entries recovered** — parsed from `/private/var/mobile/Library/Caches/com.apple.routined/` and `/private/var/root/Library/Caches/locationd/`
- Consistent geographic clustering corroborates continuous device movement logging across multiple days

### Application Activity
- `applicationState.db` identified five non-Apple health-tracking applications: MenopauseDiary2, Lunanueva, PeriodCalendar, Menolife, WomanEze
- `knowledgeC.db` installation timestamps showed all five apps installed in a concentrated window: 2021-09-18 23:53 UTC through 2021-09-22 21:20 UTC — with three apps installed within a 4-minute span
- Default Apple applications all show 2021-09-12 03:48:00 UTC — consistent with initial device setup date

---

## Evidence Integrity

Hash verification was performed using two independent methods:

```
certutil -hashfile "Apple iOS Full File system_2021-10-01_Report.ufdr" SHA256
→ d4ee0bedb24e07653d11ba1eb14f68cd4cb7862e69004a974c2819fce071b523
```

Cellebrite Reader independently verified the same hash value against the original extraction, confirming no modification between acquisition and analysis.

---

## Report

> **[→ Full Examination Report (PDF)](./report/)**

---

*Examiner: Alister A. Rodrigues. Examination conducted on a verified working copy in an isolated forensic environment. Original evidence file maintained as read-only throughout.*
