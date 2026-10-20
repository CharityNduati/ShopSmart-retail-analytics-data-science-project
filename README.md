# ShopSmart Retail: Exploratory Data Analysis (Week 1)

**Programme:** AnalystLab Africa Experience Lab | **Track:** Data Science | **Mission:** DS01
**Author:** Charity Nduati | **Client:** ShopSmart Retail Ltd. | **Hashtag:** #AnalystLabAfrica

## Overview
An exploratory data analysis of ShopSmart's 2025 retail data: 50,000 orders, 25 stores, 500 products and 5,000 customers across Nigeria. The project covers environment setup, data loading, cleaning, KPIs, 10 visualisations, correlation analysis, feature engineering, business questions, a report, and a bonus K-Means customer segmentation.

## Headline findings
1. **Only 33% of orders are Completed.** Realised revenue is ₦2.25bn against ₦6.82bn booked.
2. **Beauty leads revenue (23.3%)**; Fashion is growing fastest; Home is weakest.
3. **Performance is very even** across months, stores and customer segments (loyalty tiers spend about the same).
4. **About 75% of returns are fulfilment problems** (late delivery, wrong item, damaged).
5. **21 product-store lines are below reorder level**, while 369 of 500 lines are heavily overstocked.
6. Every store has exactly 5 employees, and 9 of 25 stores have no Store Manager on record.

## Project structure
```
Week1_DataScience_Project/
├── Week1_EDA.ipynb        # full analysis, outputs included
├── data/                  # raw CSVs as provided
├── Cleaned_Data/          # cleaned tables, master dataset, features, cleaning log
├── Visualizations/        # all charts (PNG)
├── EDA_Report.pdf         # professional report
├── Presentation.pptx      # 14-slide summary deck
├── requirements.txt
└── README.md
```

## How to run
```bash
pip install -r requirements.txt
jupyter notebook Week1_EDA.ipynb      # then Kernel > Restart & Run All
```
The notebook finds the CSVs automatically (in `data/`, the current folder, or the parent folder). If yours are elsewhere, set `DATA_DIR` in the first code cell. `missingno` is optional: without it a simple fallback chart is used.

## Datasets
All 8 supplied tables are loaded and used: Customers, Products, Orders, Stores, Returns, Employees, Suppliers and Inventory. `Order_Items.csv` and the Data Dictionary were not provided; `Orders.csv` is already one product per order, and the notebook loads both files automatically if placed in `data/`.

## Methodology and key decisions
- **Revenue** = quantity × unit price × (1 − discount %), counted for **Completed orders only**. Shipping is excluded.
- **Return rate** = returned Completed orders / Completed orders (4.83%). Duplicate returns per order were removed.
- **Inventory value** = stock on hand × product cost price.
- **Geography:** State is used instead of Region, because Region conflicts with State in the stores table.
- **Suppliers** are linked to products through Brand (supplier name = brand + " Supplies").

## Data-quality issues found
- 67% of returns (1,685 of 2,500) sit on Pending or Cancelled orders.
- About 5,000 orders are dated before the customer's registration date.
- Store names repeat (for example four "ShopSmart Abuja"); group by Store_ID.
- Order unit prices never equal catalogue selling prices, so margin analysis is unreliable.
- There is no delivery-date field, so supplier delivery performance cannot be measured.

## Bonus
K-Means customer segmentation on RFM features (notebook section 9). Limitations: one year of data, few orders per customer, and only moderate cluster separation (silhouette about 0.3).

## Tech stack
Python 3, pandas, numpy, matplotlib, seaborn, missingno, scikit-learn, Jupyter.
