
# Dataset Splits and Augmentation

## 1. Dataset Partitioning

The experiments use three nuclei segmentation datasets: MoNuSeg, TNBC, and CPM-15. Each dataset is divided into training, validation, and test subsets.

| Dataset | Train | Validation | Test | Total |
|---|---:|---:|---:|---:|
| MoNuSeg | 29 | 8 | 14 | 51 |
| TNBC | 35 | 10 | 5 | 50 |
| CPM-15 | 10 | 3 | 2 | 15 |
| **Total** | **74** | **21** | **21** | **116** |

The training subset is used for model optimization, the validation subset for model selection and hyperparameter tuning, and the test subset for final evaluation.

## 2. Data Augmentation

Training-time augmentation combines spatial transformations, photometric perturbations, and Random Erasing to improve robustness to variations in tissue morphology, staining, image quality, and local occlusion.

| Category | Transformations | Purpose |
|---|---|---|
| Spatial | Horizontal and vertical flips, rotations, affine transformations | Improve robustness to geometric variations |
| Photometric | Color jitter, noise injection, blur | Improve robustness to appearance and image-quality variations |
| Occlusion | Random Erasing | Reduce sensitivity to partial visual information |

Geometric transformations are applied consistently to images and their corresponding segmentation masks, using appropriate interpolation to preserve mask labels. Photometric transformations and Random Erasing are applied to training images only.

## 3. Reproducibility

- Stochastic augmentation is restricted to the training subset.
- Validation and test preprocessing remains consistent across experiments.
- Augmentation parameters and random seeds should be documented for reproducibility.
- Dataset partitions are established before augmentation to prevent data leakage.

**Note:** CPM-15 contains only two test images in this split; its results should therefore be interpreted cautiously. Exact augmentation parameters should be reported from the implemented configuration.
