# Hough Transform for Line and Circle Detection

A simple and practical introduction to **Hough Transform** for detecting **lines** and **circles** in digital image processing, along with the effect of preprocessing filters such as **Gaussian Blur**, **Median Blur**, and other smoothing techniques.

---

## Table of Contents

- [Introduction](#introduction)
- [What is Hough Transform?](#what-is-hough-transform)
- [Hough Transform for Line Detection](#hough-transform-for-line-detection)
- [Hough Transform for Circle Detection](#hough-transform-for-circle-detection)
- [Role of Preprocessing in Hough Transform](#role-of-preprocessing-in-hough-transform)
- [Effect of Filters on Line and Circle Detection](#effect-of-filters-on-line-and-circle-detection)
  - [Gaussian Blur](#gaussian-blur)
  - [Median Blur](#median-blur)
  - [Bilateral Filter](#bilateral-filter)
  - [Canny Edge Detection](#canny-edge-detection)
  - [Thresholding](#thresholding)
- [Advantages](#advantages)
- [Limitations](#limitations)
- [Applications](#applications)
- [Conclusion](#conclusion)

---

## Introduction

In image processing and computer vision, detecting geometric shapes such as **straight lines** and **circles** is a common and important task. One of the most well-known classical methods for this purpose is the **Hough Transform**.

The Hough Transform is especially useful when:

- the image contains noise,
- edges are incomplete,
- shapes are partially occluded,
- direct detection in image space is difficult.

This method converts the detection problem from the **image space** into a **parameter space**, where edge points vote for possible shapes.

---

## What is Hough Transform?

The **Hough Transform** is a feature extraction technique used to detect specific shapes in an image.

Instead of directly searching for lines or circles in the image, the algorithm works as follows:

1. Detect edge points in the image
2. Map each edge point into a parameter space
3. Let each point vote for possible shapes
4. Detect peaks in the accumulator space
5. Interpret these peaks as detected lines or circles

The main idea is that if many edge points support the same shape, their votes accumulate in the same region of parameter space.

---

## Hough Transform for Line Detection

### Line Representation

Although a line can be written as:

\[
y = mx + b
\]

this form is not suitable for vertical lines because the slope \(m\) becomes infinite.

So, Hough Transform uses the **polar representation** of a line:

\[
\rho = x \cos\theta + y \sin\theta
\]

Where:

- \(\rho\) is the perpendicular distance from the origin to the line
- \(\theta\) is the angle of the normal line

### Detection Process

For each edge point \((x, y)\):

- different values of \(\theta\) are considered,
- the corresponding \(\rho\) values are computed,
- votes are stored in an accumulator array.

If many image points lie on the same line, their sinusoidal curves in Hough space intersect at a common point.

### Result

The line is detected by locating peaks in the \((\rho, \theta)\) accumulator space.

---

## Hough Transform for Circle Detection

### Circle Representation

A circle is defined by:

\[
(x - a)^2 + (y - b)^2 = r^2
\]

Where:

- \((a, b)\) is the center of the circle
- \(r\) is the radius

### Detection Process

For each edge point:

- possible values of radius are assumed,
- corresponding possible circle centers are estimated,
- votes are accumulated in the parameter space.

Unlike line detection, circle detection requires estimating three parameters:

- center \(a\)
- center \(b\)
- radius \(r\)

Because of this, circle detection is more computationally expensive than line detection.

### Result

A circle is detected where a strong peak appears in the 3D parameter space of center coordinates and radius.

---

## Role of Preprocessing in Hough Transform

Hough Transform heavily depends on **edge quality**.  
If the edges are noisy, broken, or weak, the voting process becomes unreliable.

Therefore, preprocessing is usually applied before Hough Transform in order to:

- reduce noise,
- smooth unnecessary texture,
- preserve meaningful edges,
- improve the output of edge detection methods such as Canny.

A typical pipeline is:
```text
Input Image
   ↓
Convert to Grayscale
   ↓
Apply Smoothing Filter
   ↓
Edge Detection
   ↓
Hough Transform
   ↓
Shape Detection
