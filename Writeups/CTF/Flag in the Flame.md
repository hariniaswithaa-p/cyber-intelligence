# picoCTF – Flag in Flame

**Category:** Forensics | **Difficulty:** Easy

---

## What's the challenge about?

The SOC team discovered a suspiciously large log file after a recent breach. When they opened it, they found an enormous block of encoded text instead of typical logs. Something wasn't right — real log files don't look like that.

---

## First look

Opening `logs.txt` was immediately suspicious. The whole file was just a massive wall of jumbled characters. But the structure of it gave it away pretty quickly — it was Base64. The challenge even hinted at it: decode the Base64 and generate an image.

> 📸 *[Screenshot 1: logs.txt showing the encoded content]*

---

## Decoding the file

One command in Linux does the whole thing:

```bash
cat logs.txt | base64 --decode > log.jpg
```

That turned the "log file" into an actual jpg image. So it was never a log file to begin with — just an image disguised as one.

> 📸 *[Screenshot 2: decoding base64 to image]*

---

## Something at the bottom of the image

The image wasn't clean. At the bottom there were some jumbled letters sitting there that didn't belong. I assumed it was hex — and it was:

```
7069636F4354467B666F72656E736963735F616E616C797369735F69735F616D617A696E675F62653836303237397D
```

---

## Decoding the hex

I threw it into **CyberChef** using the "From Hex" operation and it decoded straight to ASCII — the flag.

I actually got to know about CyberChef from a previous picoCTF challenge, and it's been useful ever since.

> 📸 *[Screenshot 3: decoding the text in the image]*

---

## Flag

```
picoCTF{forensics_analysis_is_amazing_be860279}
```

---

## What I took away from this

Two layers of encoding — Base64 hiding an image inside a fake log file, and then hex hiding the flag inside that image. The solve chain was: spot the Base64 → decode it into a jpg → notice the hex string at the bottom → decode hex to ASCII → flag.

---

## Tools used

- `base64` (Linux) — decoding the log file into an image
- **CyberChef** — decoding the hex string found in the image
