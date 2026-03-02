# Distributed IoT Network Intrusion Detection Using Apache PySpark MLlib
## Module: Machine Learning and Big Data (7006SCN) | Coventry University

---

## Project Overview
This project applies distributed machine learning to the **NF-ToN-IoT-v2** dataset (1.98 GB, 13,552,396 records) to classify IoT network traffic into 10 categories using **Apache PySpark MLlib**. Four algorithms were implemented: Logistic Regression, Decision Tree, Random Forest, and Gradient Boosted Trees (GBT). GBT achieved the best binary accuracy of **98.10% (F1=0.9809)**.

---

## Repository Structure
```
Bhargav /
├── notebooks/
│   ├── 1_Data_Ingestion.ipynb          # CSV ingestion, Parquet conversion, EDA
│   ├── 2_feature_engineering.ipynb     # Preprocessing, feature engineering, scaling
│   ├── 3_model_training.ipynb          # LR, DT, RF, GBT training + CrossValidator
│   └── 4_evaluation.ipynb              # Metrics, confusion matrices, ROC, bootstrap CI
├── models/
│   ├── lr_model/                        # Saved Logistic Regression MLlib model
│   ├── dt_cv_model/                     # Saved Decision Tree (CrossValidator tuned)
│   ├── rf_model/                        # Saved Random Forest MLlib model
│   └── gbt_model/                       # Saved GBT MLlib model
├── parquet/
│   ├── ton_iot_data/                    # Raw ingested Parquet files
│   ├── ton_iot_processed/               # Preprocessed + feature engineered data
│   └── ton_iot_final/                   # Final 24-feature dataset for training
├── tableau_data/
│   ├── bootstrap_ci.csv                 # Bootstrap confidence interval results
│   ├── class_distribution.csv           # Class distribution data
│   ├── feature_importance.csv           # Feature importance scores
│   ├── label_distribution.csv           # Label distribution data
│   ├── model_results.csv                # All model performance metrics
│   ├── per_class_metrics.csv            # Per-class F1, precision, recall
│   └── scalability.csv                  # Strong scaling experiment results
├── Bhargav.twb                          # Tableau workbook (4 dashboards)
├── Bhargav.docx 
├── NF-ToN-IoT-v2-train.csv             # Raw dataset (1.98 GB)
├── environment.yml                      # Conda environment specification
└── README.md                            # This file
```

---

## Dataset
- **Name:** NF-ToN-IoT-v2
- **Source:** UNSW Canberra Cyber Repository (Sarhan et al., 2021)
- **Size:** 1.98 GB | 13,552,396 records | 45 features
- **Download:** https://research.unsw.edu.au/projects/toniot-datasets
- **License:** Free for academic use

---

## Environment Setup

### Option 1: Conda (Recommended)
```bash
conda env create -f environment.yml
conda activate pyspark-iot
```

### Option 2: Google Colab
All notebooks were developed and tested on **Google Colab** with the following runtime:
- Runtime type: Python 3
- Hardware: CPU (standard), 4GB RAM driver
- Install PySpark manually in each notebook:
```python
!pip install pyspark==3.4.0
```

---

## How to Run

Run notebooks **in order**:

1. **`1_Data_Ingestion.ipynb`** — Load CSV, convert to Parquet, EDA, class distribution
2. **`2_feature_engineering.ipynb`** — Clean data, engineer features, scale, select top 24 features
3. **`3_model_training.ipynb`** — Train all 4 models, CrossValidator for DT, save models
4. **`4_evaluation.ipynb`** — Evaluate models, generate all metrics, plots, bootstrap CI

> ⚠️ Place `NF-ToN-IoT-v2-train.csv` in the root folder or update the file path in `1_Data_Ingestion.ipynb` before running.

---

## Results Summary

| Model | Accuracy | F1 | Precision | Recall | Train Time |
|-------|----------|----|-----------|--------|------------|
| Logistic Regression | 0.6646 | 0.6420 | 0.6777 | 0.6646 | 98.69s |
| Decision Tree (tuned) | 0.9692 | 0.9690 | 0.9695 | 0.9692 | 81.87s |
| Random Forest | 0.9558 | 0.9551 | 0.9558 | 0.9558 | 885.95s |
| **GBT (Binary)** | **0.9810** | **0.9809** | **0.9811** | **0.9810** | 600.87s |

---

## Tableau Dashboards
- **Dashboard 1:** Data quality — attack distribution & class imbalance
- **Dashboard 2:** Model performance — accuracy comparison & training time
- **Dashboard 3:** Feature importance & per-class F1 heatmap
- **Dashboard 4:** Scalability analysis & bootstrap confidence intervals

> Tableau Public link is provided in the submitted report.

---

## Key Findings
- GBT achieves best binary accuracy (98.10%) via sequential boosting
- Parquet partitioning improved load time **4.3x** over CSV
- Strong scaling: **1.8x speedup** from 5 to 30 Spark partitions
- Class imbalance (ransomware = 0.02%) is the primary performance bottleneck for minority classes

---

## References
- Sarhan, M., Layeghy, S., Moustafa, N., & Portmann, M. (2021). NetFlow Datasets for Machine Learning-Based Network Intrusion Detection Systems. *Lecture Notes of the Institute for Computer Sciences, Social Informatics and Telecommunications Engineering*, 373, 117–135.
- Wasswa, H., Abbass, H. A., & Lynar, T. (2025). ResDNViT. *Expert Systems with Applications*, 282, 127504.

---
