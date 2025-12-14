---
title: Components
weight: 3
---

# Components

While **Templates** define the overall structure and layout of a notification (e.g., "Chat", "Driver", "Upload"), **Components** are modular widgets that provide specific functionality within those layouts.

You can mix and match components with different templates to create rich, interactive experiences. For example, you can add a **Progress Bar** component to a **Base Info** template, or add **Action Buttons** to a **Chat Info** template.

## Available Components

| Component | Class | Description |
| :--- | :--- | :--- |
| [**Actions**](/docs/components/actions/) | `HyperAction` | Buttons for user interaction (Icons, Text, Progress). |
| [**Progress Bars**](/docs/components/progress/) | `ProgressInfo` | Linear bars, multi-step nodes, and circular indicators. |
| [**Hint Info**](/docs/components/hint-info/) | `HintInfo` | A top capsule for high-priority status or quick actions. |
| [**Backgrounds**](/docs/components/backgrounds/) | `BgInfo` | Custom background colors or images for the card. |
| [**Island Config**](/docs/components/island-config/) | `ParamIsland` | Configuration for the Dynamic Island behavior (popup, timeout, etc.). |

## How to Use

Components are added using specific setter methods on the `HyperIslandNotification.Builder`.

```kotlin
val builder = HyperIslandNotification.Builder(context, "demo", "Demo")
    .setBaseInfo(...) // Template
    
    // Component 1: Progress Bar
    .setProgressBar(progress = 50, color = "#34C759")
    
    // Component 2: Action Button
    .addAction(myAction)
```