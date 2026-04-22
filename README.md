# Anomaly Detection System
### Real-Time User Login Anomaly Detection using XGBoost & FastAPI

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python)
![XGBoost](https://img.shields.io/badge/XGBoost-ML-orange?logo=python)
![FastAPI](https://img.shields.io/badge/FastAPI-API-009688?logo=fastapi)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter)

---

## Overview

Built a machine learning-powered anomaly detection system that identifies 
suspicious user login behavior in real time. The system trains an XGBoost 
model on labeled login event data, scores incoming events on a 1–10 risk 
scale, and exposes predictions via a FastAPI REST endpoint — enabling 
security teams to flag and respond to unauthorized access attempts 
programmatically.

---

## Problem Statement

Enterprise security teams struggle to identify compromised accounts and 
unauthorized access attempts from high-volume login event streams. Manual 
review is not scalable. This system automates anomaly scoring by learning 
patterns from historical login behavior and flagging deviations in real time.

---

## Architecture
Raw Login Data (CSV)
↓
Feature Engineering & Preprocessing  (Jupyter Notebook)
↓
XGBoost Model Training & Validation
↓
Serialized Model (.pkl)
↓
FastAPI REST Endpoint  (/predict)
↓
Anomaly Score (1–10) → Flag if score ≥ 3

---

## Key Features

**ML-Based Scoring** — XGBoost model trained on labeled login events, 
producing a continuous risk score (1–10) rather than a binary flag, 
giving security teams fine-grained control over alert thresholds.

**REST API Deployment** — FastAPI server exposes a `/predict` endpoint 
accepting JSON payloads, making the model consumable by any upstream 
system or dashboard.

**Feature Engineering** — engineered features include login ratios, 
device diversity, geographic spread, browser patterns, and time 
difference signals to maximize detection accuracy.

**Threshold-Based Alerting** — records scoring ≥ 3 are classified as 
anomalous, configurable based on organizational risk tolerance.

---

## Anomaly Score Logic

| Score Range | Classification |
|---|---|
| 1 – 2 | Normal behavior |
| 3 – 5 | Suspicious — review recommended |
| 6 – 10 | High risk — anomalous, flag immediately |

---

## How to Run

### Prerequisites
- Python 3.8+
- `xgboost`, `fastapi`, `uvicorn`, `scikit-learn`, `pandas`, `pickle`

### Setup

```bash
# Clone the repo
git clone https://github.com/kushalidarak/anomaly-detection.git
cd anomaly-detection

# Create virtual environment
python3 -m venv env
source env/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Train the Model

```bash
# Open and run the notebook
jupyter notebook anomaly_detection_stgi.ipynb

# Preprocessed data and trained model saved automatically
# Output: preprocessed_data.csv, regressor_model.pkl
```

### Run the API Server

```bash
uvicorn fast_api:app --reload
# Visit http://localhost:8000/docs for interactive API documentation
```

### Sample API Request

```json
POST /predict
{
  "Country": 1,
  "Device_Type": 2,
  "Login_Successful": 1,
  "LoginRatio": 0.85,
  "Final_Browser_Category": 3,
  "Total_Device_Types": 2,
  "Total_IP_Addresses": 5,
  "Total_Countries": 1,
  "Total_Browser_Categories": 2,
  "Time_Difference_in_sec": 300
}

Response: { "anomaly_score": 7 }  → Anomalous
```

---

## Tech Stack

`Python` · `XGBoost` · `FastAPI` · `Scikit-learn` · 
`Pandas` · `Jupyter Notebook` · `REST API` · `Pickle`

---

## Author

**Kushali Darak** — AI Data Engineer  
4+ years building scalable batch and real-time data pipelines 
across manufacturing and financial services environments.

[LinkedIn](https://www.linkedin.com/in/kushalidarak) · 
[Portfolio](https://Kushalidarak.github.io)
