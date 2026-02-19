---
date created: Tuesday, February 17th 2026, 9:11:39 pm
date modified: Tuesday, February 17th 2026, 10:19:20 pm
layout: default
title: Riddle Registry
platform: PicoGym
category: Forensics
difficulty: Easy
os: Linux
featured: false
tags: []

---

<a href="{{ site.baseurl }}/" class="btn-home">← Back to Home</a>

# PicoGym - Riddle Registry:

**Category:** *Forensics*

**Author:** *Prince Niyonshuti N.* 

**Difficulty:** *Easy* 

**Date:** *17-02-2026*

---

## Description:

> Hi, intrepid investigator! 📄🔍 You've stumbled upon a peculiar PDF filled with what seems like nothing more than garbled nonsense. But beware! Not everything is as it appears. Amidst the chaos lies a hidden treasure, an elusive flag waiting to be uncovered. Find the PDF file here [Hidden Confidential Document](https://challenge-files.picoctf.net/c_amiable_citadel/3f00b89eeac6ac5242f747889ea4de24c804d9144cfa71e23d754e6a8e80e435/confidential.pdf) and uncover the flag within the metadata.

**Files provided:** `confidential.pdf`

**URL:** <https://play.picoctf.org/practice/challenge/530>

---

## Approach:

I'm not sure how to redact text from a pdf file or how to forensically analyse it. - but the actual pdf content itself hints at looking beyond the file. 

So I decided to research tools to use: 
- [exiftool](https://exiftool.org/) - This tools extracts all embedded metadata from a wide range of files.
- [pdfid](https://www.kali.org/tools/pdfid/) - Scans a PDF file for keywords, which allows you to detect if a PDF document contains JavaScript or will execute an action when opened. 
- [pdf-parser](https://py-pdf-parser.readthedocs.io/en/latest/overview.html) - Python-based PDF parser that locates, classifies, and extracts specific structured data from PDF documents by treating content as manageable elements.

---

## Solution:

### Initial Recon:

Initially I tried using `pdfid` to look for any scripts or programs that would run and got nothing, then I tried using `pdf-parser` to de-construct chunks of the file, but that felt more rabbit hole-esc, since I struggled to figure out what I was looking at.

I then moved to using `exiftool`, which is more of Swiss army knife tool for looking at metadata. I then saw something interesting under the author tag. 

```Bash
exiftool confidential.pdf               
ExifTool Version Number         : 13.36
File Name                       : confidential.pdf
Directory                       : .
File Size                       : 183 kB
File Modification Date/Time     : 2026:02:17 16:14:22-05:00
File Access Date/Time           : 2026:02:17 16:16:08-05:00
File Inode Change Date/Time     : 2026:02:17 16:14:22-05:00
File Permissions                : -rw-rw-r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.7
Linearized                      : No
Page Count                      : 1
Producer                        : PyPDF2
Author                          : cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0=
```

## Decryption:

I recognised the author name as being base64 encoded. So I hopped over to [Cyber Chef](https://gchq.github.io/CyberChef/) to quickly decode the string.

Alternatively, you could also use `base64` within the terminal to decode the flag.

```Bash
echo "cGljb0NURntwdXp6bDNkX20zdGFkYXRhX2YwdW5kIV9jOTk5ZTJhNH0=" | base64 --decode
picoCTF{puzzl3d_m3tadata_f0und!_c999e2a4}  
```

---

## Flag:

```
picoCTF{puzzl3d_m3tadata_f0und!_c999e2a4}
```

---

## Lessons Learned:

- When approaching a challenge, use basic and general tools first - like `exiftool` before trying more specialised tools first.
- Using meta information from challenging like description briefings, or difficulty or hints can help lead you in more certain directions.