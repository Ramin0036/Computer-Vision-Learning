# Hough Transform: Line and Circle Detection with Image Preprocessing

## Overview

This repository explains Hough Transform for detecting lines and circles
and studies how preprocessing filters such as Gaussian Blur, Median
Blur, and Bilateral Filter affect detection performance.

### Topics

-   Hough Line Transform
-   Probabilistic Hough Transform
-   Hough Circle Transform
-   Image preprocessing
-   Canny Edge Detection
-   Filter comparison
-   Advantages and disadvantages

## Theory

A line is represented in Hough space by:

\[ `\rho `{=tex}=
x`\cos`{=tex}(`\theta`{=tex})+y`\sin`{=tex}(`\theta`{=tex}) \]

Each edge pixel votes in parameter space. Peaks correspond to detected
lines.

A circle is represented by:

\[ (x-a)^2+(y-b)^2=r\^2 \]

where `(a,b)` is the center and `r` is the radius.

## OpenCV Functions

``` python
cv2.HoughLines()
cv2.HoughLinesP()
cv2.HoughCircles()
```

## Typical Pipeline

``` text
Input Image
    ↓
Grayscale
    ↓
Blur
    ↓
Canny
    ↓
Hough Transform
    ↓
Detected Shapes
```

## Gaussian Blur

``` python
blur = cv2.GaussianBlur(image,(5,5),0)
```

Advantages: - Removes random noise - Reduces false detections - Improves
circle detection

Disadvantages: - Weakens thin edges - Large kernels remove details

## Median Blur

``` python
blur = cv2.medianBlur(image,5)
```

Advantages: - Excellent for salt & pepper noise - Preserves edges better

Disadvantages: - May distort very small circles

## Bilateral Filter

``` python
filtered = cv2.bilateralFilter(image,9,75,75)
```

Advantages: - Removes noise - Preserves sharp edges

Disadvantages: - Computationally expensive

## Filter Comparison

  Filter      Noise Removal   Edge Preservation   Speed
  ----------- --------------- ------------------- --------
  Gaussian    High            Medium              Fast
  Median      High            High                Medium
  Bilateral   High            Very High           Slow

## Effect on Hough Transform

### Too little blur

-   Many noisy edges
-   False lines
-   False circles

### Too much blur

-   Missing edges
-   Missing small circles
-   Poor radius estimation

## Requirements

``` bash
pip install opencv-python
pip install numpy
pip install matplotlib
```

## Project Structure

``` text
Hough-Transform/
├── images/
├── line_detection.py
├── circle_detection.py
├── filtering_comparison.py
├── README.md
```

## Conclusion

Choosing an appropriate preprocessing filter is essential. Moderate
Gaussian or Median Blur often improves Hough Transform by suppressing
noise while preserving important edges.
