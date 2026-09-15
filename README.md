# 🚗 DriveAlert — Real-Time Drowsiness Detection System

A real-time computer vision system that monitors a driver's eyes through a webcam and raises an instant audio-visual alert the moment signs of drowsiness are detected — helping prevent accidents caused by fatigue.

## 📌 Overview

DriveAlert continuously tracks a person's face and eyes in **real time** using a live webcam feed. It calculates the **Eye Aspect Ratio (EAR)** for both eyes on every frame — a well-known technique for detecting eye closure. If the eyes stay closed for a sustained number of consecutive frames (indicating drowsiness rather than a normal blink), the system immediately displays a warning on screen and triggers an audible alarm.

## ✨ Features

- 🎥 **Real-time video processing** directly from your webcam
- 👁️ **68-point facial landmark detection** using dlib
- 📐 **Eye Aspect Ratio (EAR)** calculation to measure eye openness
- 🔔 **Instant audio alert** when drowsiness is detected
- 🖼️ **Live visual feedback** with eye contours and on-screen warning text
- ⚙️ **Configurable sensitivity** via EAR threshold and frame count

## 🧠 How It Works

1. Captures live video frames from the webcam.
2. Detects the face in each frame using dlib's frontal face detector.
3. Locates 68 facial landmarks and extracts the left and right eye coordinates.
4. Computes the **Eye Aspect Ratio (EAR)** for each eye:

   ```
   EAR = (||p2-p6|| + ||p3-p5||) / (2 * ||p1-p4||)
   ```

5. Averages both EAR values. A low EAR indicates closed eyes.
6. If the EAR stays below the threshold (`0.3`) for a set number of consecutive frames (`48`), the system flags **"DROWSINESS DETECTED"** and sounds an alarm.
7. Resets the counter as soon as the eyes reopen.

## 🛠️ Tech Stack

| Component | Purpose |
|---|---|
| Python | Core programming language |
| OpenCV | Video capture, image processing, drawing overlays |
| dlib | Face detection & 68-point facial landmark prediction |
| imutils | Convenience utilities for image resizing & landmark handling |
| scipy | Euclidean distance calculation for EAR |
| winsound | Audio alert (Windows only) |

## 📦 Requirements

- Python 3.x
- Webcam
- The pre-trained landmark model: `shape_predictor_68_face_landmarks.dat`
  (download from the [dlib model repository](http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2) and place it in the project root)

## ⚙️ Installation

```bash
# Clone the repository
git clone https://github.com/<your-username>/Drowsiness-Detection-System.git
cd Drowsiness-Detection-System

# Install dependencies
pip install opencv-python dlib imutils scipy

# Download & extract the facial landmark model into the project folder
```

> **Note:** `winsound` is a built-in Windows-only module. On macOS/Linux, replace the alert with a library such as `playsound` or `simpleaudio`.

## ▶️ Usage

```bash
python main.py
```

- A window will open showing the live webcam feed with eye contours drawn.
- If drowsiness is detected, a red **"DROWSINESS DETECTED"** warning appears along with a beep alert.
- Press **`q`** to quit the application.

## 🎛️ Configuration

You can tune detection sensitivity in `main.py`:

| Variable | Default | Description |
|---|---|---|
| `earThresh` | `0.3` | EAR value below which an eye is considered closed |
| `earFrames` | `48` | Number of consecutive drowsy frames before triggering an alert |

## 🚀 Future Improvements

- [ ] Cross-platform audio alerts (replace `winsound`)
- [ ] Yawn detection using mouth aspect ratio
- [ ] Head-pose / nodding detection
- [ ] Mobile app / embedded (Raspberry Pi) deployment
- [ ] Logging drowsiness events with timestamps for analytics

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to open a pull request or raise an issue.

## 📄 License

This project is licensed under the [MIT License](LICENSE).

## ⭐ Support

If you find this project useful, consider giving it a ⭐ on GitHub — it helps others discover it too!
