# TryHackMe — Intro to Digital Forensics

**Platform:** TryHackMe  
**Room:** [Intro to Digital Forensics](https://tryhackme.com/room/introdigitalforensics)  
**Difficulty:** Easy  
**Date Completed:** 02-03-2026  
**Points Earned:** 40  
**Tasks Completed:** 3  

---

## What is Digital Forensics?

Digital forensics (also known as computer forensics) is the practice of collecting and analyzing evidence from digital devices such as smartphones, laptops, PCs, digital cameras, and USB flash drives. This evidence can be used in investigations by law enforcement, government agencies, or corporate bodies.

### Two Types of Digital Forensics

- **Public Sector** — Carried out by government and law enforcement agencies as part of a crime or civil investigation.
- **Private Sector** — Carried out by corporate bodies to investigate violations of company policies.

---

## Key Principles of Digital Forensics

According to Ken Zatyko, former director of the Defense Computer Forensics Laboratory, a proper digital forensics investigation must follow these principles:

- **Proper Search Authority** — Investigators cannot commence without proper legal authority.
- **Chain of Custody** — Tracks who held the evidence at every point during the case.
- **Validation with Mathematics** — Hash functions are used to confirm files have not been modified.
- **Use of Validated Tools** — All forensic tools must be validated to ensure accuracy (e.g., disk imaging tools).
- **Repeatability** — Findings must be reproducible with the same tools and skills.
- **Reporting** — The investigation concludes with a formal report of all discovered evidence.

---

## Chain of Custody

The chain of custody documents the complete journey of evidence throughout a legal case. The basic process at a forensic scene:

**At the Scene:**
1. Acquire the evidence
2. Establish a chain of custody
3. Place the evidence in a secure container
4. Transport to the lab

**At the Lab:**
1. Retrieve from secure container
2. **Create a forensic copy** — never work on the original evidence
3. Return the original digital evidence to secure storage
4. Begin processing the copy

> ⚠️ Advanced forensic software exists specifically to prevent modification of original evidence during acquisition.

---

## Scenario

> A cat named **Gato** was kidnapped. The kidnapper sent a ransom note as an MS Word document. It was converted to PDF and an image was extracted from it. We are tasked with analyzing the document and image metadata to gather evidence.

**Files provided:**
- `ransom-letter.pdf`
- `letter-image.jpg`
- `ransom-letter.doc`
- `ransom-lettter-2.zip`

---

## Task 1 — PDF Metadata Extraction

### Tool: `pdfinfo`

> If not installed: `sudo apt install poppler-utils`

**Command used:**
```bash
pdfinfo ransom-letter.pdf
```

**Screenshot:**

![pdfinfo output](screenshots/Screenshot_1.png)

**Results extracted:**

| Field | Value |
|---|---|
| Title | Pay NOW |
| Subject | We Have Gato |
| Author | **Ann Gree Shepherd** |
| Creator | Microsoft® Word 2016 |
| Producer | Microsoft® Word 2016 |
| CreationDate | Wed Feb 23 09:10:36 2022 GMT |
| ModDate | Wed Feb 23 09:10:36 2022 GMT |
| Pages | 1 |
| File Size | 71371 bytes |

---

### Tool: `exiftool`

> If not installed: `sudo apt install libimage-exiftool-perl`

**Command used:**
```bash
exiftool ransom-letter.pdf
```

**Screenshot:**

![exiftool PDF output](screenshots/Screenshot_2.png)

**Additional data from exiftool:**

| Field | Value |
|---|---|
| XMP Toolkit | 3.1-701 |
| Language | en-US |
| Document ID | uuid:9D060682-E6D1-4DC7-B375-EDCBB79A2CD4 |
| Author | Ann Gree Shepherd |
| Create Date | 2022:02:23 11:10:36+02:00 |

> 💡 **Note:** `exiftool` gave the same core data as `pdfinfo` but with additional XMP metadata fields. Both tools are useful — `pdfinfo` for quick readable output, `exiftool` for deeper metadata.

> ⚠️ **Tip for learners:** THM's room displayed an older PDF with a creation date of **October 10, 2018**. The file in the AttackBox had been updated, showing **February 23, 2022** instead. This is a known discrepancy — always trust what your own tools extract.

---

## Task 2 — Photo EXIF Data (GPS Location)

**EXIF** stands for **Exchangeable Image File Format** — a standard for embedding metadata into image files. Every photo taken on a smartphone or digital camera embeds a wealth of information.

### Extracting GPS Coordinates

**Command used:**
```bash
exiftool letter-image.jpg | grep -i gps
```

**Screenshot:**

![GPS extraction](screenshots/Screenshot_4.png)

**Results:**

| Field | Value |
|---|---|
| GPS Latitude Ref | North |
| GPS Longitude Ref | West |
| GPS Time Stamp | 13:37:33 |
| GPS Latitude | 51 deg 30' 51.90" N |
| GPS Longitude | 0 deg 5' 38.73" W |
| GPS Position | 51 deg 30' 51.90" N, 0 deg 5' 38.73" W |

### Finding the Location on Google Maps

To search on Google Maps, replace `deg` with `°` and remove extra spaces:

**Search query used:** `51°30'51.9"N 0°05'38.7"W`

**Screenshot:**

![Google Maps result](screenshots/Screenshot_5.png)

**Result: Milk Street, London EC2V 6DN, UK** ✅

---

## Task 3 — Camera Model Identification

**Command used:**
```bash
exiftool letter-image.jpg | grep -i camera
```

**Screenshot:**

![Camera model](screenshots/Screenshot_7.png)

**Result: Canon EOS R6** ✅

---

## Final Answers Summary

| Question | Answer |
|---|---|
| Author of the PDF | Ann Gree Shepherd |
| Street where photo was taken | Milk Street |
| Camera model used | Canon EOS R6 |

---

## Room Completion

![Room Completed](screenshots/Screenshot_9.png)

**Room completed at 100%! 🎉**  
40 points earned | 3 tasks completed

---

## Key Takeaways

- **Metadata is everywhere** — PDFs, images, and documents all contain hidden information about their origin, author, and even location.
- **GPS coordinates in photos** can pinpoint exactly where a photo was taken — a critical piece of evidence in real investigations.
- **`exiftool`** is one of the most powerful and versatile metadata analysis tools available in Linux.
- **`pdfinfo`** is a quick and readable way to extract PDF-specific metadata.
- Always work on a **forensic copy**, never the original evidence.
- THM rooms can sometimes have outdated screenshots — trust your own extracted data.

---

## Tools Used

| Tool | Purpose | Install Command |
|---|---|---|
| `pdfinfo` | Extract PDF metadata | `sudo apt install poppler-utils` |
| `exiftool` | Extract image/file metadata | `sudo apt install libimage-exiftool-perl` |
| Google Maps | Verify GPS coordinates | Web browser |

---

*Writeup by hariniaswitha p | TryHackMe: hariniaswithaa-p*
