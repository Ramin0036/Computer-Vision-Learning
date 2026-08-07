# 🎨 Semantic Segmentation

## 📑 Contents
- Introduction
- Architectures
- U-Net
- ResNet
- DeepLabV3
- DeepLabV3+
- Model Comparison
- References

# 📖 Introduction
Semantic segmentation assigns a class label to every pixel in an image.

# 🏗️ Architectures

## 🏥 U-Net
- **Structure**: Encoder-Decoder with Skip Connections.
- **Use Case**: Excellent for medical imaging and sharp boundary detection.

## 🔗 ResNet
- **Concept**: Residual blocks ($Output = F(x) + x$) to solve vanishing gradients.
- **Use Case**: Often used as the backbone architecture.

## 🧪 DeepLabV3
- **Feature**: Atrous convolution (Dilated) and ASPP (Atrous Spatial Pyramid Pooling).
- **Use Case**: Capturing multi-scale context.

## ✨ DeepLabV3+
- **Improvement**: Encoder-Decoder structure + better boundary refinement.

# 📊 Model Comparison

| Model | Best For | Key Trait |
|---|---|---|
| U-Net | Medical Images | Skip Connections |
| DeepLabV3 | Multi-scale Context | ASPP |
| DeepLabV3+ | Boundary Sharpness | Encoder-Decoder |

# 📚 References
- U-Net: Convolutional Networks for Biomedical Image Segmentation (MICCAI 2015)
- DeepLabV3: Rethinking Atrous Convolution (CVPR 2017)
- DeepLabV3+: Encoder-Decoder with Atrous Separable Convolution (ECCV 2018)

