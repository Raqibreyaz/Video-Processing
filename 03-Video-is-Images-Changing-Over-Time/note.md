# Chapter 3 — Frames & FPS

## What it is

A **frame** is one digital image in a video.

Since you already know:

> **Digital image = grid of pixels**

we can now build the next layer:

```text
Frame
  ↓
One image
  ↓
Grid of pixels
```

A video is a sequence of these frames shown over time.

```text
Frame 1 → Frame 2 → Frame 3 → Frame 4 → ...
```

When the frames are shown quickly one after another, we perceive the changing images as **motion**.

---

## One-sentence summary

> **A video is a sequence of frames displayed over time, and FPS (frames per second) tells us how many frames are captured or displayed each second.**

---

# Intuition

Imagine taking photographs of a moving ball.

```text
Time →

Frame 1       Frame 2       Frame 3       Frame 4

   ●             ●              ●              ●
```

The ball has a slightly different position in every photograph.

If we show those photographs one after another quickly:

```text
● → ● → ● → ●
```

our eyes perceive the ball as moving.

So the basic mental model is:

```text
One image
    ↓
One frame

Many frames
    ↓
Changing over time
    ↓
Video / motion
```

---

# 1. What is a Frame?

A **frame is one image in a video**.

For example:

```text
Frame 1        Frame 2        Frame 3

┌────────┐     ┌────────┐     ┌────────┐
│   ●    │     │    ●   │     │     ●  │
│        │     │        │     │        │
└────────┘     └────────┘     └────────┘
```

Each frame is still just an image.

Therefore:

```text
Frame
  │
  └── Grid of pixels
```

The difference between a sequence of frames is that the pixel values can change from one frame to the next.

For example, the ball's position changes:

```text
Frame 1 → ball at x = 100
Frame 2 → ball at x = 110
Frame 3 → ball at x = 120
```

Those changes create the appearance of movement.

---

# 2. What is FPS?

**FPS = Frames Per Second**

It tells us how many frames are captured or displayed during one second.

For example:

```text
30 FPS
```

means:

```text
1 second → 30 frames
```

while:

```text
60 FPS
```

means:

```text
1 second → 60 frames
```

And:

```text
120 FPS
```

means:

```text
1 second → 120 frames
```

---

# 3. Calculating the Number of Frames

For a constant frame rate:

```text
Total frames ≈ FPS × duration
```

### Example: 10 seconds at 30 FPS

```text
30 frames/sec × 10 sec
= 300 frames
```

So approximately:

> **300 frames**

---

### Example: 10 seconds at 60 FPS

```text
60 × 10
= 600 frames
```

So:

```text
30 FPS → 300 frames
60 FPS → 600 frames
```

for the same 10-second duration.

The 60 FPS video contains twice as many frames.

---

# 4. FPS is Temporal Sampling

You already learned that resolution describes **spatial sampling**.

Now FPS introduces another important idea:

> **FPS describes temporal sampling.**

### Spatial sampling

Resolution tells us how many positions we use to describe the image across space.

```text
Resolution
    ↓
Spatial samples
    ↓
Pixels
```

### Temporal sampling

FPS tells us how many snapshots we take/display over time.

```text
FPS
    ↓
Temporal samples
    ↓
Frames
```

This gives us a powerful mental model:

```text
IMAGE
  ↓
Spatial information
  ↓
Pixels


VIDEO
  ↓
Spatial information + time
  ↓
Pixels + Frames
```

---

# 5. Why Does Higher FPS Look Smoother?

Suppose an object moves from left to right.

At a very low frame rate, you might capture:

```text
5 FPS

●       ●       ●       ●       ●
```

There are relatively large jumps between the captured positions.

At a higher frame rate:

```text
30 FPS

● ● ● ● ● ● ● ● ● ● ● ● ● ● ●
```

There are many more snapshots of the movement.

The change between consecutive frames can therefore appear smaller and motion can appear smoother.

### Mental model

> **Higher FPS means more temporal snapshots of movement are captured or displayed each second.**

---

# 6. Higher FPS Does NOT Automatically Make Video Slower

This is a very important distinction.

Suppose a ball takes exactly **1 second** to travel from A to B.

At 30 FPS:

```text
1 second
   ↓
30 frames
```

At 60 FPS:

```text
1 second
   ↓
60 frames
```

Both videos still represent the same **1-second duration** if played back at their intended frame rate.

The 60 FPS version simply contains more temporal samples.

```text
30 FPS:

A -----> -----> -----> B


60 FPS:

A --> --> --> --> --> --> --> B
```

Therefore:

> **FPS does not determine playback duration by itself.**

It describes how many frames are captured/displayed per second.

---

# 7. Then Why is High FPS Useful for Slow Motion?

This is where **capture FPS** and **playback FPS** become important.

Suppose you record an event at:

```text
120 FPS
```

During one real-world second, you capture:

```text
120 frames
```

Now you take those same 120 frames and play them at:

```text
30 FPS
```

The playback duration becomes:

```text
120 frames
÷
30 frames/sec
=
4 seconds
```

So:

```text
Real-world action
      │
      │ 1 second
      ▼
120 captured frames
      │
      │ play at 30 FPS
      ▼
4 seconds of playback
```

Therefore, 1 second of real-world action becomes 4 seconds of slow-motion playback.

---

# 8. The Real Slow-Motion Principle

Recording at high FPS **does not automatically make the footage slow motion**.

The important combination is:

```text
Capture many frames
        +
Play those frames at a lower rate
        ↓
Slow motion
```

For example:

```text
Capture:
120 FPS

Playback:
30 FPS

Slowdown:
120 ÷ 30
= 4×
```

So the action plays at **one-fourth of its original speed**.

---

## Another Example

Suppose:

```text
Capture = 60 FPS
Playback = 30 FPS
```

Then:

```text
60 ÷ 30 = 2
```

The footage plays at:

> **2× slow motion**

One second of real-world action becomes two seconds of playback.

---

# 9. A Useful Formula for Slow Motion

When the same captured frames are played at a different frame rate:

```text
Playback duration
=
Number of captured frames
÷
Playback FPS
```

And for one second of real-world capture:

```text
Slow-motion factor
=
Capture FPS ÷ Playback FPS
```

Examples:

```text
120 ÷ 30 = 4×
```

```text
60 ÷ 30 = 2×
```

```text
240 ÷ 30 = 8×
```

So a 240 FPS recording played at 30 FPS can produce an **8× slowdown**, assuming the footage is handled this way.

---

# 10. Resolution + FPS

Now combine what you learned in Chapters 1–3.

Suppose a video is:

```text
1920 × 1080
60 FPS
```

This means:

### Each frame

```text
1920 × 1080 pixels
```

Therefore:

```text
1920 × 1080
= 2,073,600
```

pixel positions per frame.

### Every second

```text
60 frames
```

So every second contains:

```text
2,073,600 pixels/frame
×
60 frames/sec
=
124,416,000 pixel positions/sec
```

That's approximately:

> **124 million pixel samples per second**

---

# 11. Why Raw Video Becomes Huge

This gives you an important intuition about video data.

A single 1920×1080 frame already has:

```text
2,073,600
```

pixel positions.

At 60 FPS:

```text
2,073,600 × 60
=
124,416,000
```

pixel positions every second.

And this is before considering the actual number of bits required to represent those pixel values.

For longer videos, the amount of raw image data grows very quickly.

That's why video systems need:

* Compression
* Encoding
* Bitrate control
* Efficient storage
* Efficient transmission

These concepts become especially important in the next stages of learning video.

---

# 12. Three Important Dimensions of Video

You can now separate three different concepts:

```text
Resolution
    ↓
How many pixels are in each frame?


FPS
    ↓
How many frames are processed/displayed each second?


Bitrate
    ↓
How much encoded data is produced/transmitted per second?
```

For example:

```text
1080p
60 FPS
10 Mbps
```

roughly means:

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

Do not mix them together.

---

# 13. Resolution vs FPS

This distinction is worth memorizing.

| Property    | Describes                   | Example       |
| ----------- | --------------------------- | ------------- |
| Resolution  | Spatial dimensions          | `1920 × 1080` |
| Pixel count | Spatial samples per frame   | `2,073,600`   |
| FPS         | Temporal samples per second | `60 FPS`      |
| Bitrate     | Encoded data per second     | `10 Mbps`     |

Think:

```text
Resolution → "How detailed is each frame spatially?"
FPS        → "How frequently are frames sampled/displayed?"
Bitrate    → "How much encoded data is used per second?"
```

These questions are related, but they are not the same.

---

# 14. Connection to FFmpeg

When FFmpeg reports something like:

```text
1920x1080
60 fps
```

you can now interpret it as:

```text
Frame:
    1920 × 1080 pixels

Time:
    60 frames every second
```

So the basic structure is:

```text
Video
  │
  ├── Frame 1 → 1920 × 1080
  ├── Frame 2 → 1920 × 1080
  ├── Frame 3 → 1920 × 1080
  ├── ...
  └── 60 frames each second
```

---

# 15. Changing FPS with FFmpeg

You may encounter:

```bash
-r 30
```

in FFmpeg commands.

In the relevant FFmpeg context, this is used to set or convert the output frame rate to **30 FPS**.

However, changing FPS does not always mean exactly the same operation.

Depending on the workflow, converting:

```text
60 FPS → 30 FPS
```

can involve things such as:

* Dropping frames
* Selecting frames
* Duplicating frames in other conversions
* Changing timestamps
* Encoding at a different output frame rate

There is an important distinction between **changing the number of frames**, **changing timestamps**, and **changing playback speed**.

Those details become important when you start doing real FFmpeg transcoding.

For now, remember:

> **Changing FPS is not automatically the same thing as slowing down or speeding up a video.**

---

# 16. FPS and Playback Speed Are Different

Consider a video recorded at:

```text
60 FPS
```

If it is played normally at:

```text
60 FPS
```

then:

```text
1 second captured
→
1 second played
```

If the same frames are interpreted for playback at:

```text
30 FPS
```

then:

```text
1 second captured
→
2 seconds played
```

But if you simply convert a normal 60 FPS video into a 30 FPS video while preserving its intended duration, you generally want:

```text
60 FPS
    ↓
select fewer frames
    ↓
30 FPS
```

while keeping:

```text
1 second
→
1 second
```

So:

> **Frame-rate conversion and slow motion are not automatically the same operation.**

---

# Common Mistakes / Gotchas

## 1. "60 FPS means the video is twice as long as 30 FPS."

No.

If both are normal-speed videos:

```text
30 FPS → 1 second
60 FPS → 1 second
```

The 60 FPS video simply has more frames during that second.

---

## 2. "Higher FPS automatically means slow motion."

No.

High FPS provides more captured frames.

Slow motion happens when those frames are played back over a longer duration.

```text
High-FPS capture
       +
Lower-FPS playback
       ↓
Slow motion
```

---

## 3. "FPS controls image resolution."

No.

These are independent properties.

```text
Resolution → pixels per frame
FPS        → frames per second
```

You can have:

```text
1920 × 1080 @ 30 FPS
```

or:

```text
1920 × 1080 @ 60 FPS
```

Same resolution, different temporal sampling.

---

## 4. "Higher FPS always means better video."

Not necessarily.

Higher FPS can provide smoother motion and more useful frames for slow motion, but it also generally means more frames must be captured, processed, stored, and encoded.

It can therefore increase:

* Processing requirements
* Storage requirements
* Potential bitrate requirements
* Encoding workload

Actual quality depends on many factors.

---

## 5. "Every second always contains exactly FPS frames."

For simple constant-frame-rate video, this is a useful model.

Real video can also use **variable frame rate (VFR)**, where frame timing is not perfectly uniform.

For now, the basic constant-frame-rate model is:

```text
30 FPS → approximately 30 frames/sec
60 FPS → approximately 60 frames/sec
```

You will need timestamps and time bases later to understand VFR properly.

---

## 6. "Changing FPS always changes playback speed."

No.

For example, converting:

```text
60 FPS → 30 FPS
```

can be done while keeping the same duration by removing/selecting frames.

Slow motion is a different operation.

---

# A Deeper Mental Model: Space + Time

You can now think of video as information sampled in **space and time**.

### One frame

```text
         SPACE
    ┌───────────────┐
    │               │
    │    pixels     │
    │               │
    └───────────────┘
```

### Video

```text
TIME →

Frame 1    Frame 2    Frame 3    Frame 4
┌──────┐   ┌──────┐   ┌──────┐   ┌──────┐
│pixels│ → │pixels│ → │pixels│ → │pixels│
└──────┘   └──────┘   └──────┘   └──────┘
```

So:

```text
Resolution
    ↓
Sampling in SPACE


FPS
    ↓
Sampling in TIME
```

This is a very useful foundation for understanding video compression later.

---

# Complete Mental Model

You can now connect all three chapters:

```text
DIGITAL IMAGE
      │
      ▼
  GRID OF PIXELS
      │
      ▼
WIDTH × HEIGHT
      │
      ├──→ Total pixel positions
      │
      └──→ Aspect ratio


VIDEO
      │
      ▼
SEQUENCE OF FRAMES
      │
      ▼
Each frame = image
      │
      ▼
Each frame = grid of pixels
      │
      ▼
FPS = frames per second
```

And:

```text
             VIDEO
               │
       ┌───────┴───────┐
       ▼               ▼
    SPACE             TIME
       │               │
       ▼               ▼
 Resolution            FPS
       │               │
       ▼               ▼
 Pixels/frame      Frames/sec
```

---

# Worked Example

Suppose FFmpeg reports:

```text
1920 × 1080
60 FPS
```

Let's decode it step by step.

### Step 1 — Resolution

```text
Width = 1920
Height = 1080
```

### Step 2 — Pixel positions per frame

```text
1920 × 1080
= 2,073,600
```

### Step 3 — Frames per second

```text
60 frames/sec
```

### Step 4 — Pixel positions sampled per second

```text
2,073,600 × 60
= 124,416,000
```

So the video processes roughly:

> **124 million pixel positions per second**

This does **not** mean the encoded file necessarily stores 124 million independent pixel values every second. Video compression exploits redundancy and stores the information much more efficiently.

That distinction will become very important when we study **compression and codecs**.

---

# Key Takeaways

* A **frame** is one image in a video.
* Each frame is a grid of pixels.
* A video is a sequence of frames changing over time.
* **FPS = Frames Per Second**.
* FPS tells us how many frames are captured/displayed per second.
* `30 FPS` means approximately 30 frames per second.
* `60 FPS` means approximately 60 frames per second.
* Higher FPS gives more temporal samples and can make motion appear smoother.
* Higher FPS does **not automatically make playback slower**.
* High-FPS recording becomes useful for slow motion when the captured frames are played back at a lower rate.
* Example:

```text
120 FPS capture
÷
30 FPS playback
=
4× slow motion
```

* Resolution describes **spatial sampling**.
* FPS describes **temporal sampling**.
* Bitrate describes the amount of **encoded data per second**.
* A `1920 × 1080 @ 60 FPS` video has 2,073,600 pixel positions per frame and about 124 million pixel positions sampled per second.
* Changing FPS and changing playback speed are different operations.
* Converting `60 FPS → 30 FPS` does not necessarily mean slow motion; frames can simply be removed while keeping the same duration.
* Real-world video can use variable frame rates, so the simple FPS model is mainly for constant-frame-rate video.
* More frames also mean more work for capture, processing, storage, and encoding.

---

# Minimal Self-Test

Try these without looking back:

1. What is a frame?
2. What does `30 FPS` mean?
3. How many frames are in a 10-second video at `30 FPS`?
4. How many frames are in a 10-second video at `60 FPS`?
5. Why can higher FPS make motion appear smoother?
6. Does recording at `120 FPS` automatically make the video slow motion?
7. If 120 captured frames are played at 30 FPS, how long will those frames take to play?
8. What is the difference between spatial sampling and temporal sampling?
9. What does `1920 × 1080 @ 60 FPS` tell you?
10. Approximately how many pixel positions are sampled per second in a `1920 × 1080 @ 60 FPS` video?
11. Does converting `60 FPS → 30 FPS` necessarily make the video play at half speed?
12. What are the three different concepts represented by **resolution, FPS, and bitrate**?

---

# What to Learn Next

The natural next step is **Chapter 4 — Raw Video, Bit Depth & Pixel Formats**.

You already know:

```text
Resolution
    ↓
How many pixels?


FPS
    ↓
How many frames over time?
```

The next question is:

> **How much data is required to represent the pixels inside those frames?**

That leads naturally to:

```text
Pixel
  ↓
Pixel value
  ↓
Bit depth
  ↓
Color channels
  ↓
RGB / YUV
  ↓
Raw video size
  ↓
Bitrate
  ↓
Compression
```

This is the layer that explains why an apparently simple `1920×1080 @ 60 FPS` video can require a surprisingly large amount of raw data before compression.
