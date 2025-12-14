---
title: Hyper Picture
weight: 8
---

`HyperPicture` is the unified image container for the library. It acts as a bridge between your image data (Drawables, Bitmaps) and the notification layout.

## The Key-Value Concept

To keep the data models (like `CoverInfo` or `BigIslandArea`) clean and serializable, they do not accept `Bitmap` or `int resId` directly. Instead, they accept a **String Key**.

1.  **Create** a `HyperPicture` with a unique string ID (e.g., `"album_art"`).
2.  **Add** it to the Builder.
3.  **Reference** it by key in your components.

## Usage

### 1. Using a Drawable Resource
Best for static local icons (e.g., play/pause buttons, system icons).

```kotlin
val picResource = HyperPicture(
    key = "icon_play", 
    context = context, 
    drawableRes = R.drawable.ic_play_circle
)

// Add to builder
builder.addPicture(picResource)
```
### Using a Bitmap
Best for dynamic content downloaded from the web (e.g., User Avatars, Album Art).

```kotlin
// Assume you have a Bitmap loaded via Glide/Coil
val albumArtBitmap: Bitmap = ... 

val picBitmap = HyperPicture(
    key = "current_album_art", 
    bitmap = albumArtBitmap
)

// Add to builder
builder.addPicture(picBitmap)
```
### Referencing the Picture
Once added to the builder, you simply use the key string in any component.

```kotlin
// Example: Using the key in CoverInfo
val cover = CoverInfo(
    picCover = "current_album_art", // <--- Matches the key above
    title = "Song Title"
)
```
## API Reference (`HyperPicture`)

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `key` | `String` | **Required.** The unique identifier for this image. You will use this key to reference the image in other components. |
| `icon` | `Icon` | **Required.** The native Android `android.graphics.drawable.Icon`. |

## Constructors

| Constructor | Arguments | Description |
| :--- | :--- | :--- |
| **Resource** | `key`, `context`, `drawableRes` | Creates an Icon from a local drawable resource ID (e.g., `R.drawable.ic_play`). |
| **Bitmap** | `key`, `bitmap` | Creates an Icon from a `Bitmap` object (e.g., downloaded images). |
| **Native** | `key`, `icon` | Wraps an existing Android `Icon` object directly. |
