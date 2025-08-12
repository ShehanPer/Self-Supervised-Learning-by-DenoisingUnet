# Self-Supervised-Learning-by-DenoisingUnet
A self-supervised learning pipeline using a denoising U-Net for feature extraction, followed by transfer learning to fine-tune the encoder for binary image classification (Cat vs Turtle) with minimal labeled data


This repository demonstrates a complete **Self-Supervised Learning (SSL)** workflow using a **Denoising U-Net** as a pretext task, followed by **transfer learning** for image classification.

## 📌 Overview

In many real-world scenarios, labeled datasets are scarce and expensive to obtain, but unlabeled data is abundant.  
This project leverages **Self-Supervised Learning** to learn rich visual features from *unlabeled data* using a denoising objective, and then fine-tunes the learned encoder for a **binary classification task** (Cat 🐱 vs Turtle 🐢) using a small labeled dataset.

## 🚀 Pipeline

1. **Dataset Preparation**
   - Unlabeled dataset → Used for pretraining via denoising task.
   - Labeled dataset → Small set for fine-tuning the classification head.
   - Added artificial noise (Salt & Pepper, Gaussian) for the pretext task.
   - Dataset split into **train**, **validation**, and **test** sets.

2. **Pretext Task — Denoising**
   - Implemented a **U-Net** architecture with `Conv2D` layers, encoder-decoder structure, and skip connections.
   - Trained to remove added noise from input images.
   - Extracted and visualized **encoder feature maps** (heatmaps) to understand what the model learns at different levels.

3. **Feature Transfer**
   - Saved the pretrained encoder weights.
   - Attached a **classification head** (Conv + Linear layers).
   - Fine-tuned on a small labeled dataset while freezing most encoder layers.

4. **Evaluation**
   - Plotted denoising results (`Clean`, `Noisy`, `Denoised`) for qualitative analysis.
   - Measured classification **loss** and **accuracy** during training.
   - Visualized **predictions** on test set with predicted vs. true labels.

## 🏗 Architecture

### U-Net Encoder-Decoder
- **Encoder**: 4 downsampling blocks (Conv → BN → ReLU → MaxPool).
- **Bottleneck**: High-level feature extraction.
- **Decoder**: 3 upsampling blocks with skip connections from encoder.
- **Output**: Cleaned (denoised) image.

### Classification Head
- Global Average Pooling
- Fully Connected Layer(s) → Output layer (Binary classification with sigmoid activation)

## 📊 Results

### Denoising
- The denoising U-Net successfully removed Gaussian and Salt & Pepper noise.
- Deeper encoder layers learned more **abstract features** and sometimes emphasized background vs. object depending on learned representations.

### Classification
- Fine-tuned model achieved high accuracy on a small labeled dataset.
- Demonstrated the power of **SSL** for low-data regimes.


### 📓 Notebook

The original notebook file could not be uploaded here due to size limitations.  
You can access the full Colab notebook with all code, experiments, and visualizations here:

[Self-Supervised Learning by Denoising U-Net — Colab Notebook](https://colab.research.google.com/drive/1y6V7FnIc69GJDz3SMn5IFYEngjlPir8i?usp=drive_link)

