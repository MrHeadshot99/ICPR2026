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
```

## File Descriptions

| File | Description |
|---|---|
| `train_full_df_clean.csv` | Cleaned training dataframe used for model training and 5-fold cross-validation. |
| `test_hold_df_clean.csv` | Cleaned holdout test dataframe used only for final evaluation. |
| `cleanup_log_train_full.csv` | Log file from the NDVI-guided cleanup process for the training split. |
| `cleanup_log_test_hold.csv` | Log file from the NDVI-guided cleanup process for the holdout test split. |
| `icpr2026_wheat_rust_proposed_clean_github.ipynb` | Cleaned and refined version of the ICPR 2026 experimental code. This is the recommended notebook for reproducing the final pipeline. It includes clearer comments, organized sections, and cleaned explanations for GitHub release. |
| `notebook5c6c78846e (2).ipynb` | Original early-stage Kaggle notebook code. This version is kept for transparency and records the initial experimental development process. It may contain less organized code, temporary comments, and earlier experiment traces. |

---

## Dataset Format

The cleaned CSV files should contain at least the following columns:

```text
path,label
```

Example:

```text
Health/sample_001.tif,Health
Rust/sample_002.tif,Rust
Other/sample_003.tif,Other
```

The labels are mapped as:

```python
LABELS = ["Health", "Other", "Rust"]
```

---

## Model Pipeline

The overall pipeline consists of the following stages:

1. Load cleaned train/test CSV files
2. Load hyperspectral image cubes
3. Perform knowledge- and data-driven band selection
4. Construct 2D pseudo-RGB inputs from selected spectral bands
5. Construct 1D spectral inputs from compact selected bands
6. Train a dual-branch spectral-spatial network
7. Perform 5-fold cross-validation on the cleaned training set
8. Ensemble fold models for final holdout evaluation
9. Report classification metrics

The main evaluation metrics include:

- Overall Accuracy
- Average Accuracy
- Macro-F1 Score
- Cohen's Kappa
- Per-class Accuracy
- Confusion Matrix

---

## Environment

The experiments were developed and tested in a Kaggle notebook environment.

Install required packages if needed:

```bash
pip install timm scikit-learn matplotlib pandas numpy opencv-python tifffile
```

---

## How to Run

### Recommended Notebook

For reproducing the cleaned ICPR 2026 experiment pipeline, use:

```text
icpr2026_wheat_rust_proposed_clean_github.ipynb
```

This notebook is the cleaned and organized version of the experimental code.

### Original Kaggle Notebook

The following notebook is also included for transparency:

```text
notebook5c6c78846e (2).ipynb
```

This is the original early-stage Kaggle notebook and may contain less organized code, temporary comments, or experimental traces. It is not the recommended version for reproducing the final cleaned pipeline.

---

## Reproducibility Notes

The experiments use a fixed random seed where possible.

```python
seed = 42
```

The split files are already provided:

```text
train_full_df_clean.csv
test_hold_df_clean.csv
```

Therefore, the holdout test set should remain unchanged for fair comparison.

---

## Citation

If you use this repository, please cite our ICPR 2026 paper:

```bibtex
@inproceedings{kim2026dualbranch,
  title     = {Dual-Branch Spectral-Spatial Network with Knowledge- and Data-Driven Band Selection for UAV Hyperspectral Wheat Rust Detection},
  author    = {Kim, Subin and Qi, Xiaojun},
  booktitle = {Pattern Recognition: 28th International Conference, ICPR 2026, Lyon, France, August 17--21, 2026, Proceedings},
  year      = {2026},
  publisher = {Springer Nature},
  series    = {Lecture Notes in Computer Science}
}
```

The final citation information should be updated after the official Springer proceedings are published.

---

## Contact

For questions about this repository or the paper, please contact:

```text
Subin Kim
Utah State University
School of Computing
Email: a02452970@usu.edu
```

