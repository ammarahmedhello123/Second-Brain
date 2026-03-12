---
date: <% tp.date.now("YYYY-MM-DD") %>T<% tp.date.now("HH:mm") %>
tags:
cssclasses:
  - daily
  - <% tp.date.now("dddd", 0, tp.file.title, "YYYYMMDD").toLowerCase() %>
gym: 0
mood: 0
---

# DAILY NOTE

<% tp.date.now("dddd, MMMM Do, YYYY", 0, tp.file.title, "YYYYMMDD") %>

---

## 📓 Journal

---

## ✅ Tasks

- [ ]
- [ ]
- [ ]

---

## 🏋️ Gym

> Change `gym: 0` in frontmatter to `gym: 1` if you trained today

**Trained today?** No

---

## 😊 Mood

> Rate your mood in frontmatter `mood:` from 1 (bad) to 5 (great)

**Mood:** —