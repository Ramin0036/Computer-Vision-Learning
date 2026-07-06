# 🔊 Image Noise and Denoising

## 📌 Introduction

Image noise is an unwanted variation in pixel intensity that degrades image quality and reduces the performance of image processing and computer vision algorithms. Noise may be introduced during image acquisition, transmission, compression, or sensor limitations.

Image denoising aims to remove or suppress noise while preserving important image details such as edges and textures.

This project investigates two common types of image noise and compares several filtering techniques for removing them.

---

# 🌟 Image Noise

Noise appears as random variations in image intensity. Different types of noise require different denoising strategies.

---

# 1️⃣ Salt-and-Pepper Noise

## 📖 Definition

Salt-and-Pepper Noise (Impulse Noise) randomly replaces some image pixels with either the minimum intensity (black) or the maximum intensity (white).

Example:

```text
Original

120 121 122
121 123 124
122 124 125

↓

Salt & Pepper

120   0 122
255 123 124
122 124   0
```

### Characteristics

- Random black and white pixels
- Caused by transmission errors or faulty sensors
- Easy to identify visually

### Applications

Used mainly for evaluating denoising algorithms.

---

# 2️⃣ Gaussian Noise

## 📖 Definition

Gaussian Noise is additive random noise whose intensity follows a normal (Gaussian) distribution.

Unlike Salt-and-Pepper noise, every pixel is slightly affected.

Example Distribution

```text
Frequency
 ^
 |            ███
 |         ███████
 |      ███████████
 |   ███████████████
 +---------------------------->
        Pixel Intensity
```

### Characteristics

- Smooth random variations
- Follows a normal distribution
- Common in digital cameras and electronic sensors

---

# 🧹 Image Denoising

The goal of denoising is to remove unwanted noise while preserving image details.

Different filters behave differently depending on the noise type.

---

# 1️⃣ Blur Filter

## 📖 Definition

Blur (Average) Filter replaces each pixel with the average of its neighboring pixels.

### Advantages

- Simple
- Fast
- Reduces Gaussian noise

### Disadvantages

- Blurs edges
- Removes fine details
- Ineffective for Salt-and-Pepper noise

---

# 2️⃣ Gaussian Blur

## 📖 Definition

Gaussian Blur performs weighted averaging using a Gaussian kernel.

Pixels closer to the center contribute more than distant pixels.

### Advantages

- Excellent for Gaussian noise
- Produces smoother results than Average Blur

### Disadvantages

- Still blurs edges
- Not suitable for impulse noise

---

# 3️⃣ Median Filter

## 📖 Definition

Median Filter replaces each pixel with the median value of neighboring pixels.

Example:

```text
Neighborhood

10  11  12
11 255  13
12  13  14

↓

Sorted

10 11 11 12 12 13 13 14 255

Median = 12
```

### Advantages

- Excellent for Salt-and-Pepper noise
- Preserves edges
- Removes isolated noisy pixels

### Disadvantages

- Less effective for Gaussian noise

---

# 4️⃣ Bilateral Filter

## 📖 Definition

The Bilateral Filter smooths an image while preserving edges.

Unlike Gaussian Blur, it considers both:

- Spatial distance
- Pixel intensity difference

Therefore, neighboring pixels with very different intensities contribute less to the filtering process.

### Advantages

- Removes Gaussian noise
- Preserves edges
- Produces natural-looking images

### Disadvantages

- Slower than Gaussian Blur
- More computationally expensive

---

# 🔍 Filter Comparison

| Filter | Gaussian Noise | Salt & Pepper | Edge Preservation | Speed |
|----------|---------------|---------------|-------------------|--------|
| Blur | ⭐⭐⭐ | ⭐ | ❌ Low | ⭐⭐⭐⭐⭐ |
| Gaussian Blur | ⭐⭐⭐⭐ | ⭐ | ❌ Medium | ⭐⭐⭐⭐ |
| Median Filter | ⭐⭐ | ⭐⭐⭐⭐⭐ | ✅ High | ⭐⭐⭐ |
| Bilateral Filter | ⭐⭐⭐⭐⭐ | ⭐⭐ | ✅ Excellent | ⭐⭐ |

---

# 📊 Effect on Edges

One of the most important criteria in denoising is edge preservation.

```text
Original Edge

████████████░░░░░░░░

Blur

███████████▒▒▒▒▒▒▒▒▒

Gaussian Blur

██████████▒▒▒▒▒▒▒▒▒▒

Median

████████████░░░░░░░░

Bilateral

████████████░░░░░░░░
```

### Summary

- Blur removes both noise and edges.
- Gaussian Blur smooths images but softens boundaries.
- Median Filter preserves sharp edges while removing impulse noise.
- Bilateral Filter preserves edges while effectively reducing Gaussian noise.

---

# 🎯 Conclusions

The experiments demonstrate that no single filter is optimal for every type of noise.

- **Blur Filter** is simple but causes noticeable image blurring.
- **Gaussian Blur** performs well for Gaussian noise but weakens edges.
- **Median Filter** is the best choice for Salt-and-Pepper noise because it removes impulse noise while preserving edges.
- **Bilateral Filter** provides the best balance between noise reduction and edge preservation for Gaussian noise, although it requires more computation.

Selecting the appropriate denoising technique depends on the noise characteristics and the desired balance between smoothness and detail preservation.

---

⭐ If you found this project useful, consider giving it a star!
