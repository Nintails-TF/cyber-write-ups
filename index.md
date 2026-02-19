---
layout: default
title: Security Writeups
---

{% assign writeups = site.pages | where_exp: "page", "page.title and page.title != '' and page.platform and page.platform != ''" %}
{% assign featured = writeups | where: "featured", true %}
{% assign sorted = writeups | sort: "date_created" | reverse %}

# My Security Writeups

A collection of writeups for HackTheBox machines and CTF challenges.

## About Me

I'm Alex, developing both my Blue and Red teaming skills.

**LinkedIn:** [alex-glen](https://www.linkedin.com/in/alex-glen-59105825b/)  
**Twitter/X:** [@Nintails2](https://x.com/Nintails2)

---

## 📊 Stats

| Total Writeups | Platforms | 
|---|---|
| {{ writeups.size }} | {% assign platforms = writeups | map: "platform" | uniq %}{{ platforms | join: ", " }} |

**[Browse All Writeups →](writeups/)** — searchable index with filters.

---

{% if featured.size > 0 %}
## ⭐ Featured Writeups

| Title | Platform | Category | Difficulty |
|---|---|---|---|
{% for page in featured %}| [{{ page.title }}]({{ page.url | relative_url }}) | {{ page.platform }} | {{ page.category }} | {{ page.difficulty }} |
{% endfor %}

---
{% endif %}

## 🕐 Recent Writeups

| Title | Platform | Category | Difficulty | Date |
|---|---|---|---|---|
{% for page in sorted limit:3 %}| [{{ page.title }}]({{ page.url | relative_url }}) | {{ page.platform }} | {{ page.category }} | {{ page.difficulty }} | {{ page.date_created | date: "%d-%m-%Y" }} |
{% endfor %}

---

*See the full collection on the [Writeup Index](writeups/) page.*
