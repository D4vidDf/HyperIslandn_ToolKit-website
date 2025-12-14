---
title: Base Info
weight: 1
---

`BaseInfo` is the fundamental component used to define the primary text and layout of a notification. It corresponds to the system's "Template 1" (Standard) and "Template 2" (Banner) layouts.

It is versatile and supports multiple text fields, a primary icon, and extensive color customization.

## Usage

```kotlin
builder.setBaseInfo(
    type = 1, // Layout style
    title = "Main Title",
    content = "Primary description text",
    subTitle = "Secondary Title",
    pictureKey = "icon_key",
    
    // Custom Colors
    colorTitle = "#FF0000",
    colorContent = "#666666"
)
```

## Layout Types (`type`)

| Type | Description |
| :--- | :--- |
| `1` | **Standard Layout**. The `pictureKey` (icon) appears on the **left**. Text is stacked vertically. |
| `2` | **Banner Layout**. The `pictureKey` appears on the **right** (often larger). Useful for "Bill Payment" or "Status" notifications. |

## Content Parameters

These variables control the text and iconography displayed in the card.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `title` | `String` | **Required.** The main headline (e.g., "Heavy Snow", "Payment Successful"). |
| `content` | `String` | **Required.** The primary body text (e.g., "Chaoyang District", "September Phone Bill"). |
| `subTitle` | `String?` | Secondary title text, usually appears next to or below the main title. |
| `extraTitle` | `String?` | Supplementary text, often used for timestamps or small metadata (e.g., "Now"). |
| `specialTitle` | `String?` | A small label or tag (e.g., "Sale", "Alert"). |
| `subContent` | `String?` | Secondary body text (e.g., "Wait 20m"). |
| `pictureKey` | `String?` | Key of the `HyperPicture` to display. <br>• **Type 1:** Left Icon.<br>• **Type 2:** Right Banner Icon. |

## Configuration Flags

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `showDivider` | `Boolean?` | If `true`, shows a graphical divider between the title area and content area. |
| `showContentDivider` | `Boolean?` | If `true`, shows a divider between the `content` and `subContent` lines. |

## Color Customization

You can customize the text color for almost every field. Each field has a standard version (Light Mode) and a `Dark` version (Dark Mode).

> **Note:** Colors should be hex strings (e.g., `#FF0000` or `#FF8514`).

| Text Field | Light Mode Parameter | Dark Mode Parameter |
| :--- | :--- | :--- |
| **Title** | `colorTitle` | `colorTitleDark` |
| **Sub Title** | `colorSubTitle` | `colorSubTitleDark` |
| **Extra Title** | `colorExtraTitle` | `colorExtraTitleDark` |
| **Special Label** | `colorSpecialTitle` | `colorSpecialTitleDark` |
| **Special BG** | `colorSpecialBg` | *(Uses same)* |
| **Content** | `colorContent` | `colorContentDark` |
| **Sub Content** | `colorSubContent` | `colorSubContentDark` |

## Actions

The `setBaseInfo` builder method accepts an optional `actionKeys` list.

```kotlin
actionKeys = listOf("reply_action", "mark_read")

```
---