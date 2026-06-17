# 🔬 Polyp Segmentation with PVT-v2-B2

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?logo=pytorch&logoColor=white)
![Dataset](https://img.shields.io/badge/Dataset-Kvasir--SEG-green)
![Dice Score](https://img.shields.io/badge/Test%20Dice-90.94%25-brightgreen)
![IoU](https://img.shields.io/badge/Test%20IoU-83.74%25-brightgreen)
![License](https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey)

A medical image segmentation pipeline for colonoscopy polyp detection using **Pyramid Vision Transformer v2 (PVT-v2-B2)** as backbone with a **PolypPVT-style decoder**, trained on the Kvasir-SEG dataset.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Architecture](#-architecture)
- [Dataset](#-dataset)
- [Training Setup](#-training-setup)
- [Results](#-results)
- [XAI — Grad-CAM](#-xai--grad-cam)
- [Notebook Structure](#-notebook-structure)

---

## 🧠 Overview

This notebook implements an end-to-end polyp segmentation system using a transformer-based backbone. The model leverages multi-scale feature extraction from PVT-v2-B2 and fuses them through a Channel Feature Module (CFM) decoder for precise boundary detection.

| Property         | Value                                      |
|------------------|--------------------------------------------|
| **Model**        | PVT-v2-B2 + PolypPVT-style Decoder        |
| **Task**         | Binary Semantic Segmentation               |
| **Dataset**      | Kvasir-SEG                                 |
| **Image Size**   | 448 × 448                                  |
| **Batch Size**   | 4 (Mixed Precision / AMP)                  |
| **Seed**         | 42                                         |

---

## 🏗️ Architecture

```
Input Image (448×448)
        │
   PVT-v2-B2 Backbone (timm)
   ├── Stage 1 → P1 features
   ├── Stage 2 → P2 features
   ├── Stage 3 → P3 features
   └── Stage 4 → P4 features
        │
   Channel Feature Module (CFM)
   └── Multi-scale lateral fusion
        │
   Segmentation Head
        │
   Output Mask (448×448)
```

**Key Components:**
- **Backbone:** PVT-v2-B2 via `timm` — hierarchical transformer with linear attention
- **Decoder:** CFM (Channel Feature Module) — lightweight cross-level feature fusion
- **Deep Supervision:** Auxiliary outputs at intermediate stages during training
- **Loss:** `DiceLoss × 0.5 + BCEWithLogitsLoss × 0.5`

---

## 📂 Dataset

**Kvasir-SEG** — A publicly available colonoscopy dataset for polyp segmentation.

| Split    | Images | Percentage |
|----------|--------|------------|
| Train    | 700    | 70%        |
| Val      | 150    | 15%        |
| Test     | 150    | 15%        |
| **Total**| **1000** | **100%** |

**Augmentations (Training):**
- Random horizontal & vertical flip
- Random rotation
- Color jitter (brightness, contrast)
- Normalization (ImageNet mean/std)

---

## ⚙️ Training Setup

| Parameter        | Value                                      |
|------------------|--------------------------------------------|
| Optimizer        | AdamW (lr=1e-4, weight_decay=1e-4)        |
| Scheduler        | ReduceLROnPlateau (factor=0.5, patience=5)|
| Epochs           | 100 (max)                                  |
| Early Stopping   | 20 epochs patience                         |
| Best Epoch       | 38                                         |
| Precision        | Mixed (fp16 + fp32 AMP)                   |

---

## 📊 Results

### Validation Results (Best Epoch: 38)

| Metric        | Score   |
|---------------|---------|
| Dice Score    | **92.76%** |
| IoU Score     | **88.38%** |
| Precision     | 95.71%  |
| Sensitivity   | 92.07%  |
| Specificity   | 99.28%  |

### Test Results

| Metric        | Score   |
|---------------|---------|
| Dice Score    | **90.94%** |
| IoU Score     | **83.74%** |
| Precision     | 94.37%  |
| Sensitivity   | 87.70%  |
| Specificity   | 98.91%  |

### Multi-Threshold Evaluation (Test Set)

| Threshold | Dice   | IoU    | Precision | Sensitivity | Specificity |
|-----------|--------|--------|-----------|-------------|-------------|
| 0.3       | 0.9107 | 0.8625 | 0.9350    | 0.9134      | 0.9872      |
| 0.4       | 0.9104 | 0.8621 | 0.9395    | 0.9083      | 0.9880      |
| **0.5**   | **0.9097** | **0.8612** | **0.9432** | **0.9036** | **0.9887** |
| 0.6       | 0.9087 | 0.8596 | 0.9467    | 0.8986      | 0.9893      |
| 0.7       | 0.9071 | 0.8571 | 0.9502    | 0.8925      | 0.9900      |

> 🏆 **Best Threshold:** 0.3 → Dice = 0.9107, IoU = 0.8625

---

## 🔍 XAI — Grad-CAM

Gradient-weighted Class Activation Mapping (**Grad-CAM**) is applied to visualize which regions of the image the model focuses on during segmentation.

- **Target Layer:** `cfm4` (lateral fusion block)
- **Library:** `grad-cam` (pytorch-grad-cam)
- Heatmaps are overlaid on the original colonoscopy images to provide explainability for clinical interpretation.

---

## 📓 Notebook Structure

| Cell | Description |
|------|-------------|
| 1    | GPU Check |
| 2    | Seed Setup (seed=42) |
| 2b   | PVT-v2 Backbone + PolypPVT Decoder definition |
| 2c   | Full segmentation model (CFM + Deep Supervision) |
| 3    | Kaggle Setup & Kvasir-SEG Download |
| 4    | Path Setup |
| 5    | 70/15/15 Train-Val-Test Split |
| 6    | Dataset Class & DataLoaders |
| 7    | Sample Visualization |
| 8    | Loss, Optimizer, Scheduler Setup |
| 9    | Training Loop |
| 10   | Training Curves |
| 11   | Final Test Evaluation |
| 11b  | Multi-Threshold Evaluation |
| 12   | Prediction Visualization |
| 13   | XAI (Grad-CAM) |
| 14   | Google Drive Save |

---

## 🛠️ Dependencies

```bash
pip install torch torchvision timm einops
pip install segmentation-models-pytorch albumentations
pip install grad-cam kaggle
```

---

## 📜 License

Dataset: [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/) — Kvasir-SEG (SimulaMet)
