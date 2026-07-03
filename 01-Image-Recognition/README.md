# 🖼️ Image Types and Image Formats

This repository provides an introduction to the most common **image types**, **color spaces**, and **image file formats** used in **Image Processing**, **Computer Vision**, and **Machine Learning**.

---

## 📖 Table of Contents

- [Image Types](#-image-types)
  - [Binary Image](#binary-image)
  - [Grayscale Image](#grayscale-image)
  - [RGB Image](#rgb-image)
  - [HSV Image](#hsv-image)
- [Image Channels](#-image-channels)
- [Image Properties](#-image-properties)
  - [Intensity](#intensity)
  - [Contrast](#contrast)
  - [Brightness](#brightness)
  - [Dynamic Range](#dynamic-range)
  - [Resolution](#resolution)
  - [Bit Depth](#bit-depth)
  - [Histogram](#histogram)
- [Alpha Channel](#-alpha-channel)
- [Image Formats](#-image-formats)
  - [PNG](#png)
  - [JPEG](#jpeg)
  - [WebP](#webp)
- [Comparison Tables](#-comparison-tables)
- [Summary](#-summary)
- [References](#-references)

---

# 📷 Image Types

## Binary Image

A **Binary Image** is the simplest type of digital image. Every pixel has only **two possible values**.

| Pixel Value | Meaning |
|-------------|---------|
| 0 | Black |
| 255 (or 1) | White |

**Channels:** `1`

### Example

```text
0   0   255
255 255 0
0   255 255
```

Visual representation:

```
⬛ ⬛ ⬜
⬜ ⬜ ⬛
⬛ ⬜ ⬜
```

### Applications

- OCR (Optical Character Recognition)
- Document Processing
- Object Segmentation
- Edge Detection

---

## Grayscale Image

A **Grayscale Image** stores only the **brightness (intensity)** of each pixel.

Pixel values range from **0** to **255**.

| Value | Meaning |
|-------:|---------|
| 0 | Black |
| 128 | Gray |
| 255 | White |

**Channels:** `1`

### Example

```text
0     80    160
120   200   255
60    100   220
```

### Applications

- Medical Imaging
- Face Detection
- Computer Vision
- Image Preprocessing

---

## RGB Image

RGB is the most common color model used in digital images.

Each pixel consists of three color channels:

- 🔴 Red
- 🟢 Green
- 🔵 Blue

Each channel has a value between **0 and 255**.

**Channels:** `3`

Pixel representation:

```text
(R, G, B)
```

### Examples

| Color | RGB Value |
|--------|-----------|
| Black | (0, 0, 0) |
| White | (255, 255, 255) |
| Red | (255, 0, 0) |
| Green | (0, 255, 0) |
| Blue | (0, 0, 255) |
| Yellow | (255, 255, 0) |
| Cyan | (0, 255, 255) |
| Magenta | (255, 0, 255) |

---

## HSV Image

HSV represents colors in a way that is more intuitive than RGB.

<img width="800" height="600" alt="HSV2" src="https://github.com/user-attachments/assets/23dd1601-d628-4ec4-abc7-721b56c53921" />

<img width="1089" height="570" alt="HSV - Copy" src="https://github.com/user-attachments/assets/0b592943-979b-4315-b135-306e83cb97a5" />


HSV consists of:

- **Hue (H)** → Color
- **Saturation (S)** → Color purity
- **Value (V)** → Brightness

**Channels:** `3`

### Example

| Color | Hue | Saturation | Value |
|--------|----:|-----------:|------:|
| Red | 0° | 100% | 100% |
| Green | 120° | 100% | 100% |
| Blue | 240° | 100% | 100% |

### Why HSV?

Suppose you want to detect **red objects**.

With **RGB**, all three channels must be analyzed.

With **HSV**, you only need to check the **Hue** channel, making color detection much easier.

---

# 🎨 Image Channels

Every image is composed of one or more **channels**.

| Image Type | Channels | Description |
|------------|----------|-------------|
| Binary | 1 | Black & White |
| Grayscale | 1 | Brightness only |
| RGB | 3 | Red, Green, Blue |
| HSV | 3 | Hue, Saturation, Value |
| RGBA | 4 | RGB + Transparency |

---

# 🌈 Image Properties

Besides image types and color spaces, digital images have several important properties that affect how they look and how they are processed.

## Intensity

**Intensity** refers to the brightness value of a pixel.

- In a **Grayscale Image**, intensity is simply the pixel value.
- In an **RGB Image**, intensity is usually computed from the three color channels.

For an 8-bit image:

| Intensity | Appearance |
|-----------|------------|
| 0 | Black |
| 64 | Dark Gray |
| 128 | Gray |
| 192 | Light Gray |
| 255 | White |

### Example

```text
20   40   60
80   120  180
200  220  255
```

Pixels with higher intensity appear brighter.

---

## Contrast

**Contrast** describes the difference between the darkest and brightest parts of an image.

### Low Contrast

```text
120 125 128
126 130 132
129 131 135
```

The image appears dull because pixel values are very similar.

### High Contrast

```text
0   40   90
150 200 255
20  180 240
```

The image appears sharper because there is a larger difference between dark and bright pixels.

### Applications

- Medical image enhancement
- Object detection
- Edge detection

---

## Brightness

**Brightness** indicates the overall lightness or darkness of an image.

Increasing brightness makes every pixel lighter.

Example:

Original:

```text
50 100 150
```

Increase brightness by +50:

```text
100 150 200
```

---

## Dynamic Range

**Dynamic Range** is the difference between the minimum and maximum intensity values that an image can represent.

For an **8-bit image**:

```text
0 → 255
```

A higher dynamic range preserves more details in both dark and bright regions.

---

## Resolution

**Resolution** describes the number of pixels in an image.

Example:

```
640 × 480
1280 × 720
1920 × 1080 (Full HD)
3840 × 2160 (4K)
```

Higher resolution generally provides more image details.

---

## Bit Depth

**Bit Depth** determines how many intensity or color values can be represented for each pixel.

| Bit Depth | Possible Values |
|-----------|----------------:|
| 1-bit | 2 |
| 8-bit | 256 |
| 16-bit | 65,536 |
| 24-bit RGB | 16.7 Million Colors |

Examples:

- Binary Image → **1-bit**
- Grayscale Image → **8-bit**
- RGB Image → **24-bit** (8 bits × 3 channels)
- RGBA Image → **32-bit** (8 bits × 4 channels)

---

## Histogram

A **Histogram** is a graph showing how pixel intensities are distributed in an image.

- Peaks on the **left** indicate a dark image.
- Peaks on the **right** indicate a bright image.
- A wide histogram usually indicates high contrast.

Example:

```text
Frequency
 ^
 |
 |      ███
 |    ██████
 |  █████████
 |██████████████
 +---------------------------->
   0        128          255
        Intensity
```

Histograms are widely used for:

- Contrast Enhancement
- Histogram Equalization
- Image Analysis

---

# 🌟 Alpha Channel

Some image formats support an additional **fourth channel** called the **Alpha Channel**.

The Alpha channel controls **transparency**.

An RGBA pixel is represented as:

```text
(R, G, B, A)
```

### Examples

Fully opaque:

```text
(255, 0, 0, 255)
```

Semi-transparent:

```text
(255, 0, 0, 128)
```

Fully transparent:

```text
(255, 0, 0, 0)
```

| Alpha Value | Transparency |
|-------------|--------------|
| 255 | Fully Visible |
| 128 | Semi Transparent |
| 0 | Fully Transparent |

---

# 🗂️ Image Formats

## PNG

**PNG (Portable Network Graphics)** uses **lossless compression**, meaning image quality is preserved after saving.

### Features

- ✅ Lossless Compression
- ✅ Supports Transparency
- ✅ High Quality
- ✅ Ideal for Logos and Icons

### Supported Channels

| Image Type | Channels |
|------------|----------|
| Grayscale | 1 |
| RGB | 3 |
| RGBA | 4 |

---

## JPEG

**JPEG (Joint Photographic Experts Group)** is the most widely used image format for photographs.

It uses **lossy compression**, which reduces file size by sacrificing some image quality.

### Features

- Small file size
- Excellent for photographs
- Fast loading
- Widely supported

### Supported Channels

| Image Type | Channels |
|------------|----------|
| RGB | 3 |

> **Note:** JPEG does **not** support the Alpha Channel.

---

## WebP

**WebP** is a modern image format developed by Google.

It provides better compression than JPEG while also supporting transparency.

### Features

- Lossy & Lossless Compression
- Supports Alpha Channel
- Smaller File Size
- Excellent for Web Applications

### Supported Channels

| Image Type | Channels |
|------------|----------|
| RGB | 3 |
| RGBA | 4 |

---

# 📊 Comparison Tables

## Image Types

| Type | Channels | Color | Transparency |
|------|---------:|:-----:|:------------:|
| Binary | 1 | ❌ | ❌ |
| Grayscale | 1 | ❌ | ❌ |
| RGB | 3 | ✅ | ❌ |
| HSV | 3 | ✅ | ❌ |
| RGBA | 4 | ✅ | ✅ |

---

## Image Formats

| Format | Compression | Quality | Alpha Channel | Best Use |
|--------|-------------|---------|:-------------:|----------|
| PNG | Lossless | ⭐⭐⭐⭐⭐ | ✅ | Logos, UI, Graphics |
| JPEG | Lossy | ⭐⭐⭐⭐ | ❌ | Photographs |
| WebP | Lossy / Lossless | ⭐⭐⭐⭐⭐ | ✅ | Modern Websites |

---

# 💡 Summary

- **Binary Images** contain only black and white pixels.
- **Grayscale Images** contain only intensity values.
- **RGB Images** use three color channels: Red, Green, and Blue.
- **HSV Images** represent colors using Hue, Saturation, and Value.
- **RGBA Images** include an additional **Alpha Channel** for transparency.
- **PNG** and **WebP** support transparency, while **JPEG** does not.

---
