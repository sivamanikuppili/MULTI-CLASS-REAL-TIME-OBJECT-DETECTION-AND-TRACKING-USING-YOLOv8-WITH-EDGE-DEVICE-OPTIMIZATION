<a href="https://colab.research.google.com/drive/10NnTmXTETh-lw76BF5v4mdIMc-f6lm96?usp=drive_link" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

# Multi-Class Real-Time Object Detection and Tracking 
**Using YOLOv8 with Edge Device Optimization**

## 📌 Project Overview
This capstone project implements a comprehensive, high-performance computer vision suite utilizing state-of-the-art object detection and tracking models. The system is engineered to perform multi-class object detection, real-time video tracking, and high-resolution precision scanning. 

A primary architectural focus of this project is **Edge Device Optimization**. The models and data pipelines are constrained and optimized to run efficiently on edge hardware (such as the NVIDIA Jetson series) with limited compute and memory resources.

## 🚀 Key Features

*   **Unified Interactive Dashboard:** A sleek, glassmorphism-styled HTML/CSS UI built directly into the notebook environment, allowing users to launch different detection modules seamlessly.
*   **Static Image Analysis (Edge Optimized):** 
    *   Utilizes the highly efficient `yolov8n.pt` (Nano) model for rapid inference.
    *   Performs multi-class detection and aggregates the mathematical counts of each detected object.
*   **Video Tracking Pipeline:**
    *   Processes MP4/AVI files for persistent object tracking across frames.
    *   Employs memory-safe streaming (`stream=True`) to handle large video files without causing buffer overflows.
    *   Automatically compresses the tracked output using `ffmpeg` for efficient downloading.
*   **High-Resolution Precision Scan:**
    *   Leverages the browser's JS API to force a 4K resolution capture from webcam hardware.
    *   Utilizes `yolov8x-worldv2.pt` (Extra Large World) for intelligent, prompt-based open-vocabulary detection.
    *   Features **Custom Overlap Cleaning Logic** to mathematically filter out overlapping "ghost boxes", ensuring maximum precision.
*   **Smart Measure v4 (High-Performance Tracking):**
    *   A multi-threaded, real-time application capable of 15-30 FPS tracking.
    *   Features an advanced **Re-ID (Re-identification) Gallery**: Objects maintain their unique global IDs even if they leave and re-enter the camera frame.
    *   Integrates a MiDaS depth estimation engine running in a dedicated background thread for real-world distance scaling and calibration.

## 🛠️ Technology Stack
*   **Core AI/Vision Models:** Ultralytics YOLOv8 (Nano & XL World), MiDaS (Depth Estimation), DeepFace (Demographic Analysis).
*   **Computer Vision Engine:** OpenCV (`opencv-python`).
*   **Environment:** Google Colab.
*   **UI & Asynchronous Bridging:** HTML, CSS, JavaScript, IPython Display API.
*   **Data Handling & Math:** NumPy, SciPy, PyTorch.

## 💻 How to Run the Project

*Note: GitHub's native notebook renderer often struggles with heavy interactive elements and base64 image data. For the best experience, please run this project directly in Google Colab.*

1. Click the **"Open in Colab"** badge at the top of this page.
2. Ensure you are connected to a GPU runtime (`Runtime` > `Change runtime type` > `Hardware accelerator` > `GPU`).
3. Run the Unified Setup cell to install dependencies and launch the interactive dashboard.
4. Click any of the module buttons on the dashboard to test the models!

## ⚙️ Edge Device Optimization Strategies
To ensure this software can be deployed on IoT and Edge devices, the following optimizations were strictly implemented:
*   **Model Selection:** Defaulting to `yolov8n.pt` for standard tasks to balance maximum frame rates with acceptable mAP.
*   **Inference Downscaling:** The real-time tracker forces `imgsz=320`, cutting processing compute by up to 75% while mathematically mapping coordinates back to a 640p display frame.
*   **Thread Isolation:** Heavy tasks (like MiDaS depth mapping) are decoupled from the main inference loop using `threading.Thread` to prevent FPS bottlenecking.
*   **Single-Batched API Calls:** The Python-to-JavaScript bridge utilizes atomic, single-batched calls per frame to drastically reduce cross-language latency.

---
*Developed as a B.Tech Computer Science and Engineering Capstone Project.*
