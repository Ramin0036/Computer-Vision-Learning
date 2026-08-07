# Define the original content for each file to ensure accuracy

> 📑 Comprehensive GitHub README about the evolution of the R-CNN family.

## 📋 Table of Contents
- Introduction
- Object Detection Pipeline
- Sliding Window
- Selective Search
- R-CNN
- Fast R-CNN
- Faster R-CNN
- Region Proposal Network (RPN)
- Comparison Tables
- Advantages & Disadvantages
- References

# 💡 Introduction
Object detection aims to classify and localize objects simultaneously.

## 🎯 Classification vs Localization vs Detection

| Task | Output |
|---|---|
| Classification | Class |
| Localization | Class + Bounding Box |
| Detection | Multiple Classes + Multiple Bounding Boxes |

# 🪟 Sliding Window
Traditional methods evaluate thousands of windows across an image, making them computationally expensive.

# 🔍 Selective Search
Selective Search groups similar regions using hierarchical segmentation to generate approximately 2,000 candidate object regions.

### ✅ Pros
- No training required
- High recall

### ❌ Cons
- Slow
- Hand-crafted algorithm
- Not end-to-end

# 🧠 R-CNN (2014)

Pipeline:
1. Selective Search
2. Warp each proposal
3. CNN feature extraction
4. SVM classification
5. Bounding-box regression

### 🌟 Advantages
- Huge accuracy improvement over traditional methods.

### ⚠️ Disadvantages
- Very slow
- Multi-stage training
- Large disk storage for extracted features

# ⚡ Fast R-CNN (2015)

Improvements:
- CNN runs once on the whole image.
- ROI Pooling extracts proposal features.
- Joint classification and box regression.

### 📥 ROI Pooling
Converts proposals with different sizes into fixed-size feature maps.

### ⏳ Remaining Bottleneck
Selective Search is still required.

# 🚀 Faster R-CNN (2015)

Major innovation:
Selective Search is replaced by a Region Proposal Network (RPN).

## 🏗️ Region Proposal Network

The RPN slides a small network over the feature map and predicts:
- Objectness score
- Bounding box offsets

### ⚓ Anchor Boxes
Multiple anchors with different scales and aspect ratios are evaluated at each location.

## ⏩ Why Faster?

The backbone CNN is shared between proposal generation and detection.

# 📈 Evolution

```mermaid
graph LR
A[Sliding Window]
-->B[Selective Search]
-->C[R-CNN]
-->D[Fast R-CNN]
-->E[Faster R-CNN]
