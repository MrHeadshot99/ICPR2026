# Dual-Branch Spectral-Spatial Network for UAV Hyperspectral Wheat Rust Detection

This repository contains the dataset split files, cleanup logs, RRPR reproducibility information, saved holdout outputs, pretrained checkpoint download instructions, and Kaggle notebooks used for the ICPR 2026 paper:

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
4. **Spatial-spectral feature fusion with SAPFB**
5. **Cleaned train/test splits based on NDVI-guided data refinement**

The repository is intended to support reproducibility of the camera-ready ICPR 2026 experiments.

---

## Repository Structure

```text
.
├── DataCSV/
│   ├── train_full_df_clean.csv
│   ├── test_hold_df_clean.csv
│   ├── cleanup_log_train_full.csv
│   ├── cleanup_log_test_hold.csv
│   ├── holdout_probs.npy
│   └── holdout_predictions.csv
│
├── checkpoints/
│   └── README.md
│
├── rrpr_info/
│   ├── required_form_info_copy_paste.txt
│   ├── required_form_info.json
│   ├── hardware_info.json
│   └── library_versions.csv
│
├── notebook5c6c78846e6b4ec2fdc4 (Refined).ipynb
├── notebook5c6c78846e (2).ipynb
└── README.md
```

---

## File Descriptions

| File | Description |
|---|---|
| `DataCSV/train_full_df_clean.csv` | Fixed NDVI-refined training dataframe used for model training and 5-fold cross-validation. |
| `DataCSV/test_hold_df_clean.csv` | Fixed NDVI-refined holdout test dataframe used only for final evaluation. |
| `DataCSV/cleanup_log_train_full.csv` | Log file from the NDVI-guided cleanup process for the training split. It records how the fixed training CSV was derived from the original split. |
| `DataCSV/cleanup_log_test_hold.csv` | Log file from the NDVI-guided cleanup process for the holdout test split. |
| `DataCSV/holdout_probs.npy` | Saved softmax probability outputs from the final 5-fold holdout ensemble evaluation. |
| `DataCSV/holdout_predictions.csv` | Saved holdout prediction file containing sample paths, ground-truth labels, and predicted labels from the final ensemble evaluation. |
| `checkpoints/README.md` | Instructions for downloading pretrained fold checkpoints from the GitHub Release assets. |
| `rrpr_info/required_form_info_copy_paste.txt` | Copy-paste summary for the ICPR 2026 RRPR GitHub issue form. |
| `rrpr_info/required_form_info.json` | Structured JSON version of the RRPR form information. |
| `rrpr_info/hardware_info.json` | Recorded CPU, RAM, GPU, OS, CUDA, cuDNN, and PyTorch environment information. |
| `rrpr_info/library_versions.csv` | Key package versions used in the reproducibility environment. |
| `notebook5c6c78846e6b4ec2fdc4 (Refined).ipynb` | Refined reproducibility notebook. This is the recommended notebook for reproducing the final ICPR 2026 pipeline. It uses the fixed NDVI-refined CSV files directly and was re-run on June 9, 2026 MDT to verify that it reproduces the reported result. |
| `notebook5c6c78846e (2).ipynb` | Original early-stage Kaggle notebook. This notebook was used during the first experimental development stage and generated the NDVI-refined fixed train/test CSV files. It is kept for transparency, but it is not the recommended notebook for final reproduction. |

---

## Dataset

The experiments use the public ICPR 2024 UAV hyperspectral wheat dataset:

**Beyond Visible Spectrum - AI for Agriculture 2024**

The hyperspectral samples are expected to be organized by class:

```text
archive/train/
├── Health/
├── Rust/
└── Other/
```

Each sample is a hyperspectral `.tif` cube with 125 spectral bands. The label set is:

```python
LABELS = ["Health", "Other", "Rust"]
```

---

## Fixed Train/Test Splits

The final reproducibility pipeline uses the provided fixed split files:

```text
DataCSV/train_full_df_clean.csv
DataCSV/test_hold_df_clean.csv
```

These CSV files were generated from the original early-stage notebook:

```text
notebook5c6c78846e (2).ipynb
```

The refined reproducibility notebook:

```text
notebook5c6c78846e6b4ec2fdc4 (Refined).ipynb
```

uses these CSV files directly rather than regenerating a new split. This ensures that all benchmarking and reproducibility experiments use the same NDVI-refined train/test split reported in the paper.

The refined notebook was re-run on June 9, 2026 MDT and reproduced the same reported result.

---

## Model Pipeline

The overall pipeline consists of the following stages:

1. Load the fixed NDVI-refined train/test CSV files
2. Load hyperspectral image cubes
3. Use the final selected spectral bands reported in the paper
4. Construct 2D pseudo-RGB inputs from selected spectral bands
5. Construct 1D spectral inputs from compact selected bands
6. Train a dual-branch spectral-spatial network
7. Perform 5-fold cross-validation on the cleaned training set
8. Ensemble fold models for final holdout evaluation
9. Save holdout probabilities and predictions
10. Report classification metrics

The main evaluation metrics include:

- Overall Accuracy
- Average Accuracy
- Macro-F1 Score
- Cohen's Kappa
- Per-class Accuracy
- Confusion Matrix

---

## Selected Bands

The final 2D pseudo-RGB branch uses:

```text
674 nm, 738 nm, 782 nm
```

The final 1D spectral branch uses:

```text
530 nm, 554 nm, 570 nm, 666* nm, 698 nm, 738 nm, 782 nm
```

where:

```text
666* = average of 658, 662, 666, 670, and 674 nm
```

---

## Environment

The experiments were developed and tested in a Kaggle Linux environment.

Recorded hardware:

```text
OS: Linux
CPU: Intel(R) Xeon(R) CPU @ 2.00GHz
RAM: 31 GiB system RAM
GPU: 2 × NVIDIA Tesla T4, 15 GB each
```

Key package versions:

```text
Python: 3.11.13
PyTorch: 2.6.0+cu124
torchvision: 0.21.0+cu124
timm: 1.0.19
NumPy: 1.26.4
pandas: 2.2.3
scikit-learn: 1.2.2
scikit-image: 0.25.2
fvcore: 0.1.5.post20221221
thop: 0.1.1
```

Additional environment details are provided in:

```text
rrpr_info/hardware_info.json
rrpr_info/library_versions.csv
```

Install required packages if needed:

```bash
pip install timm scikit-learn matplotlib pandas numpy opencv-python tifffile scikit-image fvcore thop
```

---

## How to Run

### Recommended Reproducibility Notebook

For reproducing the final ICPR 2026 experiment pipeline, use:

```text
notebook5c6c78846e6b4ec2fdc4 (Refined).ipynb
```

This is the recommended notebook for RRPR evaluation. It uses the fixed NDVI-refined CSV files and reproduces the final reported pipeline.

### Original Early-Stage Notebook

The following notebook is also included for transparency:

```text
notebook5c6c78846e (2).ipynb
```

This notebook was used during the first experimental development stage and generated the NDVI-refined fixed train/test CSV files. It may contain less organized code, temporary comments, and earlier experiment traces. It is not the recommended version for final reproduction.

---

## Checkpoints

Due to GitHub’s browser upload size limit for large binary files, pretrained fold checkpoints are provided as GitHub Release assets instead of being stored directly in the repository.

Download the checkpoint files from the release page and place them under:

```text
checkpoints/
```

Expected checkpoint files:

```text
fold0_best.pth
fold1_best.pth
fold2_best.pth
fold3_best.pth
fold4_best.pth
```

The `checkpoints/README.md` file provides the download instructions.

---

## Reproducibility Notes

The experiments use a fixed random seed where possible:

```python
seed = 42
```

The fixed split files are provided:

```text
DataCSV/train_full_df_clean.csv
DataCSV/test_hold_df_clean.csv
```

The final holdout ensemble outputs are also provided:

```text
DataCSV/holdout_probs.npy
DataCSV/holdout_predictions.csv
```

Therefore, the holdout test set and the saved prediction outputs can be checked directly for reproducibility.

For full reproduction, run the refined notebook to perform 5-fold training and holdout ensemble evaluation.

For faster verification, pretrained fold checkpoints are provided as GitHub Release assets. Download the checkpoint files from the release page and place them under:

```text
checkpoints/
```

---

## Expected Reproduced Result

The final proposed model is expected to reproduce the reported holdout performance:

```text
Overall Accuracy: 85.19%
Average Accuracy: 85.65%
Macro-F1: 85.72%
Cohen's Kappa: 77.62%
```

The final holdout ensemble outputs are saved as:

```text
DataCSV/holdout_probs.npy
DataCSV/holdout_predictions.csv
```

---

## RRPR Information

The folder:

```text
rrpr_info/
```

contains supporting information for the ICPR 2026 Reproducible Research in Pattern Recognition Badge submission:

```text
required_form_info_copy_paste.txt
required_form_info.json
hardware_info.json
library_versions.csv
```

These files summarize the required form fields, hardware/software configuration, and key package versions.

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
