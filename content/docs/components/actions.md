---
title: Actions
weight: 10
---

Actions are the interactive elements of your notification. HyperIsland supports versatile button types, ranging from simple icons to text capsules and download progress rings.

All actions are defined using the `HyperAction` class and added to the builder.

---

## 1. Handling Actions (Intents)

To make a button functional, you must bind it to a `PendingIntent`. This tells the Android system what to do when the user taps the button.

### Action Types (`actionIntentType`)

You must specify the type of component the intent targets:

| Type | Value | Description |
| :--- | :--- | :--- |
| **Activity** | `1` | Opens an Activity (UI). Used for "Open Chat" or "View Details". |
| **Broadcast** | `2` | Sends a Broadcast. Best for background tasks like "Play/Pause" or "Mark Read" without opening the app. |
| **Service** | `3` | Starts a Service. |

### Example: Creating a Broadcast Action

This is the most common pattern for notification buttons (e.g., "Next Song").

```kotlin
// 1. Create the Intent
val intent = Intent(context, MyReceiver::class.java).apply {
    action = "ACTION_NEXT_SONG"
}

// 2. Wrap in PendingIntent
val pendingIntent = PendingIntent.getBroadcast(
    context, 
    0, 
    intent, 
    PendingIntent.FLAG_UPDATE_CURRENT or PendingIntent.FLAG_IMMUTABLE
)

// 3. Create HyperAction
val action = HyperAction(
    key = "next",
    title = "Next",
    context = context,
    drawableRes = R.drawable.ic_next,
    pendingIntent = pendingIntent,
    actionIntentType = 2 // 2 = Broadcast
)
```

## 2. Icon Buttons

Standard circular buttons containing an icon. These are typically used for primary controls like "Call" or media controls.

{{< callout type="warning" >}}
**Important: Icon Design**
The system displays the icon **exactly as provided**. It does **not** automatically add a circular background color behind your icon.

If you want a "Green Circle with a White Phone" button, you must provide a drawable that **already contains the green circle**. If you provide a transparent icon, it will appear transparent.
{{< /callout >}}

### Usage (Resource Icon)

```kotlin
val action = HyperAction(
    key = "call",
    title = "Call",
    context = context,
    drawableRes = R.drawable.btn_call_green_circle, // Image includes the green background
    pendingIntent = callIntent,
    actionIntentType = 1
)
builder.addAction(action)

```
### Usage (Bitmap Icon)
```Kotlin

val action = HyperAction(
    key = "profile",
    title = "Profile",
    bitmap = myBitmap,
    pendingIntent = profileIntent,
    actionIntentType = 1
)
builder.addAction(action)
```

## 3. Text Buttons

Pill-shaped buttons that display text. Unlike icon buttons, you **can** configure the background color and text color directly via code.

```kotlin
val action = HyperAction(
    key = "reply",
    title = "Reply",
    pendingIntent = replyIntent,
    actionIntentType = 1,

    // Custom Colors
    bgColor = "#007AFF",      // Blue Background
    titleColor = "#FFFFFF",   // White Text

    // Dark Mode Variants
    bgColorDark = "#0A84FF",
    titleColorDark = "#E5E5E5"
)
builder.addAction(action)
```

## 4. Progress Buttons

A special button type that displays a circular loading ring around the icon. Useful for "Stop Download" or "Syncing" states.

```kotlin
val action = HyperAction(
    key = "stop_download",
    title = "Stop",
    context = context,
    drawableRes = R.drawable.ic_stop,
    pendingIntent = stopIntent,
    actionIntentType = 2,
    
    // Enable Progress Mode
    isProgressButton = true,
    progress = 45,        // 45%
    colorReach = "#34C759", // Color of the ring
    isCCW = false         // false = Clockwise, true = Counter-Clockwise
)
builder.addAction(action)
```

## API Reference: `HyperAction`

### Common Fields
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `key` | `String` | **Required.** Unique ID. Used for binding to layouts. |
| `title` | `CharSequence?` | Label text (Visible on Text Buttons, Accessibility for Icons). |
| `pendingIntent` | `PendingIntent` | The intent to fire on click. |
| `actionIntentType` | `Int` | `1`=Activity, `2`=Broadcast, `3`=Service. |

### Text Button Styling
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `actionBgColor` | `String?` | Hex color for the button background. |
| `titleColor` | `String?` | Hex color for the text label. |
| `actionBgColorDark` | `String?` | Dark mode background. |
| `titleColorDark` | `String?` | Dark mode text color. |

### Progress Button Styling
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `isProgressButton` | `Boolean` | Set to `true` to enable the ring. |
| `progress` | `Int` | Current progress value (0-100). |
| `colorReach` | `String?` | Color of the active progress ring. |
| `progressColor` | `String?` | (Optional) Alternative color param depending on system version. |
| `isCCW` | `Boolean` | If `true`, ring fills Counter-Clockwise. |