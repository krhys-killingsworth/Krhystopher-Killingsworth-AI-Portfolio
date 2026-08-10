# Image Processing Fundamentals

## Problem Statement

Before any model can classify an image, something has to represent that image as numbers and transform it. This project works through digital image processing from first principles: images as matrices, point operations, and neighborhood operations, using OpenCV rather than a learned model.

## Approach

1. **Images as matrices.** Inspect a color image as a 3D array of height, width, and channels, with each value in the 0 to 255 range.
2. **Channel decomposition.** Separate and visualize the R, G, and B channels independently, then convert to grayscale.
3. **Point operations.** Apply per-pixel transformations, including brightness adjustment by adding a constant across the array.
4. **Neighborhood operations.** Apply convolution kernels, sliding a 3x3 matrix across the image to blur, sharpen, and detect edges.
5. **Histogram operations.** Analyze intensity distributions and apply histogram equalization for contrast enhancement.

## Results

Each transformation is rendered inline in the notebook against its source image, so the effect of every operation is visible rather than described. The convolution section shows how a single kernel choice changes an image from blurred to edge-detected.

## Key Findings

**Convolution was the hard part, and it was the important part.** Point operations are straightforward because each pixel is independent. Visualizing a 3x3 kernel sliding across a matrix, computing a weighted sum at every position, takes real effort to hold in your head. That operation is the foundation every convolutional layer in the rest of this portfolio is built on, so the difficulty was worth pushing through.

**Hand-designed filters and learned filters are the same operation.** Edge detection and texture analysis with OpenCV kernels mirror what CNN feature extraction layers do. The difference is authorship: here the kernel values are written by hand, and in a CNN millions of them are learned from data. Understanding the manual version made the learned version legible rather than magical.

**Preprocessing is not a formality.** Histogram equalization enhances contrast in a way that has real applications, such as improving visibility in X-ray imaging. Cleaning an image with classical techniques before feeding it to a neural network is a legitimate way to improve downstream accuracy.

## Technologies Used

Python, OpenCV, NumPy, Matplotlib, Google Colab

## Data

Sample images loaded within the notebook. No external dataset required.

## How to Run

Open `Image_Processing_Fundamentals.ipynb` in Google Colab and run all cells. No GPU required.

## Files

- `Image_Processing_Fundamentals.ipynb` - main notebook
- `Reflection_Journal.pdf` - written reflection on the connection between classical CV and modern CNNs
