---
date created: Tuesday, February 17th 2026, 9:55:45 pm
date modified: Tuesday, February 17th 2026, 10:50:22 pm
layout: default
title: Hidden in Plainsight
category: Forensics
event: PicoGym
difficulty: Easy
date: 2026-02-17
type: CTF
---

<a href="{{ site.baseurl }}/" class="btn-home">← Back to Home</a>

# PicoGym: Hidden in Plainsight

**Category:** Forensics

**Author:** Yahaya Meddy

**Difficulty:** Easy

**Date:** 17/02/26

---

## Description:

> You’re given a seemingly ordinary JPG image. Something is tucked away out of sight inside the file. Your task is to discover the hidden payload and extract the flag. Download the jpg image **here.**

**Files provided:** `img.jpg`

**URL:** <https://play.picoctf.org/practice/challenge/52>

---

## Initial Approach:

First I analysed the metadata using `exiftools`:

```Bash
exiftool img.jpg                                                                 
ExifTool Version Number         : 13.36
File Name                       : img.jpg
Directory                       : .
File Size                       : 74 kB
File Modification Date/Time     : 2026:02:17 16:57:03-05:00
File Access Date/Time           : 2026:02:17 16:57:03-05:00
File Inode Change Date/Time     : 2026:02:17 16:59:55-05:00
File Permissions                : -rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Comment                         : c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9
Image Width                     : 640
Image Height                    : 640
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 640x640
Megapixels                      : 0.410
```

## Solution:

### Decryption:

I wasn't sure if the comment was some sort of encrypted data type. So I first checked with base64:
```Bash
echo "c3RlZ2hpZGU6Y0VGNmVuZHZjbVE9" | base64 --decode                            
steghide:cEF6endvcmQ=
# If we run base64 decode at the end of the string again.
echo "cEF6endvcmQ=" | base64 --decode                
steghide:pAzzword 
```

I've heard of [Steghide](https://steghide.sourceforge.net/documentation/manual.pdf), its a tool used to analyse data within images and audio files. So we should use steghide along with the `pAzzword`:

```Bash
steghide extract -sf img.jpg -p pAzzword
```
Use -sf to define the stego-file. Here, we use it to extract data from img.jpg.

Steghide then gives us a file called `flag.txt`:
```Bash
cat flag.txt                
picoCTF{h1dd3n_1n_1m4g3_f051f2e8}
```

---

## Flag:

```
picoCTF{h1dd3n_1n_1m4g3_f051f2e8}
```

---

## Lessons Learned:

- Using basictools like `exiftools` to examine metadata is highly effective for forensic exercises; it should always be the **first port of call**.
- Data can be encoded multiple times, so it is vital to stay persistent. This serves as a reminder that **security through obfuscation** is a poor security practice.