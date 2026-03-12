# Feature Showcase

Complete reference of all code block types available in the Workout Plugin.

> **Tip**: For your personal dashboard, see [[Dashboard]]

---

## 1. Charts

Charts visualize your progress over time. Available types: `volume`, `weight`, `reps`, `duration`, `distance`, `heartRate`, `pace`.

### Strength Exercise (Volume + Weight)

```workout-chart
chartType: exercise
type: volume
exercise: Bench Press
dateRange: 30
limit: 50
showTrendLine: true
showTrend: true
showStats: true
```

```workout-chart
chartType: exercise
type: weight
exercise: Squat
dateRange: 30
limit: 50
showTrendLine: true
showTrend: true
showStats: false
```

### Cardio Exercise (Distance + Pace)

```workout-chart
chartType: exercise
type: distance
exercise: Running
dateRange: 30
limit: 50
showTrendLine: true
showTrend: true
showStats: false
```

```workout-chart
chartType: exercise
type: pace
exercise: Running
dateRange: 30
limit: 50
showTrendLine: true
showTrend: true
showStats: true
```

### Timed Exercise (Duration)

```workout-chart
chartType: exercise
type: duration
exercise: Plank
dateRange: 30
limit: 50
showTrendLine: true
showTrend: true
showStats: true
```

### Workout Chart (All Exercises Combined)

```workout-chart
chartType: workout
type: volume
workout: Day 1 LOWER BODY A 2.0
dateRange: 60
limit: 50
showTrendLine: true
showTrend: true
showStats: true
```

### All Data Chart

```workout-chart
chartType: all
type: volume
dateRange: 30
limit: 50
showTrendLine: true
showTrend: true
showStats: false
```

---

## 2. Tables

Tables display your workout logs with sorting and editing capabilities.

### By Exercise

```workout-log
id: mmn6ymwwrtsr1
exercise: Bench Press
limit: 10
```

### By Workout

```workout-log
id: mmn6ymwwed79e
workout: Day 1 LOWER BODY A 2.0
limit: 15
```

### Combined (Exercise + Workout)

```workout-log
id: mmn6ymwwzhygw
exercise: Squat multi power
workout: Day 1 LOWER BODY A 2.0
limit: 10
exactMatch: true
```

---

## 3. Timers

### Countdown Timer

```workout-timer
duration: 90
type: countdown
exercise: Rest Timer
showControls: true
sound: true
```

### Interval Timer

```workout-timer
duration: 30
rounds: 5
type: interval
exercise: HIIT Intervals
showControls: true
sound: true
```

---

## 4. Duration Estimator

Estimates total workout duration based on the current note's exercises.

```workout-duration
```

---

## 5. Training Protocols

The plugin supports these protocol badges in your logs:

| Protocol | Description |
|----------|-------------|
| standard | Normal sets |
| dropset | Reduce weight, continue reps |
| myo-reps | Activation set + mini sets |
| rest-pause | Brief rest, continue to failure |
| superset | Paired exercises |
| 21s | 7+7+7 partial reps |

---

## Quick Reference

| Code Block | Purpose |
|------------|---------|
| `workout-chart` | Visualize progress over time |
| `workout-log` | Display workout data table |
| `workout-timer` | Countdown or interval timer |
| `workout-duration` | Estimate workout length |
| `workout-dashboard` | Full stats overview |

**Commands** (Ctrl/Cmd + P): Create Workout Log, Insert Chart, Insert Timer, Create Exercise Page
