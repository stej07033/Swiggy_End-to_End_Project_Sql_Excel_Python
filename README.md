# 🍔 Swiggy End-to-End Data Analytics Project

![Swiggy](https://img.shields.io/badge/Swiggy-Data%20Analytics-orange?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-Analysis-blue?style=for-the-badge\&logo=python)
![SQL](https://img.shields.io/badge/SQL-Server-red?style=for-the-badge\&logo=microsoftsqlserver)
![Excel](https://img.shields.io/badge/Excel-Dashboard-green?style=for-the-badge\&logo=microsoftexcel)
![Pandas](https://img.shields.io/badge/Pandas-EDA-150458?style=for-the-badge\&logo=pandas)

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/dd5c01bf-65da-4657-8f87-8c867347f75b" />

## 📌 Project Overview

This is an **end-to-end Swiggy Food Delivery Data Analytics Project** built using a single dataset and multiple data analytics tools.

The project demonstrates how the same business dataset can be transformed from **raw data into actionable business insights** using:

* 🐍 Python
* 🗄️ SQL Server
* 📊 Microsoft Excel


The complete workflow is:

```text
Raw Dataset
     ↓
Data Understanding
     ↓
Data Cleaning & Validation
     ↓
Python EDA
     ↓
SQL Database & Star Schema
     ↓
Business KPI Analysis
     ↓
Excel Dashboard
     ↓
Business Insights
```

---

# 🎯 Business Objective

The main objective of this project is to analyze Swiggy food-delivery data and answer important business questions related to:

* Sales and revenue
* Order trends
* Restaurant performance
* Food categories
* Cities and states
* Customer ratings
* Pricing
* Monthly and quarterly performance
* Top-performing restaurants
* Geographic revenue contribution

The analysis helps identify **where sales are coming from, which restaurants and categories perform best, and how order patterns change over time.**

---

# 🗂️ Dataset

The project uses a Swiggy food-delivery dataset containing restaurant, location, food, pricing, rating and date information.

### Main Columns

| Column            | Description                         |
| ----------------- | ----------------------------------- |
| `State`           | State where the restaurant operates |
| `City`            | City                                |
| `Order_Date`      | Order date                          |
| `Restaurant_Name` | Restaurant name                     |
| `Location`        | Restaurant location                 |
| `Category`        | Food category                       |
| `Dish_Name`       | Dish name                           |
| `Price_INR`       | Price in INR                        |
| `Rating`          | Restaurant/dish rating              |
| `Rating_Count`    | Number of ratings                   |

The SQL analysis contains **394,802 records** in the analyzed dataset.

---

# 🛠️ Tools & Technologies

| Tool       | Purpose                                     |
| ---------- | ------------------------------------------- |
| Python     | Data cleaning and exploratory data analysis |
| Pandas     | Data manipulation                           |
| NumPy      | Numerical analysis                          |
| Matplotlib | Data visualization                          |
| Seaborn    | Statistical visualization                   |
| Plotly     | Interactive charts                          |
| SQL Server | Database creation and analysis              |
| T-SQL      | Business queries                            |
| SSMS       | SQL development                             |
| Excel      | Pivot tables and dashboard                  |
| Power BI   | Interactive business dashboard              |
| GitHub     | Project documentation and version control   |

---

# 📁 Project Structure

```text
Swiggy-End-to-End-Data-Analytics/
│
├── 📂 Dataset/
│   └── Swiggy_Data.csv
│
├── 📂 Python/
│   └── Swiggy_Analysis.ipynb
│
├── 📂 SQL/
│   └── Swiggy_Analysis.sql
│
├── 📂 Excel/
│   └── Swiggy_Analysis.xlsx
│
├── 📂 Screenshots/
│   ├── Excel_Dashboard.png
│   ├── Python_Analysis.png
│   ├── SQL_Results.png
│
└── README.md
```

---

# 🔄 End-to-End Project Workflow

## Step 1 — Data Collection

The raw Swiggy CSV dataset is imported into the project.

```text
Swiggy_Data.csv
       ↓
Data Exploration
```

Initial checks include:

* Number of rows
* Number of columns
* Data types
* Missing values
* Duplicate records
* Unique values
* Numerical statistics

---

# 🐍 Step 2 — Python Data Cleaning

Python is used for initial data preparation.

### Import Libraries

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
```

### Load Dataset

```python
df = pd.read_csv("Swiggy_Data.csv")

df.head()
```

### Dataset Shape

```python
df.shape
```

### Dataset Information

```python
df.info()
```

### Missing Values

```python
df.isnull().sum()
```

### Duplicate Records

```python
df.duplicated().sum()
```

### Remove Duplicates

```python
df = df.drop_duplicates()
```

### Convert Date

```python
df["Order_Date"] = pd.to_datetime(df["Order_Date"])
```

### Convert Numeric Columns

```python
df["Price_INR"] = pd.to_numeric(
    df["Price_INR"],
    errors="coerce"
)

df["Rating"] = pd.to_numeric(
    df["Rating"],
    errors="coerce"
)

df["Rating_Count"] = pd.to_numeric(
    df["Rating_Count"],
    errors="coerce"
)
```

---

# 📅 Step 3 — Feature Engineering

Additional columns are created for analysis.

```python
df["Year"] = df["Order_Date"].dt.year

df["Month"] = df["Order_Date"].dt.month

df["Month_Name"] = df["Order_Date"].dt.month_name()

df["Quarter"] = df["Order_Date"].dt.quarter

df["Day_Name"] = df["Order_Date"].dt.day_name()
```

These columns are used for:

* Monthly analysis
* Quarterly analysis
* Yearly analysis
* Day-of-week analysis
* Trend analysis

---

# 📊 Step 4 — Python Exploratory Data Analysis

## Total Orders

```python
total_orders = len(df)

print(total_orders)
```

## Total Revenue

```python
total_revenue = df["Price_INR"].sum()

print(total_revenue)
```

## Average Price

```python
avg_price = df["Price_INR"].mean()

print(avg_price)
```

## Average Rating

```python
avg_rating = df["Rating"].mean()

print(avg_rating)
```

---

# 📈 Step 5 — Monthly Order Analysis

```python
monthly_orders = (
    df.groupby(["Year", "Month", "Month_Name"])
      .size()
      .reset_index(name="Total_Orders")
      .sort_values(["Year", "Month"])
)

monthly_orders
```

Visualization:

```python
plt.figure(figsize=(12,6))

plt.plot(
    monthly_orders["Month_Name"],
    monthly_orders["Total_Orders"],
    marker="o"
)

plt.title("Monthly Order Trend")

plt.xlabel("Month")

plt.ylabel("Total Orders")

plt.xticks(rotation=45)

plt.show()
```

---

# 🏙️ Step 6 — City Analysis

```python
city_orders = (
    df.groupby("City")
      .size()
      .sort_values(ascending=False)
      .head(10)
)

city_orders
```

Visualization:

```python
city_orders.sort_values().plot(
    kind="barh",
    figsize=(10,6)
)

plt.title("Top 10 Cities by Orders")

plt.xlabel("Orders")

plt.ylabel("City")

plt.show()
```

---

# 🗺️ Step 7 — State Revenue Analysis

```python
state_revenue = (
    df.groupby("State")["Price_INR"]
      .sum()
      .sort_values(ascending=False)
      .head(10)
)

state_revenue
```

Visualization:

```python
state_revenue.sort_values().plot(
    kind="barh",
    figsize=(10,6)
)

plt.title("Top 10 States by Revenue")

plt.xlabel("Revenue (INR)")

plt.ylabel("State")

plt.show()
```

---

# 🍽️ Step 8 — Restaurant Analysis

```python
restaurant_revenue = (
    df.groupby("Restaurant_Name")["Price_INR"]
      .sum()
      .sort_values(ascending=False)
      .head(10)
)

restaurant_revenue
```

This identifies the restaurants generating the highest revenue.

---

# 🍕 Step 9 — Food Category Analysis

```python
category_orders = (
    df.groupby("Category")
      .size()
      .sort_values(ascending=False)
      .head(10)
)

category_orders
```

Visualization:

```python
category_orders.plot(
    kind="bar",
    figsize=(12,6)
)

plt.title("Top Food Categories")

plt.xlabel("Category")

plt.ylabel("Orders")

plt.xticks(rotation=45)

plt.show()
```

---

# 🗄️ Step 10 — SQL Server Database

The cleaned Swiggy dataset is loaded into SQL Server.

```sql
CREATE DATABASE Swiggy_Analytics;

USE Swiggy_Analytics;
```

Raw data is stored in:

```text
swiggy_data
```

---

# 🧹 Step 11 — SQL Data Validation

NULL values are checked before analysis.

```sql
SELECT
    SUM(CASE WHEN State IS NULL THEN 1 ELSE 0 END) AS Null_State,
    SUM(CASE WHEN City IS NULL THEN 1 ELSE 0 END) AS Null_City,
    SUM(CASE WHEN Order_Date IS NULL THEN 1 ELSE 0 END) AS Null_Date,
    SUM(CASE WHEN Restaurant_Name IS NULL THEN 1 ELSE 0 END) AS Null_Restaurant,
    SUM(CASE WHEN Price_INR IS NULL THEN 1 ELSE 0 END) AS Null_Price,
    SUM(CASE WHEN Rating IS NULL THEN 1 ELSE 0 END) AS Null_Rating
FROM swiggy_data;
```

Duplicate records are identified using:

```sql
ROW_NUMBER()
```

Example:

```sql
WITH CTE AS
(
    SELECT *,
           ROW_NUMBER() OVER
           (
               PARTITION BY
                   State,
                   City,
                   Order_Date,
                   Restaurant_Name,
                   Location,
                   Category,
                   Dish_Name,
                   Price_INR,
                   Rating,
                   Rating_Count
               ORDER BY (SELECT NULL)
           ) AS rn
    FROM swiggy_data
)

DELETE FROM CTE
WHERE rn > 1;
```

---

# 🏗️ Step 12 — SQL Star Schema

The SQL database uses a **Star Schema**.

```text
                     dim_date
                        │
                        │
dim_location ── fact_swiggy_orders ── dim_restaurant
                        │
                        │
                  dim_category
                        │
                        │
                     dim_dish
```

### Dimension Tables

```text
dim_date
dim_location
dim_restaurant
dim_category
dim_dish
```

### Fact Table

```text
fact_swiggy_orders
```

The fact table stores:

* Price
* Rating
* Rating Count
* Date ID
* Location ID
* Restaurant ID
* Category ID
* Dish ID

---

# 📊 Step 13 — SQL KPI Analysis

## Total Orders

```sql
SELECT COUNT(*) AS Total_Orders
FROM fact_swiggy_orders;
```

### Result

```text
394,802 Orders
```

---

## 💰 Total Revenue

```sql
SELECT SUM(price_inr) AS Total_Revenue
FROM fact_swiggy_orders;
```

### Result

```text
₹106,005,480.94
```

---

## 💵 Average Price

```sql
SELECT AVG(price_inr) AS Average_Price
FROM fact_swiggy_orders;
```

### Result

```text
₹268.50
```

---

## ⭐ Average Rating

```sql
SELECT AVG(rating) AS Average_Rating
FROM fact_swiggy_orders;
```

### Result

```text
4.34
```

---

# 📅 Step 14 — Monthly Business Analysis

```sql
SELECT
    d.year,
    d.month,
    d.month_name,
    COUNT(*) AS total_orders
FROM fact_swiggy_orders f
JOIN dim_date d
    ON f.date_id = d.date_id
GROUP BY
    d.year,
    d.month,
    d.month_name
ORDER BY total_orders DESC;
```

### Key Finding

**January 2025** recorded the highest monthly order volume with approximately **50,786 orders**.

---

# 📆 Step 15 — Quarterly Analysis

```sql
SELECT
    d.year,
    d.quarter,
    COUNT(*) AS total_orders
FROM fact_swiggy_orders f
JOIN dim_date d
    ON f.date_id = d.date_id
GROUP BY
    d.year,
    d.quarter
ORDER BY total_orders DESC;
```

### Key Finding

**Q2 2025** recorded the highest order volume with **148,308 orders**.

---

# 📍 Step 16 — Top Cities

```sql
SELECT TOP 10
    l.city,
    COUNT(*) AS total_orders
FROM fact_swiggy_orders f
JOIN dim_location l
    ON f.location_id = l.location_id
GROUP BY l.city
ORDER BY total_orders DESC;
```

### Top City

```text
Bengaluru → 40,144 orders
```

Other high-volume cities include:

* Mumbai
* Hyderabad
* Jaipur
* Lucknow
* New Delhi
* Ahmedabad
* Chandigarh
* Kolkata
* Chennai

---

# 🗺️ Step 17 — State Revenue Analysis

```sql
SELECT TOP 10
    l.state,
    SUM(f.price_inr) AS total_revenue
FROM fact_swiggy_orders f
JOIN dim_location l
    ON f.location_id = l.location_id
GROUP BY l.state
ORDER BY total_revenue DESC;
```

The analysis identifies **Karnataka** as the highest-revenue state in the current SQL results.

---

# 🍽️ Step 18 — Top Restaurants

```sql
SELECT TOP 10
    r.restaurant_name,
    SUM(f.price_inr) AS total_revenue
FROM fact_swiggy_orders f
JOIN dim_restaurant r
    ON f.restaurant_id = r.restaurant_id
GROUP BY r.restaurant_name
ORDER BY total_revenue DESC;
```

### Top Revenue-Generating Restaurants

```text
1. KFC
2. McDonald's
3. Pizza Hut
4. Burger King
5. Domino's Pizza
6. Olio - The Wood Fired Pizzeria
7. LunchBox - Meals and Thalis
8. Baskin Robbins
9. Faasos
10. The Good Bowl
```

---

# 📊 Step 19 — Excel Dashboard

The same dataset is analyzed in Microsoft Excel using:

* Data Cleaning
* Pivot Tables
* Pivot Charts
* Slicers
* KPI Cards
* Conditional Formatting

### Excel Dashboard KPIs

```text
Total Orders
Total Revenue
Average Price
Average Rating
Top City
Top Restaurant
```

### Excel Charts

```text
Monthly Order Trend
Revenue by State
Top 10 Cities
Top Restaurants
Food Category Distribution
Rating Analysis
```

# 🎯 Business Questions

The project answers the following business questions:

### Sales

1. What is the total revenue?
2. How many orders were recorded?
3. What is the average price?
4. Which month has the highest order volume?
5. Which quarter performs best?

### Geography

6. Which city has the highest number of orders?
7. Which state generates the most revenue?
8. What are the top 10 cities?
9. What are the top-performing states?

### Restaurants

10. Which restaurants generate the highest revenue?
11. Which restaurants have the highest ratings?
12. Which restaurants have the highest rating counts?

### Food Categories

13. Which category receives the most orders?
14. Which category generates the most revenue?
15. Which categories have the highest average price?

### Trends

16. Which day of the week has the most orders?
17. Which month generates the highest revenue?
18. Which quarter has the highest order volume?
19. How does order volume change over time?
20. Which locations contribute most to overall business performance?

---

# 💡 Key Business Insights

Based on the current SQL analysis:

### 📦 Order Volume

The dataset contains approximately **394.8K orders**.

### 💰 Revenue

The analyzed records generate approximately **₹106.0M** in total price value.

### ⭐ Customer Ratings

The average rating is approximately **4.34**, indicating strong overall ratings in the analyzed data.

### 🏙️ City Performance

**Bengaluru** is the leading city by order volume with approximately **40K orders**.

### 🗺️ State Performance

**Karnataka** is the leading state by revenue in the current SQL analysis.

### 🍗 Restaurant Performance

**KFC** is the leading restaurant by revenue in the current SQL results.

### 📅 Monthly Performance

**January 2025** recorded the highest number of orders.

### 📆 Quarterly Performance

**Q2 2025** recorded the highest quarterly order volume.

---

# 📸 Project Screenshots

Add your dashboard screenshots here after uploading them to GitHub.

## Python Analysis


<img width="1505" height="711" alt="image" src="https://github.com/user-attachments/assets/32337511-0fdc-4b60-afc5-515629ca454b" />

<img width="1500" height="662" alt="image" src="https://github.com/user-attachments/assets/3c1cecf3-1a1d-4adc-8e22-05baf6a2bb14" />

<img width="1506" height="667" alt="image" src="https://github.com/user-attachments/assets/68e13a9c-1b03-43bc-98a7-3ebec133a4bb" />


## SQL Analysis

<img width="1491" height="672" alt="image" src="https://github.com/user-attachments/assets/436c4d68-677c-4afb-bbf7-4e9e48b5a2f6" />

<img width="1506" height="697" alt="image" src="https://github.com/user-attachments/assets/3678cc3b-1a7f-4f6a-a5fd-3c1400837a8c" />

<img width="1450" height="650" alt="image" src="https://github.com/user-attachments/assets/07359fe8-b628-4870-a7f7-ed14bda5ab20" />

<img width="1816" height="422" alt="image" src="https://github.com/user-attachments/assets/b38a45e0-5a63-43bf-8e79-cef65c1b7aaf" />

## Excel Dashboard

<img width="1121" height="812" alt="image" src="https://github.com/user-attachments/assets/61534294-a2a2-4b51-b082-caa39654f8c8" />

```markdown

```

---

# 📌 Skills Demonstrated

### Data Analytics

* Data Cleaning
* Data Validation
* Exploratory Data Analysis
* KPI Analysis
* Business Analysis
* Data Visualization
* Trend Analysis

### Python

* Pandas
* NumPy
* Matplotlib
* Seaborn
* Plotly
* Jupyter Notebook

### SQL

* SELECT
* WHERE
* GROUP BY
* HAVING
* ORDER BY
* JOINs
* CTEs
* CASE
* Aggregate Functions
* Window Functions
* ROW_NUMBER()
* Star Schema
* Fact & Dimension Tables

### Excel

* Pivot Tables
* Pivot Charts
* Slicers
* KPI Cards
* Conditional Formatting
* Dashboard Design

---

# 🧠 End-to-End Architecture

```text
                 SWIGGY RAW DATA
                        │
                        ▼
               DATA CLEANING
                        │
              ┌─────────┼─────────┐
              │         │         │
              ▼         ▼         ▼
           PYTHON     EXCEL      SQL
              │         │         │
              ▼         ▼         ▼
             EDA     PIVOTS    STAR SCHEMA
              │         │         │
              └─────────┼─────────┘
                        │
                        ▼
                BUSINESS KPIs
                        │
                        ▼
                FINAL INSIGHTS
```

---

# 🚀 Future Improvements

Future versions of the project can include:

* Customer-level analysis
* Delivery-time analysis
* Profitability analysis
* Discount analysis
* Customer segmentation
* RFM analysis
* Restaurant clustering
* Predictive sales forecasting
* Machine Learning
* Automated Power BI refresh
* Cloud database integration

---

# 📂 Related Projects

This project combines the work from the following individual repositories:

### 🗄️ SQL Project

[Swiggy SQL Project](https://github.com/stej07033/Swiggy_Sql_Project)

### 📊 Excel Project

[Swiggy Excel Project](https://github.com/stej07033/Swiggy_Excel)

### 🐍 Python Project

[Swiggy Python Project](https://github.com/stej07033/Swiggy_python_project)

---

# 👨‍💻 Author

**Sai M**

Aspiring Data Analyst

### Skills

```text
Python | SQL | Excel | Power BI | Pandas | NumPy
Data Cleaning | EDA | Data Visualization | Business Analytics
```

---

# ⭐ If You Like This Project

If you find this project useful, feel free to ⭐ star the repository and connect with me on LinkedIn.

---

## 📜 Disclaimer

This project is created for **educational and portfolio purposes**. The analysis is based on the available dataset and does not represent official Swiggy business data or internal Swiggy performance.

**Linkdin : https://www.linkedin.com/posts/madanapalli-sai-19b835389_best-free-certificate-courses-online-2025-activity-7490432956604268544-Asln?utm_source=share&utm_medium=member_android&rcm=ACoAAF-yhccBFOBRwPFDl9PAbb7jDVPGHyD_Tsc
**Github  :https://github.com/stej07033
