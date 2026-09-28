# Practical 2 — Implementing Alternative Responsive Layouts

**Student ID:** 20243006990  
**Course:** COMPX234 — Android Responsive Layout 2

## Overview

This practical builds on Practical 1 (LinearLayout with Weights) and implements **alternative responsive layouts** using Android resource qualifiers. The same activity (`MainActivity`) loads a different `activity_main.xml` automatically depending on the device configuration — **no Java code changes are needed**.

## Project Structure

```
app/src/main/res/
├── layout/
│   └── activity_main.xml          # Default — phone portrait (vertical stack)
├── layout-land/
│   └── activity_main.xml          # Part 1 — Landscape orientation
└── layout-sw600dp/
    └── activity_main.xml         # Part 2 — Tablet (smallest width ≥ 600dp)
```

## Part 1 — Orientation Qualifier (Landscape)

**Directory:** `res/layout-land/`

When the device is rotated to landscape, Android automatically loads `res/layout-land/activity_main.xml`. The portrait layout is a strictly vertical stack; the landscape layout takes advantage of the wider screen by splitting the UI into **two horizontal panes**:

| Left pane (weight=1) | Right pane (weight=1) |
|---|---|
| Black title bar "Lab 1" | Four colored squares (This / is / my / first) |
| White subtitle "Responsive Layout 1" | Buttons (Change / Cancel) on light purple bg |
| Black content "Android Application" | |

## Part 2 — Width Qualifier (Smallest Width — sw600dp)

**Directory:** `res/layout-sw600dp/`

This targets devices with a smallest width of at least 600dp (e.g., a 7-inch tablet). A **multi-pane** design is used:

- **Left sidebar (weight=1, black background):** Title "Lab 1" (28sp) and subtitle (20sp), centered vertically with 24dp padding.
- **Right content area (weight=2):** Black content region, the four colored squares (20sp text), and the button row (18sp text, 24dp padding).

Text sizes and padding are increased to suit the larger screen.

## How Android Selects the Layout at Runtime

| Configuration | Layout loaded |
|---|---|
| Phone portrait | `res/layout/activity_main.xml` |
| Phone landscape | `res/layout-land/activity_main.xml` |
| Tablet (sw ≥ 600dp) | `res/layout-sw600dp/activity_main.xml` |

The layout file name is always `activity_main.xml`; the **resource directory name** tells Android which version to use.

## Rules Followed

1. **No drag-and-drop** — all XML written manually.
2. **No hard-coded pixels** — uses `match_parent`, `wrap_content`, `0dp` with `layout_weight`, and `dp`/`sp` units.
3. **Three configurations tested** — portrait, landscape (Ctrl + Left/Right in emulator), and tablet (sw600dp AVD).

## Building & Running

Open the project in Android Studio, sync Gradle, then run on:
- A phone emulator — rotate to landscape to see the `layout-land` layout.
- A tablet AVD (e.g., Pixel C / Nexus 10) to see the `layout-sw600dp` multi-pane layout.
