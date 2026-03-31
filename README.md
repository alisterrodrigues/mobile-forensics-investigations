# Mobile Forensics Investigations

<p align="center">
  <img src="https://img.shields.io/badge/iOS-Cellebrite_Reader-lightgrey?style=for-the-badge&logo=apple&logoColor=white" />
  <img src="https://img.shields.io/badge/Mobile-Autopsy_%2B_FTK-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Android-JADX_%2B_PCAPdroid-green?style=for-the-badge&logo=android&logoColor=white" />
  <img src="https://img.shields.io/badge/Method-Static_%26_Dynamic_Analysis-orange?style=for-the-badge" />
</p>

---

## Overview

Three mobile forensics examinations conducted across different device types, evidence formats, and analysis methodologies. Each investigation follows established forensic practices — hash-verified acquisition, controlled examination environment, documented artifact recovery, and structured reporting.

Taken together, they demonstrate a progression from full iOS filesystem analysis through legacy mobile artifact recovery to Android application behavioral profiling: three different platforms, three different toolchains, one consistent analytical approach.

---

## Examinations

### [01 — iOS Full Filesystem Analysis](./01-ios-full-filesystem-analysis/)
**Device:** Apple iPhone 8 · **Format:** UFDR (Cellebrite) · **Tools:** Cellebrite Reader 7.48.1.3 + DB Browser for SQLite

Full filesystem extraction from an iPhone 8. SHA-256 hash verification against both Windows CertUtil and Cellebrite's internal validator. Analysis spans device metadata, owner identification through `Accounts3.sqlite`, email communications (134 messages), application forensics via `applicationState.db` and `knowledgeC.db`, 5,790 geolocation artifacts (1,860 recovered deleted), 3,609 Wi-Fi BSSID entries with coordinates, and Bluetooth connectivity records.

Key findings: single-user device profile established through Apple ID correlation; health-tracking application cluster installed in a concentrated 4-minute window; geolocation data corroborates continuous device activity near 40.73°N, 73.87°W; no recoverable SMS/iMessage content, with documented forensic explanation.

---

### [02 — Legacy Mobile Device & SIM Card Analysis](./02-legacy-mobile-device-analysis/)
**Device:** LG VX9100 (Verizon) + Cingular SIM · **Format:** AD1/AD1X logical extractions · **Tools:** FTK Imager + Autopsy 4.22.1

Dual-source examination of a legacy early-2000s mobile device and associated SIM card. FTK Imager used for AD1/AD1X extraction into two separate case folders, ingested into Autopsy with file system analysis, keyword search, and embedded file extraction modules enabled.

Key findings: 15 SMS artifacts from SIM, 16 from handset — overlapping content confirms cross-source consistency; 18 SIM contacts + 6 handset entries reconstructing the user's communication circle; 17 image files including JPEG/BMP stored on handset; 3GPP video capturing a person at a computer; MMS database (`MMSMsg.db`) with phone numbers and PDU references; 14 email addresses recovered from IM log files; device configuration XML confirming LG VX9100 identity, Verizon distributor, firmware version, and encryption settings; Autopsy-flagged suspicious items including a Verizon email gateway string.

---

### [03 — Android APK Static & Dynamic Analysis](./03-android-apk-analysis/)
**Target:** PeriodTracker (Flo Health) v4.13.0 · **Package:** `org.iggymedia.periodtracker` · **Tools:** JADX-GUI + Apktool + PCAPdroid

Combined static and dynamic examination of an Android health-tracking application. Static analysis performed on decompiled APK using JADX-GUI and Apktool — reviewing AndroidManifest permissions, declared components, third-party SDK inventory, and embedded resource strings. Dynamic analysis conducted on a physical Android device using PCAPdroid for live traffic capture, producing a real-device behavioral profile rather than emulated output.

Key findings: permission set covers INTERNET, location (fine + coarse), external storage, account metadata, background operations, and push messaging; third-party SDK architecture includes Firebase, Crashlytics, Flurry, Adjust, AppsFlyer, Segment, and Usercentrics; all runtime traffic encrypted (HTTPS + QUIC); Usercentrics CMP requests initiated before any user interaction — a pre-consent initialization pattern with potential GDPR implications; static declarations and runtime behavior fully consistent across both analysis phases.

---

## Toolchain Summary

| Tool | Purpose | Used In |
|---|---|---|
| **Cellebrite Reader 7.48.1.3** | UFDR parsing, iOS artifact categorization | Investigation 01 |
| **DB Browser for SQLite 3.12.2** | Direct iOS database querying (`applicationState.db`, `knowledgeC.db`, `sms.db`) | Investigation 01 |
| **FTK Imager** | AD1/AD1X logical extraction and export | Investigation 02 |
| **Autopsy 4.22.1** | Multi-source artifact analysis, keyword search, file type carving | Investigation 02 |
| **JADX-GUI** | APK decompilation, manifest inspection, source code review | Investigation 03 |
| **Apktool** | APK resource extraction and raw structure analysis | Investigation 03 |
| **PCAPdroid** | Live Android network traffic capture (per-app filtering) | Investigation 03 |
| **Windows CertUtil** | SHA-256 hash verification | Investigation 01 |

---

## Evidence Formats Covered

| Format | Description |
|---|---|
| **.ufdr** | Cellebrite Universal Forensic Data Report — full iOS filesystem extraction |
| **.ad1 / .ad1x** | AccessData logical image format — mobile device and SIM extractions |
| **.apk** | Android application package — static and dynamic behavioral analysis |
| **.sqlite / .db** | iOS system databases queried directly for artifact recovery |

---

*Developed by Alister A. Rodrigues. All examinations conducted on forensic working copies within controlled environments. Original evidence files maintained as read-only throughout each examination.*
