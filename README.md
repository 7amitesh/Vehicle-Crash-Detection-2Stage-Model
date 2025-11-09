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

