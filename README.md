# MULTI-CLASS-REAL-TIME-OBJECT-DETECTION-AND-TRACKING-USING-YOLOv8-WITH-EDGE-DEVICE-OPTIMIZATION

## Project Overview

This capstone project implements a comprehensive suite of computer vision tools using state-of-the-art object detection and tracking models. The system is designed to perform multi-class object detection, real-time video tracking, and high-resolution precision scanning. A key focus of this project is **Edge Device Optimization**, ensuring that these complex models can run efficiently on hardware with constrained compute and memory resources, such as the NVIDIA Jetson series.

The project integrates various YOLOv8 models, customizing them for specific tasks, and provides a unified, interactive dashboard for easy operation within a Google Colab environment.

## Key Features

1.  **Unified Dashboard:** A sleek, interactive HTML/CSS-based UI that allows users to launch different detection modes seamlessly from a single interface.
2.  **Static Image Analysis (Edge Optimized):**
    *   Utilizes the highly efficient `yolov8n.pt` (Nano) model for rapid inference.
    *   Uploads an image, performs multi-class object detection, and aggregates the counts of each detected object.
    *   Resizes the output for optimal viewing without overwhelming browser memory.
3.  **Video Tracking Pipeline:**
    *   Processes uploaded MP4/AVI files for persistent object tracking across frames.
    *   Employs memory-safe streaming (`stream=True`) to handle large video files without crashing.
    *   Automatically compresses the tracked output video using `ffmpeg` for efficient downloading.
4.  **High-Resolution Precision Scan:**
    *   Leverages the browser's JavaScript API to force a high-resolution (up to 4K) capture from the user's webcam.
    *   Uses the powerful `yolov8x-worldv2.pt` (Extra Large World) model for intelligent, prompt-based object detection.
    *   Implements **Custom Overlap Cleaning Logic** to filter out "ghost boxes" (e.g., a low-confidence large box swallowing a high-confidence small box), ensuring clean and precise results.
5.  **Smart Measure v4 (Separate High-Performance Thread):**
    *   *Note: Runs as a separate cell due to its complex asynchronous nature.*
    *   A high-speed, multi-threaded application offering 15-30 FPS tracking.
    *   Features real-time Re-ID (Re-identification) so objects maintain their IDs even when leaving and re-entering the frame.
    *   Includes a MiDaS depth estimation engine running in a background thread for real-world distance measurement and calibration.

## Technology Stack

*   **Core AI Models:** Ultralytics YOLOv8 (Nano, Extra Large World), MiDaS (for depth estimation).
*   **Computer Vision & Image Processing:** OpenCV (`opencv-python`).
*   **Environment:** Google Colab.
*   **UI & Interactivity:** HTML, CSS (Glassmorphism design), JavaScript, IPython Display API.
*   **Data Handling & Math:** NumPy, SciPy.
*   **Video Processing:** FFmpeg.

## Installation and Setup

This project is designed to run in a Google Colab environment.

1.  Open a new Google Colab notebook.
2.  Ensure you are using a GPU runtime (Runtime > Change runtime type > Hardware accelerator > GPU).
3.  Copy the unified Python script (provided in the repository) into a code cell.
4.  Run the cell. The script will automatically install all required dependencies (Ultralytics, OpenCV, DeepFace, Timm, SciPy) silently.

## How to Use the Dashboard

Upon running the main script, an interactive dashboard will appear in the output of the cell.

1.  **Launch Image Mode:** Click this button, then use the file upload prompt to select an image. The system will process it and display the detected objects and their counts.
2.  **Launch Video Mode:** Click this button and upload a video file. The system will track objects throughout the video and automatically download a compressed, annotated version when finished.
3.  **Launch Precision Scan:** Click this button to activate your webcam. Hold your items steady and separated. The system will capture a high-res image and apply strict, logic-cleaned detection.

## Edge Device Optimization Strategies Implemented

This project specifically targets performance on edge devices by employing the following strategies:

*   **Model Selection:** Defaulting to the YOLOv8 Nano (`yolov8n.pt`) model for standard image and video tasks, which offers the best balance of speed and accuracy for constrained hardware.
*   **Inference Sizing:** For real-time tracking (like in Smart Measure v4), the inference image size is reduced (`imgsz=320`). This drastically cuts processing time while YOLO automatically maps coordinates back to the original frame size.
*   **Memory Management:** Using `stream=True` during video processing ensures the model yields results frame-by-frame as a generator, preventing memory overflow on long videos.
*   **Asynchronous Processing:** (In Smart Measure v4) Heavy tasks like Depth Estimation (MiDaS) are offloaded to background threads (`threading.Thread`) and manage data via queues, preventing them from blocking the main high-speed tracking loop.
*   **Compression:** Automatically compressing video outputs before transfer to reduce bandwidth and storage overhead.
*   **Efficient UI Bridging:** Utilizing single batched JavaScript calls per frame to pass data between Python and the browser, minimizing latency.

## Project Structure

*   `unified_dashboard.py`: Contains the consolidated code for Image, Video, and High-Res scanning modes, along with the HTML/CSS dashboard.
*   `smart_measure_v4.py`: Contains the advanced, multi-threaded real-time tracking and measurement system.

## Future Enhancements

*   Integration with specific edge hardware APIs (e.g., TensorRT for NVIDIA Jetsons) for further inference acceleration.
*   Expanding the Re-ID gallery capabilities for more robust long-term object tracking across multiple camera feeds.
*   Adding a quantitative evaluation metric (like mAP) specific to the custom overlap cleaning logic.

---
*Created as a B.Tech Computer Science and Engineering Capstone Project.*
