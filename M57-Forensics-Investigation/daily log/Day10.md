# Day 10 — 28 March 2026
**Internship:** RISE — Cyber Forensics & Threat Intelligence  
**Project:** M57 Digital Forensics Investigation  
**Phase:** Event Log Analysis + IOC Compilation  
**Status:** ✅ Complete  

---

## Overview
Today’s analysis focused on examining Windows Event Logs and consolidating Indicators of Compromise (IOCs) from previous findings.  

The Security Event Log (`SecEvent.Evt`) and System Event Log (`SysEvent.Evt`) were extracted and analyzed using Kali Linux. However, no meaningful event records were recovered from the Security log, indicating potential log tampering or corruption.

Artifacts from Autopsy provided stronger evidence, allowing reconstruction of attacker activity despite missing logs.

---

## Event Log Analysis

### Security Event Log (SecEvent.Evt)
Attempted to extract login (Event ID 528) and process creation (Event ID 592) events using `strings` and parsing tools.

**Result:**
- No readable or structured event data recovered
- Output contained only minimal/unusable strings
- Indicates possible:
  - Log clearing
  - Corruption
  - Anti-forensic activity

📸 ![no output kali](../images/secevent.png)  

---

### System Event Log (SysEvent.Evt)
Basic extraction performed.

**Observation:**
- No significant or relevant system events recovered
- Logs appear incomplete or overwritten

---

## Evidence of Anti-Forensics

Multiple artifacts indicate deliberate attempts to hide activity:

- `NTUSER.DAT` entries with **zeroed timestamps (0000-00-00)**
- `userdiff.LOG` showing invalid or wiped timestamps
- Event logs not yielding usable data

**Conclusion:**  
Attacker attempted to erase or manipulate forensic evidence.

📸 ![NTUSER.DAT timestamp anomalies](../images/ntuser.png)

---

## Program Execution Evidence (Prefetch)

Prefetch analysis revealed execution of key programs:

- `TRUECRYPT.EXE` → Encryption activity
- `CMD.EXE` → Command-line usage
- `JO.EXE` → Suspicious executable
- `SETUP.EXE` → Possible installation activity

**Key Finding:**
- `TRUECRYPT.EXE` executed on **incident day (2009-12-11)**

📸![Prefetch showing TRUECRYPT execution](../images/truecrypt.png)

---

## Run Program Artifacts

Autopsy Run Programs confirmed:

- **TrueCrypt executed on incident day**
- Python executed **one day before incident**
  - Possible scripting or automation phase

📸![Run Programs evidence](..images/runprogram.png)

---

## ShellBag Analysis (User Activity)

ShellBag artifacts revealed:

- Access to external drive: **Z:\\**
- Interaction with removable media folders
- Activity timestamped on incident day

**Interpretation:**
User accessed external storage likely used for data movement.

📸![ShellBag showing Z: drive access](..images/shellbags.png) 

---

## Additional Findings

### Recent Documents
- Multiple `.lnk` files accessed on incident day
- Abnormal entries referencing `NTUSER.DAT`
- Suggests:
  - Registry access
  - Possible forensic/tool interaction

---

### USB Activity
Previously identified:
- **Two USB flash drives connected on incident day**
- Correlates with ShellBag evidence (Z: drive)

---

## Indicators of Compromise (IOCs)

### Suspicious Files
- `JO.EXE` → `/32bits_1386`
- `TRUECRYPT.EXE`
- `.doc.part` and `.csv.part` files (from earlier analysis)

### Suspicious Activity
- Execution of encryption software (TrueCrypt)
- Use of command-line tools (CMD)
- External storage access (Z:)

### Anti-Forensic Indicators
- Cleared or corrupted event logs
- Zeroed timestamps in registry files
- Missing or incomplete log data

---

## Attack Interpretation

Based on combined evidence:

1. Files were downloaded using automated scripts (Days 7–8)
2. Data was accessed and prepared
3. TrueCrypt used to encrypt sensitive data
4. External USB drives connected (data exfiltration)
5. Logs and timestamps manipulated to hide activity

---

## What I Learned Today

- Event logs can be **intentionally wiped**, making them unreliable
- Prefetch and registry artifacts can **reconstruct activity even when logs are missing**
- ShellBags are powerful for identifying **external device usage**
- Anti-forensics (timestamp wiping, log clearing) is a strong indicator of malicious intent

---
