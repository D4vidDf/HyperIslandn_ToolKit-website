---
title: Getting Started
weight: 1
---

Learn how to integrate **HyperIsland ToolKit** into your project.

## Installation

Add the dependency to your `build.gradle.kts` (app module):

```kotlin
dependencies {
    implementation("io.github.d4viddf:hyperisland_kit:0.4.0")
}
```

## Basic Usage

To show a simple "Dynamic Island" notification, use the Builder pattern:

```kotlin
// 1. Create a Builder
val builder = HyperIslandNotification.Builder(context, "demo", "My Notification")
    .setSmallWindowTarget("com.example.app.MainActivity")

    // 2. Add Content
    .setBaseInfo(
        title = "Hello World",
        content = "This is a HyperOS notification",
        pictureKey = "my_icon"
    )

    // 3. Configure Island
    .setSmallIslandIcon("my_icon")

// 4. Build & Notify
val notification = NotificationCompat.Builder(context, CHANNEL_ID)
    .setSmallIcon(R.drawable.ic_notification)
    .addExtras(builder.buildResourceBundle()) // Essential assets
    .build()

// 5. Attach Payload
notification.extras.putString("miui.focus.param", builder.buildJsonParam())

notify(notificationId, notification)
```
## Requirements

* **Device:** Xiaomi/Poco/Redmi device running HyperOS.
* **Permission:** The user must grant "Status bar notification" permission.