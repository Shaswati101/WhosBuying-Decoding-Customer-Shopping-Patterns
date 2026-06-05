# WhosBuying — Decoding Customer Shopping Patterns

> Customer behavior analytics using Python, PostgreSQL, and Power BI — uncovering segmentation, seasonal trends, and purchase pattern insights across 3,900 records.

---

## Problem Statement

Which customer segments drive the most revenue, and how does purchasing behavior vary by season, age group, gender, and product category? This project analyzes a retail customer dataset to surface actionable insights that can inform marketing, inventory, and retention strategies — the kind of analysis a D2C or e-commerce business needs to make smarter decisions.

---

## Key Insights & Findings

- **Young adults (18–34)** contributed the highest revenue segment at ~$62K, outpacing middle-aged and senior groups
- **Clothing** was the top-performing category at $104K in revenue, with Accessories at $74K
- **Winter** was the peak revenue season — consistent with high-AOV outerwear and clothing purchases
- **Subscribers spend 39% more on average** ($68 vs $49) than non-subscribers, despite making up only 7.3% of customers
- **Female customers subscribe at a 27% higher rate** than male customers (8.1% vs 6.4%)
- **Credit card** was the dominant payment method at ~38%, followed by cash and debit card

---

## Tech Stack

| Layer | Tools Used |
|---|---|
| Data Cleaning & EDA | Python (Pandas, Matplotlib, Seaborn) |
| Data Storage & Querying | PostgreSQL |
| Dashboard & Visualization | Power BI |
| Dataset | Customer Shopping Preferences (3,900 records) |

---

## Project Structure

```
WhosBuying-Decoding-Customer-Shopping-Patterns/
│
├── data/
│   └── shopping_cleaned.csv         # Cleaned dataset used for analysis
│
├── notebooks/
│   └── customer_analysis.ipynb      # Python EDA and cleaning notebook
│
├── sql/
│   └── queries.sql                  # Key SQL queries used for analysis
│
├── dashboard/
│   └── customer_behavior.pbix       # Power BI dashboard file
│
├── assets/
│   └── dashboard-preview.png        # Dashboard screenshot
│
├── reports/
│   └── project_report.pdf           # Full project write-up
│
└── README.md
```

---

## Dashboard Preview

![Customer Behavior Dashboard](assets/dashboard-preview.png)

---

## Sample SQL Queries

**Revenue by product category:**
```sql
SELECT category, SUM(purchase_amount_usd) AS total_revenue
FROM customer_shopping
GROUP BY category
ORDER BY total_revenue DESC;
```

**Subscription rate by gender:**
```sql
SELECT gender,
       COUNT(*) AS total,
       SUM(CASE WHEN subscription_status = 'Yes' THEN 1 ELSE 0 END) AS subscribers,
       ROUND(100.0 * SUM(CASE WHEN subscription_status = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) AS sub_rate_pct
FROM customer_shopping
GROUP BY gender;
```

**Average purchase amount by age group and season:**
```sql
SELECT age_group, season, ROUND(AVG(purchase_amount_usd), 2) AS avg_purchase
FROM customer_shopping
GROUP BY age_group, season
ORDER BY age_group, avg_purchase DESC;
```

---

## Business Recommendations

1. **Target female young adults for subscription campaigns** — they have the highest subscription propensity and spend significantly more when subscribed
2. **Prioritize winter inventory for Clothing and Outerwear** — seasonal peaks are concentrated and predictable
3. **Offer credit card-linked promotions** — dominant payment method; incentivizing its use can increase AOV
4. **Invest in subscription onboarding** — with 92.7% of customers unsubscribed, even a modest conversion improvement would meaningfully lift average revenue per customer

---

## Dataset

This project uses the [Customer Shopping Preferences Dataset](https://www.kaggle.com/datasets/iamsouravbanerjee/customer-shopping-trends-dataset) from Kaggle — a synthetic dataset designed for consumer behavior analysis, containing 3,900 records across demographics, product categories, payment methods, seasons, and purchase history.
