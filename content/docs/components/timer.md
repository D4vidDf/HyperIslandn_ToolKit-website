---
title: Timer Info
weight: 13
---

# Timer Info

The `TimerInfo` component handles live counting timers. It is used across various layouts—including **Animated Info** and the **Dynamic Island** (Big Island)—to display countdowns or stopwatches that update in real-time without needing constant push updates.

## Usage

```kotlin
val now = System.currentTimeMillis()
val duration = 60_000L // 1 minute

val myTimer = TimerInfo(
    timerType = -1,             // -1 = Start Countdown
    timerWhen = now + duration, // Target End Time
    timerTotal = duration,      // Total Duration
    timerSystemCurrent = now    // Current System Time
)
```
## Data Model (`TimerInfo`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `timerType` | `Int` | **Required.** Controls the timer mode and state.<br>`-2`: Stop/Pause Countdown.<br>`-1`: **Start Countdown** (Counts down to `timerWhen`).<br>`0`: Default / Standard.<br>`1`: **Start Chronometer** (Counts up).<br>`2`: Stop/Pause Chronometer. |
| `timerWhen` | `Long` | **Required.** The absolute target timestamp (milliseconds).<br>For countdowns, this is the time when the timer hits 0. |
| `timerTotal` | `Long` | **Required.** The total duration of the timer in milliseconds. Used to calculate progress bars (if applicable). |
| `timerSystemCurrent` | `Long` | **Required.** The `System.currentTimeMillis()` at the moment of creation. This is used to synchronize the timer and calculate accurate offsets. |