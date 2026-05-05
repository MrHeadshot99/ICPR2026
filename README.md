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
├── train_full_df_clean.csv
├── test_hold_df_clean.csv
├── cleanup_log_train_full.csv
├── cleanup_log_test_hold.csv
├── icpr2026_wheat_rust_proposed_clean_github.ipynb
├── notebook5c6c78846e (2).ipynb
└── README.md

### Notebook Descriptions

| File | Description |
|---|---|
| `icpr2026_wheat_rust_proposed_clean_github.ipynb` | Cleaned and refined version of the ICPR 2026 experimental code. This is the recommended notebook for reproducing the final pipeline. It includes clearer comments, organized sections, and cleaned explanations for GitHub release. |
| `notebook5c6c78846e (2).ipynb` | Original early-stage Kaggle notebook code. This version is kept for transparency and records the initial experimental development process. It may contain less organized code, temporary comments, and earlier experiment traces. |
