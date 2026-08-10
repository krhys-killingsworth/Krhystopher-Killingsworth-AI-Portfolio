# CIFAR-10 Classification with Support Vector Machines

## Problem Statement

Classify CIFAR-10 images using a Support Vector Machine rather than a neural network. This establishes the classical baseline: what accuracy is reachable without deep learning, and what it costs to get there. Every CNN result later in the course is measured against this number.

## Approach

1. **Data.** Load CIFAR-10, filter to a subset of classes, and convert images to grayscale to reduce dimensionality.
2. **Linear baseline.** Train an SVM with a linear kernel and evaluate on 3,000 held-out test images.
3. **Kernel swap.** Replace the linear kernel with RBF, which can separate classes that are not linearly separable in the original feature space.
4. **Hyperparameter search.** Tune `C` and `gamma` with `GridSearchCV`, then evaluate the best estimator on the test set.
5. **Visual inspection.** Display sample images at each preprocessing stage and a labeled grid of training images to confirm the pipeline is doing what it claims.

## Results

| Configuration | Test Accuracy |
|---|---|
| Linear kernel SVM | 44.9% |
| RBF kernel, tuned with GridSearchCV | **70.6%** |

Evaluated on 3,000 test images with a full precision, recall, and F1 breakdown per class in the notebook output.

## Key Findings

**Kernel choice was worth 25.7 percentage points.** The linear kernel assumes classes can be separated by a flat boundary in pixel space, and on natural images they cannot. The RBF kernel projects into a space where that separation exists. No additional data and no new features, just a better-matched decision boundary.

**Grid search matters, and it is expensive.** `C` and `gamma` interact, and tuning them jointly rather than one at a time is what produced the final number. The cost is that GridSearchCV retrains the model once per parameter combination, which on image data is slow.

**70.6% is the ceiling worth knowing.** Classical methods on raw grayscale pixels plateau here because the features are the pixels. A CNN learns its own features, which is precisely why it clears this baseline. Having run the classical version, that improvement reads as a concrete gain rather than an assumed one.

**Grayscale conversion is a real tradeoff.** It cut input dimensionality by two thirds and made SVM training tractable, at the cost of discarding color, which is genuine signal on several CIFAR-10 classes.

## Technologies Used

Python, scikit-learn (SVC, GridSearchCV), TensorFlow/Keras (dataset loading), NumPy, Matplotlib, Google Colab

## Data

CIFAR-10, a standard public dataset. Not stored in this repository. It loads directly in the notebook:

```python
from tensorflow.keras.datasets import cifar10
(x_train, y_train), (x_test, y_test) = cifar10.load_data()
```

## How to Run

Open `CIFAR10_SVM_Classifier.ipynb` in Google Colab and run all cells. A GPU is not required; SVM training runs on CPU. The GridSearchCV cell takes several minutes.
