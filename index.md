---
date created: Tuesday, February 17th 2026, 5:54:59 pm
date modified: Tuesday, February 17th 2026, 7:37:39 pm
layout: default
---

# My Security Writeups

A collection of writeups for HackTheBox machines and CTF challenges.

## About Me
I'm Alex, developing both my Blue and Red teaming skills.

**LinkedIn:** [https://www.linkedin.com/in/alex-glen-59105825b/]

**Twitter/X:** [https://x.com/Nintails2]

**Email:** [AlexanderCharlesGlen@gmail.com]

---

## HackTheBox

| Machine | Category | Difficulty | Date |
|---------|----------|------------|------|
{% for writeup in site.writeups %}{% if writeup.type == "HTB" %}
| [{{ writeup.title }}]({{ site.baseurl }}{{ writeup.url }}) | {{ writeup.category }} | {{ writeup.difficulty }} | {{ writeup.date | date: "%d/%m/%Y" }} |
{% endif %}{% endfor %}

## CTF Writeups

| Challenge | Event | Category | Difficulty | Date |
|-----------|-------|----------|------------|------|
{% for writeup in site.writeups %}{% if writeup.type == "CTF" %}
| [{{ writeup.title }}]({{ site.baseurl }}{{ writeup.url }}) | {{ writeup.event }} | {{ writeup.category }} | {{ writeup.difficulty }} | {{ writeup.date | date: "%d/%m/%Y" }} |
{% endif %}{% endfor %}
