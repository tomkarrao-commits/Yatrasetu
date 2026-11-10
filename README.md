# 🛕 YatraSetu: AI Crowd Analytics & ML Anomaly Prediction Ecosystem

[![Python 3.10+](https://img.shields.io/badge/Python-3.10+-3776AB.svg?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688.svg?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![YOLOv8/11](https://img.shields.io/badge/Computer_Vision-Ultralytics_YOLO-FF6F00.svg?style=flat-square)](https://docs.ultralytics.com/)
[![React 18+](https://img.shields.io/badge/React-18+-61DAFB.svg?style=flat-square&logo=react&logoColor=black)](https://react.dev/)
[![Scikit-Learn](https://img.shields.io/badge/ML-Scikit--Learn-F7931E.svg?style=flat-square&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)

**YatraSetu** is an end-to-end intelligent crowd management and public safety ecosystem designed for high-density pilgrimage destinations, heritage corridors, and mass gatherings. It combines **edge computer vision (YOLO headcount tracking)**, a **machine learning predictive forecasting pipeline**, **real-time Z-score surge anomaly detection**, and a **responsive command-center telemetry dashboard**.

---

## 🏛️ System Architecture

```mermaid
flowchart TD
    subgraph CV["🎥 Computer Vision Pipeline (ai_pipeline/)"]
        Video["CCTV / Drone Camera Feed"] --> YOLO["Ultralytics YOLO RegionCounter"]
        YOLO --> LiveCount["Live Headcount per ROI Zone"]
        LiveCount --> Bootstrapper["Historical Dataset Generator"]
        Bootstrapper --> Dataset[("historical_crowd_data.csv")]
    end

    subgraph ML["🧠 Backend ML & Anomaly Engine (backend/)"]
        Dataset --> RF["Random Forest Regressor (Cyclic Temporal Features)"]
        RF --> Forecast["24-Hour Predictive Forecast Curve"]
        LiveCount --> ZScore["Z-Score Surge Anomaly Detector (Z ≥ 2.0)"]
        Dataset --> Optimizer["Daily Schedule Optimizer (Quiet Windows)"]
        FastAPI["FastAPI High-Concurrency REST API"] --> InMem[("Real-Time Telemetry Cache")]
    end

    subgraph UI["🎨 Mission Control Dashboard (frontend/)"]
        InMem --> Polling["3-Second Live Telemetry Poller"]
        Polling --> RadialMeter["Radial Occupancy Dial (0-100%)"]
        Polling --> SurgeBanner["🚨 Dynamic Surge Alert Banner"]
        Optimizer --> FreeWindow["🕒 Best Visiting Window Recommendation"]
        Forecast --> Timeline["📈 24h Hourly Forecast Curve"]
    end
```

---

## ⚡ Key Features

* **Real-Time Video Analytics**: Integrates Ultralytics YOLO with Region-of-Interest (ROI) Polygon counters for continuous headcount telemetry across sanctum, queue, and entry zones.
* **ML Predictive Forecasting**: Random Forest Regressor trained on cyclic time-of-day and day-of-week embeddings to generate 24-hour predictive demand curves.
* **Statistical Surge Anomaly Detection**: Real-time Z-score monitoring ($Z \ge 2.0$) that instantly flags dangerous crowd surges, bottlenecks, or gate blockages.
* **Dynamic Best Window Optimizer**: Analyzes historical patterns to recommend optimal visiting hours, flattening peak stampede risks.
* **Mission Control Telemetry Dashboard**: Built with React, Vite, and Tailwind CSS, featuring radial occupancy dials, active surge banners, and historical graphs.

---

## 🚀 Quick Start Guide

### Prerequisites
- **Python 3.10+**
- **Node.js 18+** & npm
- Git

---

### Step 1: Clone the Repository
```bash
git clone https://github.com/tomkarrao-commits/Yatrasetu.git
cd Yatrasetu
```

---

### Step 2: Launch the Backend ML Engine

```bash
cd backend
pip install -r requirements.txt
python main.py
```
> The FastAPI backend will start at **`http://localhost:8000`** (Swagger docs at `http://localhost:8000/docs`).

---

### Step 3: Launch the Frontend Dashboard

Open a separate terminal:
```bash
cd frontend
npm install
npm run dev
```
> Access the mission control dashboard at **`http://localhost:5173`** (or `http://localhost:3000`).

---

## 📁 Repository Structure

```text
Yatrasetu/
├── ai_pipeline/                     # YOLO video inference & ROI headcount pipeline
├── backend/                         # FastAPI backend & ML forecasting service
│   ├── app/
│   │   ├── routes/crowd.py          # Real-time telemetry & anomaly endpoints
│   │   └── services/ml_engine.py    # Random Forest model & Z-Score anomaly detector
│   ├── requirements.txt             # Python ML & web dependencies
│   └── main.py                      # FastAPI application entrypoint
├── frontend/                        # React + Vite + Tailwind CSS dashboard
│   ├── src/
│   │   ├── components/              # Radial gauges, timeline charts, alert banners
│   │   └── App.jsx                  # Main mission control layout
│   └── package.json
├── data/                            # Sample camera feeds, GeoJSON & historical logs
├── DEPLOYMENT_GUIDE.md              # Cross-platform installation & verification guide
└── README.md                        # Project documentation
```

---

## 📜 License
This project is open-source and licensed under the [MIT License](LICENSE).
