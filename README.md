<div align="center">

# 👁️ Computer Vision Lab

### Explore · Implement · Experiment

A growing collection of **hands-on computer vision experiments**, tutorial implementations, and mini-projects built while learning Python-based computer vision.

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![MediaPipe](https://img.shields.io/badge/MediaPipe-Hand%20Tracking-0097A7?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Learning%20in%20Progress-22C55E?style=for-the-badge)

**[Projects](#-projects) · [Quick Start](#-quick-start) · [Learning Roadmap](#-learning-roadmap) · [About](#-about-this-repository)**

</div>

---

## ✨ About This Repository

**Computer Vision Lab** is my workspace for turning concepts from courses and tutorials into working code. Each project is organized separately so I can revisit implementations, experiment with changes, and see how my skills develop over time.

**What you'll find here:**

- 📷 Webcam-based computer vision experiments
- 🧠 Hands-on practice with popular Python vision libraries
- 🧩 Reusable code modules and small application demos
- 📝 Notes, requirements, and execution instructions for each topic

> **Learning repository:** Some implementations follow tutorials. Their original sources should be credited in the relevant project README; later changes and experiments are documented alongside them.

## 🗂️ Projects

| # | Project | What it explores | Explore |
|:--:|---|---|:--:|
| 01 | **🤚 Hand Tracking** | Live webcam tracking, 21 hand landmarks, reusable detector class, landmark coordinates, and FPS display | **[View project](01-hand-tracking/)** |

More projects will be added as I work on them.

## 🧰 Tech Stack

| Technology | Role |
|---|---|
| **Python** | Main programming language |
| **OpenCV** | Webcam input, image conversion, drawing, and display |
| **MediaPipe** | Hand landmark detection and tracking |
| **NumPy** | Supporting numerical operations and package compatibility checks |

## 🚀 Quick Start

These instructions use **Windows PowerShell** and **Python 3.11**, which suits the legacy MediaPipe Hands API currently used by the hand-tracking scripts.

**1. Clone the repository**

```powershell
git clone <YOUR-REPOSITORY-URL>
cd computer-vision-lab
```

Replace `<YOUR-REPOSITORY-URL>` with the HTTPS clone URL shown on your GitHub repository's **Code** menu.

**2. Create and activate a virtual environment**

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**3. Install the hand-tracking dependencies**

```powershell
python -m pip install -r .\01-hand-tracking\requirements.txt
```

**4. Run the hand-tracking module demo**

```powershell
python .\01-hand-tracking\HandTrackingModule.py
```

Allow camera access if Windows prompts you. Press **`q`** to close the webcam window.

For implementation details, see the **[Hand Tracking README](01-hand-tracking/README.md)**.

## 📁 Repository Layout

```text
computer-vision-lab/
├── 01-hand-tracking/
│   ├── HandTrackingMin.py
│   ├── HandTrackingModule.py
│   ├── HandTrackingGame.py
│   ├── tests/
│   │   ├── Test_opencv.py
│   │   ├── test.py
│   │   └── test1.py
│   ├── requirements.txt
│   └── README.md
├── .gitignore
└── README.md
```

The local `.venv/` directory is intentionally ignored by Git.

## 🧭 Learning Roadmap

| Topic | Progress |
|---|---|
| Hand detection and landmark tracking | ✅ Implemented |
| Reusable hand-tracking module | ✅ Implemented |
| Finger counting and gesture recognition | 📌 Potential next experiment |
| Pose estimation | 📌 Planned exploration |
| Face and object detection | 📌 Planned exploration |

These are learning goals, not claims that the future projects are already implemented.

## 🤝 Notes & Acknowledgements

This repository documents practice and experimentation. Tutorial-derived code should be attributed to its original author(s), with source links added to each project README. Before reusing third-party code, check its licensing terms.

<div align="center">

---

<sub>Built step by step, one experiment at a time. 🚀</sub>

</div>
