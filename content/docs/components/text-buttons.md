---
title: Text Buttons
weight: 50
---

# Text Buttons

The **Text Buttons** component allows you to add pill-shaped, text-focused interactive elements to your notification. Unlike standard footer actions (which are icon-heavy), Text Buttons are designed for clear calls to action like "Reply," "Accept," or "View."



## Usage

You can add Text Buttons using the `setTextButtons` method on the Builder. This method accepts a variable number of `HyperAction` objects, which the library automatically converts into the internal `TextButtonInfo` model.

### Basic Text Button

```kotlin
// 1. Define the Action
val replyAction = HyperAction(
    id = "reply_action", // Unique ID
    title = "Reply",
    pendingIntent = replyPendingIntent
)

// 2. Add to Builder
builder.setTextButtons(replyAction)
```
### Multiple Buttons

You can chain multiple actions. The system usually displays them in a horizontal row, adjusting the width automatically to fit the content.

```kotlin
builder.setTextButtons(
    HyperAction("accept", "Accept", acceptIntent),
    HyperAction("decline", "Decline", declineIntent)
)
```
## Customization

The underlying `TextButtonInfo` model supports extensive color customization for both light and dark modes.

While the standard `setTextButtons(HyperAction...)` method applies system defaults, the data model allows for:

* **Background Color:** Define distinct colors for the button pill (`actionBgColor`, `actionBgColorDark`).
* **Text Color:** Define the color of the label (`actionTitleColor`, `actionTitleColorDark`).
* **Icons:** Optionally add an icon alongside the text (`actionIcon`).

## Differences from Standard Actions

| Feature | Text Buttons (`setTextButtons`) | Standard Actions (`addAction`) |
| :--- | :--- | :--- |
| **Appearance** | Pill-shaped, text-dominant (e.g., "Reply") | Icon-based or small text (standard Android style) |
| **Location** | **Below the content** (Distinct row at the bottom) | **Inside the Template** (Integrated into `BaseInfo` / `ChatInfo`) |
| **Use Case** | Primary decisions or suggestions (Accept/Reject) | Quick toggles or media controls (Play/Pause) |
| **Config** | Uses `TextButtonInfo` internally | Uses `ButtonInfo` internally |

## Advanced: Custom Colors

Currently, the `setTextButtons(vararg HyperAction)` helper uses system default styling (usually blue/gray pills). 
