# RoadWatch Agent - Multi-Agent Road Damage Triage

**ITAI 1378 Final Project** | Final evaluation: 20/22 (90.9%)

## Problem Statement

Road damage reporting is reactive and manual. Potholes and surface cracks get logged when someone complains, and triage happens by hand, which means severity ranking depends on who filed the report rather than on what the damage actually is. RoadWatch Agent automates detection and triage: it finds road damage in imagery, classifies severity, and routes each finding to the appropriate response tier.

## Approach

**Architecture.** A Tier 3 multi-agent system, where specialized agents handle detection, classification, and routing rather than a single monolithic model attempting all three.

**Detection model.** YOLO11s, selected for the balance between accuracy and inference speed that a field-deployable triage system requires.

[TODO: Describe your agent roles, how they hand off to each other, and the routing logic.]

## Results

[TODO: Add your detection metrics: mAP, precision, recall, per-class breakdown. Include the confusion matrix and any sample detection images in `results/`.]

Final evaluation: 20/22 (90.9%)

## Key Findings

[TODO: 3-4 paragraphs. What surprised you, what you would change, where the system fails.]

## Technologies Used

Python, Ultralytics YOLO11s, PyTorch, multi-agent orchestration, OpenCV, Google Colab

## Data

[TODO: Name the dataset, link where it can be downloaded, and note any preprocessing you applied. Do not upload the dataset itself if it is a standard public one.]

## How to Run

Open the notebook in Google Colab with a GPU runtime and run all cells.

## Files

[TODO: List the files once uploaded.]
