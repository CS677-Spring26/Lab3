# Lab 3: Always On Keyword Spotting on ESP32

## Overview
Students will build an IoT system where the ESP32 continuously monitors microphone input, classifies audio segments in real-time using an on-device Neural Network, and triggers a response only when the keyword **"Go"** is detected.

---

## Task Setup

### 1. Model Training & Optimization
* **Dataset:** Google Speech Commands Dataset.
* **Classification:** Three categories — `go`, `other speech`, and `silence`.
* **Preprocessing:** Raw 16 kHz audio samples are downsampled to a lower frequency to serve as inputs for a compact **Convolutional Neural Network (CNN)**.
* **Quantization:** The trained `float32` model is quantized to **Full Integer (INT8)** using the TFLite Converter and a representative dataset to ensure efficiency on edge hardware.
* **Deployment:** The optimized `.tflite` file is converted into a **C header file** for direct integration into the ESP32 firmware.

### 2. Real-Time Inference
* **Audio Capture:** The ESP32 monitors audio via the **I2S interface**, processing 1-second sliding windows.
* **Feature Extraction:** The C++ code performs on-device **MFCC (Mel-frequency cepstral coefficients)** extraction identical to the training pipeline.
* **Classification:** The INT8 tensor is fed to the **TensorFlow Lite Micro (TFLM)** interpreter.
* **Trigger:** If the "go" score exceeds a predefined threshold, the system outputs: 
    > `WAKE WORD DETECTED: ready to go`

---

## Learning Objectives
* **Model Creation & Quantization:** Build a simple CNN and optimize it using TFLite.
* **Embedded Deployment:** Understand how to run a C array model on the ESP32.
* **Peripheral Integration:** Learn to use **I2S** for continuous, real-time audio capture.
* **Logic Development:** Implement sliding window and post-processing logic for reliable, low-latency, "always-on" detection.
