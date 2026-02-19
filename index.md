---
layout: default
title: Security Writeups
---

{% assign writeups = site.writeups | where_exp: "item", "item.title != ''" %}
{% assign writeups = writeups | where_exp: "item", "item.platform != ''" %}
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

**[Browse All Writeups →](_writeups/)** — searchable index with filters.

---

{% if featured.size > 0 %}
## ⭐ Featured Writeups

| Title | Platform | Category | Difficulty |
|---|---|---|---|
{% for item in featured %}| [{{ item.title }}]({{ item.url | relative_url }}) | {{ item.platform }} | {{ item.category }} | {{ item.difficulty }} |
{% endfor %}

---
{% endif %}

## 🕐 Recent Writeups

| Title | Platform | Category | Difficulty | Date |
|---|---|---|---|---|
{% for item in sorted limit:3 %}| [{{ item.title }}]({{ item.url | relative_url }}) | {{ item.platform }} | {{ item.category }} | {{ item.difficulty }} | {{ item.date_created }} |
{% endfor %}

---

*See the full collection on the [Writeup Index](writeups/) page.*