# big-mart-retail-analytics
An executive-ready Power BI dashboard analyzing $18.59M in retail sales data across 10 locations. Features full Power Query ETL pipelines, advanced DAX metrics, and data-driven business insights.

Retail Sales Performance Dashboard (Big Mart Analytics)

### Project Overview
Transforms raw retail transactional data into an interactive, executive-ready Power BI dashboard to optimize supply chain distribution, shelf visibility, and store stock allocation.

### Files 
*   **`bigmart_data.csv`**: Core dataset containing 8,523 transactional records and 12 columns mapping product attributes against individual store performance.
*   **TASK 2.Png** : Dashboard Preview
*   **README.md**: Documentation and project walkthrough
   
  ### Key Business Insights
*   **Core Revenue Anchor:** Supermarket Type 1 is the primary driver of retail scale, accounting for **69.5% ($12.92M)** of total revenue.
*   **Geographic Spend Power:** Tier 3 locations represent the highest-earning regional segment, contributing **41.1% ($7.64M)** of total sales.
*   **Inventory High-Flyers:** Fruits/Vegetables and Snack Foods are the core volume drivers, combining for over **$5.5M** in gross sales.
*   **Premium Margin Drivers:** Household Items and Dairy command the highest Average Maximum Retail Price (MRP) at roughly **$149 per unit**.
*   **Operational Outlier:** A single location—**OUT027 (Supermarket Type 3)**—is a massive performance outlier, generating **$3.45M** on its own.

### Data Cleaning (Power Query ETL)
*   **Categorical Standardization:** Fixed typos in `Item_Fat_Content` (merged `LF`, `low fat`, and `Low Fat` $\rightarrow$ **Low Fat**; merged `reg` and `Regular` $\rightarrow$ **Regular**).
*   **Imputation of Missing Footprints:** Resolved **2,410 missing entries** in `Outlet_Size` by logically mapping them against `Outlet_Type` (e.g., Grocery Stores = **Small**).
*   **Numerical Imputation:** Filled **1,463 missing values** in `Item_Weight` using the baseline average weight of `12.85`.
*   **Anomaly Rectification:** Replaced unrealistic `0.00` scores in `Item_Visibility` (526 items) with a baseline median marker of `0.066`.

## Formulas & Analytical Logic

This project utilizes explicit formulas across both the data transformation (Power Query) and data modeling (DAX) phases to ensure absolute calculation accuracy.

### Data Modeling Measures (DAX)

*   **Total Revenue:**
```DAX
    Total Revenue = SUM(bigmart_data[Item_Outlet_Sales])
    ```
    *Aggregates gross operational retail revenue ($18.59M).*

*   **Average Item Price (MRP):**
```DAX
    Average MRP = AVERAGE(bigmart_data[Item_MRP])
    ```
*Establishes the base product cost benchmark ($140.99).*

*   **Average Sales per Store:**
```DAX
    Avg Sales per Store = 
    DIVIDE(
        SUM(bigmart_data[Item_Outlet_Sales]), 
        DISTINCTCOUNT(bigmart_data[Outlet_Identifier])
    )
    ```
    *Divides total revenue by the 10 active unique locations to set a store-level baseline ($1.86M).*

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for more details.
