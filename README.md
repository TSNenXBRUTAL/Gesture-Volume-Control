# 🖐️ Gesture Volume Control

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)](https://opencv.org/)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-Hand%20Tracking-00A67E?style=for-the-badge)](https://developers.google.com/mediapipe)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

A real-time Computer Vision application that enables touchless system master volume control using natural hand gestures captured via a webcam. Built with Python, OpenCV, Google MediaPipe, and PyCAW.

---

## 📌 Live Demo & Preview

<p align="center">
  <img src="image/Output.gif" alt="Gesture Volume Control Live Demo" width="700"/>
</p>

---

## ✨ Features

- **High-Precision Hand Tracking:** Real-time detection and 21-landmark tracking powered by Google MediaPipe Hands.
- **Natural Touchless Gestures:** Dynamic system master volume adjustment based on the Euclidean distance between thumb and index fingertips.
- **Rich Visual HUD:**
  - On-screen volume level bar with rounded corners and gradient fill.
  - Live volume percentage indicator with dark contrast background.
  - Visual tracking line and glowing endpoint nodes highlighting pinch state.
  - Contextual on-screen user instructions and quit cues.
- **Native OS Core Audio Integration:** Direct communication with Windows system audio endpoints via `pycaw`.

---

## 🧠 Hand Landmark & Gesture Recognition Architecture

The tracking pipeline relies on Google MediaPipe Hand Landmark coordinates:

<p align="center">
  <img src="image/hand_landmarks_docs.png" alt="MediaPipe 21 Hand Landmarks Reference" width="600"/>
</p>

### Diverse Gesture Detection Examples

The underlying hand landmark detector functions across varying angles, poses, and backgrounds:

<p align="center">
  <img src="image/htm.jpg" alt="Hand Tracking Model Landmark Poses" width="650"/>
</p>

---

## 🛠️ System Architecture & Workflow

```
   ┌──────────────────┐
   │   Webcam Feed    │
   └────────┬─────────┘
            │
            ▼
   ┌──────────────────────────────────────────┐
   │      MediaPipe Hands Model Pipeline       │
   │  Extracts 21 3D hand landmark coordinates │
   └────────┬─────────────────────────────────┘
            │
            ▼
   ┌──────────────────────────────────────────┐
   │        Euclidean Distance Metric         │
   │  d = √((x2 - x1)² + (y2 - y1)²)          │
   │  Between Landmark 4 (Thumb) & 8 (Index)  │
   └────────┬─────────────────────────────────┘
            │
            ▼
   ┌──────────────────────────────────────────┐
   │        Linear Interpolation (NumPy)      │
   │  [50px, 220px] ──► [minVol dB, maxVol dB]│
   │  [50px, 220px] ──► [0%, 100%] Volume     │
   └────────┬─────────────────────────────────┘
            │
            ▼
   ┌──────────────────────────────────────────┐
   │      PyCAW Endpoint Volume Control       │
   │  IAudioEndpointVolume.SetMasterVolume    │
   └────────┬─────────────────────────────────┘
            │
            ▼
   ┌──────────────────────────────────────────┐
   │        OpenCV Rendering & HUD Display    │
   │  Dynamic bar, live %, glow nodes & cues  │
   └──────────────────────────────────────────┘
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8 or higher
- A working webcam
- Operating System: Windows (required for PyCAW Core Audio API)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/abhay-singh/Gesture-Volume-Control.git
   cd Gesture-Volume-Control
   ```

2. **Create and activate a virtual environment (recommended):**
   ```bash
   # Windows (Command Prompt / PowerShell)
   python -m venv venv
   venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

---

## 🎮 Usage

Run the main application:

```bash
python main.py
```

### Controls Guide

| Action / Gesture | Visual Cue | Output |
| :--- | :--- | :--- |
| **Bring Thumb & Index closer** | Green line shortens | Volume decreases |
| **Spread Thumb & Index apart** | Green line lengthens | Volume increases |
| **Pinch tight ($d < 50\text{px}$)** | Line turns Red | Volume mutes / drops to 0% |
| **Press `q`** | — | Exits application window |

---

## 📁 Repository Structure

```text
Gesture-Volume-Control/
│
├── image/
│   ├── Output.gif                # Animated live demo recording
│   ├── hand_landmarks_docs.png   # MediaPipe 21 hand landmarks diagram
│   └── htm.jpg                   # Multi-pose hand tracking visualization
│
├── main.py                       # Core tracking and audio control script
├── requirements.txt              # Pinned Python package dependencies
├── License                       # MIT License
└── README.md                     # Project documentation
```

---

## 📦 Dependencies

- `opencv-python`: Video capture, image processing, and visual HUD rendering
- `mediapipe`: Machine learning pipeline for real-time 21 hand-landmark tracking
- `numpy`: Fast mathematical array processing and linear range interpolation
- `pycaw`: Python Core Audio Windows library for master volume control
- `comtypes`: Pure Python COM interface package backing PyCAW

---

## 👤 Author

**Abhay Singh**
- GitHub: [@abhay-singh](https://github.com/abhay-singh)

---

## 📄 License

This project is licensed under the MIT License - see the [License](License) file for details.
