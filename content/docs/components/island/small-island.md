---
title: Small Island
weight: 3
---

The `SmallIslandArea` defines the content of the Dynamic Island when it is in its **minimized** (capsule) state. This is the default state visible in the status bar before the user interacts with it or when a high-priority update arrives.

It primarily supports displaying a small icon or an icon combined with a progress ring.

## Usage

```kotlin
// Example 1: Simple Icon
val simpleSmall = SmallIslandArea(
    picInfo = PicInfo(pic = "icon_key")
)

// Example 2: Icon with Progress Ring
val progressSmall = SmallIslandArea(
    combinePicInfo = CombinePicInfo(
        picInfo = PicInfo(pic = "icon_download"),
        progressInfo = CircularProgressInfo(progress = 45)
    )
)

builder.setParamIsland(
    smallIslandArea = progressSmall,
    // ... other config
)
```
## Data Model (`SmallIslandArea`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `picInfo` | `PicInfo?` | A standalone icon. Use this for static states (e.g., "Muted", "Connected"). |
| `combinePicInfo` | `CombinePicInfo?` | A complex icon wrapper that includes a circular progress ring. Use this for "Loading", "Timer", or "Download" states. |

---

## Sub-Component: `CombinePicInfo`

This helper model allows you to wrap a standard picture with a progress indicator, commonly seen during downloads or active timers in the minimized state.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `picInfo` | `PicInfo` | **Required.** The center icon. |
| `progressInfo` | `CircularProgressInfo` | **Required.** Configuration for the surrounding progress ring (value, color, max). |