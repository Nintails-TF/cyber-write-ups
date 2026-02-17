---
date created: Tuesday, February 17th 2026, 5:54:59 pm
date modified: Tuesday, February 17th 2026, 7:37:39 pm
layout: default
---

# My Security Writeups

A collection of writeups for HackTheBox machines and CTF challenges.

## About Me
I'm Alex, developing both my Blue and Red teaming skills.

**LinkedIn:** [Alex Glen](https://www.linkedin.com/in/alex-glen-59105825b/)

**Twitter/X:** [Nintails](https://x.com/Nintails2)

**Email:** [AlexanderCharlesGlen@gmail.com](mailto:AlexanderCharlesGlen@gmail.com)

---

## HackTheBox
<table>
  <thead>
    <tr><th>Machine</th><th>Category</th><th>Difficulty</th><th>Date</th></tr>
  </thead>
  <tbody>
    {% for writeup in site.writeups %}
      {% if writeup.type == "HTB" %}
      <tr>
        <td><a href="{{ site.baseurl }}{{ writeup.url }}">{{ writeup.title }}</a></td>
        <td>{{ writeup.category }}</td>
        <td>{{ writeup.difficulty }}</td>
        <td>{{ writeup.date | date: "%d/%m/%Y" }}</td>
      </tr>
      {% endif %}
    {% endfor %}
  </tbody>
</table>

## CTF Writeups
<table>
  <thead>
    <tr><th>Challenge</th><th>Event</th><th>Category</th><th>Difficulty</th><th>Date</th></tr>
  </thead>
  <tbody>
    {% for writeup in site.writeups %}
      {% if writeup.type == "CTF" %}
      <tr>
        <td><a href="{{ site.baseurl }}{{ writeup.url }}">{{ writeup.title }}</a></td>
        <td>{{ writeup.event }}</td>
        <td>{{ writeup.category }}</td>
        <td>{{ writeup.difficulty }}</td>
        <td>{{ writeup.date | date: "%d/%m/%Y" }}</td>
      </tr>
      {% endif %}
    {% endfor %}
  </tbody>
</table>
