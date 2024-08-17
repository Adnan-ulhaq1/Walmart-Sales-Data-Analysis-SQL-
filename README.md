 Walmart Sales Data Analysis

## About

This project explores Walmart Sales data to gain insights into branch performance, product sales trends, and customer behavior. The goal is to analyze how sales strategies can be improved and optimized. The dataset was sourced from the Kaggle Walmart Sales Forecasting Competition.

> "In this recruiting competition, job-seekers are provided with historical sales data for 45 Walmart stores located in different regions. Each store contains many departments, and participants must project the sales for each department in each store. To add to the challenge, selected holiday markdown events are included in the dataset. These markdowns are known to affect sales, but it is challenging to predict which departments are affected and the extent of the impact."

## Purposes of the Project

- Understand the factors affecting sales at different branches.
- Optimize sales strategies based on insights gained from data analysis.

## About the Data

The dataset from the Kaggle Walmart Sales Forecasting Competition includes sales transactions from three branches of Walmart in Mandalay, Yangon, and Naypyitaw. It contains 17 columns and 1000 rows:

| Column                  | Description                                | Data Type          |
|-------------------------|--------------------------------------------|--------------------|
| invoice_id              | Invoice ID of the sales made               | VARCHAR(30)        |
| branch                  | Branch where the sale was made             | VARCHAR(5)         |
| city                    | Location of the branch                     | VARCHAR(30)        |
| customer_type           | Type of customer                           | VARCHAR(30)        |
| gender                  | Gender of the customer                     | VARCHAR(10)        |
| product_line            | Product line of the product sold           | VARCHAR(100)       |
| unit_price              | Price of each product                      | DECIMAL(10, 2)     |
| quantity                | Quantity of the product sold               | INT                |
| VAT                     | Tax amount on the purchase                 | FLOAT(6, 4)        |
| total                   | Total cost of the purchase                 | DECIMAL(10, 2)     |
| date                    | Date of the purchase                       | DATE               |
| time                    | Time of the purchase                       | TIMESTAMP          |
| payment_method          | Payment method used                        | VARCHAR(15)        |
| cogs                    | Cost of Goods Sold                         | DECIMAL(10, 2)     |
| gross_margin_percentage | Gross margin percentage                    | FLOAT(11, 9)       |
| gross_income            | Gross Income                               | DECIMAL(10, 2)     |
| rating                  | Rating given by the customer               | FLOAT(2, 1)        |

## Analysis List

### Product Analysis
- Analyze different product lines and their performance.
- Identify product lines that need improvement.

### Sales Analysis
- Study sales trends and the effectiveness of sales strategies.
- Identify what modifications are needed to increase sales.

### Customer Analysis
- Segment customers and analyze purchase trends.
- Evaluate the profitability of different customer segments.

## Approach Used

### Data Wrangling
1. Inspect data to detect and handle NULL or missing values.
2. Create a database and tables, ensuring NO NULL constraints.
3. Perform feature engineering to enhance the dataset:
   - Add `time_of_day` to categorize sales into Morning, Afternoon, and Evening.
   - Add `day_name` to determine the busiest day of the week.
   - Add `month_name` to identify the month with the highest sales.

### Exploratory Data Analysis (EDA)
- Conduct analysis to answer specific business questions and objectives.

## Business Questions to Answer

### Generic
- How many unique cities does the data cover?
- In which city is each branch located?

### Product
- How many unique product lines are there?
- What is the most common payment method?
- Which product line generates the most revenue?
- What month has the largest COGS?

### Sales
- Number of sales made at each time of day per weekday.
- Which customer type brings in the most revenue?

### Customer
- How many unique customer types are there?
- What is the gender distribution per branch?
- Which time of the day do customers give the most ratings?

## Revenue and Profit Calculations

- **COGS** = unit_price * quantity
- **VAT** = 5% * COGS
- **Total (Gross Sales)** = VAT + COGS
- **Gross Profit (Gross Income)** = Total - COGS
- **Gross Margin Percentage** = (Gross Income / Total) * 100

**Example Calculation:**
- Unit Price: $45.79
- Quantity: 7
- COGS: $320.53
- VAT: $16.03
- Total: $336.56
- Gross Margin: 4.76%

## Code

**Database and Table Creation:**
```sql
-- Create database
CREATE DATABASE IF NOT EXISTS walmartSales;

-- Create table
CREATE TABLE IF NOT EXISTS sales (
    invoice_id VARCHAR(30) NOT NULL PRIMARY KEY,
    branch VARCHAR(5) NOT NULL,
    city VARCHAR(30) NOT NULL,
    customer_type VARCHAR(30) NOT NULL,
    gender VARCHAR(30) NOT NULL,
    product_line VARCHAR(100) NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    quantity INT NOT NULL,
    tax_pct FLOAT(6,4) NOT NULL,
    total DECIMAL(12, 4) NOT NULL,
    date DATETIME NOT NULL,
    time TIME NOT NULL,
    payment VARCHAR(15) NOT NULL,
    cogs DECIMAL(10,2) NOT NULL,
    gross_margin_pct FLOAT(11,9),
    gross_income DECIMAL(12, 4),
    rating FLOAT(2, 1)
);
```

For the full set of SQL queries and analysis, check the [SQL_queries.sql](SQL_queries.sql) file.
