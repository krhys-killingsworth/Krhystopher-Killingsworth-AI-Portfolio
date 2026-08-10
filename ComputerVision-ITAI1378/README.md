# Computer Vision (ITAI 1378)

Houston City College | Instructor: Professor Esmali | Summer 2026

This course moved from raw pixel manipulation to multi-agent detection systems. The projects below are ordered by scope rather than chronology, so the most substantial work appears first.

## Arc of the Course

The sequence was deliberate. Early labs built images as matrices and hand-designed convolution kernels. The SVM baseline established what classical feature engineering can and cannot do on CIFAR-10. From there, a CNN designed from scratch showed how much architecture matters, and ResNet18 transfer learning showed how much a pretrained backbone matters more. The final third moved from single images to video, from detection to segmentation, and from one model to coordinated agents.

The thread I kept returning to: knowing which tool the problem actually calls for is worth more than reaching for the largest model available.

## Projects

| # | Project | Core Technique | Headline Result |
|---|---|---|---|
| 01 | [RoadWatch Agent](./01-RoadWatch-Agent-Final-Project/) | Multi-agent YOLO11s triage | 20/22 final evaluation |
| 02 | [Video Analysis & Object Tracking](./02-Video-Analysis-and-Tracking/) | ByteTrack, BoT-SORT | 79 vs. 74 IDs against 41 real people |
| 03 | [Object Detection & Segmentation](./03-Object-Detection-and-Segmentation/) | YOLO11, YOLO11-seg, SAM 2 | Detect-then-segment pipeline |
| 04 | [Transfer Learning Classifier](./04-Transfer-Learning-Classifier/) | ResNet18 transfer learning | 56.7% to 100% validation accuracy |
| 05 | [CNN From Scratch](./05-CNN-From-Scratch/) | Three-block CNN in PyTorch | 96.7% peak validation accuracy |
| 06 | [CIFAR-10 SVM Baseline](./06-CIFAR10-SVM-Baseline/) | SVM, GridSearchCV | 44.9% to 70.6% accuracy |
| 07 | [Image Processing Fundamentals](./07-Image-Processing-Fundamentals/) | OpenCV, convolution, histograms | Manual kernel design |
| 08 | [Advanced AI Agent Concepts](./08-AI-Agent-Concepts/) | DQN, policy gradient, federated | Comparative study, 100 episodes |

## Supporting Work

[`Research-and-Reflections/`](./Research-and-Reflections/) holds the written research and setup documentation from the course.

## Running These Notebooks

Every notebook was developed in Google Colab and runs there without modification. Open any `.ipynb` file, click the Colab badge or upload it directly to [colab.research.google.com](https://colab.research.google.com), and set the runtime to GPU where the project README notes it is needed.

Datasets are not stored in this repository. Each project README documents which dataset it uses and where to get it.
