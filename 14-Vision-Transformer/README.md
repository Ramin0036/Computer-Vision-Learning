# 👁️ Vision Transformer (ViT)

### 🧠 Applying Transformers to Computer Vision

---

## 🌟 Introduction

For many years, **Convolutional Neural Networks (CNNs)** were the dominant architecture in Computer Vision.

Models such as:

- 🖼️ AlexNet
- 🏗️ VGG
- 🚀 ResNet
- ⚡ EfficientNet

achieved remarkable results by using **Convolution operations** to extract visual features.

But an important question emerged:

> ❓ Do we really need Convolution to understand an image?

**Vision Transformer (ViT)** provides a different answer.

Instead of processing an image directly with convolutional layers, ViT divides the image into small **patches** and treats these patches similarly to tokens in a sentence.

The overall idea can be summarized as:

```text
🖼️ Image
   ↓
✂️ Split into Patches
   ↓
🔢 Patch Embeddings
   ↓
📍 Positional Embeddings
   ↓
🧠 Transformer Encoder
   ↓
🎯 Classification Head
   ↓
Prediction
```

---

## 🧩 Core Idea of Vision Transformer

The central idea behind ViT is surprisingly simple:

> 🧠 **If a Transformer can learn relationships between words in a sentence, why can't it learn relationships between different parts of an image?**

A sentence can be represented as a sequence of tokens:

```text
"The cat is sitting"
```

Similarly, an image can be divided into visual patches:

```text
┌────┬────┬────┬────┐
│ P1 │ P2 │ P3 │ P4 │
├────┼────┼────┼────┤
│ P5 │ P6 │ P7 │ P8 │
├────┼────┼────┼────┤
│ P9 │P10 │P11 │P12 │
├────┼────┼────┼────┤
│P13 │P14 │P15 │P16 │
└────┴────┴────┴────┘
```

Each patch becomes a **visual token** that can be processed by the Transformer.

---

# 🖼️ 1. Splitting the Image into Patches

Assume we have an RGB image with:

```text
Image = 224 × 224 × 3
```

and choose a patch size of:

```text
Patch Size = 16 × 16
```

The number of patches is:

```text
(224 / 16) × (224 / 16)

= 14 × 14

= 196 Patches
```

Each patch has the dimensions:

```text
16 × 16 × 3
```

Therefore, the number of values inside each patch is:

```text
16 × 16 × 3 = 768
```

The image can now be represented as:

```text
196 Patches
      ↓
Flatten
      ↓
196 × 768
```

---

# 🔢 2. Patch Embedding

A Transformer does not directly process raw image patches.

Each image patch is first converted into a vector with a fixed embedding dimension.

This process is called:

### 🔹 Patch Embedding

Conceptually:

```text
Image Patch
     ↓
Flatten
     ↓
Linear Projection
     ↓
Patch Embedding
```

For example, if the embedding dimension is:

```text
D = 768
```

then the sequence becomes:

```text
196 × 768
```

Each row represents one image patch.

---

# 📍 3. Positional Embedding

A major challenge now appears.

A standard Transformer does not inherently know where each token is located.

For example, it does not automatically know that:

```text
Patch 1
```

is located before:

```text
Patch 2
```

or that one patch is above another patch.

Spatial information is extremely important in images.

Therefore, ViT adds **Positional Embeddings** to the patch embeddings.

Conceptually:

```text
Patch Embedding
       +
Positional Embedding
       ↓
Transformer Input
```

This allows the model to preserve information about the spatial position of each image patch.

---

# 🎯 4. Class Token

Vision Transformer introduces a special token called:

```text
[CLS]
```

The `[CLS]` token is added to the beginning of the patch sequence.

If the image contains 196 patches:

```text
196 Image Patches
       +
   1 [CLS] Token
       =
197 Tokens
```

The sequence therefore becomes:

```text
[CLS] [P1] [P2] [P3] ... [P196]
```

During the Transformer layers, the `[CLS]` token can interact with all other tokens through Self-Attention.

At the end of the network, the representation of the `[CLS]` token can be used for classification.

---

# 🧠 5. Transformer Encoder

The sequence of tokens is passed through a stack of:

### ⚙️ Transformer Encoder Blocks

A simplified Transformer Encoder Block looks like this:

```text
Input
  │
  ▼
Layer Normalization
  │
  ▼
Multi-Head Self-Attention
  │
  ▼
Residual Connection
  │
  ▼
Layer Normalization
  │
  ▼
MLP / Feed Forward Network
  │
  ▼
Residual Connection
  │
  ▼
Output
```

The two main components are:

1. 🔍 Multi-Head Self-Attention
2. 🧮 MLP / Feed Forward Network

---

# 🔍 6. Self-Attention in Vision Transformer

One of the most important ideas in the Transformer architecture is **Self-Attention**.

Self-Attention allows the model to determine how strongly one image patch should interact with other patches.

For example, consider an image containing a dog:

```text
┌─────────────────────┐
│        🐶           │
│      👂  👂         │
│                     │
│    🐾       🐾      │
└─────────────────────┘
```

A patch containing part of the dog's head can learn relationships with patches containing the body, ears, or legs.

This allows the model to capture relationships between distant regions of an image.

---

# 🎯 7. Query, Key, and Value

Self-Attention is based on three important representations:

```text
Query (Q)
Key   (K)
Value (V)
```

For every token, the model generates these representations.

Conceptually:

```text
Input
  │
  ├────► Query
  │
  ├────► Key
  │
  └────► Value
```

The similarity between Query and Key determines how much attention should be assigned to different tokens.

The standard Attention operation is:

```text
Attention(Q, K, V)
=
softmax(QKᵀ / √dₖ)V
```

The main idea is:

> 🔍 Determine which patches are important to each other and combine their information.

---

# 👥 8. Multi-Head Attention

Instead of using only one attention operation, Transformer uses multiple attention heads.

Conceptually:

```text
              ┌──► Head 1
              │
Input ────────┼──► Head 2
              │
              ├──► Head 3
              │
              └──► Head 4
```

Each head can learn different types of relationships.

For example:

```text
Head 1 → Local relationships
Head 2 → Object-level relationships
Head 3 → Long-range relationships
Head 4 → Other visual patterns
```

The outputs of all heads are then combined.

This allows the model to learn multiple types of relationships simultaneously.

---

# 🧮 9. MLP / Feed Forward Network

After the Attention operation, the token representations pass through a Feed Forward Network.

A simplified structure is:

```text
Input
  ↓
Linear Layer
  ↓
Activation Function
  ↓
Linear Layer
  ↓
Output
```

Modern Transformer architectures commonly use activation functions such as **GELU**.

The MLP provides additional nonlinear transformations and helps the model learn richer representations.

---

# 🔄 10. Residual Connections

Another important component of Transformer architectures is the **Residual Connection**.

Conceptually:

```text
          ┌──────────────────┐
          │                  │
Input ───►│ Self-Attention    ├──► Add
          │                  │
          └──────────────────┘
                    │
                    └──────────────►
```

The original input is added to the output of the sub-layer.

Residual connections help with:

- ✅ Stable training
- ✅ Better gradient propagation
- ✅ Training deeper networks
- ✅ Preserving useful information

---

# 🏗️ Overall Vision Transformer Architecture

The complete ViT pipeline can be summarized as:

```text
                 🖼️ IMAGE
                    │
                    ▼
             Split into Patches
                    │
                    ▼
              Patch Embedding
                    │
                    ▼
          Add Positional Embedding
                    │
                    ▼
                 [CLS]
                    │
                    ▼
        ┌─────────────────────────┐
        │  Transformer Encoder    │
        │                         │
        │  Multi-Head Attention   │
        │           ↓             │
        │          MLP             │
        │           ↓             │
        │      Residual + LN      │
        └─────────────────────────┘
                    │
                    ▼
               [CLS] Token
                    │
                    ▼
             Classification Head
                    │
                    ▼
              🎯 Prediction
```

---

# 🔥 Why Is Vision Transformer Important?

CNNs typically build visual representations progressively.

Conceptually:

```text
Local Features
      ↓
More Complex Features
      ↓
High-Level Features
      ↓
Global Representation
```

Self-Attention, on the other hand, can directly model relationships between different parts of an image.

For example:

```text
Patch A ───────────────────► Patch Z
           Global Relation
```

This makes Transformers particularly powerful for learning **long-range dependencies**.

---

# 🧠 What Is Inductive Bias?

One of the major differences between CNNs and ViTs is their **Inductive Bias**.

CNNs naturally contain assumptions about images.

### 📌 Locality

Nearby pixels are often related to each other.

### 📌 Translation Equivariance

Visual patterns can appear at different locations in an image.

Because of these assumptions, CNNs have a strong image-specific inductive bias.

Vision Transformers have fewer such built-in assumptions.

Conceptually:

```text
CNN
 ↓
Strong Image-Specific Inductive Bias

ViT
 ↓
More Flexible Representation Learning
```

This flexibility can be an advantage, but it also means that ViTs generally benefit strongly from large-scale datasets and effective pretraining.

---

# ⚔️ Vision Transformer vs CNN

| Feature | CNN 🧱 | Vision Transformer 🧠 |
|---|---|---|
| Main Processing Unit | Pixel / Feature Map | Patch / Token |
| Main Mechanism | Convolution | Self-Attention |
| Local Information | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| Global Relationships | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| Inductive Bias | Strong | Relatively Weak |
| Data Requirements | Usually Lower | Often Higher |
| Parallel Processing | Good | Excellent |
| Long-Range Dependencies | More Limited | Strong |
| Representation | Hierarchical | Token-Based |

> 💡 These are conceptual comparisons. Modern CNNs and Transformer-based models can both incorporate mechanisms that reduce these differences.

---

# 📊 Advantages of Vision Transformer

## 🚀 1. Global Relationship Modeling

Self-Attention allows the model to directly model relationships between different regions of an image.

## 🧠 2. Powerful Representation Learning

Transformers can learn highly expressive visual representations.

## ⚡ 3. Parallel Processing

Unlike sequential architectures, Transformer tokens can be processed in parallel during training.

## 🌍 4. Scalability

Transformer architectures scale effectively with increasing model size and training data.

## 🔄 5. Transfer Learning

Pretrained ViT models can be adapted to many different Computer Vision tasks.

---

# ⚠️ Disadvantages of Vision Transformer

Despite their capabilities, Vision Transformers also have limitations.

## 💾 1. Data Requirements

Early ViT models were often more dependent on large datasets and strong pretraining than traditional CNNs.

## 🧮 2. Attention Computational Cost

Standard Self-Attention has significant computational and memory costs as the number of tokens increases.

More patches mean more tokens:

```text
More Patches
     ↓
More Tokens
     ↓
More Attention Computation
```

This becomes especially important for high-resolution images.

## 📍 3. Spatial Structure Is Not Built In

Unlike CNNs, ViTs do not naturally encode image locality and spatial structure through convolution.

Therefore, positional information and appropriate architectural design become important.

---

# 🧪 Training Pipeline

The overall training process can be summarized as:

```text
🖼️ Input Image
      ↓
✂️ Patch Extraction
      ↓
🔢 Patch Embedding
      ↓
📍 Positional Embedding
      ↓
🧠 Transformer Encoder
      ↓
🎯 Classification Head
      ↓
📉 Loss Calculation
      ↓
🔄 Backpropagation
      ↓
⚙️ Optimizer Update
```

This process is repeated for batches of training images across multiple epochs.

---

# 🎯 Applications of Vision Transformers

Vision Transformers are not limited to image classification.

Transformer-based architectures are now widely used across Computer Vision:

```text
🖼️ Image Classification
        ↓
🔍 Object Detection
        ↓
🎭 Semantic Segmentation
        ↓
🎯 Instance Segmentation
        ↓
🧩 Image Recognition
        ↓
🌐 Multimodal Vision
```

ViT and its descendants have therefore become an important foundation for modern Computer Vision systems.

---

# 🔬 A Simple Numerical Example

Suppose we have an image:

```text
224 × 224 × 3
```

with a patch size of:

```text
16 × 16
```

The number of patches is:

```text
(224 / 16) × (224 / 16)

= 14 × 14

= 196
```

After adding the `[CLS]` token:

```text
196 + 1 = 197 Tokens
```

The complete pipeline becomes:

```text
Image
  ↓
196 Patches
  ↓
Patch Embeddings
  ↓
+ Positional Embeddings
  ↓
+ [CLS] Token
  ↓
197 Tokens
  ↓
Transformer Encoder
  ↓
[CLS] Representation
  ↓
Linear Classification Head
  ↓
Class Prediction
```

For example, the final classifier might produce:

```text
🐱 Cat      → 0.82
🐶 Dog      → 0.13
🐦 Bird     → 0.05
```

The class with the highest probability becomes the predicted class.

---

# 🆚 CNN vs ViT — Conceptual View

The fundamental difference can be visualized as follows.

### 🧱 CNN

```text
Image
  ↓
Local Receptive Fields
  ↓
Convolution
  ↓
Feature Maps
  ↓
Higher-Level Features
  ↓
Prediction
```

### 🧠 Vision Transformer

```text
Image
  ↓
Patches
  ↓
Tokens
  ↓
Self-Attention
  ↓
Global Relationships
  ↓
Prediction
```

Therefore, the difference is not simply the type of layer being used.

It is also about **how the model represents and interacts with different parts of an image**.

---

# 📚 Key Concepts

```text
Vision Transformer
├── Image Patches
├── Patch Embedding
├── Positional Embedding
├── Class Token
├── Transformer Encoder
├── Self-Attention
├── Multi-Head Attention
├── Query / Key / Value
├── MLP
├── Layer Normalization
├── Residual Connection
├── Inductive Bias
└── Transfer Learning
```

---

# 🧭 Recommended Learning Path

A useful learning path for understanding Vision Transformers is:

```text
CNN
 ↓
ResNet
 ↓
Attention
 ↓
Transformer
 ↓
Vision Transformer
 ↓
Swin Transformer
 ↓
Modern Vision Transformers
```

This progression helps build an understanding from traditional visual feature extraction to modern attention-based Computer Vision architectures.

---

# 🧠 Final Takeaway

Vision Transformer demonstrated that images can be processed effectively using the Transformer architecture without relying directly on convolution.

The central idea is:

> 🧩 **Split the image into patches, convert those patches into tokens, and use Self-Attention to learn relationships between them.**

In short:

```text
🖼️ Image
   ↓
✂️ Patches
   ↓
🔢 Embeddings
   ↓
📍 Positional Information
   ↓
🧠 Transformer Encoder
   ↓
🔍 Self-Attention
   ↓
🎯 Prediction
```

Vision Transformer represents one of the important milestones in the evolution of modern Computer Vision and provides the foundation for many newer Transformer-based visual architectures.

---

## ⭐ Quick Summary

| Stage | Purpose |
|---|---|
| 🖼️ Image | Input visual data |
| ✂️ Patch Extraction | Divide image into smaller regions |
| 🔢 Patch Embedding | Convert patches into vectors |
| 📍 Positional Embedding | Add spatial information |
| 🎯 `[CLS]` Token | Collect global representation |
| 🧠 Transformer Encoder | Learn relationships between tokens |
| 🔍 Self-Attention | Model interactions between patches |
| 🧮 MLP | Perform nonlinear feature transformation |
| 🎯 Classification Head | Produce final prediction |

---

## 🚀 The Big Picture

```text
              🖼️ IMAGE
                  │
                  ▼
          ✂️ PATCH EXTRACTION
                  │
                  ▼
          🔢 PATCH EMBEDDING
                  │
                  ▼
       📍 POSITIONAL EMBEDDING
                  │
                  ▼
              🎯 [CLS]
                  │
                  ▼
      ┌─────────────────────┐
      │ 🧠 TRANSFORMER      │
      │                     │
      │ 🔍 Self-Attention   │
      │                     │
      │ 🧮 MLP              │
      │                     │
      │ 🔄 Residual + LN    │
      └─────────────────────┘
                  │
                  ▼
          🎯 CLASSIFICATION
                  │
                  ▼
             🏆 OUTPUT
```

> ⭐ **If CNNs learn visual patterns through convolutional filters, Vision Transformers learn relationships between visual tokens through attention.**
