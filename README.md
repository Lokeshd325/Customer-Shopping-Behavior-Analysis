# Customer Shopping Behavior Analysis

An end-to-end data analysis project exploring customer purchasing patterns, demographic segments, subscription behaviors, and product preferences using Python, PostgreSQL, and Power BI.

---

## 📌 Project Overview

This project analyzes transactional data from **3,900 customer purchases** across various product categories. By combining data manipulation in Python, query-based analysis in SQL, and dynamic visualization in Power BI, this project uncovers key insights to guide strategic retail decisions, optimize loyalty programs, and improve marketing targeting.

---

## 🔄 Project Workflow Architecture

```
[01 Business Problem] 
        │
        ▼ (Import data into Python)
[02 Data Modeling & EDA in Python] 
        │
        ▼ (Load to PostgreSQL)
[03 Data Analysis in SQL] 
        │
        ▼ (Connect to Power BI)
[04 Interactive Power BI Dashboard] 
        │
        ▼ (Summarize Findings)
[05 Project Report & Presentation] 
        │
        ▼ (Upload Files)
[06 GitHub Repository Published]
```

---

## 📊 Dataset Summary

* **Total Records:** 3,900 rows
* **Total Features:** 18 columns
* **Demographics:** Age, Gender, Location, Subscription Status
* **Purchase Attributes:** Item Purchased, Category, Purchase Amount ($), Season, Size, Color
* **Behavioral Attributes:** Discount Applied, Promo Code Used, Previous Purchases, Frequency of Purchases, Review Rating, Shipping Type, Payment Method

---

## 🛠️ Step 1: Exploratory Data Analysis (Python)

### Data Cleaning & Preprocessing
* **Exploration:** Checked structural types using `df.info()` and statistical summaries using `df.describe()`.
* **Missing Value Imputation:** Found 37 missing records in `Review Rating`; imputed missing values using the median rating of their respective product categories.
* **Column Standardization:** Transformed column names into lowercase/snake_case format for consistency across databases.
* **Feature Engineering:**
  * Created `age_group` bins (`Young Adult`, `Middle-aged`, `Adult`, `Senior`).
  * Calculated `purchase_frequency_days`.
* **Redundancy Clean-up:** Checked correlation between `discount_applied` and `promo_code_used`; dropped redundant `promo_code_used` column.
* **Database Export:** Connected Pandas to a PostgreSQL database instance and exported clean data tables.

---

## 🔍 Step 2: Data Analysis & Insights (SQL)

The following PostgreSQL queries were executed to resolve core business questions:

### 1. Revenue by Gender
```sql
SELECT 
    gender, 
    SUM(purchase_amount) AS revenue
FROM customer_behavior
GROUP BY gender;
```
* **Female:** \$75,191
* **Male:** \$157,890

### 2. High-Spending Discount Users
*Identified 839 customers who utilized discounts while maintaining spend levels above average.*
```sql
SELECT 
    customer_id, 
    purchase_amount
FROM customer_behavior
WHERE discount_applied = 'Yes' 
  AND purchase_amount > (SELECT AVG(purchase_amount) FROM customer_behavior);
```

### 3. Top 5 Products by Rating
| Rank | Item Purchased | Average Product Rating |
| :--- | :--- | :--- |
| 1 | Gloves | 3.86 |
| 2 | Sandals | 3.84 |
| 3 | Boots | 3.82 |
| 4 | Hat | 3.80 |
| 5 | Skirt | 3.78 |

### 4. Shipping Type Comparison
| Shipping Type | Average Spend ($) |
| :--- | :--- |
| Standard | \$58.46 |
| Express | \$60.48 |

### 5. Subscribers vs. Non-Subscribers
| Subscription Status | Total Customers | Avg Spend ($) | Total Revenue ($) |
| :--- | :--- | :--- | :--- |
| **Yes** | 1,053 | \$59.49 | \$62,645.00 |
| **No** | 2,847 | \$59.87 | \$170,436.00 |

### 6. Discount-Dependent Products (Top 5 Highest Discount Rates)
1. **Hat:** 50.00%
2. **Sneakers:** 49.66%
3. **Coat:** 49.01%
4. **Sweater:** 48.17%
5. **Pants:** 47.37%

### 7. Customer Segmentation
Customers segmented into levels based on past purchase history:
* **Loyal (>20 purchases):** 3,116 customers
* **Returning (2-20 purchases):** 701 customers
* **New (1 purchase):** 83 customers

### 8. Revenue Contribution by Age Group
| Age Group | Total Revenue ($) |
| :--- | :--- |
| **Young Adult** | \$62,143 |
| **Middle-aged** | \$59,197 |
| **Adult** | \$55,978 |
| **Senior** | \$55,763 |

---

## 📈 Step 3: Interactive Dashboard (Power BI)

An interactive visual report was created in Power BI highlighting Key Performance Indicators (KPIs) and breakdown slicers:

* **Key Metrics Cards:**
  * **Total Customers:** 3.9K
  * **Average Purchase Amount:** \$59.76
  * **Average Review Rating:** 3.75
* **Visual Breakdown Panels:**
  * `% of Customers by Subscription Status` (Donut Chart: 27% Yes / 73% No)
  * `Revenue & Sales Volume by Category` (Bar Charts: Clothing leading, followed by Accessories, Footwear, Outerwear)
  * `Revenue & Sales Volume by Age Group` (Horizontal Bar Charts)
  * `Interactive Slicers:` Filterable by Subscription Status, Gender, Category, and Shipping Type.

---

## 💡 Strategic Recommendations

1. **Boost Subscription Conversion:** Offer exclusive perks or tiered rewards for subscribers, as current subscription adoption sits at only 27%.
2. **Nurture Loyalty Segments:** Leverage high loyalty numbers (3,116 repeat shoppers) by establishing a dedicated VIP rewards track.
3. **Optimize Discount Strategies:** Review markdown strategies on high-discount items (e.g., Hats, Sneakers) to protect profit margins without reducing conversion rates.
4. **Targeted Campaigns:** Direct high-value marketing campaigns toward **Young Adults** and **Middle-aged** demographics who generate the highest overall revenue.

---

## 🛠️ Tools & Technologies Used
* **Data Processing & Cleaning:** Python (Pandas, NumPy)
* **Database & Querying:** PostgreSQL / SQL
* **Visualization:** Power BI
* **Presentation:** Gamma AI
* **Version Control:** Git & GitHub