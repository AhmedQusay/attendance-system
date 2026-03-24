# 🎯 AI-Based Face Recognition Attendance System (Edge AI + Azure IoT)

## 📌 Overview

This project implements a **real-time face recognition attendance system** using **Edge AI** and **Azure IoT Hub**.
It detects faces from a camera, tracks individuals across frames, recognizes identities using embeddings, and logs attendance events (IN/OUT) which are sent to the cloud.

---

## 🚀 Key Features

* 🎥 Real-time face detection using **InsightFace**
* 🧠 Face recognition with **ArcFace embeddings**
* 🔄 Multi-frame confirmation for accuracy
* 🧍 Tracking using **IoU-based tracker**
* 🧾 Attendance logic (IN / OUT events)
* 👨‍🏫 Teacher-first policy enforcement
* ☁️ Cloud integration with **Azure IoT Hub**
* 🔐 Secure secret handling using `.env`

---

## 🏗️ System Architecture

```
Camera → Face Detection → Tracking → Recognition → Attendance Engine → Azure IoT Hub → (Future: Azure Function → SQL DB)
```

---

## 📂 Project Structure

```
attendance_face/
│
├── config/                # Configuration files
├── data/
│   ├── enroll_images/     # Raw images for enrollment
│   ├── gallery/           # Generated embeddings
│
├── logs/                  # Logs (optional)
│
├── src/
│   ├── core/              # Tracking, matching, attendance logic
│   ├── pipeline/          # Main pipeline (camera, IoT sending)
│   ├── scripts/           # Enrollment and utilities
│   ├── utils/             # Helper modules
│
├── .env                   # Secrets (NOT committed)
├── .gitignore
├── requirements.txt
└── README.md
```

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/attendance_face.git
cd attendance_face
```

### 2. Create virtual environment

```bash
python -m venv venv
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

## 🔐 Environment Setup

Create a `.env` file in the root directory:

```env
IOTHUB_DEVICE_CONNECTION_STRING=HostName=your-hub.azure-devices.net;DeviceId=your-device;SharedAccessKey=your-key
```

⚠️ **Important:**

* Never commit `.env`
* Rotate keys if exposed

---

## ☁️ Azure Setup (IoT Hub)

1. Create **Azure IoT Hub**
2. Add a device (e.g., `classroom-room-a1-edge`)
3. Copy the **Primary Connection String**
4. Paste it into `.env`

---

## ▶️ Run the System

### Run camera + attendance system

```bash
python src/pipeline/run_camera.py
```

### Send test event to Azure IoT Hub

```bash
python src/pipeline/edge_send.py
```

---

## 🧠 Core Components

### 🔹 Tracking (IOUTracker)

* Maintains consistent IDs across frames
* Lightweight and real-time

### 🔹 Recognition (GalleryMatcher)

* Uses cosine similarity
* Multi-frame confirmation:

  * `confirm_hits`
  * `confirm_window`

### 🔹 Attendance Engine

* Tracks IN / OUT events
* Handles:

  * absence timeout
  * teacher-first rule

---

## 📊 Example Event

```json
{
  "event_type": "IN",
  "user_id": "student_1001",
  "role": "student",
  "confidence": 0.95,
  "timestamp": "2026-02-11T10:11:00",
  "session_id": "CS101-2026-02-11-0900",
  "room_id": "ROOM-A1",
  "camera_id": "CAM-A1",
  "track_id": 7
}
```

---

## 🔒 Security Best Practices

* Use `.env` for secrets
* Do NOT store keys in code
* Rotate keys regularly
* Use Azure secure configuration in production

---

## 📈 Future Improvements

* Replace IOU tracker with **Deep SORT**
* Add **liveness detection (anti-spoofing)**
* Multi-camera support
* Azure Function → SQL integration
* Dashboard for attendance analytics

---

## 🧪 Technologies Used

* Python
* OpenCV
* InsightFace
* NumPy
* Azure IoT SDK
* TensorFlow / Deep Learning (optional extensions)

---

## 👨‍💻 Author

**Dr. Ahmed Qusay Sabri**
Bahrain Polytechnic

---

## 📄 License

This project is for academic and research purposes.

---
