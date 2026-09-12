# 🖐️ Gesture Volume Control

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)](https://opencv.org/)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-Hand%20Tracking-00A67E?style=for-the-badge)](https://developers.google.com/mediapipe)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

A real-time Computer Vision application that lets you control your computer's system master volume using hand gestures captured via a webcam. Built using OpenCV, Google MediaPipe, and PyCAW.

---

## 📌 Demo & Preview

<p align="center">
  <img src="image/Output.gif" alt="Gesture Volume Control Demo" width="650"/>
</p>

---

## ✨ Features

- **Real-Time Hand Tracking:** Detects 21 hand landmarks at high FPS using Google MediaPipe.
- **Intuitive Touchless Control:** Adjust master volume by varying the distance between your thumb and index fingertip.
- **On-Screen Visual Feedback:**
  - Dynamic volume percentage indicator and HUD level bar.
  - Tracking lines and landmark nodes highlighting gesture states.
  - Real-time FPS counter to monitor performance.
- **Native OS Integration:** Communicates directly with system audio endpoints via `pycaw`.

---

## 🛠️ Tech Stack & Architecture

- **Language:** Python
- **Vision & Landmark Tracking:** `opencv-python`, `mediapipe`
- **Math & Transformations:** `numpy`, `math` (Euclidean distance & linear interpolation)
- **Audio Control:** `pycaw`, `comtypes` (Windows Core Audio API)

### How It Works

```
 Webcam Feed
      │
      ▼
 MediaPipe Hands ──► Extracts 21 Landmark Coordinates
      │
      ▼
 Calculate Euclidean Distance between Landmark 4 (Thumb) & Landmark 8 (Index)
      │
      ▼
 Linear Interpolation (numpy.interp): [Pixel Distance Range] ──► [System Volume dB / %]
      │
      ▼
 PyCAW Endpoint Controller ──► Adjusts System Master Audio Level
      │
      ▼
 OpenCV Render ──► Displays HUD Bar, Percentage & Real-Time FPS
```

---

## 🖐️ Landmark Reference

The gesture logic tracks Landmark 4 (Thumb Tip) and Landmark 8 (Index Finger Tip):

<p align="center">
  <img src="image/hand_landmarks_docs.png" alt="MediaPipe Hand Landmarks" width="550"/>
</p>

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8 or higher
- A working webcam
- OS: Windows (for PyCAW Core Audio API integration)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/abhay-singh/Gesture-Volume-Control.git
   cd Gesture-Volume-Control
   ```

2. **Create a virtual environment (optional but recommended):**
   ```bash
   python -m venv venv
   # On Windows:
   venv\Scripts\activate
   # On Linux/macOS:
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

---

## 🎮 Usage

Run the main application script:

```bash
python main.py
```

### Controls

| Gesture / Action | Result |
| :--- | :--- |
| **Pinch Thumb & Index closer** | Decreases system volume |
| **Spread Thumb & Index apart** | Increases system volume |
| **Distance < threshold (pinch tap)** | Volume level drops to minimum (mute) |
| **Press `q` on the video window** | Exit application cleanly |

---

## 📁 Project Structure

```text
Gesture-Volume-Control/
│
├── image/
│   ├── Output.gif                # Demo recording
│   ├── hand_landmarks_docs.png   # MediaPipe landmark diagram
│   └── htm.jpg                   # Hand tracking diagram/preview
│
├── main.py                       # Main application script
├── requirements.txt              # Required Python packages
├── License                       # MIT License
└── README.md                     # Project documentation
```

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to open an issue or submit a PR.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

---

## 👤 Author

**Abhay Singh**
- GitHub: [@abhay-singh](https://github.com/abhay-singh)

---

## 📄 License

This project is licensed under the MIT License - see the [License](License) file for details.
