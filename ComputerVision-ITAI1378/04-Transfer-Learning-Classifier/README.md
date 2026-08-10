# Transfer Learning Image Classifier

## Problem Statement

Classify images as chihuahua or muffin, a deliberately adversarial task where the two classes share color palette, texture, and rough spatial layout. The starting fully connected network reached 54% accuracy, which on a two-class problem is barely above guessing. The target was to clear 80% validation accuracy.

## Approach

**Baseline.** A fully connected network flattens each image into a vector, discarding all spatial structure. Trained for 3 epochs.

**Transfer learning.** Replace the baseline with ResNet18 pretrained on ImageNet, normalize inputs to ImageNet channel statistics, freeze the pretrained backbone, and train a new classification head for 10 epochs.

**Regularization.** Because the dataset is small, overfitting was addressed by freezing the backbone, adding dropout, and applying data augmentation.

**Architecture experiments.** A companion notebook (`Architecture_Experiments.ipynb`) logs four separate runs: a 3-epoch baseline, an extended 10-epoch run, an optimizer swap to Adam, and a deeper architecture, so that the effect of each change can be read independently.

## Results

| Model | Epochs | Train Accuracy | Validation Accuracy |
|---|---|---|---|
| Fully connected baseline | 3 | 54.2% | 56.7% |
| ResNet18 transfer learning | 10 | 100% | 100% |

Validation loss fell from 0.6602 to 0.0011 across the transfer learning run, and validation accuracy hit 100% by the first epoch.

Architecture experiment results (separate notebook): baseline 96.7%, extended training 86.7%, Adam optimizer 80.0%, deeper architecture 80.0%.

## Key Findings

**Architecture beats training time.** The baseline trained longer never approached what the pretrained backbone achieved immediately. Adding epochs to a model that discards spatial structure does not recover the information it threw away.

**100% validation accuracy is a warning, not a trophy.** The validation set here is small, and a model that is perfect on it has demonstrated that it fits this data, not that it generalizes. The experiment notebook supports this directly: the deeper architecture reached 100% train accuracy while validation drifted down to 80%, which is textbook overfitting visible in the logs.

**More capacity is not more performance.** Both the Adam swap and the deeper network underperformed the simpler baseline on validation. Adding parameters to a small dataset creates room to memorize.

**A debugging habit came out of this.** When a model performs poorly, check whether the architecture suits the problem before touching hyperparameters. Tuning a fundamentally wrong architecture wastes time.

## Real-World Application

CNN-based transfer learning transfers directly to medical imaging. Gu and Lee (2024) documented pretrained models converging faster and scoring higher on accuracy, recall, precision, and F1 than models trained from scratch when classifying pneumonia on chest X-rays. The pattern is the same one this project demonstrates: a pretrained backbone on a small labeled dataset outperforms training from zero.

## Technologies Used

Python, PyTorch, torchvision, ResNet18, CUDA, PIL, Matplotlib, Google Colab

## Data

Chihuahua vs. muffin dataset, cloned at runtime from [patitimoner/workshop-chihuahua-vs-muffin](https://github.com/patitimoner/workshop-chihuahua-vs-muffin). Not stored in this repository. The first notebook cell clones it automatically.

## How to Run

Open `Transfer_Learning_ResNet18.ipynb` in Google Colab with a GPU runtime and run all cells. The repository clone happens in the first cell. Run `Architecture_Experiments.ipynb` the same way for the comparative experiment log.

## Files

- `Transfer_Learning_ResNet18.ipynb` - main notebook, baseline through ResNet18
- `Architecture_Experiments.ipynb` - four-run comparative experiment log
- `Reflection_Journal.pdf` - written reflection with full citations

## References

Gu, Chanhoe, and Minhyeok Lee. "Deep Transfer Learning Using Real-World Image Features for Medical Image Classification, with a Case Study on Pneumonia X-Ray Images." *Bioengineering*, vol. 11, no. 4, Apr. 2024, p. 406. https://doi.org/10.3390/bioengineering11040406
