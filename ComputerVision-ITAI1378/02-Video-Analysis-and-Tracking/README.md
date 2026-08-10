# Video Analysis and Object Tracking

## Problem Statement

Detection answers "what is in this frame." Tracking answers "is this the same person as the last frame," and that second question is where most real systems break. This project moves from single-image detection into video, then measures how badly two production trackers fragment identities on genuinely crowded footage.

## Approach

1. **Video as data.** Read frame rate, resolution, and frame count directly, then calculate uncompressed bandwidth to understand why compression is not optional at video scale.
2. **Frame-by-frame detection.** Run YOLO11 across every frame to establish per-frame detections without any temporal linking.
3. **Tracking.** Apply ByteTrack and BoT-SORT to the same footage, producing persistent IDs across frames.
4. **Ground truth by hand.** Count the real people in the clip manually, which turns an unmeasurable output into an evaluable one.
5. **Comparison.** Measure unique IDs generated, tracks lasting under one second, and longest sustained track.

## Results

| Tracker | Unique IDs | Short tracks (< 1s) | Longest track |
|---|---|---|---|
| ByteTrack | 79 | 24 | 10.00 s |
| BoT-SORT | 74 | 21 | 10.00 s |

**Manual ground-truth count: 41 real people.**

ByteTrack created 38 more identities than there were people. BoT-SORT was modestly better on both fragmentation measures but did not close the gap.

## Key Findings

The headline number is that both trackers roughly doubled the true person count. That gap is ID switching and fragmentation: occlusion, people crossing paths, and detections dropping for a frame or two all cause a tracker to retire an ID and issue a fresh one.

The short-track count is the more useful diagnostic. Twenty-four tracks living under one second are almost all fragments rather than real appearances, so filtering by track lifetime is a cheap and effective post-processing step before any downstream counting.

The broader lesson is that a tracker's output cannot be trusted as a count. If a system needs "how many people walked through," the tracker is an input to that answer, not the answer.

## Technologies Used

Python, Ultralytics YOLO11, ByteTrack, BoT-SORT, OpenCV, NumPy, Google Colab

## Data

Sample video footage processed in-notebook. Output tracking videos (`track_botsort.mp4` and equivalents) are generated at runtime.

## How to Run

Open `Video_Analysis_and_Object_Tracking.ipynb` in Google Colab, set the runtime to GPU (Runtime > Change runtime type > GPU), and run all cells top to bottom. Ultralytics downloads model weights automatically on first use.

## A Note on the Notebook

The inline video players were removed from three cells so this notebook stays under GitHub's rendering size limit and displays properly in the browser. Every numerical output, table, and plot is intact. Re-running the notebook in Colab regenerates the tracked output videos.
