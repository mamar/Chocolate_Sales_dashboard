# 🍫 Chocolate Sales Dashboard 2025

[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?style=flat-square)](https://powerbi.microsoft.com/)  
[![Dataset](https://img.shields.io/badge/Dataset-CSV-blue?style=flat-square)](data/chocolate_sales.csv)  

An interactive **Power BI** dashboard analyzing chocolate sales across countries, brands, and customer segments. Includes revenue KPIs, RFM (Recency, Frequency, Monetary) segmentation, and insights into sales channels and payment methods.

![Chocolate Dashboard](data/images/chocolate_dashboard.png)

---

## 📌 Table of Contents
1. [Overview](#overview)
2. [Features](#features)
3. [Dataset](#dataset)
4. [Setup & Usage](#setup--usage)
5. [RFM Logic](#rfm-logic-dax)
6. [Dashboard Previews](#-dashboard-previews)
7. [License](#license)

---

## 📝 Overview
- Visualizes 2025 chocolate sales data.
- Tracks revenue by **brand**, **product type**, and **country**.
- Analyzes **sales channel performance** and **payment preferences**.
- Segments countries using **RFM scoring**.

---

## ✨ Features

### 🔹 Key Metrics
- Total revenue (example: `$119.45K`)
- Channel & brand contribution

### 🔹 Revenue Analysis
- **Brands**: Toblerone, Mars, Lindt, Nestlé, Ferrero, Cadbury, Hershey  
- **Product Types**: White Chocolate, Dark Chocolate, Chocolate Bar, Truffles, Milk Chocolate, Chocolate Box  
- **Countries**: France, Canada, India, UK, Germany, Saudi Arabia, Italy, Australia, UAE, USA  
- **Sales Channels**: Convenience, Specialty, Supermarket, Online

### 🔹 Customer Segmentation (RFM)
- **Recency**: Days since last purchase  
- **Frequency**: Number of transactions  
- **Monetary**: Total revenue per country  
- **Segments**: *Champions*, *Loyal Customers*, *Potential Loyalist*, *At Risk*, *Needs Attention*

### 🔹 Payment & Segment Insights
- Segment vs Payment Method  
- Segment vs Sales Channel  
- Segment vs Brand

---

## 📂 Dataset
`chocolate_sales.csv` contains:

| Column | Description |
|--------|-------------|
| `Sale_ID` | Transaction ID |
| `Date` | Transaction date |
| `Brand` | Chocolate brand |
| `Product_Type` | Category |
| `Country` | Customer country |
| `Sales_Channel` | Distribution channel |
| `Payment_Method` | Cash, Card, Digital Wallet |
| `Price_USD` | Unit price |
| `Units_Sold` | Quantity |
| `Revenue_USD` | Total revenue |

> **Note:** Adjust DAX RFM calculations if your table name differs from `'chocolate_sales_2025_dataset'`.

---

## 🛠️ Setup & Usage
1. Install **Power BI Desktop**.
2. Open `Chocolate_Sales_Dashboard.pbix`.
3. Update data source to `data/chocolate_sales.csv`.
4. Explore dashboards and RFM insights.

---

## 🔢 RFM Logic (DAX)
Calculates country-level **RFM scores** and assigns segments using percentile-based scoring:

```dax
RFM_Country = 
VAR CountryTable =
    SUMMARIZE(
        'chocolate_sales_2025_dataset',
        'chocolate_sales_2025_dataset'[Country],
        "Recency", DATEDIFF(MAX('chocolate_sales_2025_dataset'[Date]), TODAY(), DAY),
        "Frequency", COUNTROWS('chocolate_sales_2025_dataset'),
        "Monetary", SUM('chocolate_sales_2025_dataset'[Revenue_USD])
    )
RETURN
ADDCOLUMNS(
    CountryTable,
    "R_Score", SWITCH(TRUE(), [Recency]<=PERCENTILEX.INC(CountryTable,[Recency],0.25),4, [Recency]<=PERCENTILEX.INC(CountryTable,[Recency],0.50),3, [Recency]<=PERCENTILEX.INC(CountryTable,[Recency],0.75),2, 1),
    "F_Score", SWITCH(TRUE(), [Frequency]>=PERCENTILEX.INC(CountryTable,[Frequency],0.75),4, [Frequency]>=PERCENTILEX.INC(CountryTable,[Frequency],0.50),3, [Frequency]>=PERCENTILEX.INC(CountryTable,[Frequency],0.25),2, 1),
    "M_Score", SWITCH(TRUE(), [Monetary]>=PERCENTILEX.INC(CountryTable,[Monetary],0.75),4, [Monetary]>=PERCENTILEX.INC(CountryTable,[Monetary],0.50),3, [Monetary]>=PERCENTILEX.INC(CountryTable,[Monetary],0.25),2, 1),
    "RFM_Score_Text", FORMAT([R_Score],"0") & "-" & FORMAT([F_Score],"0") & "-" & FORMAT([M_Score],"0"),
    "Country_Segment", SWITCH(TRUE(), [R_Score]=4 && [F_Score]=4 && [M_Score]=4,"Champions",[R_Score]>=3 && [F_Score]>=3 && [M_Score]>=3,"Loyal Customers",[R_Score]>=2 && [F_Score]>=2 && [M_Score]>=2,"Potential Loyalist",[R_Score]=1 || [F_Score]=1 || [M_Score]=1,"At Risk","Needs Attention")
)



