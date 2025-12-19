---
title: Getting Started
weight: 1
---

Learn how to integrate the **HyperIsland ToolKit** into your Android project to create rich, dynamic notifications for Xiaomi HyperOS devices.

## Requirements

Before you begin, ensure your environment meets these criteria:

* **Device:** Xiaomi, POCO, or Redmi device running **HyperOS 3+**.
* **Permission:** The app needs the **"Show in status bar"** permission enabled in system settings.
* **Min SDK:** Android 7.0 (API 24) or higher.

## Installation

Add the dependency to your module-level `build.gradle.kts` file:

```kotlin
dependencies {
    implementation("io.github.d4viddf:hyperisland_kit:0.4.1")
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
## Checking Support

Since this library relies on specific system features present only in Xiaomi HyperOS (and some MIUI 14 versions), you should always verify device support before attempting to build a notification.

The `isSupported()` method checks for:
1.  **Manufacturer:** Is it a Xiaomi/Redmi/POCO device?
2.  **System Feature:** Does `persist.sys.feature.island` exist?
3.  **Permissions:** Has the user granted the necessary status bar permissions?

```kotlin
if (HyperIslandNotification.isSupported(context)) {
    // Device is supported: Build and show HyperIsland notification
    showHyperNotification()
} else {
    // Not supported: Fallback to standard Android notification
    showStandardNotification()
}
```

## Next Steps

Now that you have the basics running, explore the full capabilities of the toolkit:

* **[Templates](/docs/components/):** Learn about the different layouts like `ChatInfo` (messaging), `CoverInfo` (media), and `HighlightInfo` (status).
* **[Dynamic Island](/docs/components/island/configuration/):** Master the island behavior, including "Big Island" expansions, timers, and animations.
* **[Actions](/docs/components/actions/):** Add interactive buttons, progress rings, and text capsules to your notification.