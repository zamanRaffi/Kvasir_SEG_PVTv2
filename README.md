# 🔬 PVT-v2-B2-FPN: A Multi-Resolution Transformer-Based Framework for Accurate Colorectal Polyp Segmentation

> Official PyTorch implementation of our proposed transformer-based framework for colorectal polyp segmentation using a PVT-v2-B2 backbone and an FPN-inspired multi-resolution decoder.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?logo=pytorch&logoColor=white)
![Dataset](https://img.shields.io/badge/Dataset-Kvasir--SEG-green)
![Task](https://img.shields.io/badge/Task-Polyp%20Segmentation-success)
![Conference](https://img.shields.io/badge/IEEE-CSDE%202026-blue)
![Status](https://img.shields.io/badge/Status-Under%20Review-orange)

---

# 📖 Overview

Colorectal cancer remains one of the leading causes of cancer-related deaths worldwide. Accurate segmentation of colorectal polyps from colonoscopy images is essential for early diagnosis and computer-aided clinical decision-making.

This repository provides the official PyTorch implementation of our proposed **PVT-v2-B2-FPN** framework, which combines the hierarchical feature representation capability of **Pyramid Vision Transformer v2 (PVT-v2-B2)** with an **FPN-inspired multi-resolution decoder** for accurate and robust polyp segmentation.

---

# ✨ Highlights

- ✅ Transformer-based segmentation framework
- ✅ PVT-v2-B2 backbone
- ✅ FPN-inspired multi-resolution decoder
- ✅ Deep supervision
- ✅ Mixed Precision (AMP) training
- ✅ Grad-CAM explainability
- ✅ Google Colab ready
- ✅ PyTorch implementation

---

# 🏗️ Model Architecture

```
Input Image (448×448)
        │
PVT-v2-B2 Backbone
        │
Multi-scale Feature Extraction
        │
FPN-inspired Decoder
        │
Segmentation Head
        │
Predicted Polyp Mask
```

---

# 📂 Dataset

**Dataset:** Kvasir-SEG

| Split | Images |
|-------|--------|
| Training | 700 |
| Validation | 150 |
| Testing | 150 |
| Total | 1000 |

### Data Augmentation

- Random Horizontal Flip
- Random Vertical Flip
- Random Rotation
- Color Jitter
- ImageNet Normalization

---

# ⚙️ Training Configuration

| Parameter | Value |
|-----------|-------|
| Backbone | PVT-v2-B2 |
| Decoder | FPN-inspired |
| Image Size | 448 × 448 |
| Batch Size | 4 |
| Optimizer | AdamW |
| Learning Rate | 1e-4 |
| Weight Decay | 1e-4 |
| Scheduler | ReduceLROnPlateau |
| Epochs | 100 |
| Early Stopping | 20 |
| Mixed Precision | AMP |

---

# 📊 Experimental Results

## Validation Performance

| Metric | Score |
|---------|-------|
| Dice | **92.76%** |
| IoU | **88.38%** |
| Precision | 95.71% |
| Sensitivity | 92.07% |
| Specificity | 99.28% |

---

## Test Performance

| Metric | Score |
|---------|-------|
| Dice | **90.94%** |
| IoU | **83.74%** |
| Precision | 94.37% |
| Sensitivity | 87.70% |
| Specificity | 98.91% |

---

## Multi-Threshold Evaluation

| Threshold | Dice | IoU |
|-----------|------|------|
| 0.3 | **91.07%** | **86.25%** |
| 0.4 | 91.04% | 86.21% |
| 0.5 | 90.97% | 86.12% |
| 0.6 | 90.87% | 85.96% |
| 0.7 | 90.71% | 85.71% |

🏆 **Best Threshold:** **0.3**

---

# 🔍 Explainability

Grad-CAM is employed to visualize the discriminative regions used by the model during segmentation.

- Target Layer: Final Decoder Block
- Visualization: Heatmap Overlay
- Framework: pytorch-grad-cam

---

# 🚀 Installation

```bash
git clone https://github.com/zamanRaffi/pvt-v2-b2-fpn-polyp-segmentation.git

cd pvt-v2-b2-fpn-polyp-segmentation

pip install -r requirements.txt
```

---

# 📂 Repository Structure

```
pvt-v2-b2-fpn-polyp-segmentation/
│
├── PVTv2_B2_FPN.ipynb
│
├── README.md
├── LICENSE
```

---

# 📄 Paper

## Title

**PVT-v2-B2-FPN: A Multi-Resolution Transformer-Based Framework for Accurate Colorectal Polyp Segmentation**

**Conference**

**IEEE Asia-Pacific Conference on Computer Science and Data Engineering (CSDE 2026)**

**Status**

🟠 Under Review

Paper link will be added after publication.

---

# 📚 Citation

If you find this repository useful, please cite our paper.

```bibtex
@inproceedings{zaman2026,
  title={PVT-v2-B2-FPN: A Multi-Resolution Transformer-Based Framework for Accurate Colorectal Polyp Segmentation},
  author={S. M. Ashraful Zaman and Ahanaf Ibnat Abani and Surovi Rani and Md Shariful Islam and Md. Darun Nayeem and Muhammad Aminur Rahaman},
  booktitle={Proceedings of the 11th IEEE Asia-Pacific Conference on Computer Science and Data Engineering (CSDE 2026)},
  note={Under Review},
  year={2026}
}
```

---

# 🙏 Acknowledgements

- PVT-v2
- timm
- PyTorch
- Albumentations
- Kvasir-SEG
- Grad-CAM
- Google Colab

---

# 📜 License

This repository is released under the **MIT License**.

The **Kvasir-SEG** dataset is distributed under **CC BY-NC 4.0**. Please refer to the original dataset license for dataset usage.

---

# 👨‍💻 Authors

**S. M. Ashraful Zaman (Raffi Zaman)**

**Ahanaf Ibnat Abani**

**Surovi Rani**

**Md Shariful Islam**

**Md. Darun Nayeem**

**Muhammad Aminur Rahaman**

Department of Computer Science and Engineering

Bangladesh University of Business and Technology (BUBT)

---

⭐ If you find this repository useful, please consider giving it a star.
