---
date: <% tp.date.now("YYYY-MM-DD") %>
tags:
cssclasses:
  - daily
  - <% tp.date.now("dddd", 0, tp.file.title, "YYYYMMDD").toLowerCase() %>
---

---
# <% tp.date.now("dddd, MMMM Do · YYYY", 0, tp.file.title, "YYYYMMDDHHmm") %>

## Session Overview

🗓 **Day**:: `$= dv.current().day`
🏋️ **Split**:: `$= dv.current().split`
⏱ **Duration**:: `$= dv.current().duration` min
⚖️ **Bodyweight**:: `$= dv.current().bodyweight` kg
💭 **Felt**:: `$= dv.current().felt` / 5

---

## 💪 Exercises

| #   | Exercise | Set 1     | Set 2     | Set 3     | Set 4 | Notes |
| :-- | :------- | :-------- | :-------- | :-------- | :---- | :---- |
| 1   |          | kg × reps | kg × reps | kg × reps |       |       |
| 2   |          | kg × reps | kg × reps | kg × reps |       |       |
| 3   |          | kg × reps | kg × reps | kg × reps |       |       |
| 4   |          | kg × reps | kg × reps | kg × reps |       |       |

---

## 🔥 PRs / Highlights
* Any personal records, new weights, or moments worth remembering.

## 📝 Session Notes
* How did the session feel? Energy, pumps, form, anything off?

## ➡️ Next Session
* What to push harder on, fix, or try next time.
