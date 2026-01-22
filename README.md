# Multi-Object Tracking with YOLOv8 + ByteTrack (TP3)

This repository contains a complete multi-object tracking (MOT) workflow built around Ultralytics YOLOv8 for detection and Supervision ByteTrack for temporal association. The main pipeline is documented and runnable from the notebook `ByteTrack/notebook_restructured.ipynb` and includes tracking, export in MOT-style format, evaluation plotting, and optional visualization/crop extraction.

## Report
- [Read the full report (PDF)](Rapport_TP3.pdf)

## Overview

The notebook is structured in three parts:

1. **Detection + tracking** on a folder of frames (JPG images) using YOLOv8 + ByteTrack.
2. **Export** tracking results to a simple text format for evaluation or downstream use.
3. **Plot MOT metrics** (HOTA / DetA / AssA / LocA) from JSON evaluation outputs.

Additional utilities include annotated frame previews, optional MP4 export, and pedestrian crop extraction.

## Features

- YOLOv8 object detection
- ByteTrack association with stable track IDs
- Batch processing of frame folders
- Export to `frame_id track_id x y w h` format
- Optional annotated video export
- Pedestrian crop extraction (`output_DPM/`)
- HOTA-family metric plotting from JSON

## Dataset

The notebook expects MOT-style sequences stored as frames. Example path used in the notebook:

```
../MOT17/train/MOT17-10-DPM/img1
```

Update the `images_folder` variable in the configuration section of the notebook to match your local dataset layout.

## Repository layout

- `ByteTrack/notebook_restructured.ipynb` Main notebook for tracking, export, and plotting
- `MOT17/` MOT17 dataset (frames)
- `MOT17_labels/` Label data for evaluation
- `TrackEval/` Evaluation tools and scripts
- `output_data.json`, `output_data_final.json` Example evaluation JSON files
- `results.txt`, `result.jpg` Example outputs
- `Rapport_TP3.pdf` Project report
- `requirements.txt` Python dependencies

## Setup

Create a Python environment and install dependencies:

```
pip install -r requirements.txt
```

You will also need a YOLOv8 model checkpoint (e.g., `yolov8n.pt`) which is already present in this repository.

## Usage

Open the main notebook and run top-to-bottom:

```
ByteTrack/notebook_restructured.ipynb
```

Key steps inside the notebook:

- Configure paths and parameters (dataset folder, model path, classes)
- Run detection + tracking over all frames
- Export predictions (`frame_id track_id x y w h`)
- Optionally write an annotated MP4
- Plot HOTA / DetA / AssA / LocA from JSON outputs
- Extract pedestrian crops to `output_DPM/`

## Output format

Predictions are exported as:

```
frame_id track_id x y w h
```

If you need MOTChallenge format, adapt the export cell in the notebook.

## Evaluation

Evaluation plots are built from JSON files produced by TrackEval (or equivalent). The plotting utilities expect a structure like:

```
data[model][benchmark][run_name][sequence]["pedestrian"]["HOTA"][metric]
```

If your JSON schema differs, update the access paths in the plotting helper functions.

## References

- Ultralytics YOLOv8
- ByteTrack
- MOT17 dataset
- TrackEval / HOTA metrics
