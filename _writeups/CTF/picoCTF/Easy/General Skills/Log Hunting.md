---
title: Log Hunting
layout: default
platform: PicoGym
category: General Skills
difficulty: Easy
os: Linux
featured: true
tags: []
date_created: Tuesday, February 17th 2026, 6:04:46 pm
date_modified: Friday, February 20th 2026, 2:44:45 pm
---

# PicoGym - Log Hunting:

**Category:** *General Skills*

**Author:** *Yahaya Meddy*

**Difficulty:** *Easy*

**Date:** *17/02/2026*

---

## Description:

> Our server seems to be leaking pieces of a secret flag in its logs. The parts are scattered and sometimes repeated. Can you reconstruct the original flag? Download the **logs** and figure out the full flag from the fragments.

**Files provided:** `server.log (ASCII text)` 

**URL:** <https://play.picoctf.org/practice/challenge/527>

---

## Approach:

My first thought was to `cat server.log` to try and read it. But it was a long file, so I decided to use the `head` and `tail` command to read the start and end.

---

## Solution:

### Step 1 - Initial Recon:

Interestingly at the start of the `server.log` file:
```bash
head server.log
...SNIP...
[1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_
[1990-08-09 10:00:16] WARN Disk space low
[1990-08-09 10:00:19] DEBUG Cache cleared
```

We can see a chunk of the flag, with the power of grep, we could search for all lines with `INFO_FLAGPART`
### Step 2: Key Insight:

The grep technique works fine, but has lots of repeating lines, I'd like a cleaner implementation.
```bash
grep "INFO FLAGPART" server.log          
[1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_
[1990-08-09 10:02:55] INFO FLAGPART: y0urlinux_
[1990-08-09 10:05:54] INFO FLAGPART: sk1lls_
[1990-08-09 10:05:55] INFO FLAGPART: sk1lls_
[1990-08-09 10:10:54] INFO FLAGPART: cedfa5fb}
[1990-08-09 10:10:58] INFO FLAGPART: cedfa5fb}
[1990-08-09 10:11:06] INFO FLAGPART: cedfa5fb}
...SNIP...
```

### Step 3: Enhancing Our `grep` Usage:

So our advanced grep statement would be:
```bash
grep "INFO FLAGPART" server.log | awk '{print $NF}' | uniq | head -n 4 | tr -d '\n'
```

This statement can be broken down as the following:

1. First, search the log file for any lines containing `INFO FLAGPART`.
	1. `grep "INFO FLAGPART" server.log` - Pretty self-explanatory.

2. Strip the date, time, flagpart, only return the actual flag.
	1. `awk '{print $NF}'`

The `$NF` is a built in function that counts the number of words within the current line. So it splits fields by spaces. If we take the following phrase: `[1990-08-09 10:00:10] INFO FLAGPART: picoCTF{us3_` 

For example:

| **Field** | **Content**        | **Description**          |
| --------- | ------------------ | ------------------------ |
| `$1`      | `[1990-08-09`      | The date                 |
| `$2`      | `10:00:10]`        | The time                 |
| `$3`      | `INFO`             | The log level            |
| `$4`      | `FLAGPART:`        | The label                |
| `$5`      | **`picoCTF{us3_`** | **The actual flag part** |

So since we've got 5 fields, our `$NF` = 5. So by performing `{print $NF}` we print the last word in the string basically. 

3. Remove any duplicates
	1. `uniq` - Note that `uniq` only removes duplicates that are touching/adjacent to each other. It only compares the current line to the previous line.

For instance, with the file `fruits.txt`:
```Bash
Apple
Orange
Apple
```

if we tried using `uniq` by itself...
```Bash
cat fruits.txt | uniq
Apple
Orange
Apple
```
Since orange separates the apple, **the duplicate will not be removed**, as it is not adjacent. 

However we can fix this problem by first sorting the list:
```Bash
cat fruits.txt | sort | uniq # OR sort -u fruits.txt works too.
Apple
Orange
```
Now we can see that all duplicates have been removed, since our list was sorted first, meaning that `uniq` could "see" the two apples next to each other.

4. Once we've found the 4 unique parts, stop looking.
	1. `head -n 4`
	2. Since our flag is constructed out of 4 parts, once `uniq` has squashed the repeating lines, we don't need to capture more than one string containing the flag.

5. Finally, strip all new line characters
	1. `tr -d '\n'` (transform by deleting, all newline character)
	2. This ensures that our flag doesn't turn into a vertical list.

## Flag:

```Plaintext
picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}
```

---

## Lessons Learned:

- Text filtering in Linux is really useful in a wide range of applications, so taking the time, to search for details properly, is very beneficial in the long run.
- `head` and `tail` are useful beyond grabbing the top and end of a file, since you can use them within a pipe to format your inputs further.
- Be careful when using `uniq` when filtering text files. Make sure the list is already sorted or use `sort -u` or `sort | uniq` to remove all duplicates.
### Tools:
- `awk` can be used grab the first word or last word in a string.
	- First = `awk '{print $(NF-1)}'`
	- Last = `awk '{print $NF}'`