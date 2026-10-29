# Power-BI-DAX-Data-Visualization

# 📊 Power BI Sales Analysis Dashboard

 🚀 Project Overview
This project is an end-to-end business intelligence solution built using **Microsoft Power BI**. Designed to analyze comprehensive sales performance, track regional distribution, evaluate category-wise targets, and monitor key financial metrics. This dashboard empowers stakeholders to make data-driven decisions by providing clear visibility into revenue trends, profitability, and order distributions.


 🛠️ Key Features & Visualizations
The dashboard incorporates multiple interactive visualizations and high-level KPI cards:
* **High-Level KPIs:** Track overall **Total Sales**, **Total Targets**, **Order Count**, and **Year-to-Date (YTD) Sales**.
* **Sales Target Achievement by Category:** Clustered column chart comparing actual sales against target goals across categories (*Clothing, Furniture, Electronics*)[cite: 5].
* **Monthly Sales Trend:** Line chart analyzing revenue fluctuations over time (*May 2018 – March 2019*).
* **Geographic Sales Analysis:** Interactive map and city-level breakdown tracking sales distribution across regions like Delhi, Mumbai, Pune, and Indore.
* **Profit vs. Quantity Scatter Plot:** Evaluates the relationship between order quantities and profitability across various sub-categories.
* **Treemap & Donut Charts:** Showcases top-performing sub-categories (e.g., Printers, Book Cases, Saree, Phones) by sales amount and profit margins.

---

🗄️ Data Modeling & Relationships
The data model connects multiple tables using proper relational schema design to maintain data integrity and enable cross-filtering:
* **List of Orders:** Contains customer names, locations, order dates, and unique order IDs.
* **Order Details:** Houses transaction-level metrics including amount, profit, quantity, category, and sub-category.
* **Sales Target:** Stores category-wise targets mapped by order dates.
*(Relationships are established using standard **1-to-Many ($1 \to *$)** cardinality mappings between lookup tables and transaction tables)*

---

## 📐 Custom DAX Measures & Calculated Columns
To enhance reporting capabilities, several custom DAX (Data Analysis Expressions) formulas were implemented:

1. **Category Type (Calculated Column):**
   ```dax
   Category_Ttype = 'Order Details'[Category] & " " & 'Order Details'[Sub-Category]

   Revenue = 'Order Details'[Amount] * 'Order Details'[Quantity]
   
   Sales_Category = IF('Order Details'[Amount] > AVERAGE('Order Details'[Amount]), "Above Average", "Below Average")
   
   Order_Count = COUNT('Order Details'[Order ID])
   
   Year-to-Date (YTD) Sales = CALCULATE(SUM('Order Details'[Amount]), DATESYTD('List of Orders'[Order Date]))
   
   Average_Profit_in_Delhi = CALCULATE(AVERAGE('Order Details'[Profit]), 'List of Orders'[City] = "Delhi")
