# Chapter 1 — Digital Image & Pixel

## What it is

A **digital image** is a grid of tiny pieces of image information called **pixels**.

Think of an image like graph paper:

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

Each small square represents a **pixel**.

Real images may contain millions of pixels.

---

## One-sentence summary

> **A digital image is a grid of pixels, where each pixel represents image information at a particular spatial location, and resolution tells us how many pixels exist horizontally and vertically.**

---

## Intuition

Imagine taking a large photograph and placing a transparent grid over it.

Each grid position answers two questions:

```text
Where am I?
    +
What does the image look like here?
```

So an image can be thought of as:

```text
Image
 │
 ├── Pixel at location (0,0)
 ├── Pixel at location (1,0)
 ├── Pixel at location (2,0)
 ├── Pixel at location (0,1)
 └── ...
```

The important idea is that a pixel is not just a color. It is **image information associated with a particular location**.

---

# Pixel

A **pixel** is the smallest individual spatial sample in a digital image.

For a simple mental model:

```text
Pixel
  │
  └── "At this location, the image has this color/brightness."
```

For example:

```text
┌────┬────┬─────┐
│RED │RED │BLUE │
├────┼────┼─────┤
│RED │GREEN│BLUE│
├────┼────┼─────┤
│BLACK│BLACK│WHITE│
└────┴────┴─────┘
```

Each square represents one pixel.

---

# Pixels have positions

Every pixel belongs to a particular location in the image.

We can represent locations using coordinates:

```text
(0,0)  (1,0)  (2,0)  (3,0)
  ●      ●      ●      ●

(0,1)  (1,1)  (2,1)  (3,1)
  ●      ●      ●      ●
```

Therefore, a useful mental model is:

> **Image = many spatial locations + information at each location**

This becomes important when understanding **resolution**.

---

# Pixel vs Pixel Value

These two terms are related but not identical.

### Pixel

Describes **where** we are.

> "Which spatial location are we talking about?"

### Pixel value

Describes **what information is stored at that location**.

For a simplified RGB example:

```text
Pixel A → Red
Pixel B → Green
Pixel C → Blue
```

In real video systems, pixel representation can be more complicated. You will later encounter:

* RGB vs YUV
* Color channels
* Bit depth
* Chroma subsampling
* Color spaces

For now, the simple model is enough.

---

# What is Resolution?

**Resolution describes the number of pixels in the horizontal and vertical directions.**

For example:

```text
1920 × 1080
```

means:

```text
1920 pixels wide
1080 pixels tall
```

The total number of pixel positions is:

```text
1920 × 1080
= 2,073,600 pixels
```

So one frame of a 1920×1080 video contains about:

> **2.07 million pixel positions**

---

## Example: 800 × 600

For an image of:

```text
800 × 600
```

the total number of pixels is:

```text
800 × 600
= 480,000 pixels
```

If we change it to:

```text
1600 × 1200
```

then:

```text
1600 × 1200
= 1,920,000 pixels
```

So:

```text
800 × 600
     ↓
480,000 pixels

1600 × 1200
     ↓
1,920,000 pixels
```

The second image has:

```text
1,920,000 / 480,000
= 4×
```

as many pixel positions.

---

# Why do more pixels allow more detail?

Imagine trying to draw a circle using only a few pixels:

```text
   ██
 ██  ██
██    ██
 ██  ██
   ██
```

There are only a small number of spatial locations available to describe the circle.

If we have many more pixels, we have many more locations available to describe its shape.

Therefore:

> **More pixels = more spatial locations available to describe the image.**

This is why a higher-resolution image can represent finer spatial details.

However, there is an important catch when the higher resolution comes from **resizing** an existing image.

---

# Very Important: Pixels are not literally tiny physical squares

When we draw an image like this:

```text
┌───┬───┬───┐
│   │   │   │
├───┼───┼───┤
│   │   │   │
└───┴───┴───┘
```

the grid is a **visualization**.

A digital image is fundamentally **data arranged in a grid**.

A pixel does not have to correspond to a literal tiny colored square physically sitting somewhere in the real world.

A display takes the image data and uses its physical display elements to show the image.

For learning image/video processing, though, thinking of pixels as a grid of tiny image samples is a very useful model.

---

# Image vs Video

A video can be understood as:

> **A sequence of digital images called frames, changing over time.**

The relationship is:

```text
IMAGE
  │
  ▼
Grid of pixels


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
Frame 1        Frame 2        Frame 3

┌────────┐     ┌────────┐     ┌────────┐
│   ●    │     │    ●   │     │     ●  │
│        │     │        │     │        │
└────────┘     └────────┘     └────────┘
```

The object appears to move because its position changes between frames.

This connects directly to **FPS (frames per second)**, which will be covered later.

---

# Connection to FFmpeg

When FFmpeg shows:

```text
1920x1080
```

it is telling you the dimensions of the video frames.

Each frame has:

```text
Width  = 1920 pixels
Height = 1080 pixels
```

Suppose you run:

```bash
ffmpeg -i input.mp4 -vf scale=1280:720 output.mp4
```

You are asking FFmpeg to resize each frame from:

```text
1920 × 1080
      ↓
1280 × 720
```

The number of pixel positions therefore changes from:

```text
1920 × 1080 = 2,073,600
```

to:

```text
1280 × 720 = 921,600
```

So resizing the video reduces the number of spatial samples in every frame.

That is why resizing changes the video's **resolution**.

---

# Increasing Resolution

Consider:

```text
100 × 100
    ↓
200 × 200
```

Original:

```text
100 × 100
= 10,000 pixels
```

New:

```text
200 × 200
= 40,000 pixels
```

Therefore:

```text
40,000 / 10,000
= 4×
```

The new image has **4 times as many pixel positions**.

But there is an important question:

> Where did the values of all those new pixels come from?

They were not magically captured from the original image.

A resizing algorithm calculates values for the new pixel positions based on the original image.

```text
Original image
      │
      ▼
Resizing algorithm
      │
      ▼
New pixel positions
+ calculated pixel values
```

---

# Image Resizing Methods

Common resizing/interpolation methods include:

### 1. Nearest-neighbor

The new pixel gets a value based on the nearest existing pixel.

Conceptually:

```text
Original:

A B
C D

New pixels
take values from nearby
existing pixels.
```

It is simple and fast, but can produce blocky results.

---

### 2. Bilinear

Bilinear interpolation uses nearby pixels to calculate a smoother value.

Instead of simply copying one pixel:

```text
New pixel = nearby pixel
```

it effectively combines information from nearby pixels.

This generally produces smoother results than nearest-neighbor.

---

### 3. Bicubic

Bicubic interpolation considers more neighboring pixels and uses a more complex interpolation calculation.

It can produce smoother and often better-looking results, but requires more computation.

---

# The Most Important Upscaling Gotcha

Suppose we have:

```text
720p video
    ↓ upscale
1080p video
```

The resulting video has a:

```text
1080p-sized frame
```

But that does **not** mean it contains the same amount of real detail as a video originally captured at 1080p.

Why?

Because the additional pixels were calculated from the existing information.

```text
720p
 │
 │ interpolation / resizing
 ▼
1080p
```

The output has more pixel positions, but the original 720p video did not contain the missing high-frequency detail.

Therefore:

> **Increasing resolution does not magically recover detail that was never present in the original image.**

This is one of the most important concepts in image/video processing.

---

# Resolution vs Better Pixels

Do not confuse **resolution** with **pixel precision**.

These are different concepts.

### Resolution

Controls the number of spatial locations.

```text
Resolution
    ↓
More spatial locations
    ↓
More pixels
```

### Bit depth

Controls how precisely values can be represented.

```text
Bit depth
    ↓
More possible values per pixel/channel
    ↓
More precise color/brightness representation
```

So:

```text
800 × 600
    ↓
1600 × 1200
```

primarily means:

> **More spatial locations**

It does **not** mean that every existing pixel suddenly became more precise.

---

# Two Different Ways to Get "More"

This distinction is useful:

| Change                           | What increases?           | Main idea                    |
| -------------------------------- | ------------------------- | ---------------------------- |
| Higher resolution                | Number of spatial samples | More locations               |
| Higher bit depth                 | Number of possible values | More precision               |
| Upscaling                        | Number of output pixels   | New values are calculated    |
| Native higher-resolution capture | Captured spatial samples  | More real source information |

For example:

```text
1920 × 1080, 8-bit
```

and

```text
3840 × 2160, 8-bit
```

have different resolutions but the same bit depth.

Likewise:

```text
1920 × 1080, 8-bit
```

and

```text
1920 × 1080, 10-bit
```

have the same resolution but different value precision.

---

# Resolution Does Not Automatically Mean "Better"

It is tempting to think:

```text
More pixels = automatically better image
```

That is too simplistic.

More resolution gives the image **more spatial sampling capacity**, but actual image quality also depends on other factors such as:

* Original capture quality
* Lens quality
* Focus
* Noise
* Compression
* Bit depth
* Chroma subsampling
* Encoding quality
* Scaling method

For example:

```text
Low-quality 4K source
```

does not automatically look better than:

```text
High-quality 1080p source
```

in every situation.

For this chapter, remember the narrower point:

> Resolution tells us how many spatial samples/pixel positions are available.

---

# A Useful Mental Model

Think of an image as a spreadsheet.

```text
        Columns →
       0    1    2    3
    ┌────┬────┬────┬────┐
 0  │ P  │ P  │ P  │ P  │
    ├────┼────┼────┼────┤
 1  │ P  │ P  │ P  │ P  │
    ├────┼────┼────┼────┤
 2  │ P  │ P  │ P  │ P  │
    └────┴────┴────┴────┘
       ↑
     Rows
```

Each cell represents a pixel position.

Each position has some image information.

So:

```text
Image
 │
 ├── Width  → number of horizontal positions
 │
 ├── Height → number of vertical positions
 │
 └── Pixel values → information stored at those positions
```

---

# Common Mistakes / Gotchas

## 1. "A pixel is just a color."

Not quite.

A pixel is associated with a **spatial location** and has a **value** representing image information at that location.

---

## 2. "1920 × 1080 means 1920 pixels total."

No.

It means:

```text
1920 pixels wide
×
1080 pixels tall
```

So:

```text
1920 × 1080 = 2,073,600
```

pixel positions.

---

## 3. "Upscaling creates new real detail."

No.

Upscaling creates **new pixel positions** and calculates values for them.

```text
More pixels ≠ magically more original information
```

---

## 4. "Higher resolution makes each pixel better."

No.

Resolution and pixel precision are different.

```text
Resolution → number of spatial locations

Bit depth → precision of represented values
```

---

## 5. "The pixels are physically tiny squares inside the file."

Not literally.

The digital image is data arranged in a grid. The physical display has its own hardware elements for showing that data.

---

## 6. "A video is a giant 3D image."

For the basic model, it is better to think:

```text
Video
  =
Sequence of 2D image frames
  +
Time
```

Each frame is independently a grid of pixels, although video compression can introduce additional relationships between frames.

---

# Examples

### Example 1

Given:

```text
640 × 480
```

Total pixels:

```text
640 × 480
= 307,200
```

---

### Example 2

Given:

```text
1280 × 720
```

Total:

```text
1280 × 720
= 921,600
```

---

### Example 3

Compare:

```text
1920 × 1080
```

and:

```text
3840 × 2160
```

The second has:

```text
3840 × 2160 = 8,294,400
```

pixels.

The first has:

```text
1920 × 1080 = 2,073,600
```

pixels.

Ratio:

```text
8,294,400 / 2,073,600
= 4
```

So 3840×2160 has **4× as many pixel positions** as 1920×1080.

---

### Example 4 — Upscaling

```text
100 × 100
    ↓
200 × 200
```

Pixel count:

```text
10,000 → 40,000
```

There are 4× more output pixel positions.

But the extra 30,000 positions were generated through interpolation/resizing. They were not newly captured from the scene.

---

# Core Flow to Remember

```text
DIGITAL IMAGE
      │
      ▼
Grid of pixels
      │
      ▼
Each pixel has a spatial location
and image information
      │
      ▼
Resolution
      │
      ▼
Number of horizontal × vertical positions
      │
      ▼
More positions
      │
      ▼
Potentially more spatial detail
```

And for video:

```text
VIDEO
  │
  ▼
Sequence of frames
  │
  ▼
Each frame = digital image
  │
  ▼
Each image = grid of pixels
  │
  ▼
Each pixel = location + image value
```

---

# Key Takeaways

* A **digital image** is data arranged as a grid of pixels.
* A **pixel** is the smallest individual spatial sample in the image.
* A pixel has a **location** and a **value**.
* `1920 × 1080` means 1920 horizontal positions and 1080 vertical positions.
* Total pixel count is:

```text
width × height
```

* `1920 × 1080 = 2,073,600` pixel positions.
* More pixels provide more **spatial locations** for representing a scene.
* Pixels shown as tiny squares are a useful visualization, not necessarily physical objects.
* A video is a **sequence of image frames over time**.
* FFmpeg's `1920x1080` describes the dimensions of each frame.
* Resizing changes the number of spatial samples in the output frame.
* Upscaling creates more pixel positions, but does **not magically recover missing original detail**.
* Nearest-neighbor, bilinear, and bicubic are common resizing/interpolation methods.
* **Resolution ≠ bit depth**.
* Resolution controls the number of spatial samples.
* Bit depth controls the precision of represented values.

---

# Minimal Self-Test

Try answering these without looking above:

1. What is a pixel?
2. Why is a pixel more than just "a color"?
3. How many pixels are in an `800 × 600` image?
4. How many pixels are in a `1600 × 1200` image?
5. How many times more pixel positions does `1600 × 1200` have compared with `800 × 600`?
6. If a `720p` video is upscaled to `1080p`, where do the new pixel values come from?
7. Does upscaling magically recover detail that wasn't present in the source?
8. What is the difference between resolution and bit depth?
9. What does `1920 × 1080` mean when FFmpeg reports it for a video?
10. How is a video related to a digital image?

---

# What to Learn Next

The natural next step is:

> **Chapter 2 — Resolution & Aspect Ratio**

There you can build on pixel dimensions and understand why:

```text
1920 × 1080
```

has a different shape from:

```text
1080 × 1080
```

and how **resolution, aspect ratio, display shape, scaling, and letterboxing/pillarboxing** are related.
