---
title: Cover Info
weight: 3
---

`CoverInfo` is a rich media component designed to feature a large image (Cover Art) alongside hierarchical text. It supports three levels of text depth and is typically used for media notifications.

## Usage

```kotlin
builder.setCoverInfo(
    picCover = "album_art_key", // HyperPicture Key
    title = "Bohemian Rhapsody",
    content = "Queen",
    subContent = "A Night at the Opera"
)
```
## Data Model (`CoverInfo`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `picCover` | `String` | **Required.** Key of the `HyperPicture` to display as the main cover image. |
| `title` | `String` | **Required.** The primary headline (e.g., Song Title). |
| `content` | `String?` | Secondary text (e.g., Artist Name). |
| `subContent` | `String?` | Tertiary text (e.g., Album Name or Year). |

## Color Customization

You can define separate colors for Light Mode and Dark Mode for every text element.

| Text Field | Light Mode | Dark Mode |
| :--- | :--- | :--- |
| **Title** | `colorTitle` | `colorTitleDark` |
| **Content** | `colorContent` | `colorContentDark` |
| **Sub Content** | `colorSubContent` | `colorSubContentDark` |