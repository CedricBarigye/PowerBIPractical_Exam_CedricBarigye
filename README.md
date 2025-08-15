# Power BI Practical Exam – Cedric Barigye

## 📄 Project Overview
This repository contains my submission for the **DSA 3050A US 2025 End Semester Practical Exam** in **Power BI for Data Visualization**.  
The project uses a retail sales dataset modeled after the AdventureWorks sample structure to perform **data import, transformation, modeling, visualization, dashboard creation, and advanced DAX calculations**.

---

## 📂 Repository Contents
- **Retail_exam_cedric.pbix** → Final Power BI report file.
- **report_export.pdf** → PDF export of the full report (all report pages & dashboard).
- **retail_sales_dataset.xlsx** → Supporting dataset file used in the project.
- **screenshots/** → Folder containing visuals, model, and editor screenshots.
- **README.md** → Project documentation.

---

## 🛠 Approach
1. **Data Import & Cleaning**:
   - Imported the retail sales dataset into Power Query.
   - Verified data types and formatted columns (dates, currency).
   - Removed missing values (<5%) and duplicates in Products.
   - Created a calculated `Profit` column = SalesAmount – (Quantity × Cost).
   - Split Customer Name into FirstName and LastName.
   - Added a Sales Category column: **High (>1000)**, **Medium (500–1000)**, **Low (<500)**.
   - Filtered out sales before 2018.
   - Profiled outliers using a card visual.

2. **Data Modeling**:
   - Built a **star schema** with Dates, Products, Customers, and Geography linked to Sales.
   - Created hierarchies:
     - Date: Year → Quarter → Month → Day.
     - Product: Category → Subcategory → ProductName.
   - Hid unnecessary columns and formatted measures.

3. **Visualizations**:
   - **Bar Chart**: Top 10 Products by SalesAmount with Profit tooltip.
   - **Line Chart**: Monthly sales with 6-month forecast.
   - **Pie Chart**: Sales distribution by Category.
   - **Map**: Sales by Country/State with City drill-down.
   - **Scatter Plot**: Quantity vs. Profit with Sales Category coloring and play axis.
   - **KPI Card**: Total SalesAmount vs. target (10% growth).
   - **Gauge**: Profit Margin vs. 30% target.
   - **Decomposition Tree**: SalesAmount by Customer → Product → Region.
   - **Custom Visual**: Bullet Chart for Sales vs. Budget.

4. **Reports & Dashboards**:
   - **Page 1 – Sales Overview**: Line chart, KPI, and map with slicers for Year, Category, and Region.
   - **Page 2 – Product Analysis**: Bar chart, scatter plot, decomposition tree with bookmarks.
   - **Page 3 – Customer Insights**: Table of top customers with conditional formatting and multi-row cards.
   - Published dashboard in Power BI Service with Q&A tile and optimized mobile layout.

5. **DAX & Security**:
   - Created measures:
     ```DAX
     YoY Growth % = 
     DIVIDE(
         [Total Sales] - CALCULATE([Total Sales], SAMEPERIODLASTYEAR(Dates[Date])),
         CALCULATE([Total Sales], SAMEPERIODLASTYEAR(Dates[Date]))
     )

     Running Total Sales = 
     CALCULATE(
         [Total Sales],
         FILTER(
             ALL(Dates),
             Dates[Date] <= MAX(Dates[Date])
         )
     )

     Top 5 Sales = 
     IF(
         RANKX(ALL(Products[ProductName]), [Total Sales], , DESC) <= 5,
         [Total Sales]
     )
     ```
   - Implemented Row-Level Security (RLS) roles:
     - **US Manager**: Country = "United States"
     - **Europe Manager**: Region IN {"Europe"}

---

## 📊 Screenshots
![Sales Overview](screenshots/sales_overview.png)  
![Product Analysis](screenshots/product_analysis.png)  
![Customer Insights](screenshots/customer_insights.png)  
![Dashboard](screenshots/dashboard.png)  
![Model View](screenshots/model_view.png)  
![Power Query Editor](screenshots/power_query.png)  
![RLS Setup](screenshots/rls_setup.png)  

---

## 📌 Key Insights
- Electronics category contributed **40%** of total sales.
- Sales have grown **15% year-over-year** since 2021.
- High-value customers are concentrated in the US and Western Europe.
- Profit margins vary significantly by category, with accessories outperforming other segments.

---

## ⚠ Assumptions & Limitations
- Forecasting uses a linear trend model in Power BI, assuming consistent seasonal patterns.
- The dataset was generated for academic purposes and may not represent real-world market conditions.

---

## 🌐 Live Report
[View the Published Power BI Report](PASTE_YOUR_PUBLISHED_LINK_HERE)

---

## 📚 Dataset Source
Custom retail dataset modeled after Microsoft AdventureWorksDW2020 structure.
