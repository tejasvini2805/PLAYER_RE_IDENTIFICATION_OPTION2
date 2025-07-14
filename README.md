# PLAYER_RE_IDENTIFICATION_OPTION2

# Player Re-Identification using YOLOv11

This project focuses on detecting and re-identifying football players using a fine-tuned YOLOv11 model with object detection and multi-object tracking. It tracks players, referees, and the ball across video frames, assigns consistent IDs, and visually annotates them using ellipses and triangles.

##  Project Structure

This project was developed and executed in Google Colab. The major components used and saved are:

.
├── video_utils.py              # Functions to read and save videos using OpenCV
├── utils.py                    # Bounding box helper functions
├── tracker.py                 # Tracker class (YOLOv11 + ByteTrack + annotation logic)
├── final_run/                 # Folder containing the trained YOLOv11 model (best.pt)
├── tracker_stubs/            # Optional saved pickle stubs for tracking reuse
├── output_videos/            # Folder containing the final annotated output video
├── environment_info.txt      # Outputs of ultralytics.checks() and nvidia-smi
└── report.pdf                # Summary of methodology, steps, and challenges

## How to Run

This project was executed in Google Colab using a series of modular code cells. To reproduce the workflow:

1. Mount Google Drive to access datasets, videos, and to save outputs.
2. Install required packages:
   - ultralytics
   - roboflow
   - supervision
   - opencv-python

3. Load the fine-tuned YOLOv11 model (best.pt).
4. Perform object detection or tracking using the `model.predict()` or `model.track()` methods.
5. Use the `Tracker` class for structured tracking, annotation, and saving outputs.
6. Save final video output to the Drive folder.

## Object Classes and Annotation Scheme

The following objects are detected and visually annotated in the output video:

- Player: Drawn with a red ellipse and labeled with a unique track ID
- Referee: Drawn with a yellow ellipse (no ID)
- Ball: Drawn with a green triangle above the object

This annotation is done frame-by-frame using OpenCV drawing functions in the `Tracker` class.

## Training Details

The YOLOv11 model was fine-tuned on a football player detection dataset exported from Roboflow.

- Format: YOLOv11
- Dataset Source: Roboflow project – football-players-detection
- Training Platform: Google Colab
- Base Model: Pretrained YOLOv11 checkpoint
- Epochs: 80
- Image Size: 640
- Batch Size: 4

Training command used:

yolo task=detect mode=train \
  data="path_to_data.yaml" \
  model="path_to/best.pt" \
  epochs=80 imgsz=640 batch=4

## Tracking Pipeline Details

Tracking and annotation are handled using a custom `Tracker` class defined in `tracker.py`. It integrates:

- YOLOv11 model from the Ultralytics library for detection
- ByteTrack (via the Supervision library) for consistent ID tracking
- Batched inference to speed up detection on video frames
- Optional stub saving and loading using pickle to avoid reprocessing

Annotation Strategy:
- Players and referees are drawn using ellipses
- The ball is drawn using a triangle
- Player track IDs are shown in labeled boxes below the ellipse

The final annotated video is saved using OpenCV’s video writer.

## Environment and Requirements

This project was run in Google Colab with GPU enabled. Below are the key requirements:

- Python 3.10+
- CUDA-compatible GPU (recommended for fast inference)

Python Libraries used:

- ultralytics
- roboflow
- supervision
- opencv-python
- numpy

Dependencies can be installed using:

pip install ultralytics roboflow supervision opencv-python


## Dependencies (requirements.txt)

A `requirements.txt` file can be created to easily install all dependencies.

Example contents:

ultralytics
roboflow
supervision
opencv-python
numpy

Install all required packages with:

pip install -r requirements.txt

## Report Summary

A `report.pdf` is included in the project directory, summarizing:

- Objective and problem statement
- Dataset and training setup
- Detection and tracking pipeline
- Annotation strategy
- Challenges faced during development
- Suggested improvements and future work

This PDF serves as a concise overview for evaluators or reviewers.

## Author

Tejasvini Rachamalla  
B.E. – Artificial Intelligence and Data Science  
Chaitanya Bharathi Institute of Technology (CBIT), Hyderabad


