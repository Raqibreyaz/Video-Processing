# Chapter 1 — Digital Image & Pixel

## 1. What is a Digital Image?

A **digital image is a grid of tiny pieces of information called pixels**.

Think of it like graph paper:

```text
┌───┬───┬───┬───┐
│   │   │   │   │
├───┼───┼───┼───┤
│   │   │   │   │
├───┼───┼───┼───┤
│   │   │   │   │
├───┼───┼───┼───┤
│   │   │   │   │
└───┴───┴───┴───┘
```

Each small square represents one **pixel**.

A real image may contain **millions of pixels**.

---

## 2. What is a Pixel?

A **pixel** is the smallest individual **spatial sample** in a digital image.

In simple terms:

> A pixel tells us what image information exists at a particular location.

For example:

```text
┌─────┬─────┬─────┐
│ RED │ RED │BLUE │
├─────┼─────┼─────┤
│ RED │GREEN│BLUE │
├─────┼─────┼─────┤
│BLACK│BLACK│WHITE│
└─────┴─────┴─────┘
```

Each square is a pixel containing some image information.

A useful mental model is:

```text
Pixel
  │
  └── "At this location, the image has this color/brightness."
```

---

## 3. A Pixel Has a Position

A pixel is **not just a color**.

It also has a **location** in the image.

We can represent locations using coordinates:

```text
(0,0)  (1,0)  (2,0)  (3,0)
  ●      ●      ●      ●

(0,1)  (1,1)  (2,1)  (3,1)
  ●      ●      ●      ●
```

Therefore, an image can be thought of as:

> **Many spatial locations + information stored at each location**

This concept becomes important when learning about **resolution**.

---

# 4. Resolution = Number of Pixels

Suppose an image has a resolution of:

```text
1920 × 1080
```

This means:

* **1920 pixels** horizontally
* **1080 pixels** vertically

Total pixels:

```text
1920 × 1080
= 2,073,600 pixels
```

So a single 1920×1080 video frame contains about:

> **2.07 million pixels**

### General formula

```text
Total pixels = width × height
```

For example:

```text
1280 × 720
= 921,600 pixels
```

---

# 5. Why Do More Pixels Give More Detail?

Imagine drawing a circle using only a few pixels.

It might look rough:

```text
   ██
 ██  ██
██    ██
 ██  ██
   ██
```

If we have many more pixels, we have more spatial locations available to describe the shape.

The important idea is:

> **More pixels = more spatial locations available to represent the image.**

This gives a higher-resolution image the **potential to represent finer spatial details**.

### Important wording

Don't think:

> "More pixels make each pixel better."

Instead think:

> "More pixels give us more locations from which to describe the image."

---

# 6. Pixels Are Not Literally Tiny Physical Squares

The grid drawing is a **visualization**.

A digital image is fundamentally **data arranged in a grid**.

A pixel does not necessarily mean there is a tiny colored square physically sitting somewhere in the real world.

For example:

```text
Digital image data
       ↓
   pixel values
       ↓
Display system
       ↓
Physical display elements
       ↓
What your eyes see
```

The display converts the image data into something physically visible.

For learning image and video processing, however, thinking of pixels as a grid of tiny image samples is a very useful mental model.

---

# 7. Pixel vs Pixel Value

These two ideas should not be confused.

### Pixel

Think:

> **Where are we?**

### Pixel value

Think:

> **What information does this location contain?**

For a simplified RGB example:

```text
Pixel A → Red
Pixel B → Green
Pixel C → Blue
```

More formally:

```text
Image
 │
 ├── Pixel at (0,0) → some value
 ├── Pixel at (1,0) → some value
 ├── Pixel at (2,0) → some value
 └── ...
```

Later, image/video processing becomes more complicated because a pixel's representation can involve:

* RGB
* YUV
* multiple color channels
* bit depth
* chroma subsampling
* color spaces

These concepts come later. For now, remember:

> **A pixel identifies a spatial location, while its value describes the image information at that location.**

---

# 8. Why Pixels Matter for Video

A **video is a sequence of digital images called frames**.

Therefore:

```text
VIDEO
  │
  ▼
Sequence of frames
  │
  ▼
Each frame is an image
  │
  ▼
Each image contains pixels
```

For example:

```text
Frame 1          Frame 2          Frame 3

┌────────┐       ┌────────┐       ┌────────┐
│   ●    │       │    ●   │       │     ●  │
│        │       │        │       │        │
└────────┘       └────────┘       └────────┘
```

The object appears to move because its **position changes between frames**.

This leads directly to the concept of **FPS (frames per second)**.

For example:

```text
Frame 1 → object at position A
Frame 2 → object at position B
Frame 3 → object at position C
Frame 4 → object at position D
```

When these frames are displayed rapidly, we perceive motion.

---

# 9. Connection to Backend / FFmpeg Work

When FFmpeg reports:

```text
1920x1080
```

it is telling you the **width and height of each video frame**.

So:

```text
Frame
 ├── width  = 1920 pixels
 └── height = 1080 pixels
```

Total spatial samples:

```text
1920 × 1080
= 2,073,600 pixels
```

### Resizing with FFmpeg

Suppose you run:

```bash
ffmpeg -i input.mp4 -vf scale=1280:720 output.mp4
```

You are asking FFmpeg to transform the frame dimensions:

```text
1920 × 1080
       ↓
1280 × 720
```

The number of pixels changes from:

```text
1920 × 1080 = 2,073,600
```

to:

```text
1280 × 720 = 921,600
```

So resizing reduces the number of spatial samples in every frame.

This is why resizing a video changes its **resolution**.

---

# 10. Important Mental Model

Keep the entire concept in this chain:

```text
DIGITAL IMAGE
      │
      ▼
 Grid of pixels
      │
      ▼
Each pixel has a location
and image information
      │
      ▼
More pixels
      │
      ▼
More spatial locations
      │
      ▼
Potentially more spatial detail
```

For video:

```text
VIDEO
  │
  ▼
Sequence of frames
  │
  ▼
Each frame is an image
  │
  ▼
Each image contains pixels
  │
  ▼
Pixels have spatial locations
and values
```

---

# 11. Example: Understanding an Image Dimension

Suppose you have:

```text
800 × 600
```

This means:

```text
Width  = 800 pixels
Height = 600 pixels
```

Total:

```text
800 × 600
= 480,000 pixels
```

Now suppose you change it to:

```text
1600 × 1200
```

Total:

```text
1600 × 1200
= 1,920,000 pixels
```

The second image has:

```text
1,920,000 / 480,000
= 4×
```

as many pixels.

Notice what happened:

```text
800 × 600
   ↓
1600 × 1200

Width  → 2×
Height → 2×
Total pixels → 4×
```

This is an important pattern:

> If both width and height double, the total number of pixels becomes **4×**, not 2×.

---

# 12. Common Mistakes / Gotchas

### Mistake 1: Thinking resolution means physical size

```text
1920 × 1080
```

does **not** directly tell you how physically large the image is.

It tells you the number of pixels horizontally and vertically.

A 1920×1080 image could be displayed on different physical screen sizes.

---

### Mistake 2: Thinking a pixel is always a physical square

A pixel is fundamentally **digital image data**.

The grid/square representation is a useful abstraction.

---

### Mistake 3: Thinking more pixels automatically means a better image

More pixels provide more spatial sampling, but image quality also depends on many other things.

For example:

* source quality
* lens/camera quality
* focus
* compression
* noise
* bit depth
* color representation
* scaling method

So:

> **More pixels can allow more detail, but more pixels alone do not guarantee better visual quality.**

---

### Mistake 4: Confusing pixel count with pixel quality

Compare:

```text
Pixel count
    ↓
How many spatial samples exist?
```

with:

```text
Pixel value
    ↓
What information is stored at a location?
```

These are different ideas.

---

# 13. One-Sentence Summary

> **A digital image is a grid of pixels, where each pixel represents image information at a particular spatial location; resolution describes how many pixels exist horizontally and vertically.**

---

# Key Takeaways

* A **digital image** is represented as a grid of pixels.

* A **pixel** is an individual spatial sample of an image.

* Every pixel has a **location**.

* A pixel also has a **value** representing image information at that location.

* Resolution is normally written as:

  ```text
  width × height
  ```

* Total pixel count is:

  ```text
  width × height
  ```

* `1920×1080` contains **2,073,600 pixels**.

* More pixels mean more available **spatial locations**.

* More pixels can allow finer spatial detail, but do not automatically guarantee better image quality.

* A pixel is **digital data**, not necessarily a literal physical square.

* A video is a **sequence of frames**.

* Each frame is an image.

* Each frame contains pixels.

* FFmpeg's `1920x1080` describes the dimensions of each video frame.

* Resizing changes the number of spatial samples in each frame.

---

# Minimal Self-Test

Try answering these without looking back:

1. What is a pixel?
2. Why is a pixel more than just a color?
3. What does `1920×1080` mean?
4. How many pixels are in an `800×600` image?
5. If width and height both double, what happens to the total pixel count?
6. Are pixels literally tiny physical squares?
7. What is the difference between a pixel and its pixel value?
8. How is a video related to digital images?
9. In FFmpeg, what does `scale=1280:720` change?
10. Does having more pixels automatically guarantee better image quality?

---

# What to Learn Next

The natural next step is:

**Chapter 2 — Resolution & Aspect Ratio**

There you should connect:

```text
Pixels
  ↓
Resolution
  ↓
Width × Height
  ↓
Aspect Ratio
  ↓
Why 1920×1080 = 16:9
  ↓
Why resizing incorrectly can stretch/squash video
```
