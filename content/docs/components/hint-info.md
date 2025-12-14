---
title: Hint Info
weight: 4
---

`HintInfo` is a specific component that renders as a **small capsule** at the very top of the notification card. It is typically used for high-value information that needs to be separated from the main content, such as **Pickup Codes**, **Order Status**, or **Quick Actions**.

## Usage

There are three helper methods to set the Hint Info:

### 1. Simple Hint (Title + Action)
Displays a title and a clickable text button.

```kotlin
// Define the action (Hidden, so it doesn't appear at the bottom)
builder.addHiddenAction(myAction)

builder.setHintInfo(
    title = "Pickup Code: 4829",
    actionKey = "my_action_key"
)
```

### Hint with Description
Displays a title, a subtitle (content), and an action. This uses `type = 1`.

```kotlin
builder.setHintAction(
    title = "Order Ready",
    content = "Cainiao Station",
    action = myAction
)
```

### Hint with Timer

Displays a split layout, often used for live status updates like active calls or recordings.
* **Left Side:** Timer or "Front Text" (emphasized).
* **Right Side:** Main Title and Subtitle.

This uses `type = 2`.

```kotlin
builder.setHintTimer(
    frontText1 = "00:00",      // Maps to 'content' (Timer fallback)
    frontText2 = "Duration",   // Maps to 'subContent'
    mainText1 = "Recording",   // Maps to 'title'
    mainText2 = "Voice Memo",  // Maps to 'subTitle'
    timer = myTimerInfo,       // Live timer object
    action = myAction          // Right-side button
)
```
## Content Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `type` | `Int` | **Required.** <br>`1` = Action Layout (Title + Action).<br>`2` = Timer Layout (Split Text/Timer). |
| `title` | `String?` | **Type 1:** Main label.<br>**Type 2:** Right-side main text. |
| `content` | `String?` | **Type 1:** Auxiliary text.<br>**Type 2:** Left-side front text (or Timer fallback). |
| `subTitle` | `String?` | **Type 2 Only:** Right-side secondary text. |
| `subContent` | `String?` | **Type 2 Only:** Left-side secondary text. |
| `timerInfo` | `TimerInfo?` | **Type 2 Only:** A timer object to replace the `content` text with a live counter. |
| `actionInfo` | `HyperActionRef?` | The button reference to display on the right side. |