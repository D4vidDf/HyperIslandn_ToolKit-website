---
title: Highlight Info
weight: 3
---

`HighlightInfo` is designed for high-priority, ongoing tasks that need to stand out. It is ideal for **Timers**, **Stopwatches**, **Recordings**, or status updates that require emphasis.

There are two distinct versions:
1.  **Standard (V1):** Best for timers and simple status (Icon + Title + Timer/Text).
2.  **Version 3 (V3):** Best for labeled data (e.g., "Price", "Status") with an integrated action button.

---

## 1. Highlight Info (Standard)

This is the default layout used for ongoing activities.

### Usage

```kotlin
val timer = TimerInfo(type = 1, baseTime = System.currentTimeMillis())

builder.setHighlightInfo(
    title = "Recording",
    content = "Voice Note 1",
    subContent = "00:00",
    picKey = "ic_mic",
    timer = timer
)
```
## Content Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `title` | `String` | **Required.** The main emphasized text (e.g., "Timer", "Recording"). |
| `content` | `String?` | Auxiliary text 1 (often used for description). |
| `subContent` | `String?` | Auxiliary text 2 (often used for static time or status). |
| `picFunction` | `String?` | Key of the `HyperPicture` to display as the icon. |
| `type` | `Int?` | Configuration flag. Set to `1` to **hide** `content` (Aux Text 1). |
| `timer` | `TimerInfo?` | Configuration for a live ticking timer. |

## Color Customization

Full support for Light and Dark mode colors.

| Field | Light Mode | Dark Mode |
| :--- | :--- | :--- |
| **Title** | `colorTitle` | `colorTitleDark` |
| **Content** | `colorContent` | `colorContentDark` |
| **Sub Content** | `colorSubContent` | `colorSubContentDark` |

---

## Highlight Info V3

This version (Template 20) is layout-focused, featuring a "Primary" text (often large), a "Secondary" text, and a distinct **Highlight Label** (pill-shaped tag). It also supports an integrated round action button.

### Usage

```kotlin
builder.setHighlightInfoV3(
    primaryText = "$24.00",
    secondaryText = "Total",
    label = "Paid",
    
    // Strikethrough style for secondary text?
    // showSecondaryLine = true, 
    
    // Custom Colors
    primaryColor = "#000000",
    
    // Integrated Action
    action = myAction
)
```
### Content Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `primaryText` | `String` | **Required.** The main text (e.g., Price, Score). |
| `secondaryText` | `String?` | Supplement text. |
| `highLightText` | `String?` | Text for the highlighted label (pill). |
| `showSecondaryLine`| `Boolean?` | If `true`, adds a strikethrough line to the `secondaryText`. |
| `actionInfo` | `HyperActionRef?` | An action button reference to display within the layout. |

### Color Customization

V3 allows specific coloring for the highlight label background and text.

| Field | Light Mode | Dark Mode |
| :--- | :--- | :--- |
| **Primary Text** | `primaryColor` | `primaryColorDark` |
| **Secondary Text** | `secondaryColor` | `secondaryColorDark` |
| **Label Text** | `highLightTextColor` | `highLightTextColorDark` |
| **Label Background**| `highLightBgColor` | `highLightBgColorDark` |