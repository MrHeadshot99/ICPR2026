# Dual-Branch Spectral-Spatial Network for UAV Hyperspectral Wheat Rust Detection

This repository contains the dataset files and Kaggle notebook used for the ICPR 2026 paper:

**Dual-Branch Spectral-Spatial Network with Knowledge- and Data-Driven Band Selection for UAV Hyperspectral Wheat Rust Detection**

Accepted to **ICPR 2026: 28th International Conference on Pattern Recognition**, Lyon, France.

## Overview

This project focuses on UAV-based hyperspectral image classification for wheat rust detection. The goal is to build a compact and effective spectral-spatial learning pipeline that can classify hyperspectral samples into three categories:

- `Health`
- `Rust`
- `Other`

The proposed pipeline combines:
<img width="766" height="390" alt="image" src="https://github.com/user-attachments/assets/8f192709-dfcc-4d24-9b08-48579556e19f" />

1. **Knowledge- and data-driven band selection**
2. **A pseudo-RGB 2D spatial branch**
3. **A lightweight 1D spectral branch**
4. **Feature fusion for final classification**
5. **Cleaned train/test splits based on NDVI-guided data refinement**

The repository is intended to support reproducibility of the camera-ready ICPR 2026 experiments.

---

## Repository Structure

```text
.
├── Health/
│   └── hyperspectral image files for healthy wheat samples
├── Other/
│   └── hyperspectral image files for other/background/ambiguous samples
├── Rust/
│   └── hyperspectral image files for wheat rust samples
├── train_full_df_clean.csv
├── test_hold_df_clean.csv
├── cleanup_log_train_full.csv
├── cleanup_log_test_hold.csv
└── README.md
