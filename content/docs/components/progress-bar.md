---
title: Linear Progress
weight: 6
---

The Linear Progress Bar is used to visualize continuous status, such as **Downloads**, **Music Playback**, or **Delivery Tracking**. It uses the `ProgressInfo` data class.

It supports a "Moving Icon" (which slides along the bar) and a "Destination Icon" (fixed at the end).

## Usage

```kotlin
builder.setProgressBar(
    progress = 75,       // Current percentage (0-100)
    color = "#34C759",   // Color of the filled bar
    picForwardKey = "car_icon", // Icon moving with the progress
    picEndKey = "flag_icon"     // Icon at the end of the bar
)
```
## Parameters (`ProgressInfo`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `progress` | `Int` | **Required.** The current value (0 to 100). |
| `colorProgress` | `String?` | Hex color for the filled portion of the bar (Start/Main color). |
| `colorProgressEnd` | `String?` | Hex color for the end of the bar (if using a gradient). |
| `picForward` | `String?` | Key for the icon that sits on the leading edge (moves with progress). |
| `picMiddle` | `String?` | Key for an icon placed in the center of the bar (when active/passed). |
| `picMiddleUnselected`| `String?` | Key for the center icon when the progress has not yet reached the middle. |
| `picEnd` | `String?` | Key for the icon at the far right (100% mark) when active/reached. |
| `picEndUnselected`| `String?` | Key for the icon at the far right when the progress hasn't reached 100% yet. |

## Gradient Support

You can create a gradient effect on the progress bar by specifying both a start and an end color.

```kotlin
// Example: Gradient from Blue to Teal
builder.setProgressBar(
    progress = 50,
    color = "#007AFF",       // Start Color
    colorEnd = "#30B0C7"     // End Color (maps to colorProgressEnd)
)
```