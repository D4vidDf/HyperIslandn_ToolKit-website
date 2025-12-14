---
title: Multi-Node Progress
weight: 6
---

The Multi-Node Progress component visualizes a process as a series of discrete steps or dots. It is ideal for **Order Tracking** (e.g., Ordered -> Cooking -> Delivered) or **Stepped Wizards**.



## Usage

```kotlin
builder.setMultiProgress(
    title = "Preparing your order...",
    progress = 2,      // The current active step (1-based index)
    points = 4,        // Total number of steps
    color = "#FF8514"  // Color of the active nodes
)
```
## Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `title` | `String?` | Text displayed above the nodes (e.g., status description). |
| `progress` | `Int` | **Required.** The current step number (1-based index). |
| `points` | `Int` | **Required.** The total number of steps/nodes to display. |
| `color` | `String?` | Hex color for the completed/active nodes. |

## Customization

Unlike the linear bar which supports icons (`picForward`, `picEnd`), the Multi-Node progress typically focuses on simple geometry (dots/dashes).

* **Active Color:** Defined by the `color` parameter.
* **Inactive Color:** Automatically handled by the system (usually a dimmed version of the active color or gray).