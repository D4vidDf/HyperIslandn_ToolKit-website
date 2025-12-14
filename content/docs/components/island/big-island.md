---
title: Big Island
weight: 4
---
The `BigIslandArea` defines the content of the Dynamic Island when it is **expanded**. This view offers much more real estate and supports complex layouts like split views (Left/Right), progress bars, timers, and action buttons.


## Usage Overview

You do not need to populate every field. Instead, use the fields that correspond to the layout "blocks" you need.

```kotlin
val bigIsland = BigIslandArea(
    // Left Side: Icon + Text
    imageTextInfoLeft = ImageTextInfoLeft(
        picInfo = PicInfo(pic = "album_art"),
        textInfo = TextInfo(title = "Song Title")
    ),
    
    // Right Side: Waveform or Icon
    imageTextInfoRight = ImageTextInfoRight(
        picInfo = PicInfo(pic = "waveform_anim")
    ),
)
```
## Data Model (`BigIslandArea`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `imageTextInfoLeft` | `ImageTextInfoLeft?` | Configuration for the **Left** side of the island. |
| `imageTextInfoRight` | `ImageTextInfoRight?` | Configuration for the **Right** side of the island. |
| `sameWidthDigitInfo` | `SameWidthDigitInfo?` | A specialized block for **Timers** or monospaced digits. |
| `fixedWidthDigitInfo` | `FixedWidthDigitInfo?` | A simplified digit block (often for counters). |
| `progressTextInfo` | `ProgressTextInfo?` | A block combining text with a circular progress indicator. |
| `textInfo` | `TextInfo?` | Generic central text block. |
| `picInfo` | `PicInfo?` | Generic central image block. |
| `actions` | `List<SimpleActionRef>?` | A list of action keys to display as buttons at the bottom of the island. |

---

## Layout Blocks

### 1. Image Text Info (Left/Right)
These blocks control the two main "sides" of the expanded island.

**Left (`ImageTextInfoLeft`):**
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `type` | `Int` | Default `1`. Layout variant. |
| `picInfo` | `PicInfo?` | The icon/image. |
| `textInfo` | `TextInfo?` | The text label. |
| `progressInfo` | `CircularProgressInfo?`| Optional progress ring around the icon. |

**Right (`ImageTextInfoRight`):**
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `type` | `Int` | Default `2`. Layout variant. |
| `picInfo` | `PicInfo?` | The icon/image. |
| `textInfo` | `TextInfo?` | The text label. |

### 2. Digit Info (Timers & Counters)
Specialized blocks for displaying numbers that change frequently (like countdowns) to prevent jitter.

**`SameWidthDigitInfo` (Complex/Timer):**
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `digit` | `String?` | The numeric value to display. |
| `content` | `String?` | Label text. |
| `timerInfo` | `TimerInfo?` | Active timer configuration. |
| `showHighlightColor` | `Boolean` | Whether to apply the `highlightColor` (from ParamIsland) to these digits. |
| `turnAnim` | `Boolean` | Enable "odometer" style turning animation. |

**`FixedWidthDigitInfo` (Simple):**
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `digit` | `Int` | Integer value. |
| `content` | `String?` | Label text. |
| `showHighlightColor` | `Boolean` | Highlight tint. |
| `turnAnim` | `Boolean` | Animation toggle. |

### 3. Text Info
A shared wrapper used inside other blocks to define text content.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `title` | `String` | **Required.** Primary text. |
| `content` | `String?` | Secondary text. |
| `showHighlightColor`| `Boolean` | If `true`, the text uses the global highlight color. |
| `narrowFont` | `Boolean?` | If `true`, applies a condensed font style. |

### 4. Progress Text Info
Combines a circular progress indicator with text description.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `progressInfo` | `CircularProgressInfo` | **Required.** The ring configuration. |
| `textInfo` | `TextInfo?` | The accompanying label. |