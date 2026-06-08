# Project Sentinel-II: Real-Time Edge Intrusion, Driver Fatigue Detection & Big Data Analytics Pipeline

Project Sentinel-II is an end-to-end cyber-physical safety system that integrates real-time IoT edge monitoring, biometric face-recognition authentication, physical multi-sensor risk categorization, a distributed Databricks Medallion architecture, and business intelligence dashboards. 

The project aims to secure vehicles/spaces against unauthorized physical entry and analyze high-velocity streaming driver telemetry to predict, classify, and visualize driver drowsiness and risk factors in real time.

---

## System Architecture Overview

The system is structured across three cohesive computational layers:
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                     I. EDGE & INGESTION LAYER                                    │
│                                                                                                  │
│  ┌─────────────────────────┐         ┌─────────────────────────┐         ┌────────────────────┐  │
│  │    HARDWARE / IoT       │         │     EDGE CORE ENGINE    │         │  BIOMETRIC ENGINE  │  │
│  │  - Vibration Sensor     │  ───►   │  - FastAPI App Server   │  ───►   │  - Face Detection  │  │
│  │  - Pressure Transducer  │         │  - Throttling & Metrics │         │  - Identity Auth   │  │
│  │  - Sound ADC Streams    │         │  - Async Event Loop     │         │  - Target Matching │  │
│  └─────────────────────────┘         └─────────────────────────┘         └────────────────────┘  │
└──────────────────────────────────────────────────┬───────────────────────────────────────────────┘
                                                   │
                                                   ▼ [HTTPS Multi-Part Streams]
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                II. CLOUD HOT STATE PERSISTENCE                                   │
│                                                                                                  │
│       ┌──────────────────────────────────────────────────────────────────────────────────┐       │
│       │                         FIREBASE UNIFIED BACKPLANE                               │       │
│       │                  - Realtime Database (NoSQL Sensor Nodes)                        │       │
│       │           - Cloud Storage Buckets (Biometric Capture Payloads)                   │       │
│       └────────────────────────────────────────┬─────────────────────────────────────────┘       │
└──────────────────────────────────────────────────┼───────────────────────────────────────────────┘
                                                   │
                                                   ▼ [Spark Structured Streaming / REST Sync]
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│                             III. DISTRIBUTED DATA LAKEHOUSE LAYER                                │
│                                                                                                  │
│  ┌──────────────────────────────┐    ┌──────────────────────────────┐    ┌────────────────────┐  │
│  │    BRONZE LAYER (RAW)        │    │   SILVER LAYER (ENRICHED)    │    │ GOLD LAYER (CURED) │  │
│  │  - High-Velocity Ingestion   │    │ - Sliding Window Smoothing   │    │ - Random Forest ML │  │
│  │  - Schema Enforcement        │───►│ - Risk Volatility calculation│───►│ - Severity Buckets │  │
│  │  - Delta Table Landing Zone  │    │ - Fatigue Velocity (Δr/Δt)   │    │ - Dashboard Ready  │  │
│  └──────────────────────────────┘    └──────────────────────────────┘    └────────────────────┘  │
└──────────────────────────────────────────────────┬───────────────────────────────────────────────┘
                                                   │
                                                   ▼ [Direct Hive Metastore / Delta Connectors]
┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
│                              IV. ANALYTICS & EXECUTIVE REPORTING                                 │
│                                                                                                  │
│       ┌─────────────────────────────────────┐     ┌──────────────────────────────────────┐       │
│       │        R STATISTICAL SUITE          │     │          POWER BI DASHBOARD          │       │
│       │  - Multivariate Density Plots       │     │  - Live Fleet Telemetry Streams      │       │
│       │  - ANOVA Significance Verification  │     │  - Geographic Intrusion Map Feeds    │       │
│       │  - Correlation Matrices (corrplot)  │     │  - Operational Risk Severities       │       │
│       └─────────────────────────────────────┘     └──────────────────────────────────────┘       │
└──────────────────────────────────────────────────────────────────────────────────────────────────┘

1. **Edge-to-Cloud Backend:** A Dockerized **FastAPI** application acting as the system gateway. It ingests physical multi-sensor feeds (vibration, pressure, sound) alongside a video camera pipeline processing edge-based biometric verification via a custom-trained `face_recognition` workflow, streaming state-machine changes directly to **Firebase**.
2. **Distributed Data Lakehouse (Databricks / PySpark):** Processes high-velocity NoSQL telemetry from Firebase using a 3-tier **Medallion Architecture**:
   * **Bronze Layer:** Schema enforcement and raw event snapshot structural configurations.
   * **Silver Layer:** Advanced time-series calculations utilizing Spark Window functions for noise filtering, running moving averages (5-minute windows), calculating risk volatility ($\sigma$), and tracking fatigue velocity ($\Delta r / \Delta t$).
   * **Gold Layer:** Machine Learning pipelines implementing a distributed **Random Forest Classifier** to bucket driver states and identify high-risk fleet operational trends.
3. **Advanced Analytics & BI Visualizations:** * A programmatic statistical suite written in **R** to execute ANOVA testing, multi-window sensor telemetry streams, and correlation matrices.
   * A **Power BI Desktop (`.pbix`) Dashboard** translating raw spatial alerts into operational intelligence for fleet managers.

---

## File Structure Breakdown

* **`main.py`**: The core API backend engine built using **FastAPI**. Orchestrates multi-sensor state-machine updates, secure file handling, Firebase Firestore / Realtime Database synchronizations, and edge face-recognition scoring.
* **`risk.py`**: Implementation of the mathematical and algorithmic threshold metrics. Implements a rolling-cooldown state tracker evaluating physical anomalies (Sound, Weight/Pressure, and Vibration) to compute low/high/critical threat contexts.
* **`REAL-TIME databricks.ipynb`**: A production-grade Databricks/PySpark development notebook containing the data-lake engineering stages, statistical feature extractions, distributed window operations, and predictive modeling using Random Forest.
* **`r-code.txt`**: Complete script for descriptive statistics, multivariate correlation layouts, and time-series multi-window canvas rendering using `ggplot2` and `corrplot`.
* **`visuals_bi.pbix`**: The compiled Power BI document delivering rich visualizations of spatial alerts, fleet status checks, and sensor interdependencies.
* **`docker.compose.yml`**: Production container orchestration environment mapping persistent volumes, secure environment vectors, and automatic restart hooks for deployment.

---

## Detailed Component Deep-Dive

### 1. Edge Ingestion & Risk Scoring (`main.py` & `risk.py`)
The system ingest structure leverages real-world physics metrics mapped via a strict multi-hit window constraints calculation matrix:
* **Sound Threshold:** `500` (Raw ADC Values)
* **Pressure / Mass Threshold:** `500` (Grams force equivalence)
* **Vibration State:** Binary logic (`VIBRATION_ACTIVE = 1`)

To eliminate environmental jitter, an alert triggers **only** if a configurable minimum of consecutive hits (`REQUIRED_HITS = 3`) occurs within a narrow, moving time envelope (`TIME_WINDOW = 7.0 seconds`). A mandatory `COOLDOWN_SECONDS = 10.0` throttle blocks duplicate notifications from flooding the system during an ongoing intrusion incident.

### 2. The Databricks Medallion Spark Pipeline
* **Bronze (Raw Ingestion):** Pulls raw telemetry directly from Firebase JSON roots into structured data rows with typed column signatures.
* **Silver (Feature Engineering):** Eliminates momentary natural human eye-blinking noise by setting up a chronological Look-Back Window:
  $$\text{Window} = \text{Window.rangeBetween}(-300, 0)$$
  It tracks *Risk Volatility* (the standard deviation of the rolling metrics) and *Fatigue Velocity* (the rapid spike rate over small temporal delta windows).
* **Gold (ML Execution):** Fits training metrics into an optimized PySpark `RandomForestClassifier`. The model flags continuous fatigue patterns to notify centralized corporate logistics desks.

### 3. R Analytics (`r-code.txt`)
Provides standard deviations, variance summaries, and correlation matrices targeting:
$$\{\text{Eye Closure (s)}, \text{Steering Sway (\%)}, \text{Vehicle Speed (km/h)}, \text{Risk Score}\}$$
Generates diagnostic visualizations, showing the strict correlation between continuous micro-sleeps and high-amplitude steering overrides.

---

## 🚀 Deployment Instructions

### Prerequisites
Make sure your environment has **Docker**, **Python 3.10+**, and a active **Firebase Project Service Account Account Link**.

### 1. Local Configuration Setup
Create a `.env` file in the root directory containing the proper environmental endpoints:
```env
FIREBASE_STORAGE_BUCKET=car-intrusion-detection-f13de.firebasestorage.app
FIREBASE_DATABASE_URL=[https://car-intrusion-detection-f13de-default-rtdb.asia-southeast1.firebasedatabase.app/](https://car-intrusion-detection-f13de-default-rtdb.asia-southeast1.firebasedatabase.app/)
2. Initializing via Docker Compose
To construct the images, link network volumes, expose Port 8000, and launch the system container stack, run:

Bash
docker compose up --build -d
3. Running the Databricks Pipeline
Upload the REAL-TIME databricks.ipynb file into your Databricks Workspace.

Mount your target storage endpoints or paste your Firebase access credentials directly within Cell 2 configurations.

Attach the notebook to a running Spark cluster and click Run All.

4. Running the R Visualization Suite
Open your preferred R environment (e.g., RStudio), ensure you have installed your dependencies, and run:

R
install.packages(c("dplyr", "ggplot2", "tidyr", "corrplot"))
# Source or execute the content of r-code.txt
## Dashboard Insights
Open visuals_bi.pbix inside Power BI Desktop to view:

Active Intrusions: Real-time spatial tracking indicators triggered by critical edge alarms.

Driver Risk Profiler: Aggregated time charts tracking steering stability against eye closure metrics.

Fleet Integrity: A unified operational status summary indicating which vehicles are safe, in warning states, or in need of an immediate emergency dispatch check.


***

### 💡 What changed/improved here?
1. **Accurate Mapping:** It explicitly references your specific Firebase project variables (like `car-intrusion-detection-f13de`), specific code boundaries (`REQUIRED_HITS = 3`), and names every file you have actually tracked in your commit.
2. **Academic & Professional Tone:** It frames your code cleanly as a **cyber-physical safety system using the Medallion Architecture**, making it look exceptional for project vivas, evaluations, or GitHub profiles. 
3. **Structured Setup Guide:** Gives concrete steps on how to execute everything together (Docker $\rightarrow$
