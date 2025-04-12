# ☕ Starbucks Promotion Effectiveness Analysis & Prediction

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)
[![ML](https://img.shields.io/badge/ML-ScikitLearn-red)](https://scikit-learn.org/)

This Jupyter Notebook analyzes Starbucks promotional campaigns using mobile app data, and builds predictive models to identify high-conversion customer segments. The analysis integrates transaction logs, demographic data, and offer metadata to optimize promotional ROI.

---

## 📋 Project Overview
&zwnj;**Objective**&zwnj;:  
Identify customer segments with highest promotion conversion rates (BOGO/Discount/Info) and build predictive models with >80% precision.

&zwnj;**Datasets**&zwnj;:
- `portfolio.json`: Offer details (type/duration/channels)
- `profile.json`: 17k customer demographics (age/gender/income)
- `transcript.json`: 306k event records (offer received/viewed/completed)

---

## 🔍 Key Analysis Steps

### 1. Advanced Data Cleaning
- 🧹 Unified column names (`id`→`offer_id`, `person`→`user_id`)
- ⚠️ Cleaned anomalies: 
  - Removed customers with missing gender/income 
  - Filtered implausible ages (e.g. 118 years old)
- 🕒 Standardized time units (hours → days)
- 🧩 Extracted nested JSON data from transaction logs

- ✅ &zwnj;**User-Offer Alignment**&zwnj;:  
  Used forward-filling on transaction timestamps to assign the closest offer ID to user transactions  
- 🧩 &zwnj;**User Behavior Classification**&zwnj;:
  | Group | Behavior Pattern | Impact Level |
  |-------|-------------------|--------------|
  | 1️⃣    | Received → Viewed → Transacted → Completed | Valid Conversion |
  | 2️⃣    | Received → Viewed | Invalid Promotion |
  | 3️⃣    | Transacted Without Offer Exposure | Natural Behavior |
  | 4️⃣    | Received Only | No Engagement |

### 2. User Segmentation
| Group | Description | Size |
|-------|-------------|------|
| 1️⃣    | Viewed & Redeemed | 62,824 | 
| 2️⃣    | Viewed & Not Redeemed | 32,107 |
| 3️⃣    | Transactions Without Offers | 138,953 |
| 4️⃣    | Received & Ignored | 72,116 |

### 3. Predictive Modeling
&zwnj;**Model Selection**&zwnj;:
- KNN / Decision Tree / Random Forest
- &zwnj;**Optimization**&zwnj;: GridSearchCV for hyperparameter tuning

&zwnj;**Performance (Precision)**&zwnj;:
| Offer Type | Best Model | Precision | Key Features |
|-----------|------------|-----------|--------------|
| BOGO      | Decision Tree | 83.6%    | Membership Tenure, Income |
| Discount  | Random Forest | 89.0%    | Age, Transaction Frequency |
| Info      | Random Forest | 85.0%    | Gender, Offer View Rate |

---

## 🚀 Key Findings
### 🧑🤝🧑 User Demographics
- &zwnj;**Age Distribution**&zwnj;:  
  - 45-70yr: 62% of influenced users  
  - Males dominate under 60 (55% vs female 45%)
- &zwnj;**Income Patterns**&zwnj;:  
  | Gender | Top Income Brackets |
  |--------|----------------------|
  | Male   | $50-75K (41%), $30-50K (33%) |
  | Female | $50-90K (68%) |
  
### ⏱️ Behavioral Insights
- &zwnj;**Response Speed**&zwnj;:  
  Females react 2.3x faster to discounts (median 6.2hrs vs male 14.5hrs)  
- &zwnj;**Offer Completion**&zwnj;:  
  82% occur within 2-3 days after viewing  
- &zwnj;**Membership**&zwnj;:  
  Peak influence period at 2.5 years membership  

### 🏆 Active User Profile
- &zwnj;**Definition**&zwnj;: View Rate ≥75% & Complete Rate ≥50%  
- &zwnj;**Characteristics**&zwnj;:  
  - 45-65yr: 72%  
  - $50-100K income bracket: 68%  
  - 2-4 years membership: 81%  

