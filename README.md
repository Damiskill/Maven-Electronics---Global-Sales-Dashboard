# Maven-Electronics---Global-Sales-Dashboard
This is a sales performance dashboard for a global electronics retailer to consolidate and analyze sales, customer, product, and store data. The dashboard tracks key performance metrics, uncover sales trends, and provide actionable insights for management to make data-driven decisions.

---

```markdown
# 📊 Maven Electronics – Global Sales Dashboard (Power BI)

An interactive **Power BI executive dashboard** built to analyze global sales, customer behavior, product performance, and store trends for *Maven Electronics* — a multinational retailer of consumer electronics.

![Dashboard Preview](./images/dashboard_preview.png)

---

## 🧭 Project Overview

Maven Electronics faced a **revenue decline since 2020** and lacked a unified reporting system.  
This project consolidates multiple datasets (Sales, Customers, Products, Stores, Exchange Rates) into a single data model — enabling insights into revenue, profit, and customer trends across regions.

**Objectives**
- Track overall performance (Revenue, Profit, Quantity Sold, Customer Count)
- Identify high-performing and underperforming products and stores
- Analyze customer demographics and buying patterns
- Compare YoY and seasonal trends to uncover growth opportunities

---

## 🗂️ Dataset Description

| Table | Description |
|-------|--------------|
| **Sales** | Transactional data – order details, quantities, dates, and product/store links |
| **Customers** | Customer demographics (gender, geography, birthdate, etc.) |
| **Products** | Product attributes (brand, category, cost, price, etc.) |
| **Stores** | Store locations, sizes, and open dates |
| **Exchange Rates** | Daily currency-to-USD rates for consistent reporting |

---

## 🧱 Data Model (Star Schema)

```

Sales (Fact)
│
├── Customers (Dim)
├── Products (Dim)
├── Stores (Dim)
└── Exchange Rates (Support)

````

Relationships are built via foreign keys (`CustomerKey`, `ProductKey`, `StoreKey`).

---

## ⚙️ Project Stages

### **1️⃣ Data Preparation (Power Query)**
- Removed nulls, duplicates, and invalid data (e.g., postal codes, missing dates)
- Converted data types (Date, Currency, Numbers)
- Created calculated columns:
  ```DAX
  StoreAgeYears = DATEDIFF(Stores[Open Date], TODAY(), YEAR)
````

---

### **2️⃣ Data Modeling**

* Established **one-to-many** relationships between dimension tables and the Sales fact table
* Applied proper cardinality and referential integrity for consistent aggregation

---

### **3️⃣ Measure Development (DAX Formulas)**

**Performance KPIs**

```DAX
Total Revenue = SUM(Sales[Quantity] * RELATED(Products[Unit Price USD]))
Total Cost = SUM(Sales[Quantity] * RELATED(Products[Unit Cost USD]))
Total Profit = [Total Revenue] - [Total Cost]
Profit Margin % = DIVIDE([Total Profit], [Total Revenue])
```

**Customer Metrics**

```DAX
Unique Customers = DISTINCTCOUNT(Sales[CustomerKey])
Customer Growth % = DIVIDE([Unique Customers] - [Unique Customers LY], [Unique Customers LY])
```

**Product Metrics**

```DAX
Unique Brands = DISTINCTCOUNT(Products[Brand])
Unique Categories = DISTINCTCOUNT(Products[Category])
Unique Subcategories = DISTINCTCOUNT(Products[Subcategory])
Total Products = COUNTROWS(Products)
```

**Store Metrics**

```DAX
Total Stores = COUNTROWS(Stores)
Avg Store Size = AVERAGE(Stores[Square Meters])
Revenue per Store = DIVIDE([Total Revenue], [Total Stores])
```

**Trend & YoY**

```DAX
Revenue LY = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(Dates[Date]))
Revenue YoY % = DIVIDE([Total Revenue] - [Revenue LY], [Revenue LY])
```

---

### **4️⃣ Visualization & Dashboard Design**

**Page 1 – Executive Summary**

* KPIs: Revenue, Profit, Quantity, Customers
* YoY Growth Cards
* Trend Line (Revenue over Time)
* Region Performance Map

**Page 2 – Product & Customer Insights**

* Top 10 vs Bottom 10 Products (Bar Chart)
* Profit Margin by Category
* Customer Demographics (Gender, Age, Geography)
* Revenue by Segment (Pie/Donut Chart)

**Page 3 – Store Performance**

* Revenue by Store and Region (Map or Matrix)
* Store Age vs Profit (Scatter Plot)
* Revenue per m² (KPI)
* Open Date Impact (Line Trend)

---

## 📈 Key Insights

* Revenue grew from **$6.85M (2016)** to **$18.31M (2019)** before halving in **2020 ($9.32M)**
* Profit followed a similar drop: **$10.72M → $5.46M**
* Customer base shrank from **9K → 5K** post-2020
* Clear **seasonal pattern:** Metrics dip **Jan–Apr**, then surge until **December**
* Older stores contributed **higher revenue per square meter**
* Most profitable segments: **Computers and Smartphones**

---

## 💡 Tools & Skills Demonstrated

* **Power BI** – Data modeling, DAX measures, interactive visuals, and navigation buttons
* **Power Query** – Data cleaning, transformation, and integration
* **Data Storytelling** – Insight extraction and executive-level reporting
* **Data Modeling** – Star schema design and performance optimization

---

## 🚀 How to View the Dashboard

You can explore the full interactive report here:
🔗 [Maven Electronics Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiZDZmNmVkYTUtOWViMy00NDAyLWIzZmQtZTk5ODU0ZDZmYjIzIiwidCI6IjgxYzdiMWY1LWRhMmMtNGFiYy04YjhkLTFlZDA2NTVhYjE4NiJ9)

---

## 🧩 Future Enhancements

* Add dynamic date filtering (e.g., “Last 12 Months”)
* Integrate real-time data from SQL database
* Create drill-through pages for store-level deep dives

---

## ✍️ Author

**Emmanuel Philip**
📧 [emmanuelphilip685d@gmail.com]
💼 [LinkedIn Profile](https://linkedin.com/in/PhilipEmmanuel)

---

> “Data tells a story — dashboards make it visible.”

```

---
