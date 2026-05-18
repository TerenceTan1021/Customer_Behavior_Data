# Customer Shopping Behavior Analysis

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0-red.svg)](https://pandas.pydata.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-blue.svg)](https://www.postgresql.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

## How to run

1. pip install pandas psycopg2-binary sqlalchemy jupyter
2. CREATE DATABASE customer_behavior;
3. username = 'your_username'
   password = 'your_password'
4. jupyter notebook Project_1_Employee/Cus_Shopping_Behv.ipynb
5. psql -d customer_behavior -f database_setup.sql
## Project Overview

This project analyzes customer shopping behavior using a dataset of **3,900 transactions**. The work includes data cleaning, feature engineering, loading into PostgreSQL, and extracting business insights through SQL queries.

**Key skills demonstrated:** Data cleaning (pandas), feature engineering, PostgreSQL integration, SQL for business intelligence, customer segmentation.

## Objectives

- Clean and standardize raw customer transaction data
- Handle missing values using category-based median imputation
- Create new features (`age_group`, `purchase_frequency_days`)
- Load processed data into PostgreSQL database
- Answer business questions using SQL (revenue by gender, discount effectiveness, product performance, customer segmentation)

## Dataset Description

The dataset contains **3,900 rows** (2,652 male, 1,248 female customers) and **19 columns** after processing:

| Column | Description |
|--------|-------------|
| `customer_id` | Unique customer identifier |
| `age` | Customer age (18-70) |
| `gender` | Male / Female |
| `item_purchased` | Name of product purchased (25 unique items) |
| `category` | Clothing, Footwear, Accessories, Outerwear |
| `purchase_amount_usd` | Transaction amount ($20-$100) |
| `location` | U.S. state (50 states) |
| `size` | S, M, L, XL |
| `color` | Product color (25 unique colors) |
| `season` | Spring, Summer, Fall, Winter |
| `review_rating` | Customer rating (2.5-5.0) |
| `subscription_status` | Yes / No |
| `shipping_type` | Express, Free Shipping, Next Day Air, Standard, Store Pickup, 2-Day Shipping |
| `discount_applied` | Yes / No |
| `previous_purchases` | Number of prior purchases (1-50) |
| `payment_method` | Venmo, Cash, Credit Card, PayPal, Debit Card, Bank Transfer |
| `frequency_of_purchases` | Weekly, Fortnightly, Monthly, Quarterly, Annually, Every 3 Months, Bi-Weekly |
| `age_group` | Teen, Young Adult, Adult, Middle-aged, Senior (engineered) |
| `purchase_frequency_days` | Days between purchases (engineered from frequency) |

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3.10 | Data cleaning & transformation |
| Pandas | Data manipulation |
| Jupyter Notebook | Interactive development |
| PostgreSQL | Data warehousing & SQL analysis |
| SQLAlchemy + psycopg2 | Database connection |


## Data Processing Steps (Jupyter Notebook)

### 1. Initial Data Inspection
- Loaded CSV with 3,900 rows and 18 columns
- Identified 37 missing values in `review_rating`

### 2. Missing Value Handling
```python
# Filled missing review ratings with category median (unbiased approach)
df['review_rating'] = df.groupby('category')['review_rating'].transform(lambda x: x.fillna(x.median()))

