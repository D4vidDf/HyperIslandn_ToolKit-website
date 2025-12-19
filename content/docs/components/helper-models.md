---
title: Helper Models
weight: 12
---

These are specialized data classes used within specific templates or advanced configurations.

## 1. Pic Info

`PicInfo` is a versatile wrapper used to define images or animations within components like **Highlight Info**. It allows you to specify whether a resource is a static image or an animation, and control its playback behavior.

### Data Model (`PicInfo`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `type` | `Int` | `1` = Static Image.<br>`2` = Animation (Lottie/GIF). |
| `pic` | `String` | **Required.** The resource key (e.g., `HyperPicture` key or system resource). |
| `loop` | `Boolean` | (Animation only) Whether to loop the animation. |
| `autoplay` | `Boolean` | (Animation only) Whether to auto-play on load. |
| `number` | `Int` | Optional integer value associated with the picture (e.g., for badge counts). |
| `contentDescription`| `String?` | Accessibility text for screen readers. |
| `effectColor` | `String?` | Optional tint color to apply to the image. |
| `effectSrc` | `String?` | Optional secondary resource for effects. |

---

## 2. Text Button Info (Component 18)

`TextButtonInfo` defines the layout for the **Text Button** component (internally known as Component 18). This is used to create a grid or list of text-based actions that look distinct from the standard bottom action bar.

### Data Model (`TextButtonInfo`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `actionTitle` | `String` | **Required.** The button text label. |
| `actionIcon` | `String?` | Key for an icon to display next to the text. |
| `actionIconDark` | `String?` | Key for the icon in Dark Mode. |
| `actionIntent` | `String?` | The Intent string or URI to execute when clicked. |
| `actionIntentType` | `Int` | `0` = Standard, `1` = Activity, etc. |

### Color Customization

| Field | Light Mode | Dark Mode |
| :--- | :--- | :--- |
| **Background** | `actionBgColor` | `actionBgColorDark` |
| **Text Color** | `actionTitleColor` | `actionTitleColorDark` |