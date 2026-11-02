<div align="center">

# 🤚 Real-Time Hand Tracking

### OpenCV + MediaPipe · Python

Detect hands from a webcam, visualize landmarks, and extract fingertip coordinates using a reusable Python class.

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-Webcam%20Processing-5C3EE8?style=flat-square&logo=opencv&logoColor=white)
![MediaPipe](https://img.shields.io/badge/MediaPipe-Hands-0097A7?style=flat-square)
![Landmarks](https://img.shields.io/badge/Landmarks-21%20per%20hand-16A34A?style=flat-square)

**[Features](#-features) · [How It Works](#-how-it-works) · [Run It](#-getting-started) · [Module API](#-using-the-reusable-module)**

[← Back to Computer Vision Lab](../README.md)

</div>

---

## 🎯 Overview

This is a **tutorial-based hand-tracking experiment** using a live webcam feed. It started as a straightforward MediaPipe implementation and evolved into a reusable `handDetector` class.

The current code can find hand landmarks, draw the hand skeleton, extract landmark pixel positions, and display the approximate camera FPS. `HandTrackingGame.py` is currently a **demonstration script** that uses the reusable module; it is not yet a complete game.

## ✨ Features

- 📸 **Real-time tracking** through an OpenCV webcam feed
- 🖐️ **Up to two hands** with configurable detection settings
- 📍 **21 landmarks per detected hand** (IDs `0`–`20`)
- 🎨 **Landmark and connection drawing** over camera frames
- 🎯 **Pixel coordinate extraction** as `[landmark_id, x, y]`
- ⚡ **FPS overlay** to monitor the processing rate
- 🧩 **Reusable `handDetector` class** for other experiments

## 🔄 How It Works

```mermaid
flowchart LR
    A[Webcam frame] --> B[OpenCV: BGR to RGB]
    B --> C[MediaPipe Hands]
    C --> D[Hand landmarks]
    D --> E[Draw skeleton and points]
    D --> F[Extract pixel coordinates]
    E --> G[Display live video + FPS]
    F --> G
```

**Example output:**

```text
[4, 245, 280]
```

This is an illustrative landmark entry—not a recorded result. `4` identifies the **thumb tip**; the remaining values are its `x` and `y` pixel coordinates in the frame.

## 📂 Files Explained

| File | Purpose |
|---|---|
| `HandTrackingMin.py` | Introductory implementation that detects hands, draws landmarks, and prints positions |
| `HandTrackingModule.py` | Reusable `handDetector` class plus a standalone webcam demonstration |
| `HandTrackingGame.py` | Separate demo that imports and tests `HandTrackingModule.py` |
| `tests/Test_opencv.py` | Checks webcam capture and display using OpenCV |
| `tests/test.py` | Prints OpenCV and MediaPipe versions |
| `tests/test1.py` | Checks package versions and availability of the legacy `mp.solutions` API |
| `requirements.txt` | Python package requirements |

## 🚀 Getting Started

### 1. Requirements

- **Python 3.11** recommended for this project's legacy MediaPipe code
- A working webcam
- Windows PowerShell (commands below)

### 2. Set up your environment

From the **repository root**:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r .\01-hand-tracking\requirements.txt
```

> **Compatibility note:** This tutorial uses `mp.solutions.hands` from the legacy MediaPipe API. The project pins `mediapipe==0.10.21` for compatibility; newer MediaPipe versions may not support the same interface.

### 3. Run the programs

From the **repository root**:

```powershell
# Reusable detector module (includes a demo)
python .\01-hand-tracking\HandTrackingModule.py

# Simple first implementation
python .\01-hand-tracking\HandTrackingMin.py

# Demo that imports the reusable module
python .\01-hand-tracking\HandTrackingGame.py
```

Press **`q`** to close the video window.

### 4. Run it as a Python module

From inside the `01-hand-tracking` directory:

```powershell
cd .\01-hand-tracking
python -m HandTrackingModule
```

The `if __name__ == "__main__":` guard runs the demonstration only when this module is executed—not when another file imports it.

## 🧩 Using the Reusable Module

```python
import cv2
import HandTrackingModule as htm

cap = cv2.VideoCapture(0)
detector = htm.handDetector(maxHands=2, detectionCon=0.5)

while True:
    success, frame = cap.read()
    if not success:
        break

    frame = detector.findHands(frame)
    landmarks = detector.findPosition(frame)

    if landmarks:
        print("Thumb tip:", landmarks[4])

    cv2.imshow("Hand Tracking", frame)
    if cv2.waitKey(1) & 0xFF == ord("q"):
        break

cap.release()
cv2.destroyAllWindows()
```

Save this example in the **same folder as `HandTrackingModule.py`** so the import works as shown.

### Detector settings

| Parameter | Default | Meaning |
|---|:--:|---|
| `mode` | `False` | Treat frames as a continuous video stream |
| `maxHands` | `2` | Maximum number of hands to detect |
| `detectionCon` | `0.5` | Minimum hand-detection confidence |
| `trackCon` | `0.5` | Minimum hand-tracking confidence |

The current implementation uses a fixed MediaPipe `model_complexity` value of `1`.

### Available methods

| Method | Output |
|---|---|
| `findHands(img, draw=True)` | Annotated image frame |
| `findPosition(img, handNo=0, draw=True)` | Landmark list with entries `[id, x, y]` |

Call `findHands()` **before** `findPosition()` for each frame, since the latter uses landmark results created by the former. The `handNo` index must identify a detected hand.

## 💡 What I Learned

- How to capture frames and convert between BGR and RGB
- How MediaPipe represents a hand with 21 normalized landmarks
- How to convert normalized values into image pixel coordinates
- How to organize a reusable Python class and import it from another script
- How to calculate and display approximate FPS

## 🛠️ Troubleshooting

<details>
<summary><strong>Camera window does not open</strong></summary>

Check Windows camera permissions and close applications that may be using the webcam. Test with `tests/Test_opencv.py`.

</details>

<details>
<summary><strong><code>AttributeError: module 'mediapipe' has no attribute 'solutions'</code></strong></summary>

Check that you are running the intended Python virtual environment and that the installed MediaPipe version matches `requirements.txt`.

</details>

<details>
<summary><strong><code>ModuleNotFoundError: No module named 'HandTrackingModule'</code></strong></summary>

Run the sample from the `01-hand-tracking` folder or save the importing script alongside `HandTrackingModule.py`.

</details>

## 📚 Credits & Learning Resources

This project was developed while following hand-tracking tutorials and experimenting with their examples.

- **Original tutorial:** _Add the tutorial title, author, and link here._
- [OpenCV documentation](https://docs.opencv.org/)
- [MediaPipe documentation](https://ai.google.dev/edge/mediapipe/solutions/guide)

When you extend tutorial code, document what you changed and respect the original license.

<div align="center">

---

[⬆ Back to top](#-real-time-hand-tracking) · [← All projects](../README.md)

<sub>Part of the Computer Vision Lab learning repository.</sub>

</div>
