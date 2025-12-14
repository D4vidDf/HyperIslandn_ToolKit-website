---
title: Chat Info
weight: 2
---

`ChatInfo` is a specialized template component designed for messaging scenarios. Unlike `BaseInfo`, which is generic, `ChatInfo` optimizes the layout for conversation updates, focusing on the sender's avatar (profile picture) and the message body.

It is typically used in conjunction with the **Dynamic Island** to show the sender's avatar when the notification is expanded.

## Usage

```kotlin
builder.setChatInfo(
    title = "John Doe",
    content = "Hey, are we still meeting for lunch?",
    pictureKey = "avatar_john",
    
    // Optional: Badge the avatar with an app icon
    appPkg = "com.whatsapp",
    
    // Custom Colors
    titleColor = "#000000",
    contentColor = "#666666"
)

```

## Content Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `title` | `String` | **Required.** The sender's name or group title. |
| `content` | `String?` | The message body text. <br>*(Note: Mutually exclusive with `timer`. If a timer is provided, content is ignored).* |
| `pictureKey` | `String?` | Key of the `HyperPicture` to use as the user avatar. |
| `pictureKeyDark` | `String?` | Optional different avatar image for Dark Mode. |
| `appPkg` | `String?` | Package name of an app (e.g., `com.whatsapp`). If provided, the system may overlay the app's small icon on the avatar. |

## Timer Configuration

You can replace the text `content` with a live timer (useful for "Call in progress" or "Voice recording").

```kotlin
// Example: Timer counting UP from a specific start time
val timer = TimerInfo(
    type = 1, // 1 = Count Up
    baseTime = System.currentTimeMillis()
)

builder.setChatInfo(
    title = "Voice Call",
    timer = timer,
    pictureKey = "caller_avatar"
)
```
## Color Customization

Like `BaseInfo`, you can customize the text colors for both Light and Dark modes.

| Text Field | Light Mode Parameter | Dark Mode Parameter |
| :--- | :--- | :--- |
| **Sender Name** | `titleColor` | `titleColorDark` |
| **Message** | `contentColor` | `contentColorDark` |

## Actions

The `setChatInfo` method accepts an optional `actionKeys` list. These actions appear as standard buttons at the bottom of the card.

```kotlin
actionKeys = listOf("reply", "mark_read")