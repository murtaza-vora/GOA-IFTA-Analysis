# GOA-IFTA-Analysis


# IFTA Audit ML System 🚛⛽

### Evidence Normalization, Analytics & Machine Learning for IFTA Compliance Auditing

An end-to-end Machine Learning pipeline built on AWS to automate anomaly detection and audit prioritization for International Fuel Tax Agreement (IFTA) compliance.

This project extracts and normalizes fuel invoices and distance logs, engineers audit-focused compliance features, and applies multiple anomaly detection techniques to identify suspicious fuel-tax reporting behavior.

---

## 📌 Problem Statement

The **International Fuel Tax Agreement (IFTA)** requires carriers operating across provinces/states to report fuel purchases and travel distances accurately.

Manual auditing is:

* Time-consuming
* Difficult to scale
* Prone to inconsistencies

This project aims to:

✅ Detect suspicious fuel-distance behavior
✅ Prioritize audit risk automatically
✅ Provide explainable ML outputs for auditors
✅ Build a scalable AWS-native audit pipeline

---

# 🏗️ Project Architecture

```text
Raw Files (S3)
      ↓
AWS Textract OCR
      ↓
Data Cleaning & Normalization
      ↓
AWS Location Service
      ↓
Feature Engineering
      ↓
Anomaly Detection Models
      ↓
Risk Scoring & Audit Prioritization
      ↓
AWS Glue + Athena Query Layer
```

---

# ☁️ AWS Services Used

| Service              | Purpose                           |
| -------------------- | --------------------------------- |
| Amazon S3            | Central data storage              |
| Amazon Textract      | OCR extraction from invoices/PDFs |
| AWS Location Service | City & province normalization     |
| Amazon SageMaker     | ML experimentation & notebooks    |
| AWS Glue             | Schema cataloging                 |
| Amazon Athena        | SQL analytics on ML outputs       |
| MLflow               | Experiment tracking               |

---

# 📂 Project Structure

```bash
.
├── 01_Data_Extraction_FINAL.ipynb
├── 02_Data_Curation_FINAL.ipynb
├── 03_Feature_Engineering_FINAL.ipynb
├── 04_ML_Anomaly_Detection_FINAL.ipynb
├── IFTA_Audit_ML_Presentation_v5.pptx
└── README.md
```

---

# 📊 Dataset Overview

## Data Sources

| File Type             | Description                   |
| --------------------- | ----------------------------- |
| Fuel Invoices         | OCR extraction using Textract |
| Distance Logs (PDF)   | Table extraction              |
| Distance Logs (Excel) | Structured trip records       |
| Assessment Handout    | Business requirements         |

### Key Challenges

* Mixed date formats
* Missing values
* OCR inconsistencies
* City name normalization
* Missing VIN/truck identifiers
* Compound location strings

---

# 🔍 Feature Engineering

The system engineers audit-focused compliance features directly tied to IFTA fraud patterns.

| Feature                         | Purpose                           |
| ------------------------------- | --------------------------------- |
| Fuel Litres per KM              | Detect impossible fuel efficiency |
| Fuel Cost per KM                | Detect invoice inflation          |
| Trips Without Fuel Purchases    | Identify unreconciled distance    |
| Jurisdiction Distance vs Fuel % | Detect tax arbitrage behavior     |
| Temporal Trends                 | Detect fabricated trip spikes     |

---

# 🤖 Machine Learning Approaches

## 1️⃣ Statistical Outlier Detection (Z-Score)

* Transparent and auditor-friendly
* Flags records where:

```math
|Z| > 2.5
```

---

## 2️⃣ Rule-Based Detection

Hard-coded IFTA compliance checks:

* Missing fuel receipts
* Implausible fuel efficiency
* Jurisdiction imbalance
* Temporal anomalies

---

## 3️⃣ Isolation Forest

Unsupervised anomaly detection using:

* `contamination = 0.05`
* SHAP explainability
* Robust to correlated features

---

## 4️⃣ K-Means Clustering

Risk segmentation into:

* High Risk
* Medium Risk
* Low Risk

---

# 📈 Key Results

| Metric                   | Result               |
| ------------------------ | -------------------- |
| Total Records            | 40                   |
| Critical Records Flagged | 2                    |
| ML Models Applied        | 4                    |
| AWS Services Used        | 7                    |
| OCR Extraction Accuracy  | 95.5% Avg Confidence |

### Risk Findings

* Manitoba showed highest average audit risk
* Isolation Forest consistently flagged the same high-risk records across 20 runs
* Rule-based methods produced higher false positives

---

# 🧠 Explainability

This project emphasizes **audit defensibility**.

## Explainability Techniques

* SHAP values
* Plain-English audit explanations
* Transparent statistical thresholds
* Full evidence retention

Example:

> “Red Deer → Edmonton flagged due to abnormal litres_per_km compared to peer trips.”

---

# 📉 Limitations

* Small dataset (~40 rows)
* No VIN/truck-level identifiers
* Limited labeled fraud cases
* OCR confidence variability
* Date matching tolerance may inflate anomalies

---

# 🚀 Future Improvements

## Phase 1 (Current)

* Unsupervised anomaly detection
* Rule-based audit logic

## Phase 2

* Semi-supervised learning
* XGBoost with labeled audit outcomes

## Phase 3

* Real-time fraud scoring endpoint
* GPS + VIN integration
* Fully supervised ML pipeline

---

# 🛠️ Installation

## Clone Repository

```bash
git clone https://github.com/murtaza-vora/GOA-IFTA-Analysis.git
cd GOA-IFTA-Analysis
```

---

# 📦 Required Libraries

```bash
pip install pandas numpy scikit-learn matplotlib seaborn shap boto3 mlflow awswrangler
```

---

# ▶️ Running the Pipeline

Execute notebooks in sequence:

```bash
01_Data_Extraction_FINAL.ipynb
        ↓
02_Data_Curation_FINAL.ipynb
        ↓
03_Feature_Engineering_FINAL.ipynb
        ↓
04_ML_Anomaly_Detection_FINAL.ipynb
```

---

# 📊 Example Athena Query

```sql
SELECT audit_priority,
       COUNT(*) as total,
       ROUND(AVG(combined_risk_score),2) as avg_risk
FROM goa_audit_db.audit_results
GROUP BY audit_priority
ORDER BY avg_risk DESC;
```

---

# 🎯 Business Impact

✅ Faster audit investigations
✅ Reduced manual review effort
✅ Scalable fraud detection
✅ Explainable ML for government compliance
✅ Serverless AWS-native architecture

---

# 📸 Presentation

The complete project walkthrough and architecture explanation can be found in:

```bash
IFTA_Audit_ML_Presentation_v5.pptx
```

---

# 👨‍💻 Author

**Murtaza Vora**
Data Analyst | Data Scientist | AWS & Azure Enthusiast

* Microsoft Certified: Azure Data Scientist Associate
* Master's in Analytics
* Focus Areas:

  * Machine Learning
  * Fraud Detection
  * Cloud Analytics
  * Explainable AI

---

