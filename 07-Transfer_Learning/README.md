# 🧠 Deep Learning with Functional API & Transfer Learning


---

# 📖 Overview

This repository provides an educational introduction to two of the most important concepts in modern Deep Learning using TensorFlow/Keras:

- **Functional API**
- **Transfer Learning**

These techniques are widely used for building flexible neural network architectures and leveraging powerful pre-trained models.

---

# 📑 Table of Contents

- [Why Functional API?](#-why-functional-api)
- [Sequential vs Functional API](#-sequential-vs-functional-api)
- [Advantages of Functional API](#-advantages-of-functional-api)
- [Transfer Learning](#-transfer-learning)
- [Feature Extraction vs Fine-Tuning](#-feature-extraction-vs-fine-tuning)
- [Popular Pretrained Models](#-popular-pretrained-models)
- [TensorFlow/Keras Applications](#-tensorflowkeras-applications)
- [Understanding the Model Table](#-understanding-the-model-table)
- [References](#-references)

---

# 🔷 Why Functional API?

The **Functional API** is an advanced way to build deep learning models in TensorFlow/Keras.

Unlike the Sequential API, it allows developers to create complex architectures where:

- Multiple inputs are possible.
- Multiple outputs are supported.
- Layers can be reused.
- Skip connections can be created.
- Branching architectures become easy.
- Residual networks and attention mechanisms can be implemented naturally.

The Functional API represents the neural network as a **Directed Acyclic Graph (DAG)** rather than a simple stack of layers.

---

# 🔄 Sequential vs Functional API

| Sequential API | Functional API |
|----------------|---------------|
| Single input | Multiple inputs |
| Single output | Multiple outputs |
| Linear architecture | Arbitrary graph architecture |
| No skip connections | Supports skip connections |
| Difficult layer sharing | Easy layer reuse |
| Limited flexibility | Highly flexible |

---

# ✅ Advantages of Functional API

✔ Flexible network architecture

✔ Residual Connections (ResNet)

✔ Dense Connections (DenseNet)

✔ Multi-input networks

✔ Multi-output networks

✔ Siamese Networks

✔ U-Net

✔ Autoencoders

✔ Attention-based architectures

✔ Easy visualization

---

# 🚀 Transfer Learning

Transfer Learning is a machine learning technique where a model trained on a very large dataset is reused as the starting point for another task.

Instead of training millions of parameters from scratch, we leverage knowledge that has already been learned.

Typically:

- Load a pretrained model
- Remove the classification head
- Add new custom layers
- Train only the new layers
- Optionally fine-tune part of the backbone

This significantly reduces:

- Training time
- Required dataset size
- Computational cost

while often improving accuracy.

---

# 🎯 Feature Extraction vs Fine-Tuning

## Feature Extraction

The pretrained backbone remains **frozen**.

```
Pretrained Model
        ↓
 Frozen Layers
        ↓
 New Dense Layers
        ↓
 Prediction
```

Advantages

- Very fast
- Requires little data
- Prevents overfitting

---

## Fine-Tuning

Some pretrained layers are unfrozen and trained again.

```
Pretrained Model
        ↓
 Partially Trainable Layers
        ↓
 New Classification Layers
        ↓
 Prediction
```

Advantages

- Higher accuracy
- Better domain adaptation
- Learns task-specific features

Requires:

- Lower learning rate
- More training time
- Larger dataset

---

# 🏗 Popular Pretrained Models

TensorFlow/Keras provides many state-of-the-art pretrained CNN architectures.

Some popular examples include:

| Model | Main Idea |
|--------|-----------|
| MobileNet | Lightweight CNN |
| MobileNetV2 | Inverted Residual Blocks |
| MobileNetV3 | Efficient Mobile Architecture |
| EfficientNet | Compound Scaling |
| EfficientNetV2 | Faster Training |
| ResNet50 | Residual Learning |
| ResNet101 | Deep Residual Network |
| DenseNet121 | Dense Connections |
| DenseNet169 | Dense Connectivity |
| DenseNet201 | Improved Dense Blocks |
| InceptionV3 | Multi-scale Filters |
| InceptionResNetV2 | Inception + Residual |
| NASNetMobile | Neural Architecture Search |
| NASNetLarge | Large NAS Architecture |
| Xception | Depthwise Separable Convolutions |
| VGG16 | Classic CNN |
| VGG19 | Deeper VGG |
| ConvNeXt | Modern CNN Architecture |

---

# 📚 TensorFlow/Keras Applications

Official documentation:

https://keras.io/api/applications/

This page contains all pretrained models available in Keras along with their performance metrics and usage examples.

---

# 📊 Understanding the Model Table

Inside the Keras Applications page, you'll find a comparison table containing several important metrics.

Understanding these metrics helps you choose the most appropriate model for your project.

| Metric | Description |
|---------|-------------|
| Top-1 Accuracy | Percentage of images whose correct class is the model's highest-confidence prediction. Higher is better. |
| Top-5 Accuracy | Percentage of images where the correct label appears within the five most probable predictions. Commonly used for ImageNet evaluation. |
| Parameters | Total number of trainable parameters. Larger models usually require more memory and computation. |
| Depth | Number of weighted layers in the network. Deeper networks generally learn more complex representations. |
| Size (MB) | Approximate storage size of the pretrained model weights. |
| CPU Inference Time | Average prediction time when running on a CPU. Lower values indicate faster inference. |
| GPU Inference Time | Average prediction time on a GPU. Useful for estimating deployment performance. |

---

# ⚖ Choosing the Right Model

Different applications require different trade-offs.

### Mobile & Embedded Devices

- MobileNet
- MobileNetV2
- MobileNetV3
- EfficientNetB0

Advantages:

- Small size
- Fast inference
- Low memory usage

---

### High Accuracy

- EfficientNetV2
- ConvNeXt
- ResNet101
- DenseNet201

Advantages:

- Better feature extraction
- Higher ImageNet accuracy
- Excellent transfer learning performance

---

### Balanced Choice

- EfficientNetB0
- EfficientNetB3
- ResNet50
- DenseNet121

These models provide a good compromise between speed and accuracy.

---

# 💡 Typical Transfer Learning Workflow

```
Dataset
   │
   ▼
Load Pretrained Model
   │
   ▼
Freeze Backbone
   │
   ▼
Add New Layers
   │
   ▼
Train Classifier
   │
   ▼
(Optional)
Fine-Tune Backbone
   │
   ▼
Evaluate Model
```

---

# 📖 References

- TensorFlow Documentation  
  https://www.tensorflow.org/

- Keras Applications  
  https://keras.io/api/applications/

- ImageNet Dataset  
  https://www.image-net.org/

- TensorFlow Transfer Learning Guide  
  https://www.tensorflow.org/tutorials/images/transfer_learning

---

# ⭐ If this repository was helpful, consider giving it a star!

```
⭐ Star the repository
🍴 Fork it
📚 Learn
🚀 Build amazing Deep Learning projects!
```

---
