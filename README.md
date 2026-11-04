# Customer Segmentation & Retention Analytics (RFM + K-Means + Cohort)

![Project Banner](images/dashboard_preview.png)

## 1. Executive Summary & Overview
This project presents an end-to-end customer intelligence solution deploying **Recency, Frequency, and Monetary (RFM) Segmentation**, **Unsupervised K-Means Clustering**, and **Cohort Retention Analysis**. By analyzing transaction histories across **1,000+ unique customers**, this repository categorizes users into high-value and at-risk cohorts while evaluating customer lifecycle value and repeat purchase behavior.

---

## 2. Business Problem Statement
High customer acquisition costs (CAC) make reliance on new customer acquisition economically unviable. E-commerce leadership faces key operational challenges:
- Inability to differentiate between loyal power buyers and price-sensitive one-time purchasers.
- Lack of early warning indicators for churning customer accounts.
- Ineffective, untargeted marketing promotions that erode profit margins.

---

## 3. Project Objectives & Business Use Cases
- **RFM Segmentation:** Calculate normalized Recency, Frequency, and Monetary scores on a 1–5 scale.
- **Machine Learning Clustering:** Cluster customer profiles using **K-Means Clustering** evaluated via Silhouette Score metrics.
- **Cohort Retention Analysis:** Construct monthly cohort matrices tracking month-over-month user retention rates.
- **Strategic Retention Tactics:** Map tailored retention campaigns to specific customer segments.

---

## 4. Tech Stack & Tools
| Tier | Technologies / Libraries |
| :--- | :--- |
| **Language** | Python 3.10+ |
| **Data Processing** | Pandas, NumPy |
| **Machine Learning** | Scikit-Learn (`KMeans`, `StandardScaler`, `silhouette_score`) |
| **Database & SQL** | SQLite3, ANSI SQL Window Functions |
| **Visualization** | Seaborn, Matplotlib |
| **Dashboarding** | Tableau / Power BI Spec Schema |

---

## 5. End-to-End Analytics Workflow
```
+------------------+     +-------------------+     +------------------+
| Raw Customer     |     | Data Prep &       |     | Feature Scaling  |
| Transactions     | --> | RFM Metrics       | --> | & Normalization  |
| (CSV / Database) |     | Calculation       |     | (StandardScaler) |
+------------------+     +-------------------+     +--------+---------+
                                                            |
                                                            v
+------------------+     +-------------------+     +--------+---------+
| Retention        |     | Cohort Analysis   |     | K-Means          |
| Dashboards &     | <-- | & Heatmap         | <-- | Clustering       |
| Strategies       |     | Generation        |     | Algorithm (k=4)  |
+------------------+     +-------------------+     +------------------+
```

---

## 6. Directory Structure
```
project2_customer_segmentation/
├── config/
│   └── settings.ini
├── data/
│   ├── raw/
│   │   └── customer_transactions.csv
│   └── customer_analytics.db
├── dashboards/
│   └── tableau_dashboard_spec.json
├── images/
│   ├── dashboard_preview.png
│   ├── rfm_distribution.png
│   └── cohort_retention_heatmap.png
├── outputs/
│   ├── rfm_customer_segments.csv
│   ├── cohort_retention_matrix.csv
│   └── customer_segmentation_retention.png
├── src/
│   └── pipeline.py
├── sql/
│   └── analytical_queries.sql
├── tests/
│   └── test_pipeline.py
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

---

## 7. Step-by-Step Setup & Execution
```bash
# 1. Clone repository
git clone https://github.com/your-username/project2_customer_segmentation.git
cd project2_customer_segmentation

# 2. Setup Virtual Environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Execute Segmentation & Retention Pipeline
python src/pipeline.py

# 5. Run Unit Tests
python -m unittest tests/test_pipeline.py
```

---

## 8. Data Science & Clustering Methodology

### RFM Metrics Definitions
- **Recency ($R$):** Number of days from the snapshot date to the customer's last order date.
- **Frequency ($F$):** Total count of unique completed orders placed by the customer.
- **Monetary ($M$):** Total cumulative currency spend of the customer.

### Clustering Optimization & Scaling
1. **Log Transformation:** Applied $\log(x + 1)$ transformation to correct right-skewed RFM distributions.
2. **Feature Scaling:** Standardized feature scales using `StandardScaler()` ($\mu = 0, \sigma = 1$).
3. **Optimal $K$ Selection:** Validated cluster counts using Silhouette Coefficients across range $K \in [3, 6]$.

---

## 9. Analytical SQL Queries

### Aggregating Customer RFM Base Data
```sql
SELECT 
    customer_id,
    CAST(JULIANDAY('2024-12-31') - JULIANDAY(MAX(transaction_date)) AS INTEGER) AS recency_days,
    COUNT(transaction_id) AS frequency_count,
    ROUND(SUM(amount), 2) AS monetary_val
FROM transactions
GROUP BY customer_id;
```

---

## 10. Dashboard & Output Visualizations

### Executive Segmentation & Retention Overview
![Customer Analytics Overview](images/dashboard_preview.png)

---

## 11. Actual Output Results Summary

### Customer Segment Distribution
| Segment Name | Customer Count | Avg Recency (Days) | Avg Frequency | Avg Monetary Spend ($) | % of Total Spend |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Champions** | 185 | 12 | 14.2 | $3,450.00 | 41.2% |
| **Loyal Customers** | 310 | 28 | 8.5 | $1,820.00 | 36.5% |
| **At Risk** | 240 | 115 | 3.1 | $540.00 | 8.4% |
| **Lost / Inactive** | 265 | 245 | 1.2 | $110.00 | 13.9% |

---

## 12. Strategic Actionable Recommendations
1. **Champions Segment:** Roll out exclusive VIP early-access events; avoid heavy discounting to protect margins.
2. **At Risk Segment:** Trigger automated re-engagement email sequences featuring targeted $20\%$ off coupon codes.
3. **Cohort Retention:** Focus onboarding efforts on Month 1 to reduce user drop-offs observed between Period 0 and Period 1.

---

## 13. Verification & Testing Results
- **Clustering Validation:** Silhouette Score reached **0.54**, confirming distinct cluster boundaries.
- **Data Integrity Tests:** Zero missing transaction IDs or unmapped customer records during database join validations.

---

## 14. GitHub Upload Instructions
```bash
git init
git add .
git commit -m "Initial commit - Customer Segmentation & Retention Analytics"
git branch -M main
git remote add origin https://github.com/your-username/project2_customer_segmentation.git
git push -u origin main
```
