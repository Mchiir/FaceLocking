# Face Locking System with ArcFace (ONNX) and 5-Point Alignment

This repository presents a **face locking system** built on top of a previously implemented face recognition pipeline using ArcFace (ONNX) and 5-point facial alignment.

While the project includes a complete face recognition workflow, the **primary focus of this repository is the Face Locking feature**, which extends recognition into **identity-aware behavior tracking over time**.

The system recognizes a selected enrolled identity, locks onto that face, tracks it consistently across frames, detects simple facial actions, and records an action history.

---

## Core Capabilities

### Face Recognition (Foundation)

- Real-time camera capture with FPS measurement
- Face detection using Haar Cascades
- 5-point facial landmark extraction
- Geometric face alignment
- Face embedding extraction (ArcFace-style, ONNX-ready)
- Enrollment of multiple identities
- Cosine similarity–based recognition

### Face Locking (Main Assignment Feature)

- Manual selection of one enrolled identity to lock onto
- Automatic locking when the selected face is recognized
- Stable tracking across frames
- Tolerance to brief recognition failures
- Explicit release of lock only after sustained face loss
- Action detection while locked
- Persistent action history recording

---

## Project Structure

```
face-recognition-5pt/
├── models/
├── data/
│   ├── db/                 # Stored face embeddings
│   └── enroll/             # Enrollment images
├── src/
│   ├── enroll.py           # Identity enrollment
│   ├── recognize.py        # Face recognition pipeline
│   ├── facelock.py         # Face locking and behavior tracking
│   ├── haar_5pt.py         # Face detection + 5-point landmarks
│   ├── embed.py            # ArcFace ONNX embedding
│   ├── align.py            # Geometric alignment
│   └── config.py           # System configuration
├── requirements.txt
└── README.md
```

---

## Face Locking Workflow

1. The user enrolls one or more identities.
2. The system prompts the user to **manually select one identity** to lock.
3. When the selected face appears and is confidently recognized:
   - The system locks onto that identity.
   - The lock status is clearly displayed.
4. While locked:
   - The same face is tracked across frames.
   - Other faces are ignored.
   - Brief recognition failures are tolerated.
5. The lock is released **only if the face disappears for a defined duration**.

This behavior ensures stable identity tracking rather than frame-by-frame recognition.

---

## Detected Actions (While Locked)

The system detects and records the following actions using explainable geometric logic:

- **Face moved left** – horizontal displacement of the face center
- **Face moved right** – horizontal displacement of the face center
- **Eye blink** – Eye Aspect Ratio (EAR) thresholding
- **Smile or laugh** – relative mouth width increase

Perfect accuracy is not required; the goal is clear, interpretable detection logic.

---

## Action History Recording

While the face is locked, all detected actions are written to a history file.

### File naming format (mandatory)

```
<face>_history_<timestamp>.txt
```

Example:

```
chrispin_history_20260129112099.txt
```

### File contents

Each line in the file contains:

- timestamp (Unix time)
- action type
- brief description

Example:

```
1706523341.52  eye_blink  eye blink
1706523343.10  face_moved_left  face moved left
```

History files are stored automatically and persist after program exit.

---

## Installation

```bash
git clone https://github.com/Mchiir/FaceLocking.git
cd FaceLocking
python -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

**Main dependencies**

- opencv-python
- numpy
- onnxruntime (Also Download ONNX embeder [here](https://huggingface.co/facefusion/models-3.0.0/blob/main/arcface_w600k_r50.onnx))
- mediapipe
- scipy

---

## Running Face Locking

Enroll identities first:

```bash
python -m src.enroll
```

Start the face locking system:

```bash
python -m src.facelock
```

The system will prompt for the identity name to lock onto.

---

## Conclusion

This project moves beyond face recognition into **identity-aware behavior tracking**.
It demonstrates how a recognized face can become a persistent subject whose actions are observed, interpreted, and recorded over time using explainable computer vision logic.
