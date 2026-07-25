# Hough Transform: Line and Circle Detection

<p align="center">

![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-blue?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-Programming-green?style=for-the-badge)

</p>

> An educational introduction to the **Hough Transform**, including line detection, circle detection, and the impact of image filtering on detection performance.

---

## Introduction

The **Hough Transform** is a classical feature extraction technique used in computer vision to detect geometric shapes such as straight lines and circles. Unlike simple edge-based methods, it remains effective even when objects are partially occluded, noisy, or discontinuous. Instead of detecting shapes directly in the image space, the algorithm maps edge pixels into a **parameter space**, where each pixel votes for all possible shapes passing through it. Peaks in this voting space indicate the presence of a valid geometric object.

---

## Hough Line Transform

A line is represented in polar form rather than slope-intercept form:

$$
\rho=x\cos\theta+y\sin\theta
$$

where **ρ** is the perpendicular distance from the origin and **θ** is the angle of the line normal.

Each edge pixel contributes votes in the accumulator space. The parameters receiving the highest number of votes correspond to the detected lines. This representation naturally handles vertical lines and improves robustness against image noise.

---

## Hough Circle Transform

A circle is defined by its center $(a,b)$ and radius $r$:

$$
(x-a)^2+(y-b)^2=r^2
$$

Circle detection requires estimating three parameters, making it more computationally demanding than line detection. OpenCV therefore uses the **Hough Gradient Method**, which exploits edge gradients to estimate circle centers before searching for the radius, significantly reducing computational cost.

---

## Effect of Image Filtering

Proper preprocessing strongly influences detection accuracy.

| Filter | Effect on Detection |
|---------|---------------------|
| Gaussian Blur | Reduces Gaussian noise and improves circle detection. |
| Median Blur | Removes salt-and-pepper noise while preserving edges. |
| Bilateral Filter | Smooths the image while maintaining sharp edges. |
| Box Blur | Fast but may blur important edge information. |

Choosing an appropriate filter is a trade-off between **noise suppression** and **edge preservation**. Excessive smoothing may remove weak edges and reduce the number of detected lines or circles.

---

## Conclusion

The Hough Transform remains one of the most reliable classical algorithms for detecting geometric primitives. When combined with edge detection and suitable image filtering, it provides accurate and robust results for applications such as lane detection, industrial inspection, medical imaging, and autonomous systems.

---

## References

- Richard O. Duda and Peter E. Hart, *Use of the Hough Transformation to Detect Lines and Curves in Pictures*, 1972.
- Rafael C. Gonzalez & Richard E. Woods, *Digital Image Processing*.
- OpenCV Documentation.

---

## ⭐ Support

If you found this repository useful, please consider giving it a **⭐ Star** on GitHub.
