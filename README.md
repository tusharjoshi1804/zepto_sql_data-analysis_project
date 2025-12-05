# Zepto Inventory Data Analysis using SQL

This project focuses on analyzing Zepto product data using SQL.  
The data was cleaned, explored, and transformed into meaningful business insights.


## 📌 Project Overview

The aim of this project is to:

- Build a realistic inventory database
- Perform **Exploratory Data Analysis (EDA)**
- Clean raw data to remove invalid or unreadable values
- Solve **business-driven SQL questions** focused on discounts, revenue, inventory, and product performance

---

## Dataset Overview

The dataset was sourced from [Kaggle](https://www.kaggle.com/datasets/palvinder2006/zepto-inventory-dataset/data?select=zepto_v2.csv) and was originally scraped from Zepto’s official product listings. It mimics what we would typically encounter in a real-world e-commerce inventory system.

Each row represents a unique SKU (Stock Keeping Unit) for a product. Duplicate product names exist because the same product may appear multiple times in different package sizes, weights, discounts, or categories to improve visibility – exactly how real catalog data looks.


### Data Fields

- sku_id  
- name  
- category  
- mrp  
- discountPercent  
- discountedSellingPrice  
- availableQuantity  
- weightInGms  
- outOfStock  
- quantity  

Duplicate product names exist because the same product appears in **multiple sizes, weights, and discount combinations** — reflecting real catalog behavior.

---

## 🔧 Project Workflow

### 1️⃣ Database & Table Creation

```sql
CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);
---

2️⃣ Data Import
\copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv'
WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');


Encoding issues were solved by converting the CSV into UTF-8 format.

3️⃣ Data Exploration

-Total product count

-Sample preview

-NULL value checks

-Listing unique categories

-In-stock vs Out-of-stock comparison

-Duplicate product names → different SKUs

4️⃣ Data Cleaning
Issue Identified	Action Taken
Zero MRP or zero discounted price	Removed rows
Prices stored in paise	Converted to rupees (/100)
Duplicate names	Treated as multiple SKUs

5️⃣ Business Insights
 Found top 10 best-value products based on discount percentage

- Identified high-MRP products that are currently out of stock
- Estimated potential revenue for each product category
- Filtered expensive products (MRP > ₹500) with minimal discount
- Ranked top 5 categories offering highest average discounts
- Calculated price per gram to identify value-for-money products
- Grouped products based on weight into Low, Medium, and Bulk categories
- Measured total inventory weight per product category

