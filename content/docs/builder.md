---
title: The Builder
weight: 2
---

The `HyperIslandNotification.Builder` is the core entry point of the library. It is responsible for assembling your templates, components, and data into a final `Notification` object that can be posted to the Android system.

## 1. Initialization

The builder requires a Context and a Notification Channel ID.

```kotlin
// Basic Init
val builder = HyperIslandNotification.Builder(
    context, 
    "channel_id",   // Android Notification Channel ID
    "Channel Name"  // Human-readable Channel Name
)
```
## Setting the Template

Every notification **must** have exactly one template set. The template determines the physical layout of the notification card in the system shade (e.g., standard text, messaging style, upload progress).

Call **one** of the following methods on the builder. If you call multiple, the last one wins.

### Available Template Methods

| Method | Data Model | Description |
| :--- | :--- | :--- |
| `setBaseInfo(...)` | `BaseInfo` | **Standard.** The most common layout. Title, content, and optional large image. |
| `setChatInfo(...)` | `ChatInfo` | **Messaging.** Displays an avatar and message content, optimized for chat apps. |
| `setCoverInfo(...)` | `DriverInfo` | **Navigation/Taxi.** Specialized layout for ride-sharing or delivery updates. |
| `setUploadInfo(...)` | `UploadInfo` | **Progress.** Focused on file operations (upload/download) with status details. |

### Code Example

```kotlin
val builder = HyperIslandNotification.Builder(context, "channel_id", "My Channel")

// Option 1: Standard Layout
builder.setBaseInfo(
    BaseInfo(
        title = "System Update",
        content = "Download complete"
    )
)

// Option 2: Chat Layout (Do not use both)
/*
builder.setChatInfo(
    ChatInfo(
        chatTitle = "Alice",
        chatContent = "Hey, are we still on for lunch?",
        chatIcon = "alice_avatar_key"
    )
)
*/