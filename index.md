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

## 📊 Write-up Stats

**[{{ writeups.size }} writeups and counting!](browse/)** 

{% if featured.size > 0 %}
## ⭐ Featured Writeups

| Title | Platform | Category | Difficulty | Date |
|---|---|---|---|---|
{% for item in featured %}| [{{ item.title }}]({{ item.url | relative_url }}) | {{ item.platform }} | {{ item.category }} | {{ item.difficulty }} | {{ item.date_created | date: "%d/%m/%Y" }} |
{% endfor %}

---
{% endif %}

## 🕐 Recent Writeups

| Title | Platform | Category | Difficulty | Date |
|---|---|---|---|---|
{% for item in sorted limit:3 %}| [{{ item.title }}]({{ item.url | relative_url }}) | {{ item.platform }} | {{ item.category }} | {{ item.difficulty }} | {{ item.date_created | date: "%d/%m/%Y" }} |
{% endfor %}

---

*See the full collection on the [Writeup Index](browse/) page.*

