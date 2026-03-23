# 🍫 Chocolate Sales Dashboard – Power BI

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=power%20bi&logoColor=black)  
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

An interactive **Power BI dashboard** that analyzes chocolate sales across brand, product type, country, sales channel, and payment method. It includes advanced segmentation with **RFM analysis by country** and **revenue‑based transaction segmentation**.

📄 **PDF export**: [`Chocolate_sales_dashboard.pdf`](./Chocolate_sales_dashboard.pdf)

---

## 📊 Dashboard Preview

*(Insert a screenshot – e.g., `images/Checolate_sales_dashboard_page-0001.jpg`)*

**Key Visuals**:  
- KPIs (Revenue, Units Sold, Avg Price, Orders)  
- Revenue by Brand & Product Type  
- Sales over time  
- Geographic map  
- RFM segmentation table (Country scores & segments)  
- Revenue segment breakdown (Lowest, Medium, Higher, Highest)  
- Slicers for date, country, brand, channel

---

## 🎯 Objective

Provide a clear, interactive view to:
- Identify top brands, products, and sales channels.
- Track sales trends over time.
- Prioritize marketing efforts via RFM country segmentation.
- Classify transaction value via revenue quartiles.

---

## 📁 Dataset

Sample chocolate sales data (CSV) with fields:

| Column | Description |
|--------|-------------|
| `Sale_ID`, `Date` | Transaction details |
| `Brand`, `Product_Type` | Brand and product category |
| `Country`, `Sales_Channel`, `Payment_Method` | Geographic and transactional context |
| `Price_USD`, `Units_Sold`, `Revenue_USD` | Revenue metrics |

---

## 📐 Key DAX Measures

### 1. RFM Analysis by Country (`RFM_Country`)
Segments countries based on **Recency** (days since last sale), **Frequency** (transaction count), and **Monetary** (total revenue). Scores 1–4 (percentile‑based) combine into segments: *Champions*, *Loyal Customers*, *Potential Loyalist*, *At Risk*, *Needs Attention*.  
*[Full code available in the repository]*

### 2. Revenue Segmentation (`Revenue_Segment`)
Classifies each transaction into quartiles using the 25th, 50th, and 75th percentiles of `Revenue_USD`:
- **Lowest** (≤ Q25)
- **Medium** (Q25 < x ≤ Q50)
- **Higher** (Q50 < x ≤ Q75)
- **Highest** (> Q75)

---

## 🚀 Usage

1. **Clone** the repo:  
   `git clone https://github.com/mamar/chocolate-sales-dashboard.git`
2. Open `Chocolate_Sales_Dashboard.pbix` in Power BI Desktop.
3. Update data source if needed to point to `data/chocolate_sales.csv`.
4. Explore visuals, slicers, and drill‑downs.
5. (Optional) View the exported PDF for a static report.

---

## 📈 Key Insights (Sample)

- **RFM**: [e.g., “France is a ‘Champion’ country; Italy is ‘At Risk’.”]
- **Revenue Segments**: Highest‑value transactions represent the top 25% of revenue.
- **Top Brand**: Cadbury leads in revenue.
- **Product**: Milk Chocolate is the most sold type.
- **Channel**: Convenience store dominates transactions.
- **Payment**: Cash is the most used method.

*Update with actual findings from your dashboard.*

---

## 📂 Repository Structure
*(Insert a screenshot – e.g., `images/Readme_structure.jpg`)*


---

## 🔮 Future Enhancements

- Forecasting & profit margin analysis  
- Customer‑level RFM  
- Power BI Service publishing  
- Live data connection (SQL/API)

---

## 🤝 Contributing

Open issues or pull requests for improvements.

---

## 📄 License

Educational/demo use only. Data is fictional.

---

## 📬 Contact

Linkedin – [@mamar-habtamu-61818597](https://www.linkedin.com/in/mamar-habtamu-61818597/) 
[GitHub Repository](https://github.com/mamar/chocolate-sales-dashboard)
