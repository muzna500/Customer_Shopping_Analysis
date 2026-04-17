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
```sql
    SELECT gender, SUM(purchase_amount) AS revenue
    FROM customer
    GROUP BY gender
    ORDER BY revenue DESC

2. Identification of high-spending customers who used discounts
```sql
    SELECT customer_id,purchase_amount
    FROM customer
    WHERE discount_applied ='Yes' AND purchase_amount>= (SELECT AVG(purchase_amount) FROM customer)

3. Top 5 products by average review rating
```sql
    SELECT item_purchased , ROUND(AVG(review_rating:: numeric),2) AS avg_review
    FROM customer
    GROUP BY item_purchased
    ORDER BY avg_review DESC
    LIMIT 5

4. Comparison of average purchase value by shipping type
```sql
    SELECT shipping_type, ROUND(AVG(purchase_amount),2) AS average_amount
    FROM customer
    WHERE shipping_type IN ('Standard', 'Express')
    GROUP BY shipping_type
    ORDER BY average_amount DESC

5. Spending analysis of subscribers vs non-subscribers
```sql
    SELECT subscription_status, 
    COUNT(customer_id) AS total_customers,
    ROUND(AVG(purchase_amount),2) AS average_spend,
    SUM(purchase_amount) AS total_revenue
    FROM customer
    GROUP BY subscription_status
    ORDER BY average_spend, total_revenue DESC

6. Identification of discount-dependent products
```sql
    SELECT item_purchased,
    ROUND(100 * SUM(CASE WHEN discount_applied ='Yes' THEN 1 ELSE 0 END)/COUNT(*),2)AS discount_rate
    FROM customer
    GROUP BY item_purchased
    ORDER BY discount_rate DESC
    LIMIT 5;

7. Customer segmentation (New, Returning, Loyal)
```sql
    WITH customer_type AS (
    SELECT customer_id, previous_purchases,
    CASE 
	    WHEN previous_purchases = 1 THEN 'New'
	    WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
	    ELSE 'Loyal'
	    END AS customer_segment
    FROM customer
    )

    SELECT customer_segment, COUNT(*) AS "Number of Customers"
    FROM customer_type
    GROUP BY customer_segment

8. Top 3 products per category
```sql
    WITH item_counts AS (
    SELECT category,
    item_purchased,
    COUNT(customer_id) AS total_orders,
    ROW_NUMBER() OVER(partition by category order by count(customer_id) DESC) AS item_rank
    FROM customer
    GROUP BY category, item_purchased
    )

    SELECT item_rank, category, item_purchased, total_orders
    FROM item_counts
    WHERE item_rank <= 3
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











