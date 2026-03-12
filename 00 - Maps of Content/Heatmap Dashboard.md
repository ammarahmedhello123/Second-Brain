# Heatmap Dashboard

---

## 🏋️ Gym

```dataviewjs
const calendarData = {
    colors: {
        orange: ["#ffa244", "#fd7f00", "#dd6f00", "#bf6000", "#9b4e00"]
    },
    showCurrentDayBorder: true,
    defaultEntryIntensity: 4,
    entries: [],
}

for (let page of dv.pages('"02 - Areas/Fitness"').where(p => p.tags && p.tags.includes("workout"))) {
    calendarData.entries.push({
        date: page.date,
        intensity: page.felt ?? 4,
        color: "orange",
    })
}

renderHeatmapCalendar(this.container, calendarData)
```

---

## 📝 Daily Notes

```dataviewjs
const calendarData = {
    colors: {
        blue: ["#8cb9ff", "#69a3ff", "#428bff", "#1872ff", "#0058e2"]
    },
    showCurrentDayBorder: true,
    defaultEntryIntensity: 4,
    entries: [],
}

for (let page of dv.pages('"06 - Daily"')) {
    calendarData.entries.push({
        date: page.file.name,
        intensity: 4,
        color: "blue",
    })
}

renderHeatmapCalendar(this.container, calendarData)
```
