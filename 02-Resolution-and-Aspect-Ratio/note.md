# Chapter 2 — Resolution & Aspect Ratio

## What it is

Two important properties describe the basic shape and size of a video frame:

* **Resolution** → how many pixel positions the frame has.
* **Aspect ratio** → the proportional relationship between its width and height.

For example:

```text
1920 × 1080
```

means:

```text
Width  = 1920 pixels
Height = 1080 pixels
```

and its aspect ratio is:

```text
1920 : 1080
     ↓
    16 : 9
```

---

## One-sentence summary

> **Resolution describes an image's pixel dimensions (`width × height`), while aspect ratio describes the proportional shape formed by those dimensions.**

---

# Intuition

Think of resolution as the **number of tiles** in a rectangular floor and aspect ratio as the **shape of the floor**.

For example:

```text
1920 × 1080
```

has many pixels arranged in a wide rectangle:

```text
┌────────────────────────────┐
│                            │
│                            │
│                            │
└────────────────────────────┘
             16:9
```

While:

```text
1080 × 1080
```

has the same height but forms a square:

```text
┌───────────────┐
│               │
│               │
│               │
└───────────────┘
      1:1
```

So:

> **Resolution tells you the pixel dimensions. Aspect ratio tells you the shape.**

---

# 1. What is Resolution?

Resolution tells us how many pixels a frame has horizontally and vertically.

For example:

```text
1920 × 1080
```

means:

```text
Width  → 1920 pixels
Height → 1080 pixels
```

The total number of pixel positions is:

```text
1920 × 1080
= 2,073,600
```

So every frame contains about:

> **2.07 million pixel positions**

---

## General formula

For a frame:

```text
W × H
```

the total number of pixel positions is:

```text
Total pixels = W × H
```

Examples:

```text
1280 × 720
= 921,600 pixels
```

```text
1920 × 1080
= 2,073,600 pixels
```

```text
3840 × 2160
= 8,294,400 pixels
```

---

# 2. What Does "1080p" Mean?

This is a common source of confusion.

When people say:

> **1080p**

they usually mean a video format with approximately **1080 pixels vertically**.

The common 16:9 version is:

```text
1920 × 1080
```

Similarly:

```text
720p → commonly 1280 × 720
480p → commonly 854 × 480 for 16:9 video
```

The `p` historically refers to **progressive scanning**.

You will study progressive vs interlaced scanning later, so for now simply remember:

> **1080p commonly refers to a format with about 1080 vertical pixels.**

---

## Important: Don't blindly equate 1080p with 1920×1080

In everyday usage:

```text
1080p
≈
1920 × 1080
```

But technically, `1080p` describes the **vertical resolution/scanning format**, not every possible width.

The width depends on the aspect ratio.

For example:

```text
16:9 + 1080 vertical pixels
        ↓
1920 × 1080
```

But a different aspect ratio could have a different width while still having 1080 vertical pixels.

Therefore:

```text
1080p
   ↓
roughly 1080 vertical pixels
```

is a safer mental model.

---

# 3. What is Aspect Ratio?

**Aspect ratio describes the relationship between width and height.**

The basic form is:

```text
width : height
```

For:

```text
1920 × 1080
```

we have:

```text
1920 : 1080
```

Simplify the ratio by dividing both numbers by their greatest common divisor:

```text
1920 ÷ 120 = 16
1080 ÷ 120 = 9
```

Therefore:

```text
1920 : 1080
     ↓
    16 : 9
```

So the frame has a:

> **16:9 aspect ratio**

---

# 4. Aspect Ratio Describes Shape

Aspect ratio does **not** tell you the total number of pixels.

It tells you the **proportional shape**.

Common examples:

```text
16:9 → wide rectangle
1:1  → square
9:16 → tall rectangle
```

Visualized:

```text
16:9

┌────────────────────────────┐
│                            │
│                            │
│                            │
└────────────────────────────┘
```

```text
1:1

┌───────────────┐
│               │
│               │
│               │
└───────────────┘
```

```text
9:16

┌───────┐
│       │
│       │
│       │
│       │
│       │
└───────┘
```

---

# 5. Same Height, Different Width

This is an important concept.

Compare:

```text
1920 × 1080
```

and:

```text
1080 × 1080
```

Both have:

```text
Height = 1080 pixels
```

But:

```text
1920 × 1080 → 16:9
1080 × 1080 → 1:1
```

So their shapes are different:

```text
1920 × 1080

┌──────────────────┐
│                  │
│                  │
│                  │
└──────────────────┘
       16:9
```

```text
1080 × 1080

┌───────────────┐
│               │
│               │
│               │
└───────────────┘
       1:1
```

Therefore:

> **Knowing only one dimension, such as "1080", is not enough to completely describe the frame's shape.**

You also need the other dimension or the aspect ratio.

---

# 6. Landscape vs Portrait

Now compare:

```text
1920 × 1080
```

with:

```text
1080 × 1920
```

### 1920 × 1080

```text
Width  = 1920
Height = 1080
```

Since width is greater than height, it is:

> **Landscape**

Its aspect ratio is:

```text
1920 : 1080
= 16 : 9
```

---

### 1080 × 1920

```text
Width  = 1080
Height = 1920
```

Since height is greater than width, it is:

> **Portrait**

Its aspect ratio is:

```text
1080 : 1920
= 9 : 16
```

Visual comparison:

```text
1920 × 1080                 1080 × 1920

┌──────────────────┐           ┌───────┐
│                  │           │       │
│                  │           │       │
│                  │           │       │
└──────────────────┘           │       │
                               │       │
                               └───────┘

      16:9                       9:16
    Landscape                   Portrait
```

---

# 7. Same Number of Pixels, Different Shape

This is a particularly useful point.

Consider:

```text
1920 × 1080
```

and:

```text
1080 × 1920
```

Their total pixel counts are:

```text
1920 × 1080
= 2,073,600
```

and:

```text
1080 × 1920
= 2,073,600
```

So they contain exactly the same number of pixel positions.

But their arrangement is different:

```text
1920 × 1080
→ 16:9
→ landscape

1080 × 1920
→ 9:16
→ portrait
```

This leads to an important distinction:

> **Pixel count and image shape are different properties.**

The pixels can be rearranged into different width/height dimensions while keeping the same total number of pixels.

---

# 8. Resolution vs Aspect Ratio

Keep these concepts separate:

| Concept      | Meaning                      | Example       |
| ------------ | ---------------------------- | ------------- |
| Resolution   | Pixel dimensions             | `1920 × 1080` |
| Width        | Horizontal pixel count       | `1920`        |
| Height       | Vertical pixel count         | `1080`        |
| Pixel count  | Total pixel positions        | `2,073,600`   |
| Aspect ratio | Width-to-height relationship | `16:9`        |
| Orientation  | Landscape/portrait/square    | Landscape     |

A useful way to remember it:

```text
Resolution
    │
    ├── Width
    │
    └── Height
          │
          ▼
     Width : Height
          │
          ▼
    Aspect Ratio
```

---

# 9. How to Calculate Aspect Ratio

Given:

```text
W × H
```

write:

```text
W : H
```

Then simplify the ratio.

### Example

```text
1280 × 720
```

becomes:

```text
1280 : 720
```

Divide by 80:

```text
1280 ÷ 80 = 16
720 ÷ 80 = 9
```

Therefore:

```text
1280 × 720
→ 16:9
```

---

### Example

```text
1080 × 1920
```

becomes:

```text
1080 : 1920
```

Divide by 120:

```text
1080 ÷ 120 = 9
1920 ÷ 120 = 16
```

Therefore:

```text
1080 × 1920
→ 9:16
```

---

### Example

```text
1080 × 1080
```

becomes:

```text
1080 : 1080
```

Divide both by 1080:

```text
1 : 1
```

Therefore:

```text
1080 × 1080
→ 1:1
```

---

# 10. Resolution and Aspect Ratio in FFmpeg

This matters directly when working with FFmpeg.

Suppose your source video is:

```text
1920 × 1080
16:9
```

If you resize it to:

```text
1280 × 720
```

the aspect ratio remains:

```text
1280 : 720
= 16 : 9
```

So the video gets smaller in resolution but keeps the same shape.

```text
1920 × 1080
      ↓
1280 × 720

16:9              16:9
```

But if you resize to:

```text
1080 × 1080
```

you have changed the shape:

```text
16:9
  ↓
1:1
```

This can lead to stretching, squashing, cropping, or padding depending on how the transformation is performed.

---

# 11. Why Aspect Ratio Matters in Real Video Systems

Aspect ratio becomes important when video is displayed on different devices and platforms.

Examples include:

* Landscape video
* Portrait/mobile video
* Square video
* Web video players
* LMS video players
* YouTube-style players
* Instagram/TikTok-style vertical content

For example:

```text
Landscape
1920 × 1080
16:9
```

is shaped very differently from:

```text
Portrait
1080 × 1920
9:16
```

Even though both contain:

```text
2,073,600 pixels
```

per frame.

---

# 12. Important Connection: Resolution Does Not Determine Aspect Ratio by Itself

It is easy to make this mistake:

> "1080p means the video is always 1920×1080."

A better understanding is:

```text
1080p
   ↓
approximately 1080 vertical pixels
```

Then the aspect ratio helps determine the width.

For example:

```text
16:9
+
1080 height
    ↓
1920 width
```

So:

```text
1920 × 1080
```

But:

```text
9:16
+
1080 width
    ↓
1920 height
```

gives:

```text
1080 × 1920
```

This distinction becomes useful when working with vertical video.

---

# 13. Resolution, Aspect Ratio, and Orientation

These three ideas work together:

```text
Resolution
   ↓
Width × Height
   ↓
Width : Height
   ↓
Aspect Ratio
   ↓
Shape / Orientation
```

For example:

```text
1920 × 1080
      ↓
1920 : 1080
      ↓
16 : 9
      ↓
Landscape
```

Another:

```text
1080 × 1920
      ↓
1080 : 1920
      ↓
9 : 16
      ↓
Portrait
```

Another:

```text
1080 × 1080
      ↓
1080 : 1080
      ↓
1 : 1
      ↓
Square
```

---

# Common Mistakes / Gotchas

## 1. "1080p means exactly 1920×1080."

Usually in common 16:9 usage, yes.

Technically, `1080p` refers primarily to the vertical resolution and progressive scanning format. The exact width depends on the format/aspect ratio.

---

## 2. "More pixels always means a different aspect ratio."

No.

You can increase resolution while preserving the same aspect ratio.

For example:

```text
1280 × 720
→ 16:9
```

and:

```text
1920 × 1080
→ 16:9
```

Different resolutions, same shape.

---

## 3. "Same number of pixels means same shape."

No.

For example:

```text
1920 × 1080
```

and:

```text
1080 × 1920
```

both contain 2,073,600 pixels, but one is landscape and the other is portrait.

---

## 4. "Aspect ratio is the total number of pixels."

No.

Aspect ratio is a **relationship**, not a pixel count.

```text
1920 × 1080 → 2,073,600 pixels
1920 : 1080 → 16:9
```

The first is pixel count information.

The second is shape information.

---

## 5. "Changing width and height always changes the aspect ratio."

Not necessarily.

For example:

```text
1280 × 720
```

and:

```text
1920 × 1080
```

have different dimensions but both are:

```text
16:9
```

You can scale an image while maintaining its aspect ratio.

---

# FFmpeg Mental Model

When dealing with video dimensions in FFmpeg, think:

```text
Video frame
    │
    ├── Width
    │
    ├── Height
    │
    ├── Total pixel positions
    │
    └── Aspect ratio
```

For:

```text
1920 × 1080
```

you can derive:

```text
Width  = 1920
Height = 1080

Pixels = 1920 × 1080
       = 2,073,600

Aspect ratio
= 1920 : 1080
= 16 : 9

Orientation
= Landscape
```

---

# Core Mental Model

Keep this chain in your head:

```text
DIGITAL IMAGE
      │
      ▼
    PIXELS
      │
      ▼
 WIDTH × HEIGHT
      │
      ├───────────────┐
      ▼               ▼
 Pixel count      Width : Height
      │               │
      ▼               ▼
Total samples    Aspect ratio
                      │
                      ▼
                 Image shape
```

For example:

```text
1920 × 1080
    │
    ├── 2,073,600 pixels
    │
    ├── 16:9 aspect ratio
    │
    └── Landscape
```

And:

```text
1080 × 1920
    │
    ├── 2,073,600 pixels
    │
    ├── 9:16 aspect ratio
    │
    └── Portrait
```

---

# Key Takeaways

* **Resolution** describes the pixel dimensions of a frame.
* Resolution is normally written as:

```text
width × height
```

* Total pixel count is:

```text
width × height
```

* `1080p` commonly refers to a format with about **1080 vertical pixels**.
* `1080p` is commonly `1920 × 1080` for 16:9 video, but the term should not be treated as an absolute synonym for that exact dimension.
* **Aspect ratio** describes:

```text
width : height
```

* `1920 × 1080` → `16:9`.
* `1280 × 720` → `16:9`.
* `1080 × 1920` → `9:16`.
* `1080 × 1080` → `1:1`.
* `1920 × 1080` and `1080 × 1920` contain the same number of pixels but have different shapes.
* Resolution and aspect ratio are related, but they describe different things.
* You can change resolution while keeping the same aspect ratio.
* Changing the aspect ratio can change the frame from landscape to portrait, square, or another shape.
* This distinction is essential when resizing and transcoding video with FFmpeg.

---

# Minimal Self-Test

Try these without looking back:

1. What does `1920 × 1080` tell you?
2. How many pixels are in a `1280 × 720` frame?
3. What is the aspect ratio of `1280 × 720`?
4. What is the aspect ratio of `1080 × 1920`?
5. What is the difference between `1080p` and `1920 × 1080`?
6. Why can `1920 × 1080` and `1080 × 1920` have the same number of pixels but different orientations?
7. Can `1280 × 720` and `1920 × 1080` have different resolutions but the same aspect ratio? Why?
8. What happens to the aspect ratio when `1920 × 1080` is resized proportionally to `1280 × 720`?
9. What are the width and height of a `9:16` portrait video if its width is `1080` pixels?
10. In FFmpeg, what does `1920x1080` tell you about each video frame?

---

# What to Learn Next

The next logical layer is **scaling, cropping, padding, and preserving aspect ratio**.

That is where these ideas become practical:

```text
Source:  1920 × 1080 (16:9)
             │
             ├── Scale → resize while preserving shape
             │
             ├── Crop → remove part of the frame
             │
             └── Pad → add empty space around the frame
```

Understanding these operations will make FFmpeg commands such as `scale`, `crop`, and `pad` much easier to reason about.
