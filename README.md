# Face Recognition with ArcFace (ONNX) and 5-Point Alignment

This repository demonstrates a **complete, runnable face recognition pipeline** built as a practical application of modern face recognition concepts. The project integrates face detection, 5-point facial landmark extraction, geometric alignment, embedding generation using an ArcFace-style interface (ONNX-ready), identity enrollment, and similarity-based recognition.

The goal of this project is to move beyond theory and present a **clear, modular, and reproducible system** suitable for academic assessment, experimentation, and further extension.

---

## Features

- Real-time camera capture with FPS measurement
- Face detection using Haar Cascades
- 5-point facial landmark extraction (MediaPipe FaceMesh)
- Geometric face alignment
- Face embedding extraction (ArcFace-style, ONNX-ready interface)
- Enrollment of multiple identities
- Similarity-based face recognition and evaluation
- Modular design with independent runnable components

---

## Project Structure

```
face-recognition-5pt/
├── book/
├── models/
├── data/
│   ├── db/           # Stored face embeddings
│   └── enroll/       # Optional enrollment data
├── src/
│   ├── camera.py     # Video capture & FPS test
│   ├── detect.py     # Face detection
│   ├── landmarks.py  # 5-point landmark extraction
│   ├── align.py      # Geometric face alignment
│   ├── embed.py      # Embedding extraction
│   ├── enroll.py     # Identity enrollment
│   ├── evaluate.py   # Threshold / similarity evaluation
│   ├── haar_5pt.py   # Haar + 5-point integration
│   ├── recognize.py  # Recognition pipeline
│   └── __init__.py
├── requirements.txt
└── README.md
```

---

## Pipeline Overview

1. **Camera Input** → Capture video frames
2. **Face Detection** → Locate face bounding boxes
3. **5-Point Landmarks** → Extract key facial points
4. **Alignment** → Normalize face geometry
5. **Embedding Extraction** → Generate identity vectors (ArcFace-style)
6. **Enrollment** → Store embeddings per identity
7. **Recognition / Evaluation** → Compare embeddings using cosine similarity

Each step can be executed independently or as part of a full workflow.

---

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/Mchiir/face-recognition-5pt.git
cd face-recognition-5pt
```

### 2. Create and activate a virtual environment (recommended)

```bash
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

**Main dependencies:**

- opencv-python
- numpy
- onnxruntime ([Also Download ONNX embeder](https://huggingface.co/facefusion/models-3.0.0/blob/main/arcface_w600k_r50.onnx))
- scipy
- mediapipe (0.10.14)
- tqdm

---

## Running the Project

All modules are runnable using Python’s `-m` flag.

### Camera & FPS Test

```bash
python -m src.camera
```

### Face Detection

```bash
python -m src.detect
```

### 5-Point Landmark Extraction

```bash
python -m src.landmarks
```

### Geometric Alignment

```bash
python -m src.align
```

### Embedding Test

```bash
python -m src.embed
```

### Enroll a New Identity

```bash
python -m src.enroll
```

### Evaluate Similarity / Thresholds

```bash
python -m src.evaluate
```

### Haar + 5-Point Integration

```bash
python -m src.haar_5pt
```

### Recognition

```bash
python -m src.recognize
```

---

## Evaluation

- Embeddings are compared using **cosine similarity**
- Threshold tuning can be performed via `evaluate.py`
- The modular design allows easy replacement with a real ArcFace ONNX model

---
