---
title: The Builder
weight: 2
---

The `HyperIslandNotification` class is the engine of the library. It collects your templates, components, and media, and serializes them into the specific formats (JSON and Bundles) required by the HyperOS/MIUI system.


## 1. Initialization & Support Check

Before attempting to build a notification, you should always check if the device supports the Dynamic Island features to prevent errors or unexpected behavior.

```kotlin
// 1. Check Support
if (!HyperIslandNotification.isSupported(context)) {
    // Fallback to standard Android notification
    return
}

// 2. Initialize Builder
val builder = HyperIslandNotification.Builder(
    context, 
    "business_id",   // Unique Business/Channel ID
    "Ticker Text"    // Ticker text
)
```
## Registering Resources

The HyperIsland architecture separates your data into two parts:
1.  **JSON Payload:** Describes the layout, text, and structure.
2.  **Resource Bundle:** Holds heavy objects like `Bitmap`, `Icon`, and `PendingIntent`.

To link them, you must **register** your resources with the Builder using a unique **String Key**. You then use this key in your templates to tell the system which resource to display.

### 1. Registering Images (`addPicture`)

All images—whether they are local drawables or downloaded bitmaps—must be wrapped in a `HyperPicture` object and added to the builder.

```kotlin
// 1. Create the object
val myIcon = HyperPicture(
    key = "icon_profile",            // Unique ID
    context = context, 
    drawableRes = R.drawable.avatar
)

// 2. Register it
builder.addPicture(myIcon)

// 3. Use the key in a template
builder.setBaseInfo(
    title = "New Message",
    pictureKey = "icon_profile"      // <--- Matches the key above
)
```
### 2. Registering Actions

Actions (buttons) carry `PendingIntent`s, which cannot be serialized into JSON. Therefore, they must also be registered with the builder so the system can link your clicks to the correct intents.

There are two methods for adding actions, depending on where you want them to appear:

#### A. Visible Actions (`addAction`)
Adds the button to the standard **Footer** action bar at the bottom of the notification card.

```kotlin
val replyAction = HyperAction(
    key = "btn_reply",
    title = "Reply",
    pendingIntent = replyIntent,
    actionIntentType = 1
)

// Appears in the bottom row of the notification
builder.addAction(replyAction)
```
#### B. Hidden Actions (`addHiddenAction`)

Registers the action so it functions and is available to the system, but **does not** display it in the standard notification footer.

This is essential for components that need interactivity but shouldn't clutter the main action bar, such as:
* **Dynamic Island Clicks:** Making the Island itself (or parts of it) clickable.
* **Text Buttons:** Using `setTextButtons`, which are separate from the footer but reference actions by key.
* **Hint Capsules:** Adding a click action to the top `HintInfo` capsule.

```kotlin
// 1. Define the action
val openAppAction = HyperAction(
    key = "open_app_internal",
    title = "Open",
    pendingIntent = appIntent, // The intent to fire
    actionIntentType = 1
)

// 2. Register it as hidden
// It will NOT appear in the bottom row
builder.addHiddenAction(openAppAction)

// 3. Reference it in a component (e.g., the Big Island)
builder.setBigIslandCountdown(
    countdownTime = 50000,
    pictureKey = "timer_icon",
    actionKeys = listOf("open_app_internal") // <--- Uses the key registered above
)
```
## Setting the Template

You must set **one** primary template to define the structure of the notification card (the view in the notification shade). Call **one** of the following methods on the builder.

| Method | Data Model | Description |
| :--- | :--- | :--- |
| `setBaseInfo` | `BaseInfo` | **Standard.** The most common layout. Title, content, and optional images. |
| `setChatInfo` | `ChatInfo` | **Messaging.** Displays an avatar and message content, optimized for chat apps. |
| `setCoverInfo` | `CoverInfo` | **Media.** A layout dominated by a large cover image (e.g., Album Art). |
| `setHighlightInfo` | `HighlightInfo` | **Status.** A layout for high-priority status updates (e.g., "Charging"). |
| `setHighlightInfoV3` | `HighlightInfoV3` | **Status V3.** Alternative status layout with support for an action button. |
| `setAnimTextInfo` | `AnimTextInfo` | **Animated.** Uses system-provided animated icons (e.g., Ringing, Battery). |

### Code Example

```kotlin
// Example: Setting a Media Template
builder.setCoverInfo(
    picKey = "album_art_key", // Must be registered via addPicture()
    title = "Song Title",
    content = "Artist Name",
    subContent = "Album Name"
)
```
## Configuring the Island

The builder provides a suite of helper methods to configure both the **Behavior** (priority, timeout) and the **Content** (Small/Big layouts) of the Dynamic Island.

### Behavior Configuration (`setIslandConfig`)

Use this method to define how the island interacts with the system—whether it pops up, how long it stays, and if it auto-dismisses.

```kotlin
builder.setIslandConfig(
    priority = 2,           // 2 = High (Popup), 0-1 = Low (Background)
    timeout = 5000,         // Auto-minimize after 5000ms (null = forever)
    dismissible = false,    // Can the user swipe it away?
    needCloseAnimation = true
)
```
## 5. Building & Posting

Unlike standard notification builders, `HyperIslandNotification` **does not** create the final `Notification` object itself. Instead, it acts as a "Data Generator" that produces the specific payloads required by HyperOS.

You must generate these payloads and attach them to a standard Android Notification.

### Step 1: Generate the Payloads
Call the build methods to get the JSON configuration and the Resource Bundle (images/intents).

```kotlin
// 1. Get the JSON configuration (Layouts, Text, Colors)
val jsonPayload: String = builder.buildJsonParam()

// 2. Get the Resource Bundle (Bitmaps, PendingIntents)
val resourcesBundle: Bundle = builder.buildResourceBundle()
```
### Step 2: Create a Standard Notification
Use Android's native `Notification.Builder` (or `NotificationCompat.Builder`) to create the container notification.

This notification serves two purposes:
1.  **Transport:** It carries the HyperOS payloads to the system.
2.  **Fallback:** It is displayed on devices that do not support HyperIsland (e.g., non-Xiaomi phones or older versions).

```kotlin
val notificationBuilder = Notification.Builder(context, "your_channel_id")
    .setSmallIcon(R.drawable.ic_notification) // Required standard icon
    .setContentTitle("Fallback Title")        // Shown if HyperIsland fails
    .setContentText("Fallback Content")
    .setAutoCancel(true)
```
### Step 3: Attach the Extras
This is the bridge between standard Android and HyperOS. You must insert the generated data into the notification's extras using specific keys that the system looks for.



1.  **JSON Payload:** Stored under the key `"miui.focus.param"`.
2.  **Resource Bundle:** Merged directly into the extras using `putAll()`.

```kotlin
val extras = Bundle()

// A. Attach the JSON Layout
extras.putString("miui.focus.param", jsonPayload)

// B. Attach the Resources (Images & Actions)
// This merges the "miui.focus.pics" and "miui.focus.actions" bundles
extras.putAll(resourcesBundle)

// C. Set the extras on the builder
notificationBuilder.setExtras(extras)
```
### Step 4: Notify
Finally, post the notification using the standard system service. The Android system will detect the special extras you added and render the HyperIsland notification instead of the standard layout (on supported devices).

```kotlin
val notificationManager = context.getSystemService(NotificationManager::class.java)

// Post it (ID can be any integer)
notificationManager.notify(1001, notificationBuilder.build())
```
### Full Example Snippet

Here is a complete function showing the entire lifecycle from initialization to posting.

```kotlin
fun postNotification(context: Context) {
    val channelId = "hyper_channel"
    val notificationId = 1001

    // 1. Setup HyperIsland Builder
    val hyperBuilder = HyperIslandNotification.Builder(context, "demo_id", "Ticker Text")
        // Template
        .setBaseInfo(title = "Download", content = "Finished successfully")
        
        // Register Resources
        .addPicture(HyperPicture("icon_check", context, R.drawable.ic_check))
        
        // Configure Island (Optional)
        .setSmallIslandIcon("icon_check")
        .setIslandConfig(priority = 2) // Popup

    // 2. Generate Data Payloads
    val jsonPayload = hyperBuilder.buildJsonParam()
    val resBundle = hyperBuilder.buildResourceBundle()

    // 3. Create Standard Android Notification
    val notifBuilder = Notification.Builder(context, channelId)
        .setSmallIcon(R.drawable.ic_launcher)
        .setContentTitle("Download Finished") // Fallback
        .setContentText("Check app for details")
        .setAutoCancel(true)

    // 4. Attach HyperOS Extras
    val extras = Bundle()
    extras.putString("miui.focus.param", jsonPayload) // JSON
    extras.putAll(resBundle)                          // Resources
    notifBuilder.setExtras(extras)

    // 5. Post to System
    val notificationManager = context.getSystemService(NotificationManager::class.java)
    notificationManager.notify(notificationId, notifBuilder.build())
}
```
## API Summary

### General Configuration

| Method | Parameters | Description |
| :--- | :--- | :--- |
| `setLogEnabled` | `enabled: Boolean` | Enables debug logging for the generated JSON payload. Default is `true`. |
| `setTimeout` | `durationMs: Long` | Sets the duration before the notification auto-cancels. |
| `setEnableFloat` | `enable: Boolean` | Enables or disables the "Heads Up" (floating) behavior. Default is `true`. |
| `setShowNotification` | `show: Boolean` | Controls if the notification is shown. Default is `true`. |
| `setScene` | `sceneName: String` | Sets a specific scene identifier for system analytics/theming. |
| `setShareData` | `title`, `content`, `picKey`, `shareContent`, `sharePicKey` | Configures the data used if the user shares the notification. |

### Component Setters

| Method | Parameters | Description |
| :--- | :--- | :--- |
| `setTextButtons` | `vararg HyperAction` | Adds pill-shaped text buttons (distinct from footer actions). Often used with `BaseInfo`. |
| `setProgressBar` | `progress`, `color`, `images...` | Adds a linear progress bar with optional start/end icons. |
| `setMultiProgress` | `title`, `progress`, `color`, `points` | Adds a segmented progress bar (up to 4 segments). |
| `setStepProgress` | `current`, `total`, `color` | Adds a step counter (e.g., "Step 1 of 4"). |
| `setHintInfo` | `title`, `actionKey` | Adds a top capsule hint with an optional click action. |
| `setHintTimer` | `frontText`, `mainText`, `timer`, `action` | Adds a top capsule hint containing a live timer. |
| `setBackground` | `picKey`, `color`, `type` | Sets a custom background image or solid color for the entire card. |
| `setBannerIcon` | `type`, `picKey` | Adds a banner-style image (alias for `setPicInfo`). |