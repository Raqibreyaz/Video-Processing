# Chapter 5 — Resolution vs Bitrate

## What it is

**Resolution** tells us how many spatial samples (pixels) exist in each frame.

**Bitrate** tells us how much encoded data is available per second to represent the video.

The important question is:

> **If 1080p contains many more pixels than 720p, how can both videos use the same 10 Mbps?**

The answer is **compression**.

A video codec does not simply store every pixel independently. It uses patterns, predictions, transforms, and other techniques to represent the visual information efficiently.

---

## One-sentence summary

> **Resolution determines how much spatial detail can be represented, while bitrate determines how much encoded data is available to represent that information; compression allows videos with very different pixel counts to use the same bitrate.**

---

# 1. Compare the Visual Information

Let's compare:

```text
1080p @ 60 FPS
1920 × 1080
```

Pixels per frame:

```text
1920 × 1080
= 2,073,600 pixels
```

At 60 FPS:

```text
2,073,600 × 60
= 124,416,000
```

So there are approximately:

> **124 million pixel positions per second.**

Now consider:

```text
720p @ 60 FPS
1280 × 720
```

Pixels per frame:

```text
1280 × 720
= 921,600 pixels
```

At 60 FPS:

```text
921,600 × 60
= 55,296,000
```

So:

> **720p @ 60 FPS has about 55 million pixel positions per second.**

---

## Comparing Them

1080p has:

```text
2,073,600
──────────
  921,600
≈ 2.25
```

So:

> **1080p has 2.25× as many pixels per frame as 720p.**

This does **not**, however, mean that a 1080p video must use 2.25× the bitrate.

Why?

**Compression.**

---

# 2. Give Both Videos the Same Bitrate

Suppose:

```text
1080p → 10 Mbps
720p  → 10 Mbps
```

Both have approximately:

```text
10,000,000 bits/sec
```

available in their encoded streams.

But:

```text
1080p
    ↓
More pixels
    ↓
More spatial information
```

while:

```text
720p
    ↓
Fewer pixels
    ↓
Less spatial information
```

So you might ask:

> **Where did all the extra 1080p pixels go?**

They didn't disappear.

The key is:

> **The codec does not necessarily store every pixel independently.**

---

# 3. Compression Changes Everything

Consider a very simple image:

```text
████████████████
████████████████
████████████████
████████████████
```

There are many pixels here, but they are all very similar.

A naive representation might think:

```text
Pixel 1 = value X
Pixel 2 = value X
Pixel 3 = value X
Pixel 4 = value X
...
```

But that would waste data.

A compression system can instead represent the pattern more efficiently.

Conceptually:

```text
"Large region = same/similar value"
```

The exact representation depends on the compression algorithm, but the intuition is:

```text
Many pixels
    ↓
Lots of redundancy/patterns
    ↓
Compression
    ↓
Much less encoded data
```

Therefore:

> **Number of pixels ≠ number of bits required to represent them.**

This is one of the fundamental ideas behind compression.

---

# 4. Video Compression Goes Further

A video has another major source of redundancy:

> **Consecutive frames are often very similar.**

Imagine:

```text
Frame 1                 Frame 2

┌──────────────┐        ┌──────────────┐
│      ●       │        │       ●      │
│              │        │              │
└──────────────┘        └──────────────┘
```

Most of the image hasn't changed.

Only the object's position changed.

A video codec can therefore conceptually represent the second frame as:

```text
"Most of this frame is similar
to an earlier frame.
Here is the information that changed."
```

This is called **temporal compression**.

---

## Two Important Types of Redundancy

### Spatial redundancy

Redundancy **within a frame**.

Example:

```text
Large blue sky
Large flat wall
Repeated texture
```

The image contains nearby areas with similar information.

### Temporal redundancy

Redundancy **between frames**.

Example:

```text
Frame 1 → person standing
Frame 2 → person moves slightly
Frame 3 → person moves slightly again
```

Most of the scene remains unchanged.

Video codecs exploit both types.

---

# 5. Why 1080p and 720p Can Have the Same Bitrate

Let's simplify:

```text
1080p
More pixels
    ↓
More spatial information
    ↓
Compression
    ↓
10 Mbps
```

while:

```text
720p
Fewer pixels
    ↓
Less spatial information
    ↓
Compression
    ↓
10 Mbps
```

Both can therefore produce an encoded stream around:

```text
10 Mbps
```

The codec is simply doing different amounts of compression.

---

# 6. Don't Imagine Bits Being Assigned Directly to Pixels

A common mental model is:

```text
Pixel 1 → 5 bits
Pixel 2 → 5 bits
Pixel 3 → 5 bits
```

This is **not how modern video codecs work**.

Modern codecs use sophisticated representations involving concepts such as:

* Prediction
* Transforms
* Quantization
* Entropy coding
* Spatial information
* Temporal information

So saying:

> "720p gets more bits per pixel"

is useful as a rough comparison.

But it is **not literally how H.264 or similar codecs allocate bits**.

---

# 7. Bits Per Pixel — A Useful Metric

We can still calculate a useful comparison metric called **Bits Per Pixel (BPP)**.

A simplified formula is:

```text
BPP ≈
bitrate
────────────────────
width × height × FPS
```

For:

```text
1080p @ 60 FPS @ 10 Mbps
```

we get:

```text
10,000,000
────────────────────────────
1920 × 1080 × 60
```

Approximately:

```text
0.080 bits/pixel
```

For:

```text
720p @ 60 FPS @ 10 Mbps
```

we get:

```text
10,000,000
──────────────────────
1280 × 720 × 60
```

Approximately:

```text
0.181 bits/pixel
```

So:

```text
1080p → ~0.080 BPP
720p  → ~0.181 BPP
```

The 720p video has a much larger **average bit budget per pixel position**.

---

## Important Warning

Don't interpret BPP too literally.

The codec does **not** simply say:

```text
Every pixel gets exactly 0.181 bits.
```

Modern codecs work with compressed representations, predictions, blocks, transforms, and other structures.

So BPP is best treated as:

> **A useful comparison metric for bitrate efficiency, not a literal description of codec storage.**

---

# 8. Why Doesn't 720p Always Look Better?

At the same bitrate, 720p may have more encoded data available per pixel position.

But resolution itself still matters.

Compare:

```text
720p
████████████
```

with:

```text
1080p
████████████████████
```

The 1080p video has more spatial samples.

Therefore:

```text
Higher resolution
    ↓
More potential spatial detail
```

while:

```text
Higher bitrate
    ↓
More encoded data available
to represent that detail
```

These are different advantages.

---

# 9. The Resolution–Bitrate Trade-off

Think of it as a balance:

```text
                Resolution
                    ↕
             Spatial detail
                    ↕
                Bitrate
                    ↕
          Encoding efficiency
                    ↕
             Visual quality
```

If you increase resolution without giving the encoder enough bitrate, the additional pixels may not translate into useful additional detail.

For example:

```text
1080p @ very low bitrate
```

can look worse than:

```text
720p @ appropriate bitrate
```

because the 1080p stream may be heavily compressed.

So:

> **Higher resolution does not automatically mean higher perceived quality.**

---

# 10. Why Higher Resolution Usually Needs More Bitrate

Suppose we want comparable visual quality.

Compare:

```text
720p → 3 Mbps
1080p → 5 Mbps
```

This makes intuitive sense because 1080p has more spatial information to represent.

Conceptually:

```text
Higher resolution
       ↓
More spatial information
       ↓
More data may be needed
       ↓
Higher bitrate can help preserve quality
```

But this is **not an absolute rule**.

The required bitrate also depends on:

* Codec efficiency
* Encoder settings
* Scene complexity
* Motion
* Source quality
* Content type
* Desired quality level

A simple animation and a highly detailed sports scene can have very different bitrate requirements even at the same resolution and FPS.

---

# 11. This Explains Bitrate Ladders

This concept becomes very important in streaming.

A streaming service might create representations such as:

```text
1080p → 5 Mbps
720p  → 3 Mbps
480p  → 1.5 Mbps
360p  → 0.8 Mbps
```

These versions form a **quality/bitrate ladder**.

Why not simply use:

```text
1080p → 1 Mbps
720p  → 1 Mbps
480p  → 1 Mbps
360p  → 1 Mbps
```

Because higher resolutions generally need more bitrate to preserve their additional spatial detail effectively.

So a bitrate ladder balances:

```text
Resolution
    ↕
Visual quality
    ↕
Bitrate
    ↕
Network bandwidth
    ↕
File size
    ↕
Delivery cost
```

---

# 12. Connection to ABR Streaming

Now connect this to adaptive streaming.

Suppose the player has:

```text
Available network ≈ 2 Mbps
```

And the available representations are:

```text
720p → 3 Mbps
480p → 1.5 Mbps
360p → 0.8 Mbps
```

The player may choose:

```text
480p
```

because it requires less bandwidth than the 720p representation.

If the network improves:

```text
2 Mbps
   ↓
5 Mbps
```

the player may move to:

```text
720p
```

or potentially another higher-quality representation.

So in adaptive streaming:

> **Resolution and bitrate are closely connected.**

The player is effectively choosing between different combinations of:

```text
Resolution + Bitrate
```

based on network conditions, buffer state, device capability, and other factors.

---

# 13. Why Bitrate Is a Better File-Size Predictor Than Resolution

Consider:

```text
Video A
1080p
10 Mbps
5 minutes
```

and:

```text
Video B
720p
10 Mbps
5 minutes
```

Their resolutions are different.

Their FPS might even be different.

But because they have approximately the same bitrate and duration:

```text
File size ≈ bitrate × duration
```

their video-stream sizes will be roughly similar.

This is why:

> **Resolution does not directly determine final compressed file size.**

The codec compresses the visual information, and the encoded bitrate describes the resulting data rate.

---

# 14. The Full Encoding Pipeline

This is the mental model to remember:

```text
Source scene
    ↓
Camera / input
    ↓
Frames
    ↓
Resolution + FPS
    ↓
Visual information
    ↓
Codec
    ↓
Compression
    ↓
Encoded video stream
    ↓
Bitrate
    ↓
File size / bandwidth
```

Another useful view:

```text
Resolution
    ↓
Pixels per frame

FPS
    ↓
Frames per second

Resolution + FPS
    ↓
Amount of visual information

Codec
    ↓
Compresses the information

Bitrate
    ↓
Encoded bits per second

Duration
    ↓
Total encoded data
```

---

# 15. Raw Information vs Encoded Information

This distinction is extremely important.

Imagine:

```text
1920 × 1080 @ 60 FPS
```

Before compression, you have a huge amount of pixel data.

After compression, you might have:

```text
10 Mbps
```

These numbers describe different things.

### Raw representation

Describes the actual pixel information.

```text
Pixels
×
Frames
×
Bits per pixel
```

### Encoded representation

Describes compressed data.

```text
Compressed video
→
bits per second
→
bitrate
```

Therefore:

```text
Raw pixel data
       ≠
Encoded video data
```

This distinction will become even more important when you learn **pixel formats, bit depth, and raw video size**.

---

# 16. Important FFmpeg Connection

When working with FFmpeg, you may encounter:

```bash
ffmpeg -i input.mp4 -b:v 5M output.mp4
```

Here:

```text
-b:v 5M
```

specifies a video bitrate target/setting of approximately:

```text
5 Mbps
```

The encoder then tries to produce the encoded stream according to its rate-control behavior and other settings.

It does **not** mean:

```text
Every pixel receives 5 Mbps.
```

And it does not mean:

```text
Every frame gets exactly the same number of bits.
```

The actual distribution depends on the encoder and rate-control mode.

---

# 17. A Subtle but Important Point: Same Bitrate ≠ Same Quality

Consider:

```text
A: 1080p @ 10 Mbps
B: 720p  @ 10 Mbps
```

Same bitrate.

But quality is not automatically the same.

Now consider:

```text
A: H.264 @ 5 Mbps
B: More efficient codec @ 5 Mbps
```

Again, same bitrate does not guarantee the same quality.

Codec efficiency matters.

Similarly:

```text
Simple scene @ 5 Mbps
```

and:

```text
Complex scene @ 5 Mbps
```

can look very different.

Therefore:

> **Bitrate is a data-rate measurement, not a direct quality measurement.**

---

# Common Mistakes / Gotchas

## 1. "1080p must always use more bitrate than 720p."

No.

You can have:

```text
1080p → 5 Mbps
720p  → 10 Mbps
```

Bitrate is an encoding choice.

However, for similar quality, 1080p will often benefit from a higher bitrate.

---

## 2. "More pixels means proportionally more bits."

No.

Compression breaks that simple relationship.

A 1080p frame has 2.25× the pixels of a 720p frame, but the encoded stream does not have to use 2.25× the bitrate.

---

## 3. "Every pixel gets a fixed number of bits."

No.

BPP is a useful average metric, not a literal description of how modern codecs allocate data.

---

## 4. "Same bitrate means same quality."

No.

Quality depends on many factors:

```text
Codec
Encoder
Resolution
FPS
Scene complexity
Source quality
Encoding settings
```

---

## 5. "Higher resolution always looks better."

No.

A highly compressed 1080p video can look worse than a well-encoded 720p video.

Resolution provides the **potential** for more spatial detail. It doesn't guarantee that the detail survives compression.

---

## 6. "Compression only compares neighboring pixels."

No.

Video codecs can exploit both:

```text
Spatial redundancy
```

within frames and:

```text
Temporal redundancy
```

between frames.

---

## 7. "The bitrate is always exactly constant."

Not necessarily.

Depending on the encoding method, bitrate can vary over time.

For example:

```text
Time →
3 Mbps
5 Mbps
8 Mbps
4 Mbps
7 Mbps
```

This is common with variable-bitrate approaches.

So a stated bitrate can represent a target, average, or nominal value depending on context.

---

# Comparison Table

| Concept              | What it tells you                                      |
| -------------------- | ------------------------------------------------------ |
| Resolution           | Number of pixels per frame                             |
| FPS                  | Number of frames per second                            |
| Bitrate              | Encoded bits per second                                |
| BPP                  | Rough average bitrate budget per pixel position        |
| Compression          | How visual information is represented using fewer bits |
| Temporal compression | Uses similarities between frames                       |
| Spatial compression  | Uses similarities/patterns within frames               |
| File size            | Total encoded data over the duration                   |

---

# Core Mental Model

Remember this:

```text
RESOLUTION
    ↓
How many spatial samples exist?
    ↓
Pixels per frame


FPS
    ↓
How many temporal samples exist?
    ↓
Frames per second


RESOLUTION + FPS
    ↓
Amount of visual information
```

Then:

```text
Visual information
        ↓
Codec
        ↓
Compression
        ↓
Encoded representation
        ↓
Bitrate
        ↓
File size / bandwidth
```

The most important statement is:

> **More pixels do not automatically mean proportionally more encoded data because video codecs compress the visual information. However, higher resolution generally requires more bitrate to preserve comparable visual quality.**

---

# Worked Exercise

Given:

```text
A: 1920 × 1080 @ 30 FPS @ 6 Mbps

B: 1280 × 720 @ 30 FPS @ 6 Mbps
```

## 1. Pixels per frame — A

```text
1920 × 1080
= 2,073,600 pixels
```

## 2. Pixels per frame — B

```text
1280 × 720
= 921,600 pixels
```

## 3. Which has more pixels?

A:

```text
2,073,600
```

B:

```text
921,600
```

Ratio:

```text
2,073,600
───────────
  921,600
= 2.25
```

Therefore:

> **A has 2.25× more pixels per frame than B.**

Because both are 30 FPS, A also has 2.25× more pixel positions sampled per second.

---

## 4. Which has the higher rough BPP budget?

Both have:

```text
6 Mbps
```

and:

```text
30 FPS
```

So the difference comes from resolution.

For A:

```text
6,000,000
────────────────────────────
1920 × 1080 × 30
```

≈

```text
0.096 bits/pixel
```

For B:

```text
6,000,000
──────────────────────
1280 × 720 × 30
```

≈

```text
0.217 bits/pixel
```

Therefore:

```text
A → ~0.096 BPP
B → ~0.217 BPP
```

So:

> **B (720p) has the higher rough bits-per-pixel budget at the same 6 Mbps.**

Again, this is an average comparison metric. It does **not** mean the codec literally gives every 720p pixel 0.217 bits.

---

# Key Takeaways

* **Resolution** determines pixels per frame.
* **FPS** determines frames per second.
* **Bitrate** determines encoded bits per second.
* 1080p has **2.25× more pixels** per frame than 720p.
* More pixels do **not** require proportionally more encoded bits because codecs compress the visual information.
* Compression exploits redundancy within frames and across frames.
* **Spatial compression** exploits patterns within an image.
* **Temporal compression** exploits similarities between consecutive frames.
* The codec does not simply assign a fixed number of bits to every pixel.
* **BPP** is useful for comparison but is not a literal description of codec storage.
* At the same bitrate, a lower-resolution video has a higher average bit budget per pixel position.
* Higher resolution provides the potential for more spatial detail.
* Higher bitrate gives the encoder more encoded-data budget to preserve visual information.
* Higher resolution often needs higher bitrate for comparable quality.
* Same bitrate does not mean same visual quality.
* Same resolution does not guarantee the same quality either.
* Codec efficiency and scene complexity matter.
* Bitrate ladders balance resolution, quality, bandwidth, and cost.
* ABR players select among different resolution/bitrate representations based on conditions.
* Resolution and FPS describe the **visual information being sampled**.
* Bitrate describes the **compressed representation of that information**.
* For a given duration, average bitrate is a much more direct predictor of compressed video-stream size than resolution alone.

---

# Minimal Self-Test

1. Why can 1080p and 720p both use 10 Mbps?
2. Does 1080p having 2.25× more pixels mean it needs 2.25× the bitrate?
3. What is spatial compression?
4. What is temporal compression?
5. Why isn't BPP a literal description of how a codec stores pixels?
6. At the same bitrate and FPS, which has a higher rough BPP: 1080p or 720p?
7. Can 720p at 10 Mbps look better than 1080p at 5 Mbps?
8. Does higher resolution automatically mean higher bitrate?
9. What factors besides bitrate affect video quality?
10. Why are bitrate ladders useful in ABR streaming?
11. What is the difference between raw pixel data and encoded video data?
12. Why does bitrate matter for both streaming bandwidth and file size?

---

# What to Learn Next

The next logical step is to understand **what a pixel actually contains before compression**.

So the next layer is:

```text
Pixel
  ↓
Color representation
  ↓
Channels
  ↓
Bit depth
  ↓
RGB vs YUV
  ↓
Pixel formats
  ↓
Raw frame size
  ↓
Raw video size
  ↓
Why compression is necessary
```

This will answer an important question:

> **If a frame contains millions of pixels, how many bytes does one uncompressed frame actually require?**

Once you understand that, the huge difference between **raw video data** and **compressed video bitrate** will become much more intuitive.
