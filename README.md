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


## Technology Stack

| Category | Technologies |
|----------|-------------|
| Backend & APIs | FastAPI, Python, Firebase Admin SDK |
| Computer Vision | OpenCV, face_recognition |
| Data Engineering | Databricks, Apache Spark, PySpark, Delta Lake |
| Machine Learning | Random Forest Classifier, Feature Engineering, Time-Series Analytics |
| Analytics & BI | Power BI, R, ggplot2, corrplot |
| DevOps & Deployment | Docker, Docker Compose |

## Core Modules

### Edge Monitoring & Intrusion Detection

A real-time security monitoring module that combines vibration, pressure, and sound sensor data to detect potential intrusion events with high reliability and low false-positive rates.

#### Detection Inputs
- Sound Activity Monitoring
- Pressure-Based Anomaly Detection
- Vibration Event Tracking

#### Key Features
- Multi-Sensor Correlation Engine
- Consecutive-Hit Verification Logic
- Configurable Detection Windows
- Alert Cooldown Mechanism
- Real-Time Risk Scoring
- False Positive Mitigation
##  Driver Fatigue Detection

The driver fatigue analytics module continuously monitors behavioral and vehicle telemetry data to identify early signs of drowsiness, reduced alertness, and potentially unsafe driving conditions.

#### Monitored Metrics
- Eye Closure Duration
- Driver Risk Score
- Steering Variability
- Vehicle Speed Trends
- Fatigue Velocity

#### Risk Classification

| Level | Status |
|---------|---------|
| 🟢 | Safe |
| 🟡 | Moderate Risk |
| 🟠 | High Risk |
| 🔴 | Critical Risk |

#### Key Capabilities
- Real-Time Fatigue Monitoring
- Behavioral Pattern Analysis
- Risk Score Calculation
- Early Warning Detection
- Driver Safety Assessment
- Machine Learning–Based Risk Classification

The module leverages engineered features and predictive analytics to classify driver states, enabling proactive intervention before fatigue-related incidents occur.
##  Databricks Medallion Architecture

The data engineering pipeline follows the Medallion Architecture pattern to transform raw telemetry into high-quality, analytics-ready datasets for machine learning and business intelligence.

### Bronze Layer — Raw Data Ingestion
- Real-time telemetry ingestion from Firebase
- Schema validation and standardization
- Immutable storage of raw sensor events
- Foundation for downstream processing

### Silver Layer — Data Transformation & Feature Engineering
- Data cleansing and noise reduction
- Rolling window aggregations and smoothing
- Risk volatility calculations
- Fatigue velocity tracking
- Feature engineering for predictive analytics

### Gold Layer — Analytics & Machine Learning
- Driver risk classification using Random Forest
- Operational risk assessment
- Dashboard-ready business metrics
- Curated datasets for reporting and visualization

#### Key Benefits
- Scalable Real-Time Data Processing
- Reliable Data Quality Management
- Advanced Feature Engineering
- Machine Learning–Ready Datasets
- Business Intelligence Optimization

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

## 🚀 Getting Started

Follow the steps below to set up and run Project Sentinel-II locally.

### Prerequisites

Ensure the following dependencies are installed on your system:

* Python 3.10 or later
* Docker
* Docker Compose
* Firebase Project with Service Account Credentials
* Databricks Workspace (for analytics pipeline execution)

### Configure Environment Variables

Create a `.env` file in the project root directory and add the following configuration:

```env
FIREBASE_STORAGE_BUCKET=your_bucket_name
FIREBASE_DATABASE_URL=your_database_url
```

### Launch the Application

Build and start all services using Docker Compose:

```bash
docker compose up --build -d
```

### Access the Application

Once the containers are running, the FastAPI service will be available at:

```text
http://localhost:8000
```

### Verify Deployment

* Confirm Docker containers are running successfully.
* Verify Firebase connectivity and data synchronization.
* Access the FastAPI endpoint to ensure the API is operational.
* Monitor incoming sensor telemetry and event streams.
## 📊 Dashboard Insights

The Power BI dashboard transforms raw telemetry and security events into actionable operational intelligence for fleet managers and security teams.

### 🔐 Security Monitoring

* Real-Time Intrusion Alerts
* Threat Severity Analysis
* Event Timeline Visualization
* Sensor Activity Monitoring
* Incident Tracking & Investigation

### 😴 Driver Safety Monitoring

* Driver Fatigue Trend Analysis
* Risk Classification Dashboard
* Safety Score Tracking
* Behavioral Pattern Monitoring
* High-Risk Driver Identification

### Fleet Intelligence

* Fleet Health Overview
* Historical Incident Analysis
* Operational Risk Monitoring
* Vehicle Performance Insights
* Fleet-Wide Safety Analytics

---

## Business Impact

Project Sentinel-II delivers measurable operational and safety benefits by combining real-time monitoring, predictive analytics, and intelligent decision support.

* Enhanced Physical Security Through Automated Intrusion Detection
* Reduced False Positives Using Multi-Sensor Validation
* Proactive Driver Safety Monitoring and Early Risk Detection
* Scalable Fleet Intelligence and Operational Visibility
* Data-Driven Decision Making Through Advanced Analytics
* Improved Incident Response and Risk Management
* Centralized Monitoring Across Vehicles and Assets

---

## Future Enhancements

The platform is designed for extensibility and future innovation.

* Real-Time SMS, Email, and Push Notifications
* GPS-Based Geofencing and Location Tracking
* Deep Learning Models for Advanced Fatigue Detection
* Edge AI Deployment on Embedded Devices
* Predictive Maintenance and Vehicle Health Analytics
* Real-Time Streaming Dashboards with Live Alerts
* Mobile Application for Fleet Monitoring
* Cloud-Native Scalable Microservices Architecture
