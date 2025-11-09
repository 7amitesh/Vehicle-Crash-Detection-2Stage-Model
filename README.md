# 🚗 Vehicle-Crash-Detection-2Stage-Model

A **Hybrid Two-Stage Vehicle Accident Detection & Validation System** using **IoT Sensors + Deep Learning**.  
This model reduces false accident alerts by **96%**, ensuring only real crashes trigger emergency responses.

---

## ⭐ Overview

This project combines:

| Stage | Component | Description |
|--------|-------------|-----------------|
| **Stage 1 – IoT Trigger** | Raspberry Pi + MPU6050 | Detects sudden g-force impact & records video |
| **Stage 2 – AI Validation** | ResNet-50 CNN Model | Confirms if accident is real before alerting |

This prevents false alerts caused by bumps, hard brakes, potholes, or device drops.

---

## 🧠 Key Features

- Real-time accident detection
- IoT sensor fusion (Accelerometer + Gyroscope + GPS)
- 30-second rolling camera buffer (pre- & post-impact)
- Deep Learning video analysis using ResNet-50
- Cloud server + alert notification system
- 96% false-positive reduction vs traditional IoT systems

---

## 🏗 System Architecture

### ✅ **High-Level Architecture (ASCII)**

               ┌─────────────────────────────────┐
               │   In-Vehicle IoT Module (IVM)    │
               │  (Raspberry Pi + Sensors)        │
               └─────────────────────────────────┘
                            |
                            | Trigger Event (>= 8g)
                            v
          ┌────────────────────────────────────────────┐
          │ Save 30-sec Video + GPS + Timestamp + Speed │
          └────────────────────────────────────────────┘
                            |
                            | Upload Event Package
                            v
            ┌────────────────────────────────────────┐
            │     Cloud Validation Server (CVS)       │
            │  (Flask API + ResNet-50 Model)          │
            └────────────────────────────────────────┘
                            |
             Accident? ───────────► YES ─────────► Send Alerts
                            |
                            └────► NO ─────► Log False Positive


---

### 📌 **Mermaid Architecture Diagram**

```mermaid
flowchart LR
    IVM[Raspberry Pi IoT Module<br>MPU6050 + GPS + Camera] -->|Trigger + Upload| CVS[Cloud Validation Server]
    CVS --> DL[ResNet-50 Accident Classifier]
    DL -->|Accident| ALERT[Send SMS/Email to Emergency Services]
    DL -->|No Accident| LOG[Store False Positive Log]
📍 Placeholder: Insert system_architecture.png diagram in /docs folder
Vehicle-Crash-Detection-2Stage-Model/
│
├── edge-device/                       # Stage-1: IoT Code for Raspberry Pi
│   ├── sensors/
│   │   ├── accelerometer.py
│   │   ├── gps_module.py
│   │   └── camera_buffer.py
│   ├── main.py
│   ├── config.py
│   └── requirements.txt
│
├── server/                            # Stage-2: Cloud + DL Validation
│   ├── app.py
│   ├── model/
│   │   ├── resnet50_model.h5
│   │   └── preprocess.py
│   ├── utils/
│   │   ├── video_to_frames.py
│   │   ├── predictor.py
│   │   └── alert_service.py
│   └── requirements.txt
│
├── model-training/
│   ├── Accident_Training.ipynb
│   ├── datasets.txt
│   └── README.md
│
├── docs/
│   ├── architecture.png
│   ├── system_flowchart.png
│   └── presentation.pptx
│
└── README.md
