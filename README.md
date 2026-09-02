# MNIST Transformations and CNN Robustness Evaluation

## Overview

This project investigates the performance of a Convolutional Neural Network (CNN) for handwritten digit classification using the MNIST dataset. The CNN is trained on regular MNIST images and evaluated on both the original and transformed MNIST test datasets.

Two image transformations are investigated:

1. **Colored MNIST** – MNIST digits are transformed using three colors: red, green, and blue.
2. **Rotated MNIST** – MNIST digits are rotated through different angles to investigate the effect of orientation on classification performance.

The project also includes subgroup analysis across individual colors and rotation angles. As an optional improvement, a second CNN is trained using color and rotation augmentation to investigate whether data augmentation improves robustness to the transformed datasets.

## Methodology

The baseline CNN was trained exclusively on the regular MNIST training dataset for five epochs. The same trained model was then evaluated on:

- Original MNIST
- Colored MNIST
- Rotated MNIST

The CNN consists of two convolutional layers followed by max-pooling, dropout, and fully connected layers. Cross-entropy loss was used as the classification loss, and the model was trained using the Adam optimizer.

## Baseline Results

| Test Dataset | Accuracy | Test Loss |
|---|---:|---:|
| Original MNIST | 99.18% | 0.0244 |
| Colored MNIST | 91.65% | 0.6340 |
| Rotated MNIST | 64.24% | 2.0599 |

The baseline CNN performed very well on the original MNIST test dataset. Coloring reduced accuracy by **7.53 percentage points**, while rotation produced a much larger reduction of **34.94 percentage points**.

## Color-Wise Analysis

| Color | Accuracy |
|---|---:|
| Red | 96.43% |
| Green | 97.21% |
| Blue | 82.15% |

The model achieved its highest accuracy on green digits and its lowest accuracy on blue digits.

## Rotation-Angle Analysis

| Rotation Angle | Accuracy |
|---:|---:|
| -60° | 27.03% |
| -40° | 62.28% |
| -20° | 94.61% |
| +20° | 95.72% |
| +40° | 70.12% |
| +60° | 33.49% |

Performance remained relatively high for rotations of ±20°, while larger rotations caused substantial degradation.

## Model Improvement

An additional experiment was performed using color and rotation augmentation during training.

The augmented model's training loss decreased from **0.4508** in Epoch 1 to **0.0946** in Epoch 5.

| Test Dataset | Baseline Accuracy | Improved Accuracy | Change |
|---|---:|---:|---:|
| Original MNIST | 99.18% | 97.94% | -1.24 pp |
| Colored MNIST | 91.65% | 97.80% | +6.15 pp |
| Rotated MNIST | 64.24% | 97.25% | +33.01 pp |

Data augmentation substantially improved robustness to both transformations, particularly rotation. This improvement was accompanied by a small reduction in accuracy on the original MNIST test dataset.

## Key Findings

- The baseline CNN achieved **99.18% accuracy** on original MNIST.
- Color transformation reduced baseline accuracy to **91.65%**.
- Rotation had a substantially greater effect, reducing baseline accuracy to **64.24%**.
- Larger rotation angles generally resulted in greater performance degradation.
- Transformation-aware data augmentation increased Colored MNIST accuracy to **97.80%**.
- The largest improvement occurred on Rotated MNIST, where accuracy increased from **64.24% to 97.25%**.
- Improved robustness to transformed images came with a small decrease in original MNIST accuracy from **99.18% to 97.94%**.

## Technologies

- Python
- PyTorch
- Torchvision
- NumPy
- Pandas
- Matplotlib
- Google Colab

## Repository Contents

- `MNIST_Transformations_and_CNN_Improvement.ipynb` – complete executable notebook containing data preparation, transformations, CNN training, evaluation, visualizations, subgroup analysis, and model improvement.
- `README.md` – project description and summary of experimental results.

## How to Run

The notebook can be opened and executed in Google Colab or in a local Jupyter Notebook environment with the required Python packages installed.

For faster CNN training in Google Colab, a GPU runtime can be used.

## Conclusion

The experiment demonstrates that a CNN trained only on regular MNIST can achieve excellent performance on the original test distribution but can be sensitive to previously unseen image transformations. Rotation caused substantially greater performance degradation than coloring. Training with color and rotation augmentation greatly improved robustness to both transformed datasets, particularly for rotated digits.
