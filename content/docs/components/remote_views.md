---
title: Custom Views (RemoteViews)
weight: 90
---

Version **0.4.3** introduces **Custom Mode** (DIY), allowing you to completely bypass the standard templates and render your own Android `RemoteViews` within the Notification Renderer, you can still specify your own IslandParams.

This is useful when the standard layouts (Chat, Media, etc.) do not fit your specific design requirements.

## Usage

To use Custom Views, you must use the `setCustomRemoteView` method.

{{< callout type="warning" >}}
**Important:** Switching to Custom Mode changes how you build the notification.
You must use **`buildCustomExtras()`** instead of `buildJsonParam()` + `buildResourceBundle()`.
{{< /callout >}}

### Basic Example

```kotlin
// 1. Create your RemoteViews
val myLayout = RemoteViews(context.packageName, R.layout.my_custom_notification)
myLayout.setTextViewText(R.id.tv_title, "My Custom Title")

// 2. Initialize Builder
val builder = HyperIslandNotification.Builder(context, "custom_id", "Ticker Text")

// 3. Set the Custom View
builder.setCustomRemoteView(myLayout)

// 4. Set Ticker Icon (Required for Custom Mode)
builder.setTickerIcon(Icon.createWithResource(context, R.drawable.ic_notification))

// 5. Build & Notify
val notification = Notification.Builder(context, channelId)
    .setSmallIcon(R.drawable.ic_notification)
    .setExtras(builder.buildCustomExtras()) // <--- Use this single method
    .build()

notificationManager.notify(id, notification)
```
### Supported Customizations

In **Custom Mode**, you have granular control over every state of the notification system. You can provide distinct `RemoteViews` for Dark Mode, Always-On Display (AOD), and the Dynamic Island states.

| Method | Description |
| :--- | :--- |
| **Standard Views** | |
| `setCustomRemoteView` | **Required.** The main notification banner layout (Light Mode). |
| `setCustomNightRemoteView` | The notification banner layout for **Dark Mode**. |
| **Always-On Display (AOD)** | |
| `setCustomAodRemoteView` | Custom layout displayed on the AOD screen. |
| **Dynamic Island (Small)** | |
| `setCustomTinyRemoteView` | Layout for the **Small Island** (Capsule state). |
| `setCustomTinyNightRemoteView` | Layout for the Small Island in **Dark Mode**. |
| **Dynamic Island (Expanded)** | |
| `setCustomIslandExpandRemoteView`| Layout for the **Expanded Island** (Long-press state). |
| **Decorations (Side Views)** | |
| `setCustomDecoLandRemoteView` | Decoration view for **Landscape** orientation. |
| `setCustomDecoLandNightRemoteView`| Decoration view for Landscape in **Dark Mode**. |
| `setCustomDecoPortRemoteView` | Decoration view for **Portrait** orientation. |
| `setCustomDecoPortNightRemoteView`| Decoration view for Portrait in **Dark Mode**. |

### Helper Configuration

Even in Custom Mode, you can still use some helper methods to configure behavior:

* **`setIslandConfig(...)`**: Controls priority, timeouts, and edge lighting.
* **`setBigIsland()`**: Configure the Island.
* **`setTickerIcon(...)`**: **Required.** The icon shown in the status bar.
* **`setAodConfig(...)`**: Helper to set a simple AOD title if you don't want to build a full RemoteView for it.