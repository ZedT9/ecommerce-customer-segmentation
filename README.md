# E-Commerce Customer Segmentation
**Tools:** SQL (DuckDB) · R · Power BI  
**Dataset:** [Olist Brazilian E-Commerce Public Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

## Overview
End-to-end customer segmentation analysis on 93,470 e-commerce customers using RFM (Recency, Frequency, Monetary) methodology. Raw transactional data was queried with SQL, analysed and clustered in R, and visualised in a Power BI dashboard.

## Business Problem
How can an e-commerce platform identify distinct customer groups to enable targeted marketing, improve retention, and allocate resources more effectively?

## Methodology

### 1. SQL — RFM Table Construction
Used DuckDB to join three relational tables (orders, customers, payments) and aggregate to one row per unique customer, computing:
- **Recency** — days since last purchase
- **Frequency** — number of orders placed
- **Monetary** — total spend

### 2. R — EDA & K-Means Clustering
- Removed top 1% monetary outliers (935 customers)
- Applied log transformation to normalize skewed distributions
- Used elbow plot to determine optimal k=4 clusters
- Profiled and labelled each cluster with business-friendly segment names

### 3. Power BI — Dashboard
Built a 4-visual dashboard displaying segment counts, average spend, average recency, and a recency vs monetary scatter plot.

## Results

| Segment | Customers | Avg Recency (days) | Avg Spend (BRL) |
|---|---|---|---|
| Champions | 2,634 | 271 | 275 |
| Promising | 29,756 | 218 | 260 |
| At-Risk | 26,457 | 476 | 120 |
| Casual Browsers | 33,688 | 199 | 65 |

## Key Insights
- 96% of customers purchased only once — repeat buyers are a critical minority worth protecting
- Champions represent only 2.8% of customers but are the highest value segment
- At-Risk customers (26,457) haven't purchased in ~15 months on average — a significant re-engagement opportunity
- Promising customers have solid spend but low frequency — strong candidates for loyalty conversion

## Business Recommendations
- **Champions** → Reward with loyalty programs and early product access
- **Promising** → Trigger follow-up emails and second-purchase incentives
- **At-Risk** → Launch win-back campaigns with time-limited discounts
- **Casual Browsers** → Upsell with category-based promotions

## Repository Structure

```
├── notebooks/
│   ├── 01_rfm_sql.ipynb
│   └── 02_eda_segmentation.ipynb
├── visuals/
│   └── olist_dashboard.pdf
└── README.md
```
## How to Reproduce
1. Download the Olist dataset from [Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
2. Upload CSVs to Google Drive under `ecommerce-segmentation/data/`
3. Open `01_rfm_sql.ipynb` in Google Colab (Python runtime)
4. Open `02_eda_segmentation.ipynb` in Google Colab (R runtime)
5. Load `rfm_segmented.csv` into Power BI Desktop
