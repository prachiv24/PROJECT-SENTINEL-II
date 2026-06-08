Project Sentinel-II
Real-Time Intrusion Detection, Driver Fatigue Monitoring & Big Data Analytics Platform

Project Sentinel-II is an end-to-end intelligent safety and monitoring system that combines IoT sensors, computer vision, edge computing, cloud services, big data engineering, machine learning, and business intelligence to detect physical intrusions and monitor driver fatigue in real time.

The platform processes sensor and biometric data at the edge, streams telemetry to the cloud, performs large-scale analytics using a Databricks Medallion Architecture, and visualizes operational insights through Power BI dashboards.

Key Features

✅ Real-time intrusion detection using vibration, pressure, and sound sensors

✅ Face recognition–based identity verification

✅ Edge-to-cloud event streaming with FastAPI and Firebase

✅ Distributed data processing using Databricks & PySpark

✅ Driver fatigue detection and risk classification

✅ Machine Learning–based risk prediction using Random Forest

✅ Statistical analysis using R

✅ Interactive operational dashboards in Power BI

System Architecture
┌────────────────────────────────────────────┐
│              Edge Layer                    │
├────────────────────────────────────────────┤
│ • Vibration Sensor                         │
│ • Pressure Sensor                          │
│ • Sound Sensor                             │
│ • Camera Feed                              │
└───────────────┬────────────────────────────┘
                │
                ▼
┌────────────────────────────────────────────┐
│          FastAPI Edge Gateway              │
├────────────────────────────────────────────┤
│ • Event Processing                         │
│ • Face Recognition                         │
│ • Risk Scoring                             │
│ • Alert Management                         │
└───────────────┬────────────────────────────┘
                │
                ▼
┌────────────────────────────────────────────┐
│               Firebase                     │
├────────────────────────────────────────────┤
│ • Realtime Database                        │
│ • Cloud Storage                            │
└───────────────┬────────────────────────────┘
                │
                ▼
┌────────────────────────────────────────────┐
│      Databricks Medallion Architecture     │
├────────────────────────────────────────────┤
│ Bronze → Raw Data                          │
│ Silver → Feature Engineering               │
│ Gold   → ML & Analytics                    │
└───────────────┬────────────────────────────┘
                │
                ▼
┌────────────────────────────────────────────┐
│ Analytics & Visualization                  │
├────────────────────────────────────────────┤
│ • Power BI                                 │
│ • R Statistical Analysis                   │
└────────────────────────────────────────────┘
Technology Stack
Backend & Edge Computing
FastAPI
Python
OpenCV
face_recognition
Firebase Admin SDK
IoT & Sensors
Vibration Sensors
Pressure Sensors
Sound Sensors
Camera Module
Cloud & Data Engineering
Firebase Realtime Database
Firebase Cloud Storage
Databricks
Apache Spark
PySpark
Delta Lake
Machine Learning
Random Forest Classifier
Feature Engineering
Time-Series Analytics
Analytics & Visualization
Power BI
R
ggplot2
corrplot
DevOps
Docker
Docker Compose
Medallion Data Pipeline
Bronze Layer – Raw Data Ingestion
Streams sensor telemetry from Firebase
Stores raw events with schema validation
Maintains immutable historical records
Silver Layer – Data Transformation
Noise reduction and smoothing
Rolling window calculations
Risk volatility computation
Fatigue velocity analysis
Feature engineering for ML models
Gold Layer – Business Intelligence
Driver risk categorization
Operational risk metrics
Machine learning predictions
Dashboard-ready datasets
Intrusion Detection Engine

The intrusion detection module combines multiple sensor signals to minimize false positives.

Detection Inputs
Sound Level
Pressure Changes
Vibration Activity
Safety Mechanisms
Consecutive-hit validation
Sliding detection window
Alert cooldown period
Multi-sensor verification

This approach improves detection reliability under real-world environmental conditions.

Driver Fatigue Analytics

The fatigue monitoring pipeline analyzes behavioral and sensor-derived indicators to identify potentially dangerous driving patterns.

Key Metrics
Eye Closure Duration
Risk Score
Steering Variability
Vehicle Speed Trends
Fatigue Velocity
ML-Based Classification

A PySpark Random Forest model classifies drivers into:

Safe
Moderate Risk
High Risk
Critical Risk
Project Structure
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
File Descriptions
File	Purpose
main.py	FastAPI backend and event processing
risk.py	Intrusion detection and risk scoring logic
REAL-TIME databricks.ipynb	Databricks ETL and ML pipeline
r-code.txt	Statistical analysis scripts
visuals_bi.pbix	Power BI dashboard
docker-compose.yml	Container orchestration
Installation
Prerequisites
Python 3.10+
Docker
Docker Compose
Firebase Project
Databricks Workspace
Environment Variables

Create a .env file:

FIREBASE_STORAGE_BUCKET=your_bucket
FIREBASE_DATABASE_URL=your_database_url
Run with Docker
docker compose up --build -d

Application will be available at:

http://localhost:8000
Databricks Setup
Import REAL-TIME databricks.ipynb
Configure Firebase credentials
Attach a Spark cluster
Run all notebook cells
R Analytics Setup

Install required packages:

install.packages(
  c(
    "dplyr",
    "ggplot2",
    "tidyr",
    "corrplot"
  )
)

Execute the scripts inside:

r-code.txt
Dashboard Insights
Security Monitoring
Active intrusion alerts
Sensor event timeline
Threat severity tracking
Driver Safety
Driver fatigue trends
Risk classification distribution
Vehicle safety indicators
Fleet Operations
Fleet health overview
Risk hotspot identification
Historical incident analysis
Business Impact
Improves vehicle and asset security
Reduces false intrusion alerts
Enables proactive driver safety monitoring
Supports data-driven fleet management
Scales from single vehicles to enterprise fleets
Future Enhancements
Real-time notification system (SMS/Email)
GPS-based geofencing
Deep Learning fatigue models
Edge AI deployment on embedded devices
Predictive maintenance analytics
Authors

Prachi Verma
B.Tech (2027) | Software Engineering & Data Engineering Enthusiast
