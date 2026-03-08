# Day 4 — 07 March 2026
**Internship:** RISE — Cyber Forensics & Threat Intelligence  
**Project:** M57 Digital Forensics Investigation  
**Phase:** Phase 2 — Browser, Email & Communication Artifacts  
**Status:** ✅ Complete

---

## Overview
Took a step back today. I've been poking around Autopsy without fully understanding 
what I'm looking at so I spent the day watching tutorials instead of forcing progress. 
Glad I did — a few things from Day 2 that confused me finally make sense now.

---

## What I Covered

- How the MFT works and why deleted files can still have timestamps even when 
  marked as unallocated — clears up the sc10.bin.tmp situation from Day 2
- How Autopsy detects extension mismatches using magic bytes, not just the filename
- What Shell Bags actually are — basically Windows logging which folders you opened, 
  even if the folder is gone. 72 entries on Jo's machine is worth a closer look
- The blank IE URL entries from Day 2 are probably just session records, IE does that 
  even in normal use — not necessarily evidence of tampering

---

## What I Learned Today
- Slowing down to understand the tool is better than rushing through artifacts you 
  can't properly explain
- Shell Bags are more useful than I initially gave them credit for — going to look at 
  those properly on Day 7

---

## Next Steps (Day 5)
- Back into the investigation — browser history, email artifacts, web downloads
- Keep the sc10.bin.tmp and Shell Bags findings in mind going forward
