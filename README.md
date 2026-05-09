# 🌊 Flood & Flash Flood Prediction in Malaysia
### A Multi-City Machine Learning Comparative Analysis

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

This project builds a machine learning framework to predict **flood** and **flash flood** events across **8 major Malaysian cities** using 16 years of daily satellite weather data. Three models — Decision Tree, Random Forest, and XGBoost — are trained and compared against two rainfall intensity thresholds.

---

## 📍 Cities Covered

| City | State | Region |
|------|-------|--------|
| Kota Bharu | Kelantan | East Coast |
| Kuantan | Pahang | East Coast |
| Johor Bahru | Johor | South |
| Kuala Lumpur | W.P. Kuala Lumpur | Central |
| Shah Alam | Selangor | Central |
| Melaka | Melaka | South |
| Kuching | Sarawak | East Malaysia |
| Kota Kinabalu | Sabah | East Malaysia |

---

## 📦 Dataset

- **Source:** NASA POWER (MERRA-2 Satellite Reanalysis)
- **Period:** 1 January 2010 – 31 March 2026
- **Records:** 47,367 daily records across all 8 cities
- **Variables:** Temperature, Humidity, Wind Speed, Rainfall (used for labels only)

### Labels
| Label | Threshold | Positive Cases | Rate |
|-------|-----------|---------------|------|
| `Flood` | Rainfall ≥ 50mm/day | 676 days | 1.43% |
| `Flash_Flood` | Rainfall ≥ 80mm/day | 226 days | 0.48% |

> ⚠️ `Rainfall_mm` was removed from features to prevent data leakage. All rolling features use past data only, simulating a real early warning system.

---

## ⚙️ Features Used

| Feature | Description |
|---------|-------------|
| `Rainfall_3day` | 3-day rolling average rainfall |
| `Rainfall_7day` | 7-day rolling average rainfall |
| `Rainfall_14day` | 14-day rolling average rainfall |
| `Rainfall_cumsum7` | 7-day cumulative rainfall sum |
| `Month` | Calendar month (1–12) |
| `Is_Monsoon` | 1 if Nov/Dec/Jan, else 0 |
| `Temperature_C` | Air temperature at 2m |
| `Humidity_pct` | Relative humidity at 2m |
| `Wind_Speed_ms` | Wind speed at 2m |

---

## 🤖 Models & Results

### Task 1 — Flood Prediction (≥ 50mm/day)

| Model | Accuracy | Precision | Recall | F1 | AUC-ROC |
|-------|---------|-----------|--------|-----|---------|
| Decision Tree | 0.9723 | 0.1150 | 0.8049 | 0.2012 | 0.8925 |
| Random Forest | 0.9954 | 0.3333 | 0.0732 | 0.1200 | 0.9479 |
| **XGBoost** ⭐ | **0.9930** | **0.2642** | **0.3415** | **0.2979** | **0.9824** |

### Task 2 — Flash Flood Prediction (≥ 80mm/day)

| Model | Accuracy | Precision | Recall | F1 | AUC-ROC |
|-------|---------|-----------|--------|-----|---------|
| Decision Tree | 0.9979 | 0.0588 | 0.2000 | 0.0909 | 0.5993 |
| Random Forest ⭐ | 0.9995 | **0.5000** | 0.2000 | **0.2857** | 0.7968 |
| **XGBoost** ⭐ | 0.9992 | 0.2000 | 0.2000 | 0.2000 | **0.9651** |

> **XGBoost** is the best overall model for flood prediction (highest F1 + AUC-ROC).
> For flash flood, **XGBoost** leads on AUC-ROC while **Random Forest** leads on Precision and F1.

---

## 🔑 Key Findings

- **Johor Bahru** has the highest flood risk at 2.85% — nearly 8× higher than Melaka (0.37%)
- Flood risk is **~20× higher** during the Northeast Monsoon (Nov/Dec/Jan)
- **Rainfall_3day** is the strongest predictor across all models
- High AUC-ROC values (0.88–0.98) confirm models learned genuine flood patterns despite class imbalance

---

## 🚀 How to Run

### Option 1 — Google Colab (Recommended)
1. Upload `malaysia_flood_master.csv` to your Colab session
2. Open `flood_prediction_malaysia_v2.ipynb` in Google Colab
3. Run all cells

### Option 2 — Local
```bash
# Clone the repo
git clone https://github.com/3bdullah-waleed/flood-flash-flood-prediction-malaysia.git
cd flood-flash-flood-prediction-malaysia

# Install dependencies
pip install pandas numpy scikit-learn xgboost matplotlib seaborn scipy

# Launch Jupyter
jupyter notebook flood_prediction_malaysia_v2.ipynb
```

---

## 📁 Repository Structure
