# 🖼️ Image Sharpening Using Custom Convolution Filters

## 📌 Introduction

Image sharpening is an important technique in **digital image processing** used to enhance edges and fine details in an image.

In this tutorial, we learn how to create and apply **custom sharpening filters (kernels)** using:

- Python
- NumPy
- OpenCV

Instead of using built-in sharpening functions, we manually define convolution kernels and observe their effects on images.

---

# 🧠 What is Image Sharpening?

Sharpening is a process that increases the visibility of edges and small details in an image.

A sharpened image usually has:

- Stronger edges
- Higher local contrast
- More visible details

This is achieved by applying a **convolution operation** using a predefined kernel.

---

# 🔍 Convolution Kernel

A convolution kernel is a small matrix that slides over the image pixels and modifies each pixel based on its neighbors.

Example:

```python
kernel = np.array([
    [0, -1, 0],
    [-1, 5, -1],
    [0, -1, 0]
])
```

The center value increases the contribution of the current pixel, while negative values reduce the influence of surrounding pixels.

---

# ✨ Sharpening Filter 1

```python
sharpen_filter1 = np.array([
    [ 0, -1,  0],
    [-1,  5, -1],
    [ 0, -1,  0]
])
```

### Characteristics:

- Moderate sharpening effect
- Enhances edges while keeping a natural appearance
- Commonly used for general image enhancement

Mathematically, this kernel increases the original pixel intensity and subtracts neighboring information to highlight changes.

---

# 🔥 Sharpening Filter 2

```python
sharpen_filter2 = np.array([
    [-1, -1, -1],
    [-1,  9, -1],
    [-1, -1, -1]
])
```

### Characteristics:

- Stronger sharpening effect
- Produces more noticeable edges
- Can increase noise in images

This filter uses all neighboring pixels, making the sharpening effect more aggressive.

---

# ⚙️ Applying the Filter

Using OpenCV, convolution can be applied with:

```python
import cv2

sharpened_image = cv2.filter2D(
    image,
    -1,
    sharpen_filter1
)
```

Where:

- `image` → input image
- `-1` → keeps the original image depth
- `sharpen_filter1` → custom convolution kernel

---

# 📊 Comparing Filters

Different kernels create different sharpening behaviors:

| Filter | Strength | Result |
|--------|----------|--------|
| Filter 1 | Medium | Natural sharpening |
| Filter 2 | Strong | More detailed but may amplify noise |

---

# 🖼️ Example Workflow

```
Original Image
       |
       ↓
Create Custom Kernel
       |
       ↓
Apply Convolution
       |
       ↓
Sharpened Image
```

---

# 📚 Learning Goals

After completing this tutorial, you will understand:

- What image sharpening means
- How convolution works in image processing
- How kernels affect image quality
- How to design custom filters using NumPy
- How OpenCV applies convolution operations

---

# 🛠️ Requirements

Install required libraries:

```bash
pip install numpy opencv-python matplotlib
```

---
