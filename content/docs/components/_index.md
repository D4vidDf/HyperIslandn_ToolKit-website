---
title: Components
weight: 3
---

While **Templates** define the overall structure and layout of a notification (e.g., "Chat", "Driver", "Upload"), **Components** are modular widgets that provide specific functionality within those layouts.

You can mix and match components with different templates to create rich, interactive experiences. For example, you can add a **Cover Info** component to a **Base Info** template, or add **Action Buttons** to a **Chat Info** template.

## Available Components

| Component | Class | Description |
| :--- | :--- | :--- |
| [**Actions**](/docs/components/actions/) | `HyperAction` | Buttons for user interaction (Icons, Text, Progress). |
| [**Hyper Picture**](/docs/components/hyper-picture/) | `HyperPicture` | Unified image container (Bitmap/Drawable) referenced by key. |
| [**Anim Text Info**](/docs/components/anim-text-info/) | `AnimTextInfo` | Animated headers using Xiaomi system resources. |
| [**Base Info**](/docs/components/base-info/) | `BaseInfo` | Standard hierarchical text layout (Title, Content, Sub). |
| [**Chat Info**](/docs/components/chat-info/) | `ChatInfo` | Standard layout perfect for messaging apps. |
| [**Cover Info**](/docs/components/cover-info/) | `CoverInfo` | Large media cover art (Album/Book) with metadata text. |
| [**Timer Info**](/docs/components/timer/) | `TimerInfo` | Live counting timers (Countdowns/Chronometers). |
| [**Island Config**](/docs/components/island/configuration/) | `ParamIsland` | Behavior configuration for Dynamic Island (Priority, Queue). |
| [**Island Areas**](/docs/components/island/) | `Big/SmallIslandArea` | Content definitions for Expanded and Minimized island states. |
| [**Progress Bars**](/docs/components/progress-bar/) | `ProgressInfo` | Linear bars and indicators. |
| [**Backgrounds**](/docs/components/background/) | `BgInfo` | Custom card backgrounds. |

## How to Use

Components are added using specific setter methods on the `HyperIslandNotification.Builder`.

```kotlin
val builder = HyperIslandNotification.Builder(context, "demo", "Demo")
    .setBaseInfo(...) // Template
    
    // Component 1: Cover Art
    .setCoverInfo(myCoverInfo)
    
    // Component 2: Action Button
    .addAction(myAction)
```