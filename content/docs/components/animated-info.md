---
title: Animated Info
weight: 5
---

These components are designed to display an **Animated Icon** paired with text. They are commonly used for dynamic status indicators like "Charging", "Loading", or "Processing".

There are two variations:
1.  **AnimTextInfo:** Supports a Timer.
2.  **IconTextInfo:** Supports an additional text line (Sub-content).

---

## 1. Anim Text Info

This component pairs an animation with a title and either a description or a live timer.

### Usage

```kotlin
// Define the animation source
val animConfig = AnimIconInfo(
    src = "voiceWaveBig", // System Lottie Key
    loop = true
)

// Example with Timer
builder.setAnimTextInfo(
    animIconInfo = animConfig,
    title = "Recording",
    timerInfo = myTimer // Replaces 'content'
)
```
### Data Model (`AnimTextInfo`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `animIconInfo` | `AnimIconInfo` | **Required.** Configuration for the animation (Source, loop, etc). |
| `title` | `String` | **Required.** Main text label. |
| `content` | `String?` | Auxiliary text. |
| `timerInfo` | `TimerInfo?` | Optional live timer. If set, it may replace or complement `content`. |

### Color Customization

| Field | Light Mode | Dark Mode |
| :--- | :--- | :--- |
| **Title** | `colorTitle` | `colorTitleDark` |
| **Content** | `colorContent` | `colorContentDark` |

---
## 2. Icon Text Info

This component is similar to `AnimTextInfo` but focuses purely on text depth, offering three levels of text: Title, Content, and Sub-Content.

### Usage

```kotlin
builder.setIconTextInfo(
    animIconInfo = animConfig,
    title = "System Update",
    content = "Installing...",
    subContent = "Do not turn off device"
)
```
### Data Model (`IconTextInfo`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `animIconInfo` | `AnimIconInfo` | **Required.** Configuration for the animation source. |
| `title` | `String` | **Required.** Main text label. |
| `content` | `String?` | Secondary text. |
| `subContent` | `String?` | Tertiary text (e.g., footer or small detail). |

### Color Customization

| Field | Light Mode | Dark Mode |
| :--- | :--- | :--- |
| **Title** | `colorTitle` | `colorTitleDark` |
| **Content** | `colorContent` | `colorContentDark` |

## Shared Configuration: `AnimIconInfo`

Both components use this model to define the animation resource.

{{< callout type="warning" >}}
**Format Restriction**
Currently, HyperOS **only supports internal Xiaomi system Lottie files** (e.g., system resources).
* **GIFs are NOT supported.**
* Custom Lottie JSON files are not supported in this version.
{{< /callout >}}

```kotlin
data class AnimIconInfo(
    val type: Int = 0,           // 0 = Default
    val src: String,             // Key for Xiaomi System Lottie
    val srcDark: String? = null, // Optional key for Dark Mode
    val loop: Boolean = true,    // Should it loop?
    val autoplay: Boolean = true // Should it start automatically?
)
```
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `src` | `String` | **Required.** The key string for a **Xiaomi system Lottie** resource (e.g., `"voiceWaveSmall"`). |
| `srcDark` | `String?` | Optional alternative resource key for dark mode. |
| `loop` | `Boolean` | If `true`, the animation repeats indefinitely. |
| `autoplay` | `Boolean` | If `true`, the animation starts immediately upon rendering. |