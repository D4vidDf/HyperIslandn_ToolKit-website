---
weight: 1
---

# Island Configuration (ParamIsland)

The `ParamIsland` component acts as the control center for the Dynamic Island. It defines the notification's behavior (priority, timeout, ordering), display properties, and holds the data for the Expanded (`BigIslandArea`) and Minimized (`SmallIslandArea`) states.

## Usage

```kotlin
builder.setParamIsland(
    // Behavior
    islandPriority = 2,          // Default High Priority
    islandTimeout = 5,           // Auto-dismiss after 5s
    islandOrder = false,         // Queue behavior

    // Config Flags
    dismissIsland = false,       // Should it close immediately?
    maxSize = false,             // Force max expansion?
    needCloseAnimation = true,
    
    // Appearance
    highlightColor = "#FF5722",
    
    // Content Areas (Defined separately)
    bigIslandArea = myBigArea,
    smallIslandArea = mySmallArea,
    
    // Optional Share Config
    shareData = ShareData(
        title = "Song Name",
        content = "Artist",
        pic = "album_art_key",
        shareContent = "Check out this song!"
    )
)
```
## Parameters (`ParamIsland`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `islandProperty` | `Int` | General display property. Default is `1`. |
| `islandPriority` | `Int` | **Required.** Determines importance.<br>`2`: High (Popup). Default.<br>`0-1`: Lower priority/Background. |
| `islandTimeout` | `Int?` | Time in milliseconds before the island automatically minimizes or dismisses. |
| `islandOrder` | `Boolean` | Controls queue ordering. `false` (default) typically implies standard First-In-First-Out behavior. |
| `dismissIsland` | `Boolean` | If `true`, this update command will force the existing island to close immediately. |
| `maxSize` | `Boolean` | If `true`, forces the island to use the maximum available layout size. |
| `needCloseAnimation`| `Boolean` | Whether to play the shrink/fade animation when closing. Default `true`. |
| `expandedTime` | `Int?` | Specific duration (ms) to stay in the **Expanded** state before minimizing. |
| `highlightColor` | `String?` | Hex color code for accenting specific UI elements within the island. |
| `bigIslandArea` | `BigIslandArea?`| Defines the layout and content for the **Expanded** state. |
| `smallIslandArea` | `SmallIslandArea?`| Defines the layout and content for the **Minimized** (capsule) state. |
| `shareData` | `ShareData?` | Configuration for system sharing functionality. |

## Share Data Configuration

If your notification includes a "Share" action, this object defines the content that gets passed to the Android system share sheet.

### Data Model (`ShareData`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `title` | `String` | **Required.** The title of the content being shared. |
| `content` | `String` | **Required.** The main text body or description. |
| `pic` | `String` | **Required.** Key for the main image thumbnail. |
| `shareContent` | `String` | **Required.** The actual text/link payload shared to other apps. |
| `sharePic` | `String?` | Optional alternative image key specifically for the share payload. |