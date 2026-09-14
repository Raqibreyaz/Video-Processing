# Chapter 6 — Bit Depth & Color

## What it is

A pixel represents image information at a particular location. To represent **color**, a computer needs numerical values.

A simple and common model is **RGB**:

```text
R = Red
G = Green
B = Blue
```

For example:

```text
Pixel
 ├── Red value
 ├── Green value
 └── Blue value
```

If:

```text
R = 255
G = 0
B = 0
```

the pixel is pure red.

If:

```text
R = 0
G = 0
B = 255
```

the pixel is pure blue.

---

## One-sentence summary

> **Bit depth determines how precisely color-channel values can be represented, while RGB uses separate red, green, and blue channel values to describe a pixel's color.**

---

# 1. Pixel vs Channel

This distinction is very important.

## Pixel

A **pixel** represents one spatial location in an image.

```text
Image
┌───┬───┬───┐
│ P │ P │ P │
├───┼───┼───┤
│ P │ P │ P │
├───┼───┼───┤
│ P │ P │ P │
└───┴───┴───┘
```

Each `P` is one pixel.

Think:

> **Pixel = where?**

---

## Channel

A **channel** is one component of the color representation.

For RGB:

```text
One Pixel
   │
   ├── Red
   ├── Green
   └── Blue
```

For example:

```text
R = 200
G = 100
B = 50
```

These three values together describe the pixel's color.

Think:

> **Channel = what kind of value?**

---

## Bit depth

Bit depth tells us how many bits are available to represent a value.

Think:

> **Bit depth = how precisely can that value be represented?**

So the mental model is:

```text
Pixel
  ↓
location in the image

Channel
  ↓
component of the color representation

Bit depth
  ↓
precision/range of that component
```

---

# 2. RGB Color Model

RGB represents a color using three channels:

```text
R → Red
G → Green
B → Blue
```

A pixel could therefore be:

```text
R = 255
G = 0
B = 0
```

→ pure red

```text
R = 0
G = 255
B = 0
```

→ pure green

```text
R = 0
G = 0
B = 255
```

→ pure blue

And:

```text
R = 255
G = 255
B = 255
```

→ white

while:

```text
R = 0
G = 0
B = 0
```

→ black.

Other colors are combinations of the three channels.

For example:

```text
R = 255
G = 255
B = 0
```

produces yellow.

---

# 3. What Does 8-Bit Mean?

Suppose each RGB channel uses **8 bits**.

Remember:

```text
8 bits = 1 byte
```

Therefore:

```text
Red   → 8 bits → 1 byte
Green → 8 bits → 1 byte
Blue  → 8 bits → 1 byte
```

So:

```text
One RGB pixel
= 8 + 8 + 8 bits
= 24 bits
= 3 bytes
```

This is where the common **3 bytes/pixel** assumption comes from.

---

# 4. Why Does 8 Bits Give 0–255?

An 8-bit value has:

```text
2⁸ = 256
```

possible combinations.

Because we start counting from zero:

```text
0 → 255
```

That gives exactly 256 possible values.

Therefore, with 8-bit RGB:

```text
R = 0–255
G = 0–255
B = 0–255
```

Each channel has 256 possible values.

---

# 5. How Many Colors Can One Pixel Represent?

Each channel independently has 256 possible values.

Therefore:

```text
256 × 256 × 256
```

which gives:

```text
16,777,216
```

So 8-bit-per-channel RGB can represent approximately:

> **16.7 million possible RGB colors per pixel.**

This is also called:

> **24-bit color**

because:

```text
8 bits R
+ 8 bits G
+ 8 bits B
──────────
24 bits
```

And:

```text
24 bits ÷ 8
= 3 bytes
```

---

# 6. Connecting Color to Frame Size

Now we can finally understand the earlier **3 bytes/pixel** assumption.

Suppose we have an uncompressed RGB frame:

```text
1280 × 720
```

Number of pixels:

```text
1280 × 720
= 921,600 pixels
```

With 3 bytes per pixel:

```text
921,600 × 3
= 2,764,800 bytes
```

So one uncompressed 1280×720 RGB frame requires approximately:

> **2.76 MB**

using decimal MB for this rough calculation.

At 30 FPS:

```text
2,764,800 × 30
= 82,944,000 bytes/sec
```

Approximately:

> **82.9 MB/sec**

So uncompressed video becomes extremely large very quickly.

---

# 7. From One Frame to Raw Video

The general idea is:

```text
Pixels per frame
        ×
Bytes per pixel
        ↓
Bytes per frame
```

Then:

```text
Bytes per frame
        ×
FPS
        ↓
Bytes per second
```

Then:

```text
Bytes per second
        ×
Duration
        ↓
Total raw video size
```

For simple RGB:

```text
Width × Height × 3 × FPS × Duration
```

gives the approximate raw video size.

For example:

```text
1280 × 720
× 3 bytes
× 30 FPS
× 60 seconds
```

This is dramatically larger than a typical compressed video.

That huge difference is one of the main reasons **video compression is necessary**.

---

# 8. What Is Bit Depth?

Bit depth tells us how many bits are available to represent a value.

The number of possible values is:

```text
2^(bit depth)
```

Examples:

| Bit depth | Possible values |
| --------: | --------------: |
|     8-bit |             256 |
|    10-bit |           1,024 |
|    12-bit |           4,096 |
|    16-bit |          65,536 |

So:

```text
8-bit
→ 2⁸
→ 256 values
```

while:

```text
10-bit
→ 2¹⁰
→ 1,024 values
```

and:

```text
12-bit
→ 2¹²
→ 4,096 values
```

---

# 9. What Does More Bit Depth Actually Give Us?

More bit depth gives us **more possible steps between values**.

Imagine a brightness gradient:

```text
BLACK ───────────────────────── WHITE
```

With fewer possible values, the transition has fewer available steps.

With more values:

```text
BLACK
  ↓
very dark
  ↓
dark
  ↓
slightly dark
  ↓
...
  ↓
slightly light
  ↓
light
  ↓
WHITE
```

This gives the system more precision when representing gradual changes.

This can be useful for:

* Smooth gradients
* Color grading
* Reducing visible banding
* Preserving subtle differences in color/brightness

---

# 10. Bit Depth Is NOT Resolution

Keep this distinction very clear.

### Resolution

Answers:

> **How many pixels are there?**

```text
1920 × 1080
```

means:

```text
2,073,600 pixels
```

### Bit depth

Answers:

> **How many possible values can each channel represent?**

For example:

```text
8-bit
```

means:

```text
256 possible values/channel
```

So:

```text
1920 × 1080
8-bit RGB
```

has:

```text
2,073,600 pixels
```

with:

```text
8 bits R
8 bits G
8 bits B
```

Changing it to:

```text
1920 × 1080
10-bit RGB
```

does **not** create more pixels.

It keeps:

```text
1920 × 1080
```

but gives each channel more possible values:

```text
8-bit  → 256 values
10-bit → 1,024 values
```

---

# 11. Simple Analogy

Imagine you're drawing on graph paper.

## Resolution = number of places

Compare:

```text
100 × 100
```

with:

```text
1000 × 1000
```

The second has many more grid positions.

Therefore:

> **Resolution = how many places do I have to describe the image?**

---

## Bit depth = precision at each place

Now imagine each position can choose from:

```text
256 shades
```

or:

```text
1,024 shades
```

The second gives you finer control over the value.

Therefore:

> **Bit depth = how precisely can I describe the value at each place?**

---

## Mental model

```text
Resolution
    ↓
How many places?

Bit depth
    ↓
How precise is the value?

Pixel
    ↓
One place

Channel
    ↓
One component of the value
```

---

# 12. 8-Bit RGB vs 10-Bit RGB

Consider:

```text
8-bit RGB
```

Each pixel has:

```text
R → 8 bits
G → 8 bits
B → 8 bits
```

Total:

```text
24 bits/pixel
```

or:

```text
3 bytes/pixel
```

Now consider:

```text
10-bit RGB
```

Each channel has:

```text
R → 10 bits
G → 10 bits
B → 10 bits
```

Total:

```text
30 bits/pixel
```

Conceptually:

```text
8-bit RGB
→ 24 bits/pixel

10-bit RGB
→ 30 bits/pixel
```

However, **real video formats may pack and store these values differently**, so don't assume that every 10-bit video file literally uses exactly 30 bits per pixel in memory or storage.

That distinction becomes important when we study **pixel formats**.

---

# 13. Why 10-Bit Video Matters

Consider a smooth gradient:

```text
BLACK ───────────────────────── WHITE
```

If the representation has limited precision, some gradual changes may have to be approximated using larger steps.

Those steps can sometimes become visible as **banding**:

```text
████
████
████
████
```

instead of a smooth transition.

More bit depth provides more available values:

```text
8-bit
→ 256 values/channel

10-bit
→ 1,024 values/channel
```

This can make gradual transitions easier to represent and can provide more room for **color grading**.

---

# 14. Bit Depth and Color Grading

Suppose you're editing a video and want to make significant color adjustments.

With more available values, there is more precision available for representing intermediate colors and brightness levels.

Conceptually:

```text
Original
   ↓
Color grading
   ↓
Adjusted values
```

If the source has very limited precision, aggressive adjustments can make quantization or banding more noticeable.

Higher bit depth gives the workflow more numerical precision.

This doesn't mean:

> **10-bit automatically makes every video look better.**

The source, codec, display, processing pipeline, and final output all matter.

---

# 15. A Very Important Distinction: Channel Bit Depth

When we say:

```text
8-bit video
```

we often need to ask:

> **8 bits per what?**

In this chapter's simple RGB model, we're talking about:

```text
8 bits per channel
```

So:

```text
R = 8 bits
G = 8 bits
B = 8 bits
```

Likewise:

```text
10-bit RGB
```

means:

```text
10 bits per channel
```

This distinction becomes especially important when we move to **YUV**, because YUV does not represent color as simple RGB channels.

---

# 16. Why This Matters for Video

Now connect everything we've learned:

```text
Image
  ↓
Pixels
  ↓
Each pixel has color information
  ↓
Color is represented using channels
  ↓
Each channel has a bit depth
  ↓
Pixel values become numerical data
```

For simple 8-bit RGB:

```text
Pixel
 ├── R → 8 bits
 ├── G → 8 bits
 └── B → 8 bits
```

Therefore:

```text
24 bits/pixel
= 3 bytes/pixel
```

And:

```text
Resolution × bytes/pixel
        ↓
Raw frame size
```

Then:

```text
Raw frame size × FPS
        ↓
Raw data rate
```

This is the bridge toward understanding why raw video is so large.

---

# 17. Raw Video vs Compressed Video

This distinction is becoming important now.

### Raw RGB video

You can roughly calculate:

```text
Width × Height × bytes/pixel × FPS
```

For example:

```text
1920 × 1080
× 3 bytes
× 30 FPS
```

≈

```text
186 MB/sec
```

That is enormous.

### Compressed video

A codec can compress this information into something like:

```text
5 Mbps
```

or:

```text
10 Mbps
```

depending on the encoding.

So:

```text
Raw pixel data
        ↓
Compression
        ↓
Encoded video
```

This is why:

```text
1920 × 1080 RGB @ 30 FPS
```

does **not** mean the final video file must consume hundreds of MB every second.

The codec removes/reduces redundancy and represents the visual information much more efficiently.

---

# 18. Common Mistakes / Gotchas

## Mistake 1: "More bit depth means more pixels."

No.

```text
Resolution → number of pixels

Bit depth → number of possible values
```

---

## Mistake 2: "A pixel and a channel are the same thing."

No.

```text
Pixel
→ one spatial location

Channel
→ one component of the color representation
```

For RGB:

```text
One pixel
→ R + G + B values
```

---

## Mistake 3: "8-bit means only 8 colors."

No.

An 8-bit channel has:

```text
2⁸ = 256 values
```

And 8-bit RGB has:

```text
256³
= 16,777,216
```

possible RGB color combinations.

---

## Mistake 4: "10-bit means 10 colors."

No.

A 10-bit channel has:

```text
2¹⁰
= 1,024 values
```

---

## Mistake 5: "10-bit RGB always means exactly 30 bits in the video file for every pixel."

Not necessarily.

The simple mathematical model gives:

```text
10 + 10 + 10
= 30 bits/pixel
```

But actual video pixel formats can pack data differently.

This is why **pixel format** is an important topic we will study later.

---

## Mistake 6: "Higher bit depth automatically makes a video look better."

Not necessarily.

It provides more possible values and can improve precision, but final quality also depends on:

* Source quality
* Resolution
* Codec
* Bitrate
* Encoding
* Display
* Color pipeline
* Content

---

## Mistake 7: "Bit depth and bitrate are the same thing."

They are completely different.

```text
Bit depth
    ↓
Bits used to represent a value

Bitrate
    ↓
Bits used/transmitted per second
```

For example:

```text
10-bit
```

describes precision.

```text
10 Mbps
```

describes a data rate.

---

# Comparison Table

| Concept          | Meaning                                   |
| ---------------- | ----------------------------------------- |
| Pixel            | One spatial location/sample               |
| Channel          | One component of the color representation |
| RGB              | Red + Green + Blue color model            |
| Bit depth        | Number of bits available for a value      |
| 8-bit channel    | 256 possible values                       |
| 10-bit channel   | 1,024 possible values                     |
| Resolution       | Number of pixels in width × height        |
| Bitrate          | Encoded bits per second                   |
| 8-bit RGB pixel  | 24 bits = 3 bytes in the simple model     |
| 10-bit RGB pixel | 30 bits in the simple mathematical model  |
| 24-bit color     | 8 bits each for R, G, B                   |

---

# Core Mental Model

Keep these concepts separate:

```text
RESOLUTION
    ↓
How many pixels?
```

```text
PIXEL
    ↓
One spatial location
```

```text
CHANNEL
    ↓
One component of the color representation
```

```text
BIT DEPTH
    ↓
How many possible values for that channel?
```

```text
FPS
    ↓
How many frames per second?
```

```text
BITRATE
    ↓
How many encoded bits per second?
```

Put them together:

```text
Resolution
    ↓
Number of pixels

Pixel
    ↓
Contains channel values

Channel
    ↓
Has a certain bit depth

Pixel values
    ↓
Raw image data

Raw frames
    ↓
FPS

Raw video
    ↓
Codec/compression

Compressed video
    ↓
Bitrate
```

---

# Worked Example

Consider:

```text
1280 × 720
30 FPS
8-bit RGB
```

### Step 1 — Pixels per frame

```text
1280 × 720
= 921,600 pixels
```

### Step 2 — Bytes per pixel

8-bit RGB:

```text
8 + 8 + 8
= 24 bits
= 3 bytes
```

### Step 3 — Bytes per frame

```text
921,600 × 3
= 2,764,800 bytes
```

≈ **2.76 MB/frame**

### Step 4 — Raw data rate

At 30 FPS:

```text
2,764,800 × 30
= 82,944,000 bytes/sec
```

≈ **82.9 MB/sec**

### Step 5 — Why compression is needed

Without compression, the raw data rate is enormous.

A codec can compress the video into a much smaller encoded stream, for example:

```text
Raw video
≈ 82.9 MB/sec

        ↓ compression

Encoded video
≈ a few Mbps
```

The exact bitrate depends on the content and encoding settings.

---

# Key Takeaways

* A **pixel** represents a spatial location in an image.
* A **channel** is one component of the color representation.
* RGB uses three channels: **Red, Green, Blue**.
* With 8-bit RGB, each channel has **256 possible values**.
* 8-bit RGB therefore has **16,777,216 possible RGB color combinations**.
* 8 bits × 3 channels = **24 bits = 3 bytes** in the simple RGB model.
* **Bit depth** controls the precision/range of channel values.
* 8-bit → 256 values/channel.
* 10-bit → 1,024 values/channel.
* 12-bit → 4,096 values/channel.
* Higher bit depth can help represent smooth gradients and provide more precision for color grading.
* **Bit depth is not resolution.**
* **Bit depth is not bitrate.**
* Increasing resolution creates more pixels.
* Increasing bit depth gives each channel more possible values.
* Actual video formats may store pixel data differently from the simple RGB model.
* Raw video can be extremely large.
* Compression converts huge raw pixel data into a much smaller encoded stream.
* This chapter's **3 bytes/pixel** model is specifically for simple **8-bit RGB**, not all video formats.

---

# Minimal Self-Test

1. What is the difference between a pixel and a channel?
2. What are the three channels in RGB?
3. Why does an 8-bit value have 256 possible values?
4. How many possible RGB colors can an 8-bit-per-channel RGB pixel represent?
5. How many bytes does an 8-bit RGB pixel use in the simple model?
6. What does 10-bit-per-channel mean?
7. Does moving from 8-bit to 10-bit increase resolution?
8. What is the difference between bit depth and bitrate?
9. Why can higher bit depth help with gradients and color grading?
10. Why can't we assume every 10-bit video uses exactly 30 bits per pixel?
11. Why is raw video much larger than compressed video?
12. For `1280×720, 30 FPS, 8-bit RGB`, approximately how many MB/sec of raw data are produced?

---

# What to Learn Next

The next important step is **YUV and chroma subsampling**.

So the progression becomes:

```text
RGB
 ↓
Why RGB isn't the whole story for video
 ↓
YUV
 ↓
Luma + Chroma
 ↓
Why human vision allows chroma compression
 ↓
4:4:4
 ↓
4:2:2
 ↓
4:2:0
 ↓
Actual video pixel formats
 ↓
Raw frame size in real video
```

This is where video starts to differ significantly from the simple **3 bytes per pixel RGB** model.
