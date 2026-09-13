# Chapter 4 — Bitrate

## What it is

A **bitrate** tells us how much digital data is used or transmitted **per second**.

For video:

> **Video bitrate = amount of encoded video data per second.**

For example:

```text
5 Mbps
```

means approximately:

```text
5 million bits per second
```

Bitrate is one of the most important concepts in video because it connects directly to:

* File size
* Streaming bandwidth
* HLS
* Adaptive Bitrate (ABR)
* CDN costs
* Video quality
* FFmpeg encoding

---

## One-sentence summary

> **Bitrate is the amount of encoded data used per second; for a roughly constant bitrate, file size is approximately bitrate × duration, while resolution and FPS describe how much visual information the video contains.**

---

# 1. First: What is a Bit?

A **bit** is the smallest basic unit of digital information.

It can have two possible values:

```text
0
1
```

So:

```text
1 bit → either 0 or 1
```

Eight bits make one byte:

```text
8 bits = 1 byte
```

This distinction is important because video bitrate is normally measured in **bits**, while file sizes are commonly expressed in **bytes**.

---

## Bits vs Bytes

Remember:

```text
b → bit
B → Byte
```

Therefore:

```text
8 bits = 1 Byte
```

Common storage units:

```text
KB
MB
GB
```

Common video/network bitrate units:

```text
Kbps
Mbps
Gbps
```

For example:

```text
8 Mbps
```

means:

```text
8 megabits/second
```

not:

```text
8 megabytes/second
```

To approximately convert bits to bytes:

```text
bits ÷ 8 = bytes
```

---

# 2. What is Bitrate?

The word **rate** means "amount per unit of time."

Therefore:

```text
Bitrate = bits / second
```

For example:

```text
5 Mbps
```

means approximately:

```text
5 million bits every second
```

The important part is:

> **per second**

That's why bitrate is a rate.

```text
      bits
Bitrate = ──────
      second
```

---

# 3. Video Bitrate

When we say:

```text
Video bitrate = 5 Mbps
```

we are roughly saying:

> The encoded video stream uses about 5 million bits of data every second.

For a 10-second video:

```text
5 Mbps × 10 seconds
= 50 megabits
```

Now convert bits to bytes:

```text
50 megabits ÷ 8
= 6.25 megabytes
```

So the video stream is approximately:

```text
6.25 MB
```

for those 10 seconds.

### Important

This is an approximation for the **video stream itself**.

A real media file can also contain:

* Audio
* Container metadata
* Headers
* Other stream information
* Container overhead

Therefore, the actual file size can be different.

---

# 4. The Basic File-Size Relationship

For a roughly constant bitrate:

```text
File size ≈ Bitrate × Duration
```

When converting bits to bytes:

```text
File size in bytes
≈
Bitrate in bits/sec × Duration in seconds ÷ 8
```

So the most useful formula is:

```text
File size ≈ bitrate × duration ÷ 8
```

---

## Example: 8 Mbps for 60 seconds

```text
8 Mbps × 60 seconds
= 480 megabits
```

Convert to megabytes:

```text
480 ÷ 8
= 60 MB
```

So:

> **1 minute of video at 8 Mbps is approximately 60 MB of video data.**

---

# 5. Why Does Bitrate Affect File Size?

Suppose we have two videos:

```text
Video A → 2 Mbps
Video B → 10 Mbps
```

Assume both have the same duration.

Video B is allowed to use much more encoded data every second.

Therefore:

```text
Higher bitrate
      ↓
More encoded bits per second
      ↓
Usually larger file
```

While:

```text
Lower bitrate
      ↓
Fewer encoded bits per second
      ↓
Usually smaller file
```

For the same duration, doubling the average bitrate approximately doubles the video-stream size.

---

# 6. Bitrate Is NOT "Amount of Color"

This is an important correction.

It is tempting to think:

> "Bitrate tells us how much color each pixel gets."

That is not what bitrate means.

Bitrate is:

> **The amount of encoded data available to represent the video over time.**

The encoder decides how those bits are used.

For example, consider:

```text
Scene A
Simple blue sky
```

and:

```text
Scene B
Fast-moving crowd
with lots of detail
```

The second scene may require more encoded information to maintain similar visual quality.

The encoder therefore has to decide how to spend its available bits.

Conceptually:

```text
Visual information
        ↓
      Encoder
        ↓
 ┌──────┴──────┐
 ▼             ▼
Simple       Complex
scene        scene
 ▼             ▼
fewer bits   more bits
```

The exact behavior depends on the codec and rate-control mode, but this is the correct intuition.

---

# 7. Bitrate vs Resolution

This is one of the most important distinctions in video.

Consider:

```text
1080p
60 FPS
10 Mbps
```

and:

```text
720p
60 FPS
10 Mbps
```

Both have the same approximate bitrate:

```text
10 Mbps
```

But their resolutions are different.

### 1080p

```text
1920 × 1080
```

Pixel positions per frame:

```text
1920 × 1080
= 2,073,600
```

At 60 FPS:

```text
2,073,600 × 60
= 124,416,000
```

pixel positions per second.

---

### 720p

```text
1280 × 720
```

Pixel positions per frame:

```text
1280 × 720
= 921,600
```

At 60 FPS:

```text
921,600 × 60
= 55,296,000
```

pixel positions per second.

---

So:

```text
1080p @ 60 FPS
≈ 124 million pixel positions/sec

720p @ 60 FPS
≈ 55 million pixel positions/sec
```

Yet both have:

```text
10 million bits/sec
```

of encoded data budget.

This means the encoder is representing very different amounts of visual information using approximately the same number of bits per second.

---

# 8. Why Bitrate Alone Doesn't Tell You Quality

Suppose we compare:

```text
Video A:
1080p
10 Mbps
```

and:

```text
Video B:
720p
10 Mbps
```

The bitrate is identical.

But that does **not** mean the visual quality is identical.

The 1080p video has more spatial information to represent.

Likewise, two videos with the same resolution and bitrate can look different because of:

* Codec
* Encoder settings
* Scene complexity
* Motion
* Source quality
* Compression efficiency
* Rate-control strategy

So:

> **Bitrate alone does not determine video quality.**

---

# 9. Bitrate and Network Bandwidth

Now the concept becomes important for streaming.

Suppose a video requires:

```text
5 Mbps
```

and the user's network can sustainably deliver:

```text
10 Mbps
```

The network has enough capacity to download the video stream at the required rate, assuming other conditions are favorable.

Conceptually:

```text
Video needs
   5 Mbps
      │
      ▼
Network provides
  10 Mbps
      │
      ▼
Enough capacity
```

But consider:

```text
Video needs
   5 Mbps
      │
      ▼
Network provides
   2 Mbps
```

Now the network cannot continuously deliver data as quickly as the video consumes it.

Conceptually:

```text
Video consumption
       5 Mbps
          │
          ▼
      [Buffer]
          ▲
          │
Network delivery
       2 Mbps

Delivery < Consumption
        ↓
Buffer decreases
        ↓
Eventually
        ↓
Buffering
```

This is one of the reasons streaming systems use **Adaptive Bitrate (ABR)**.

---

# 10. Bitrate and ABR

Imagine a streaming service has several versions of the same video:

```text
1080p → 8 Mbps
720p  → 5 Mbps
480p  → 2 Mbps
360p  → 1 Mbps
```

If the user's network can comfortably support 8 Mbps, the player may use the 1080p representation.

If the network becomes poor:

```text
8 Mbps
  ↓
5 Mbps
  ↓
2 Mbps
```

the player can switch to lower-bitrate representations.

The goal is to balance:

```text
Video quality
      ↕
Available bandwidth
      ↕
Buffer stability
```

This is the connection between bitrate and the ABR systems you'll encounter later with HLS and similar streaming technologies.

---

# 11. Bitrate, FPS, and Resolution Are Different

Keep this table in your notes:

| Property   | Meaning                 |
| ---------- | ----------------------- |
| Resolution | Pixels per frame        |
| FPS        | Frames per second       |
| Bitrate    | Encoded bits per second |

For example:

```text
1920 × 1080
60 FPS
10 Mbps
```

means approximately:

```text
Each frame
    ↓
1920 × 1080 pixels

Every second
    ↓
60 frames

Encoded stream
    ↓
~10 million bits/sec
```

These are **three different properties**.

---

# 12. A Better Mental Model

Think about a video in three layers:

```text
                 VIDEO
                   │
       ┌───────────┼───────────┐
       ▼           ▼           ▼
   Resolution     FPS       Bitrate
       │           │           │
       ▼           ▼           ▼
  Pixels/frame  Frames/sec  Bits/sec
       │           │           │
       ▼           ▼           ▼
    Spatial      Temporal     Encoded
  information  information     data
```

This is one of the most useful mental models to keep.

---

# 13. Resolution + FPS → Visual Information

From the previous chapters:

```text
Resolution
    ↓
Pixels per frame

FPS
    ↓
Frames per second
```

Together, they give us an intuition for how much visual information is being sampled:

```text
Resolution × FPS
        ↓
Pixel positions sampled per second
```

For example:

```text
1920 × 1080 @ 60 FPS
```

gives:

```text
2,073,600 pixels/frame
×
60 frames/sec
=
124,416,000 pixel positions/sec
```

But these are **not necessarily 124 million independently stored values in the encoded file**.

Why?

Because video compression removes redundancy and represents the visual information much more efficiently.

That leads directly to codecs and compression.

---

# 14. Why Resolution and FPS Aren't Directly in the Basic File-Size Formula

You might wonder:

> If resolution and FPS affect the amount of visual information, why isn't the basic file-size formula something like `resolution × FPS × duration`?

Because bitrate describes the **encoded data rate after compression**.

The basic relationship is:

```text
File size
≈
Encoded bitrate × Duration
```

The larger process is:

```text
Resolution + FPS
        ↓
Amount of visual information
        ↓
Codec / compression
        ↓
Encoded stream
        ↓
Bitrate
        ↓
File size
```

So resolution and FPS influence the encoding problem, but the final file size is primarily determined by the amount of encoded data produced over time.

---

# 15. Same Bitrate, Different Resolution

Consider:

```text
Video A
1080p
60 FPS
10 Mbps
```

and:

```text
Video B
720p
30 FPS
10 Mbps
```

Assuming the same duration and roughly the same average bitrate:

> **Their video-stream sizes will be roughly the same.**

Why?

Because:

```text
File size ≈ bitrate × duration
```

The first video contains more pixels and more frames per second, but its encoder is still producing approximately:

```text
10 million bits/sec
```

The compression system has to represent that information within that data budget.

---

# 16. Higher Resolution/FPS Often Needs More Bitrate

There is another important distinction.

Higher resolution or higher FPS does **not automatically force** a higher bitrate.

You can technically have:

```text
1080p @ 10 Mbps
```

and:

```text
720p @ 10 Mbps
```

But if you want similar visual quality, the higher-resolution/higher-FPS video will often need more bitrate.

Why?

Because it has more visual information to represent.

Conceptually:

```text
More resolution
      +
More FPS
      ↓
More visual information
      ↓
Potentially more encoded bits needed
      ↓
Higher bitrate may be useful
```

But this is not an absolute mathematical rule.

Codec efficiency and scene complexity matter too.

---

# 17. Constant vs Variable Bitrate

There is another distinction you will encounter later.

### Constant Bitrate — CBR

The encoder attempts to maintain a relatively consistent bitrate.

Conceptually:

```text
Time →
10 10 10 10 10 10 10
Mbps
```

### Variable Bitrate — VBR

The bitrate can vary depending on the content.

For example:

```text
Time →
3   5   9   4   8   3
Mbps
```

A simple scene might need fewer bits.

A complex scene might need more.

This is why saying:

> "The video is 5 Mbps"

can sometimes be shorthand for an **average or target bitrate**, depending on the encoding mode and context.

---

# 18. Bitrate Can Be Average or Target-Oriented

When dealing with real encoders, bitrate terminology can become more nuanced.

For example, an encoder may be configured with a target:

```text
5 Mbps
```

but individual moments of the video may use more or fewer bits depending on the rate-control strategy.

So:

```text
5 Mbps
```

does not always mean:

```text
Every single second = exactly 5,000,000 bits
```

Instead, it may represent a target or average depending on the encoding mode.

This distinction becomes important when you study:

* CBR
* VBR
* CRF
* Two-pass encoding
* Rate control
* VBV

---

# 19. Connection to FFmpeg

You may eventually use a command such as:

```bash
ffmpeg -i input.mp4 -b:v 5M output.mp4
```

Here:

```text
-b:v 5M
```

is used to specify a target video bitrate of approximately:

```text
5 Mbps
```

The important idea is:

> You are giving the video encoder a bitrate-related constraint/target for the video stream.

The exact behavior depends on the codec and other encoder settings.

---

# 20. What if the Input Is Already 5 Mbps?

Suppose the source is:

```text
Input:
5 Mbps
```

and you encode it again with:

```text
-b:v 10M
```

You might think:

> "The quality will automatically double."

Not necessarily.

The source has already gone through its previous encoding/compression process.

If information was lost during the original compression, increasing the bitrate during a later encode cannot magically recover it.

```text
Original high-quality source
        ↓
5 Mbps encoding
        ↓
Information may be lost
        ↓
10 Mbps re-encoding
```

The 10 Mbps output may be larger, but it does not automatically contain the detail that was already discarded.

This is another reason why **source quality matters**.

---

# 21. Bitrate and File Size: Worked Examples

## Example 1 — 5 Mbps for 10 seconds

```text
5 Mbps × 10
= 50 megabits
```

Convert:

```text
50 ÷ 8
= 6.25 MB
```

Approximate video-stream size:

> **6.25 MB**

---

## Example 2 — 8 Mbps for 2 minutes

Two minutes:

```text
2 × 60
= 120 seconds
```

Data:

```text
8 Mbps × 120
= 960 megabits
```

Convert:

```text
960 ÷ 8
= 120 MB
```

Approximate:

> **120 MB**

---

## Example 3 — 16 Mbps for 2 minutes

```text
16 × 120
= 1,920 megabits
```

Convert:

```text
1,920 ÷ 8
= 240 MB
```

So doubling:

```text
8 Mbps → 16 Mbps
```

while keeping duration unchanged approximately doubles:

```text
120 MB → 240 MB
```

---

# 22. A Practical File-Size Formula

For quick calculations:

```text
Size (MB)
≈
Bitrate (Mbps) × Duration (seconds)
÷ 8
```

For minutes:

```text
Size (MB)
≈
Bitrate (Mbps) × Duration (minutes) × 60
÷ 8
```

Since:

```text
60 ÷ 8 = 7.5
```

you can also remember:

```text
Size in MB
≈
Bitrate in Mbps × Duration in minutes × 7.5
```

### Example

```text
10 Mbps × 5 minutes × 7.5
= 375 MB
```

So approximately:

> **375 MB**

for the video stream.

---

# 23. A Useful Rule of Thumb

At a constant bitrate:

```text
1 Mbps for 1 minute
```

produces approximately:

```text
7.5 MB
```

of video data.

Therefore:

```text
5 Mbps for 1 minute
≈ 37.5 MB
```

```text
10 Mbps for 1 minute
≈ 75 MB
```

```text
20 Mbps for 1 minute
≈ 150 MB
```

These are rough decimal-unit calculations for the encoded video stream.

---

# 24. Why Bitrate Matters for CDN Costs

For streaming systems, bitrate is not just a video-quality setting.

It also affects how much data must be delivered.

Suppose a video stream uses:

```text
10 Mbps
```

A lower bitrate version might use:

```text
5 Mbps
```

The lower bitrate representation requires roughly half as much data to deliver over the same playback duration.

At large scale, this affects:

* Network bandwidth
* CDN data transfer
* Storage
* Egress costs
* User data consumption

This is why streaming engineers care deeply about the relationship between:

```text
Quality
   ↕
Bitrate
   ↕
Bandwidth
   ↕
Cost
```

---

# Common Mistakes / Gotchas

## 1. "5 Mbps means 5 MB per second."

No.

`Mbps` means **megabits per second**.

Since:

```text
8 bits = 1 byte
```

approximately:

```text
5 Mbps ÷ 8
≈ 0.625 MB/s
```

---

## 2. "Bitrate is the amount of color per pixel."

No.

Bitrate is:

> **Encoded bits per second.**

It describes the data rate of the encoded stream over time.

---

## 3. "Higher bitrate always means better quality."

Not necessarily.

A higher bitrate can provide more room for the encoder, but quality also depends on:

* Source quality
* Codec
* Encoder
* Resolution
* FPS
* Scene complexity
* Encoding settings

A poorly encoded 20 Mbps video can still look worse than a well-encoded 10 Mbps video.

---

## 4. "Higher bitrate always means higher resolution."

No.

You can have:

```text
720p @ 10 Mbps
```

or:

```text
1080p @ 10 Mbps
```

Bitrate and resolution are separate properties.

---

## 5. "Higher resolution automatically means higher bitrate."

Not necessarily.

You can encode:

```text
1080p @ 5 Mbps
```

or:

```text
720p @ 10 Mbps
```

The higher-resolution video often needs more bitrate for comparable quality, but bitrate is an encoding choice.

---

## 6. "FPS directly determines file size."

Not by itself.

If two videos have the same:

```text
average bitrate
+
duration
```

their video-stream sizes will be roughly similar, even if their resolutions or FPS differ.

---

## 7. "Bitrate is always exactly constant."

No.

Real encodes may use:

* CBR
* VBR
* Other rate-control strategies

A bitrate number can represent a target, average, or nominal rate depending on context.

---

## 8. "Increasing output bitrate recovers lost source quality."

No.

Once compression has discarded information:

```text
Lost information
       ↓
Cannot be recreated simply
by increasing output bitrate
```

A larger output file does not necessarily mean more actual source detail.

---

# Core Mental Model

Keep these three concepts together:

```text
RESOLUTION
    ↓
How much spatial information?
    ↓
Pixels per frame


FPS
    ↓
How much temporal information?
    ↓
Frames per second


BITRATE
    ↓
How much encoded data?
    ↓
Bits per second
```

Then connect them:

```text
Resolution + FPS
        ↓
Visual information
        ↓
Codec / Compression
        ↓
Encoded data
        ↓
Bitrate
        ↓
File size
```

And for streaming:

```text
Bitrate
   ↓
Data required per second
   ↓
Network bandwidth
   ↓
Buffer behavior
   ↓
Streaming experience
```

---

# The Full Picture So Far

After four chapters, you can now reason about video from the bottom up:

```text
DIGITAL IMAGE
      │
      ▼
    PIXELS
      │
      ▼
Width × Height
      │
      ▼
  RESOLUTION
      │
      ├───────────────┐
      │               │
      ▼               ▼
Pixel count       Aspect ratio
      │
      ▼
One FRAME
      │
      ▼
Many frames over time
      │
      ▼
     VIDEO
      │
      ▼
Resolution + FPS
      │
      ▼
Visual information
      │
      ▼
Codec / Compression
      │
      ▼
Encoded stream
      │
      ▼
    BITRATE
      │
      ▼
File size / Bandwidth
```

This is the core foundation for everything that follows.

---

# Key Takeaways

* A **bit** is either `0` or `1`.
* `8 bits = 1 byte`.
* **Bitrate** means the amount of encoded data per second.
* `5 Mbps` means approximately 5 million bits per second.
* To convert bits to bytes:

```text
bits ÷ 8 = bytes
```

* For roughly constant bitrate:

```text
File size ≈ bitrate × duration
```

* More precisely:

```text
File size ≈ bitrate × duration ÷ 8
```

when converting bits to bytes.

* Higher bitrate usually means a larger file for the same duration.
* Bitrate does **not** mean the amount of color per pixel.
* Resolution describes pixels per frame.
* FPS describes frames per second.
* Bitrate describes encoded bits per second.
* Resolution and FPS affect how much visual information must be represented.
* Compression converts that visual information into an encoded stream.
* The resulting encoded data rate is the bitrate.
* Two videos with different resolutions/FPS can have roughly the same file size if their average bitrates and durations are the same.
* Higher resolution or FPS often benefits from a higher bitrate for comparable quality, but this is not an absolute rule.
* Network bandwidth must be sufficient to sustain the video's bitrate for smooth streaming.
* ABR systems switch between different bitrate representations as network conditions change.
* CBR aims for a relatively stable bitrate.
* VBR allows bitrate to vary according to content and encoding needs.
* A bitrate number can represent a target, average, or nominal rate depending on the encoding setup.
* Increasing bitrate during a later encode cannot recover detail already lost during earlier compression.
* Bitrate also affects storage, bandwidth, CDN transfer, and streaming costs.

---

# Minimal Self-Test

Try these without looking back:

1. What is a bit?
2. How many bits are in one byte?
3. What does `8 Mbps` mean?
4. Approximately how many megabytes are produced by `8 Mbps` for 2 minutes?
5. What is the basic relationship between bitrate, duration, and file size?
6. Why doesn't bitrate mean "amount of color per pixel"?
7. What is the difference between resolution, FPS, and bitrate?
8. Can a `1080p` video and a `720p` video have the same bitrate?
9. If two videos have the same average bitrate and duration, can they have roughly the same file size even if their resolutions differ?
10. Why might a 1080p video need more bitrate than a 720p video to achieve similar visual quality?
11. Why can a 5 Mbps video cause buffering on a 2 Mbps connection?
12. What is the difference between CBR and VBR?
13. If a source video has already lost detail through compression, can encoding it again at a higher bitrate recover that lost detail?
14. Why does bitrate matter for CDN and streaming costs?
15. How are **resolution → FPS → compression → bitrate → file size** connected?

---

# What to Learn Next

The next logical layer is **raw video and pixel representation**.

You now know:

```text
Resolution
    ↓
Pixels/frame

FPS
    ↓
Frames/sec

Bitrate
    ↓
Encoded bits/sec
```

The next question is:

> **Before compression, how much data does each pixel actually require?**

That leads to:

```text
Pixel
  ↓
Color channels
  ↓
Bit depth
  ↓
RGB / YUV
  ↓
Pixel formats
  ↓
Raw frame size
  ↓
Raw video size
  ↓
Why compression is necessary
```

This will make the jump from **pixels and frames** to **codecs and compression** much easier.
