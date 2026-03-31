# 🕵️ Digital Investigation Report

## 📌 Overview

This repository contains a detailed digital forensic investigation conducted to analyze suspicious activity identified in a system image.

## 🎯 Objectives

* Identify malicious artifacts
* Analyze execution traces
* Determine attacker behavior
* Document forensic findings

## 📂 Report

👉 [Download Full Investigation Report](./M57-Forensics-Investigation/Final_report.pdf)

## 🔍 Key Findings

- Sensitive US government document (STU-III briefing) was downloaded multiple times using automated scripts  
- TrueCrypt encryption tool was installed and used on the incident date  
- External USB drive connected; encrypted files accessed shortly after insertion  
- 1,690 files deleted; timestamps wiped → clear anti-forensics activity  
- Windows Security Event Logs were cleared  
- Files disguised with fake extensions to avoid detection  
- Evidence of scripted activity using Python and browser automation  
- Spoofed phishing email targeting 25 government recipients identified  
- Suspicious files found (e.g., `sc10.bin.tmp`, `jo.exe`)  
- Possible credential access via SAM and SECURITY registry hive  

## 🧾 Conclusion

Deliberate insider threat involving data collection, encryption, USB-based exfiltration, and anti-forensics techniques.
## 🧰 Tools Used

* Autopsy
* kali linux
* MITRE ATT&CK Framework
* Hash analysis tools

## 📁 Evidence

Relevant artifacts are stored in the `daily log/` directory:

* Logs
* Extracted files
* Hash values

## ⚠️ Disclaimer

This investigation is conducted for educational and forensic analysis purposes only.

## 👩‍💻 Author

Harniaswitha P
