# 📊 Heatmap Dashboard

---

## 🏋️ Gym Consistency

```dataviewjs
dv.span("** 🏋️ Gym **")
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
        content: "🏋️",
        color: "orange",
    })
}

renderHeatmapCalendar(this.container, calendarData)
```

---

## 📝 Daily Notes Written

```dataviewjs
dv.span("** 📝 Consistency **")
const calendarData = {
    colors: {
        green: ["#c6e48b", "#7bc96f", "#49af5d", "#2e8840", "#196127"]
    },
    showCurrentDayBorder: true,
    defaultEntryIntensity: 4,
    entries: [],
}

for (let page of dv.pages('"06 - Daily"')) {
    calendarData.entries.push({
        date: page.file.name,
        intensity: 4,
        content: "📝",
        color: "green",
    })
}

renderHeatmapCalendar(this.container, calendarData)
```