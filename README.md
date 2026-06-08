#  Project Sentinel-II

## Real-Time Intrusion Detection, Driver Fatigue Monitoring & Big Data Analytics Platform

Project Sentinel-II is an end-to-end intelligent safety system that combines **IoT sensors**, **Computer Vision**, **Cloud Computing**, **Big Data Engineering**, **Machine Learning**, and **Business Intelligence** to detect unauthorized physical intrusions and monitor driver fatigue in real time.

The platform processes sensor and biometric data at the edge, streams telemetry to the cloud, performs large-scale analytics using a **Databricks Medallion Architecture**, and visualizes operational insights through **Power BI dashboards**.

---
#  Key Features

### Smart Intrusion Detection
- Real-time monitoring using vibration, pressure, and sound sensors
- Multi-sensor validation to reduce false positives
- Automated threat categorization and alert generation

### Face Recognition Authentication
- Edge-based biometric verification
- Authorized user identification
- Secure access validation

### Real-Time Data Processing
- FastAPI-powered event ingestion
- Firebase cloud synchronization
- High-throughput telemetry streaming

### Machine Learning Risk Analysis
- Driver fatigue prediction
- Random Forest–based risk classification
- Continuous behavioral monitoring

### Advanced Analytics & Visualization
- Databricks Medallion Architecture
- Statistical analysis using R
- Interactive Power BI dashboards

---

#  System Architecture

```text
Edge Devices
      │
      ▼
FastAPI Gateway
      │
      ▼
Firebase Cloud
      │
      ▼
Databricks Lakehouse
      │
      ▼
ML Analytics & Power BI
```

# Technology Stack
###Backend & APIs
###FastAPI
-Python
-Firebase Admin SDK
-Computer Vision
-OpenCV
-face_recognition
-Data Engineering
-Databricks
-Apache Spark
-PySpark
-Delta Lake
-Machine Learning
-Random Forest Classifier
-Feature Engineering
-Time-Series Analytics
-Analytics & BI
-Power BI
-R
-ggplot2
-corrplot
-DevOps
-Docker
-Docker Compose

##Core Modules
###Edge Monitoring & Intrusion Detection

The intrusion detection engine continuously evaluates:

-Sound Activity
-Pressure Changes
-Vibration Events

To improve reliability, alerts are generated only after multiple consecutive detections within a configurable time window.

Key Capabilities

- Multi-sensor fusion

-Consecutive-hit validation

- Alert throttling

-False-positive reduction
## Driver Fatigue Detection

###The fatigue analytics pipeline monitors behavioral indicators and identifies potentially dangerous driving patterns.

Tracked Metrics
-Eye Closure Duration
-Risk Score
-Steering Variability
-Vehicle Speed
-Fatigue Velocity
-Risk Categories
🟢 Safe
🟡 Moderate Risk
🟠 High Risk
🔴 Critical Risk
## Databricks Medallion Architecture
### Bronze Layer

Raw telemetry ingestion and schema validation.

### Silver Layer

Feature engineering, rolling windows, smoothing, and risk calculations.

### Gold Layer

Machine learning predictions and dashboard-ready datasets

## PROJECT STRUCTURE

Project-Sentinel-II/
│
├── main.py
├── risk.py
├── REAL-TIME databricks.ipynb
├── r-code.txt
├── visuals_bi.pbix
├── docker-compose.yml
├── .env
└── README.md

## Getting Started
### Prerequisites
Python 3.10+
Docker
Docker Compose
Firebase Project
Databricks Workspace
###Configure Environment Variables
FIREBASE_STORAGE_BUCKET=your_bucket
FIREBASE_DATABASE_URL=your_database_url
###Start the Application
docker compose up --build -d

Application URL:

http://localhost:8000

##Dashboard Insights
###Security Monitoring
-Active intrusion alerts
-Threat severity tracking
-Event timeline analysis
###Driver Safety Monitoring
-Fatigue trends
-Risk classification
-Safety score tracking
###Fleet Intelligence
-Fleet health overview
-Historical incident analysis
-Operational risk monitoring
##Business Impact
-Enhanced physical security
-Reduced false alarms
-Proactive driver safety monitoring
-Scalable fleet intelligence platform
-Data-driven operational decision making
##Future Enhancements
-Real-time SMS & Email alerts
-GPS geofencing integration
-Deep Learning fatigue models
-Edge AI deployment
-Predictive maintenance analytics

