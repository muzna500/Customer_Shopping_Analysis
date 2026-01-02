# 📊 Customer Shopping Behavior Analysis

## 📌 Project Overview

This project analyzes customer purchasing behavior using transactional retail data from 3,900 individual purchases across multiple product categories.

The goal is to uncover spending trends, customer segments, product performance, and subscription behavior to support data-driven marketing, pricing, and retention strategies.

## Dataset Summary
- Total Records: 3,900
- Total Columns: 18

## Key Features
- Customer Demographics: Age, Gender, Location, Subscription Status
- Purchase Details: Item Purchased, Category, Purchase Amount, Season, Size, Color
- Shopping Behavior:
    - Discount Applied
    - Previous Purchases
    - Frequency of Purchases
    - Review Rating
    - Shipping Type

 ## Missing Data
 - 37 missing values in the Review Rating column

## Data Cleaning & Exploratory Data Analysis (Python)
Data preparation and exploration were performed using Python.

- Data Loading: Imported dataset using pandas
- Initial Exploration:
   - Used df.info() to understand structure
   - Used df.describe() for summary statistics
- Missing Value Handling:
   - Imputed missing values in the review_rating column using the median rating per product category
- Column Standardization:
   - Renamed columns to snake_case for readability and consistency
- Feature Engineering:
   - Created age_group by binning customer ages
   - Created purchase_frequency_days based on purchase behavior
 - Data Consistency Check:
    - Identified redundancy between discount_applied and promo_code_used
    - Dropped promo_code_used
- Database Integration:
   - Loaded cleaned dataset into PostgreSQL for SQL-based analysis

## Data Analysis Using SQL (PostgreSQL)
SQL queries were written to answer key business questions:

1. Revenue comparison by gender
2. Identification of high-spending customers who used discounts
3. Top 5 products by average review rating
4. Comparison of average purchase value by shipping type
5. Spending analysis of subscribers vs non-subscribers
6. Identification of discount-dependent products
7. Customer segmentation (New, Returning, Loyal)
8. Top 3 products per category
9. Relationship between repeat buyers and subscription status
10. Revenue contribution by age group

## Power BI Dashboard
An interactive Power BI dashboard was created to visualize insights, including:

- Revenue trends
- Customer segments
- Product performance
- Subscription behavior
- Discount usage patterns
  
📌 The dashboard enables stakeholders to quickly explore trends and make informed decisions.

## Business Recommendations
Based on the analysis, the following actions are recommended:

- Boost Subscriptions: Promote exclusive benefits for subscribers
- Customer Loyalty Programs: Reward repeat customers to convert them into loyal buyers
- Review Discount Strategy: Balance revenue growth with margin control
- Product Positioning: Highlight top-rated and best-selling products
- Targeted Marketing: Focus campaigns on high-revenue age groups and express-shipping users

## Tools & Technologies

- Python (pandas, numpy)
- PostgreSQL
- SQL
- Power BI
- Jupyter Notebook

## Learning Outcome
This project strengthened skills in:

- Data cleaning & preprocessing
- SQL querying for business insights
- Customer segmentation
- Dashboard creation
- Translating data insights into actionable business recommendations











