# Hough Transform: Line and Circle Detection

## Introduction

The **Hough Transform** is one of the most widely used feature extraction techniques in computer vision for detecting geometric shapes from digital images. Unlike conventional edge-based approaches, the Hough Transform is robust to noise, partial occlusion, and discontinuous object boundaries. It converts image points from the spatial domain into a parameter space, where geometric structures can be identified through a voting process.

The algorithm is commonly applied after edge detection, typically using the Canny operator, to reduce computational complexity while preserving meaningful edge information.

---

## Hough Line Transform

A straight line cannot be represented reliably by the slope-intercept equation because vertical lines produce infinite slopes. Instead, the Hough Line Transform represents a line using the polar equation

\[
\rho = x\cos\theta + y\sin\theta
\]

where **ρ** is the perpendicular distance from the origin to the line and **θ** is the angle between the x-axis and the line's normal vector.

Each edge pixel votes for all possible lines passing through it in the parameter space (ρ, θ). Peaks in the accumulator indicate the existence of dominant lines in the original image.

This voting mechanism enables the algorithm to detect lines even when they are partially missing or corrupted by noise.

---

## Hough Circle Transform

Circle detection is more challenging because a circle is described by three parameters: its center coordinates (a, b) and radius r.

\[
(x-a)^2+(y-b)^2=r^2
\]

Searching the entire three-dimensional parameter space is computationally expensive. Therefore, OpenCV implements the **Hough Gradient Method**, which combines gradient information with the voting process to estimate circle centers efficiently before determining the radius.

Compared with the standard Hough Transform, this approach significantly reduces computational cost while maintaining high detection accuracy.

---

## Line vs Circle Detection

Although both algorithms rely on the same voting principle, they differ in their parameter spaces and computational complexity. Line detection operates in a two-dimensional accumulator, whereas circle detection requires three parameters, making it more sensitive to noise and parameter selection.

Proper preprocessing is therefore essential to improve detection performance.

---

## Effect of Image Filtering

Image filtering plays an important role before applying the Hough Transform.

- **Gaussian Blur** suppresses Gaussian noise and reduces false edge responses, making it the preferred preprocessing step for circle detection.
- **Median Blur** effectively removes salt-and-pepper noise while preserving edge boundaries, improving robustness in noisy images.
- **Bilateral Filtering** smooths homogeneous regions without significantly blurring edges, often providing the highest detection accuracy.
- Excessive smoothing, however, may remove weak edges, resulting in missed lines or circles.

Selecting an appropriate filtering technique requires balancing noise reduction and edge preservation.

---

## Conclusion

The Hough Transform remains one of the most reliable classical computer vision techniques for detecting geometric primitives. Hough Line Transform provides efficient and robust line detection using a two-parameter representation, while Hough Circle Transform extends the same principle to circular objects through gradient-based optimization. When combined with suitable preprocessing and edge detection, these methods continue to achieve accurate results in industrial inspection, autonomous driving, medical imaging, and many other real-world applications.
