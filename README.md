

## 🛍️ Zepto Inventory Data Analysis using SQL

This project focuses on analyzing **Zepto product data** using **SQL**. The data was meticulously cleaned, explored, and transformed into meaningful **business insights** to optimize inventory and sales strategy.

---

## 📌 Project Overview: Inventory Intelligence

The core objectives of this project were to:

* Build a **realistic inventory database** structure.
* Perform **Exploratory Data Analysis (EDA)** to understand data characteristics.
* Clean raw data to handle invalid or unreadable values.
* Solve **business-driven SQL questions** focused on **discounts, revenue, inventory, and product performance**.

---

## 📦 Dataset Overview

The dataset was sourced from **Kaggle** and was originally scraped from Zepto’s official product listings. It mimics a typical real-world e-commerce inventory system, providing a robust base for analysis.

* **Source:** [Kaggle](https://www.kaggle.com/datasets/palvinder2006/zepto-inventory-dataset/data?select=zepto_v2.csv)
* **Structure:** Each row represents a **unique SKU (Stock Keeping Unit)** for a product.

> **Note:** Duplicate product names exist because the same product may appear multiple times across different package sizes, weights, discounts, or categories to maximize visibility—a common reflection of real catalog data.

### Data Fields

| Field Name | Description |
| :--- | :--- |
| `sku_id` | Unique Identifier (Stock Keeping Unit) |
| `name` | Product Name |
| `category` | Product Category |
| `mrp` | Maximum Retail Price |
| `discountPercent` | Percentage discount offered |
| `discountedSellingPrice` | Final selling price after discount |
| `availableQuantity` | Stock count |
| `weightInGms` | Product weight in grams |
| `outOfStock` | Boolean flag (True/False) |
| `quantity` | Package quantity (e.g., number of units in a pack) |

---

## 🔧 Project Workflow & Execution

### 1️⃣ Database & Table Creation 

A PostgreSQL table was created to host the inventory data, ensuring proper data types and constraints.

---

### 2️⃣ Data Import

\copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv'
WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');


Encoding issues were solved by converting the CSV into UTF-8 format.

---

### 3️⃣ Data Exploration (EDA)

The initial phase focused on understanding the dataset's scope and quality through standard exploratory checks:

* **Total product count**
* **Sample preview** of the data
* **NULL value checks** across all columns
* Listing **unique categories**
* **In-stock vs. Out-of-stock** product comparison
* Analysis of **duplicate product names** corresponding to different SKUs

---

### 4️⃣ Data Cleaning and Transformation

| Issue Identified | Action Taken |
| :--- | :--- |
| **Zero MRP or zero discounted price** | Rows containing these values were **removed** as they represented unusable data points. |
| **Prices stored in paise** | Both `mrp` and `discountedSellingPrice` were **converted to rupees** by dividing by 100. |
| **Duplicate names** | These were **treated as multiple unique SKUs**, as they represented distinct product variants (e.g., different weights or sizes). |

---

### 5️⃣ Business Insights & SQL Query Results

A series of targeted SQL queries were executed to extract actionable business intelligence:

* Found **top 10 best-value products** based on the highest discount percentage.
* Identified **high-MRP products** that are currently **out of stock**, highlighting potential missed revenue opportunities.
* Estimated **potential revenue** for each product category (based on current stock and discounted price).
* Filtered **expensive products (MRP > ₹500)** with minimal discount to assess pricing strategy.
* Ranked **top 5 categories** offering the highest average discounts.
* Calculated **price per gram** to identify true value-for-money products.
* Grouped products based on weight into **Low, Medium, and Bulk categories** for logistics analysis.
* Measured **total inventory weight** per product category to optimize warehousing and shipping.


