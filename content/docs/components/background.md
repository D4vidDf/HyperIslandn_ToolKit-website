---
title: Background
weight: 8
---

The `BgInfo` component allows you to customize the visual background of the notification card. You can use it to set a full-card image (like album art) or a specific color background.

It supports two distinct layout modes: **Fullscreen** and **Right Side**.

## Usage

```kotlin
builder.setBgInfo(
    // 1. Set the image key (HyperPicture)
    picBg = "album_art_key",
    
    // 2. Define the layout type
    type = 1, // 1 = Fullscreen, 2 = Right Side
    
    // 3. Optional solid color fallback/overlay
    colorBg = "#FF0000"
)
```
## Layout Types

| Type | Description |
| :--- | :--- |
| `1` | **Fullscreen:** The image or color covers the entire background of the notification card. Ideal for media players or immersive alerts. |
| `2` | **Right Side:** The image is positioned on the right side of the card. This is often used for specific templates where the text needs to remain on a solid background on the left. |

## Parameters (`BgInfo`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `type` | `Int` | **Required.** Layout mode.<br>`1` = Fullscreen (Default).<br>`2` = Right Side. |
| `picBg` | `String?` | Key of the `HyperPicture` to use as the background image. |
| `colorBg` | `String?` | Hex color string. Used as a solid background if no image is provided, or potentially as a tint depending on the template. |