# Legacy Mobile Device & SIM Card Analysis — LG VX9100

<p align="center">
  <img src="https://img.shields.io/badge/Device-LG_VX9100_(Verizon)-informational?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Evidence-AD1%2FAD1X_Logical_Extractions-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Tool-FTK_Imager-red?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Tool-Autopsy_4.22.1-darkblue?style=for-the-badge" />
</p>

---

## Case Summary

| Field | Detail |
|---|---|
| **Case Reference** | Practical_AD1_Case, Case No. 001 |
| **Evidence Sources** | FTK_Export_Cingular_SIM (SIM card dump) · FTK_Export_LG_LG-VX9100 (device dump) |
| **Evidence Format** | AD1 / AD1X logical extraction |
| **Device** | LG VX9100 (Verizon Wireless) |
| **Companion Evidence** | Cingular SIM card |
| **Acquisition Tool** | FTK Imager |
| **Analysis Tool** | Autopsy 4.22.1 |
| **Examiner** | Alister A. Rodrigues |

---

## What This Examination Covers

Dual-source forensic analysis of a legacy early-2000s feature phone and its associated SIM card. Two logical AD1/AD1X extractions were ingested into Autopsy and examined across user data, file types, databases, multimedia, keyword artifacts, and system configuration — demonstrating that legacy devices preserve substantial forensic evidence when examined with current tooling.

---

## Methodology

**Acquisition:** Two logical extractions provided in AD1/AD1X format, extracted via FTK Imager into separate case folders (`FTK_Export_Cingular_SIM`, `FTK_Export_LG_LG-VX9100`).

**Case Setup:** New case created in Autopsy 4.22.1 (`Practical_AD1_Case`, Case No. 001), configured with file system analysis, keyword search, and embedded file extraction modules.

**Examination:** Evidence analyzed under both Data Sources and File Views tabs. Artifacts cross-referenced across categories (e.g., text messages found under both User Data and keyword search) to validate consistency. Metadata (timestamps, file paths, hash values) preserved for all notable artifacts.

**Verification:** Extracted evidence cross-referenced across multiple categories to confirm consistency. Screenshots documented at each major step.

---

## Key Findings

### Text Messages
- **15 SMS artifacts** from SIM card under `FTK_Export_Cingular_SIM → User Data → TextMessages`
- **16 SMS artifacts** from LG handset under `FTK_Export_LG_LG-VX9100 → User Data → TextMessages`
- Fragment-style short messages consistent with early-2000s feature phone format
- Overlapping messages across both sources confirm cross-source consistency, strengthening evidentiary reliability
- Message content indicates active personal communications and social exchanges

### Contacts
- **18 contacts** on SIM card — including Casey Hammond, Greg Gallant, Holly Bryant, Sara Smith, Lance Logan
- **6 entries** on handset phonebook — including BAL, MIN, PMT, Zack
- Overlap and distinction between SIM and handset contact sets provides behavioral insight into device usage patterns

### Images & Media
- **17 image files** recovered: JPEG, BMP formats — stored on handset, none on SIM
- Images include: Happy Birthday.jpg, Smile.jpg, Congratulations.jpg, Hearts.jpg, Thinking of you.jpg
- **5 audio files**: MIDI ringtones including Beethovens_fifth.mid, Rainforest.mid
- **2 video files** in 3GPP format — one depicts an individual seated at a computer desk
- Multiple SWF Flash animation files (wallpapers, world clock utility)

### Databases
- `MMSMsg.db` — contains phone numbers and MMS PDU message identifiers
- `alert.db`, `clip.db`, `ldb.db` — additional system databases recovered
- MMS database corroborates phone number associations identified in other artifact categories

### Keyword Hits & Email Artifacts
- **14 email addresses** recovered from IM log files via Autopsy keyword search
- Providers include: hotmail.com, aol.com, msn.com
- `mobileim.bar` file contained `john@hotmail.com` linked to mobile IM messaging activity
- Keyword hits for "Good Night" located in `mediacan000.dat`

### System Metadata
- Device configuration XML confirmed: LG VX9100, Verizon Wireless distributor, firmware 1.0, hardware 0, encryption enabled
- Device-level metadata extracted from system configuration files within the filesystem

### Suspicious Items
- Autopsy flagged items including `.bar`, `.dat`, `.fil` files with embedded service references
- One item contained the string `0000001315@vzw3g.com` — associated with Verizon's mobile email/messaging gateway
- Flagged items provide investigative leads for service account correlation

---

## Report

> **[→ Full Examination Report (PDF)](./report/)**

---

*Examiner: Alister A. Rodrigues. All analysis conducted on logical extractions in a controlled forensic environment.*
