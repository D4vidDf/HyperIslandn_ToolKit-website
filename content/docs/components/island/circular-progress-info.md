---
title: Circular Progress Info
weight: 14
---

The `CircularProgressInfo` helper model defines the appearance of ring-shaped progress indicators used within the Dynamic Island (both Small and Big areas). It controls the current value, colors, and direction of the progress fill.

## Usage

```kotlin
val progressRing = CircularProgressInfo(
    progress = 75,              // 75% complete
    colorReach = "#34C759",     // Green filled part
    colorUnReach = "#333333",   // Dark grey background track
    isCCW = false               // Clockwise direction
)
```
## Data Model (`CircularProgressInfo`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `progress` | `Int` | **Required.** The current progress value (0-100). |
| `colorReach` | `String?` | Hex color string for the **filled** portion of the ring (the "reached" progress). |
| `colorUnReach` | `String?` | Hex color string for the **unfilled** background track (the "unreached" part). |
| `isCCW` | `Boolean` | Direction of the fill.<br>`false`: **Clockwise** (Default).<br>`true`: **Counter-Clockwise**. |