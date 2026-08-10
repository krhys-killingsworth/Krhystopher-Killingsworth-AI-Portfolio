# Object Detection and Image Segmentation

## Problem Statement

A bounding box tells you roughly where something is. A segmentation mask tells you exactly which pixels belong to it. This project builds both, then combines them into the detect-then-segment pipeline that modern vision systems actually use.

## Approach

1. **Detection with YOLO11.** Run inference, read the raw output structure (boxes, classes, confidence scores), and interpret what the model returns rather than only viewing the annotated image.
2. **Confidence threshold experiment.** Sweep the threshold and observe how the detection count changes, then reason about which threshold suits which application.
3. **Segmentation with YOLO11-seg.** Generate per-object masks and inspect their shape and tightness.
4. **SAM 2 integration.** Load Segment Anything 2, which produces high-quality masks but carries no class vocabulary.
5. **Combined pipeline.** Use YOLO11 to find and label objects, then hand those regions to SAM 2 for precise masks.
6. **IoU evaluation.** Compare a prediction against ground truth to quantify overlap.

## Results

Detection on test imagery correctly identified people, a bus, and a stop sign. On a second image the model returned two people at 84% and 78% confidence and a tie at 45%, which itself illustrates how confidence maps to reliability.

YOLO11-seg produced 6 masks on the bus scene at 640x480 resolution, each mask a full-size per-pixel tensor. Inference ran at roughly 145 to 290 ms per image.

SAM 2 produced noticeably tighter masks than YOLO11-seg but returned no class names, confirming why the two models pair rather than compete.

## Key Findings

The confidence threshold is a product decision, not a technical one. A workplace safety alert should run a low threshold and tolerate false positives, because a missed hazard costs more than a spurious warning. A photo tagger should run high, because wrong tags erode trust faster than missing ones. The same model serves both; only the threshold changes.

The SAM 2 result reframed how I think about model composition. SAM 2 is excellent at the "which pixels" question and useless at the "what is it" question. Rather than searching for one model that does both well, the working answer is to route each question to the model built for it.

Segmentation costs meaningfully more inference time than detection. That tradeoff decides which one belongs in a real-time path.

## Technologies Used

Python, Ultralytics YOLO11, YOLO11-seg, SAM 2 (Segment Anything 2), PyTorch, Matplotlib, Google Colab

## Data

Standard Ultralytics sample images (`bus.jpg`, `zidane.jpg`), fetched automatically at runtime. Model weights (`yolo11n-seg.pt`, `sam2.1_s.pt`) download on first use.

## How to Run

Open `Object_Detection_and_Segmentation.ipynb` in Google Colab with a GPU runtime and run all cells. No manual downloads required.
