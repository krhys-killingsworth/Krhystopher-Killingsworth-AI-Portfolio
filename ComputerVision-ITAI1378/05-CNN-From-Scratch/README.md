# Convolutional Neural Network From Scratch

## Problem Statement

Design and train a convolutional network from zero on the chihuahua vs. muffin dataset, without a pretrained backbone. Where the transfer learning project asked "can a pretrained model solve this," this one asks "can I build the thing that solves it, and do I understand why it works."

## Approach

**Architecture.** Three convolutional blocks, each pairing a 3x3 convolution with a ReLU activation and 2x2 max pooling. The stack flattens into fully connected layers for classification.

**Training configurations.** Three separate runs were trained for 10 epochs each so that architecture and hyperparameter choices could be compared against each other rather than assumed.

**Data handling.** Explicit train and validation split, with the split logic documented in the notebook rather than hidden behind a helper.

## Results

| Configuration | Best Validation Accuracy | Final Train Accuracy | Runtime |
|---|---|---|---|
| Run 1 | 93.3% | 95.0% | 233.3 s |
| Run 2 | 56.7% | 54.2% | 217.9 s |
| Run 3 | 96.7% | 95.8% | 229.7 s |

Run 3 reached 96.7% validation accuracy at epoch 9 with training and validation loss falling together, which is the healthy pattern.

Run 2 failed to learn. Training loss opened at 217.312, collapsed to roughly 0.69, and then flatlined for seven epochs with validation accuracy pinned at 56.7%.

## Key Findings

**The failed run taught more than the successful ones.** A loss stuck at approximately 0.693 on a two-class problem is the natural log of 2, the exact loss of a model outputting 50/50 for every input. Recognizing that number on sight identifies a dead network immediately, and the enormous opening loss of 217 points at unstable initialization or an unsuitable learning rate rather than a flaw in the architecture.

**Convolution preserves what flattening destroys.** A fully connected layer discards the spatial relationship between adjacent pixels. Convolutional filters slide across the image and keep it, which is exactly why the CNN clears 90% on a task where the flattened baseline sat near chance.

**A from-scratch CNN got within a few points of transfer learning, at a cost.** Roughly 230 seconds per run and three attempts to find a configuration that trained well, against a pretrained backbone that converged in one epoch. That tradeoff is the practical argument for transfer learning on small datasets, and it is more convincing having built both.

## Technologies Used

Python, PyTorch, torchvision, CUDA, Matplotlib, Google Colab

## Data

Chihuahua vs. muffin dataset, loaded at runtime. Not stored in this repository. See the notebook's data preparation section for the source and directory structure.

## How to Run

Open `CNN_From_Scratch_Chihuahua_Muffin.ipynb` in Google Colab with a GPU runtime and run all cells. Expect roughly four minutes per training run.

## Files

- `CNN_From_Scratch_Chihuahua_Muffin.ipynb` - main notebook
- `Reflection_Journal.docx` - written reflection covering architecture rationale
