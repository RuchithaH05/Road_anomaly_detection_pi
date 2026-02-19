# Real-Time Road Anomaly Detection System 🚗💨

## 📌 Project Description
This project focuses on the development of an **IoT-driven Smart Dashcam** designed to detect road anomalies such as potholes and speed bumps in real-time. Utilizing a **Raspberry Pi 4**, the system processes live video feed from the road to identify damage, enabling safer navigation and providing data for urban road maintenance, specifically tailored for high-traffic environments like **Bengaluru**.

---

## 🛠️ Hardware Requirements
* **Processing Unit:** Raspberry Pi 4 Model B (4GB/8GB RAM)
* **Camera:** Raspberry Pi Camera Module 3 Wide or 1080p USB Webcam
* **Power Supply:** 5V/3A USB-C Power Adapter (or dedicated Car Charger for field testing)
* **Storage:** 32GB Class 10 MicroSD Card

---

## 💻 Software Stack
* **Operating System:** Raspberry Pi OS (64-bit)
* **Language:** Python 3.x
* **Libraries:** OpenCV (Image Processing), TensorFlow Lite / Tiny-YOLO (Deep Learning Inference), NumPy
* **Remote Management:** SSH (Secure Shell) via Mac Terminal

---

## ⚙️ System Configuration & Setup
The system is configured for **"Headless" operation**, allowing it to be controlled remotely without a monitor.

* **OS Flashing:** Raspberry Pi OS installed via Raspberry Pi Imager v2.0.6.
* **Network:** Pre-configured to connect automatically to a **Mobile Hotspot** (SSID/Password enabled during flashing).
* **Remote Access:** **SSH** enabled for wireless development from a laptop.
* **Localisation:** Timezone set to **Asia/Kolkata** for accurate log timestamping.

---

## 🚀 Execution & Deployment

### 1. Environment Preparation
Once logged into the Pi via SSH, run the following to install dependencies:

sudo apt update && sudo apt upgrade -y
sudo apt install python3-opencv python3-pip -y
pip3 install tflite-runtime numpy
2. Manual Execution
To run the detection system manually:

Bash
cd ~/road_anomaly_project
python3 main_detection.py
3. Automated Deployment (Production)
To ensure the dashcam starts working the moment the vehicle is powered on, the script is deployed as a Systemd Service:

Create a service file: sudo nano /etc/systemd/system/road_detector.service

Enable and start the service:

Bash
sudo systemctl daemon-reload
sudo systemctl enable road_detector.service
sudo systemctl start road_detector.service
📊 Methodology
Data Acquisition: Live frames are captured by the Pi Camera.

Preprocessing: Frames are resized and converted to grayscale/RGB using OpenCV.

Inference: The TensorFlow Lite model analyzes the frames for anomaly patterns.

Logging: Anomalies are logged with a local timestamp for further review.

📂 Repository Structure
/Documentation: Project reports and architecture diagrams.

/Hardware: Circuit diagrams and component specifications.

/Media: Demo videos and setup photos.
