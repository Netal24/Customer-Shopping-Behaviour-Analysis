# Customer Shopping Behavior Analysis Dashboard

## Project Overview
This project focuses on analyzing customer shopping behavior using Python, Pandas, MySQL, and Power BI. The dataset is cleaned, transformed, and visualized through an interactive dashboard to generate meaningful business insights.

The main objectives of this project are:
- Understand customer purchasing behavior
- Analyze sales and shopping trends
- Identify high-performing product categories
- Study customer demographics
- Create interactive dashboards for business decision-making

---

# Technologies Used

- Python
- Pandas
- NumPy
- MySQL
- SQLAlchemy
- Power BI
- Jupyter Notebook

---

# Dataset Information

Dataset Used:
`customer_shopping_behavior.csv`

The dataset contains customer shopping information such as:
- Customer Age
- Gender
- Product Category
- Purchase Amount
- Review Ratings
- Frequency of Purchases
- Discount Applied
- Subscription Status
- Payment Method
- Shipping Type
- Seasonal Purchases
- And more...

---

# Python Data Preprocessing

The dataset was cleaned and transformed using Python and Pandas before visualization in Power BI.

---

## 1. Importing Required Libraries

```python
import pandas as pd
import mysql.connector
from sqlalchemy import create_engine
```

### Explanation

- `pandas` → Used for data manipulation and analysis
- `mysql.connector` → Connects Python with MySQL
- `create_engine` → Creates SQLAlchemy connection for database export

---

## 2. Loading the Dataset

```python
df = pd.read_csv('customer_shopping_behavior.csv')
```

### Explanation

- Reads the CSV file into a Pandas DataFrame
- `df` stores the dataset in tabular form

---

## 3. Data Exploration

```python
df.head()
df.info()
df.describe()
```

### Explanation

### `df.head()`
Displays first 5 rows of dataset.

### `df.info()`
Shows:
- Column names
- Data types
- Missing values

### `df.describe()`
Generates statistical summary:
- Mean
- Min/Max
- Standard deviation
- Quartiles

---

## 4. Standardizing Column Names

```python
df.columns = df.columns.str.lower()
df.columns = df.columns.str.replace(' ', '_')
```

### Explanation

- Converts column names to lowercase
- Replaces spaces with underscores

Example:

```python
Purchase Amount → purchase_amount
```

Benefits:
- Cleaner naming
- Easier SQL queries
- Easier coding

---

## 5. Handling Missing Values

```python
df['review_rating'] = df.groupby('category')['review_rating'] \
                        .transform(lambda x: x.fillna(x.median()))
```

### Explanation

- Groups data by category
- Fills missing review ratings using category median

Purpose:
- Prevent data loss
- Maintain category-level accuracy

---

## 6. Creating Age Groups

```python
labels = ['Youth Adult', 'Adult', 'Middle-Age', 'Senior']

df['age_group'] = pd.qcut(df['age'], q=4, labels=labels)
```

### Explanation

- Divides customers into 4 age categories
- Helps demographic analysis

Generated groups:
- Youth Adult
- Adult
- Middle-Age
- Senior

---

## 7. Converting Purchase Frequency

```python
purchase_frequency_mapping = {
    'Fortnightly': 14,
    'Weekly': 7,
    'Annually': 365,
    'Quarterly': 90,
    'Bi-Weekly': 14,
    'Monthly': 30,
    'Every 3 Months': 90
}

df['purchase_frequency_days'] = df['frequency_of_purchases'].map(
    purchase_frequency_mapping
)
```

### Explanation

Converts textual purchase frequency into numerical days.

| Frequency | Days |
|-----------|------|
| Weekly | 7 |
| Monthly | 30 |
| Quarterly | 90 |
| Annually | 365 |

Purpose:
- Numerical analysis
- Better dashboard calculations

---

## 8. Removing Redundant Columns

```python
df = df.drop('promo_code_used', axis=1)
```

### Explanation

- Removes unnecessary columns
- Reduces redundancy
- Improves dataset quality

---

## 9. Connecting Python with MySQL

```python
conn = mysql.connector.connect(
    host='localhost',
    user='root',
    password='root',
    database='customer_behaviour'
)
```

### Explanation

Creates connection between:
- Python
- MySQL database

Used for:
- Data storage
- SQL querying
- Power BI integration

---

## 10. Exporting Data to MySQL

```python
engine = create_engine(
    'mysql+mysqlconnector://root:root@localhost/customer_behaviour'
)

df.to_sql('customer_data', engine, if_exists='replace', index=False)
```

### Explanation

### `create_engine()`
Creates SQLAlchemy engine.

### `to_sql()`
Exports cleaned DataFrame into MySQL table.

Parameters:
- `replace` → Replaces existing table
- `index=False` → Prevents index column export

---

# Power BI Dashboard

The cleaned dataset is visualized in Power BI to generate business insights.

---

# Dashboard Features

## Customer Demographics
- Age group distribution
- Gender analysis
- Subscription analysis

## Sales Analysis
- Total sales overview
- Category-wise sales
- Seasonal trends
- Average purchase amount

## Customer Behavior Analysis
- Purchase frequency trends
- Discount usage analysis
- Payment method analysis
- Shipping preference trends

## Product Performance
- Best-selling categories
- High-rated categories
- Revenue contribution by category

---

# Dashboard Visualizations

The dashboard includes:
- KPI Cards
- Bar Charts
- Pie Charts
- Donut Charts
- Line Charts
- Filters and Slicers
- Interactive Visual Analysis

---

# Business Insights Generated

The dashboard helps businesses:
- Understand customer behavior
- Improve marketing strategies
- Identify profitable products
- Analyze seasonal demand
- Enhance customer retention
- Make data-driven decisions

---

# Future Improvements

Possible future enhancements:
- Real-time dashboard integration
- Customer segmentation
- Machine learning models
- Sales forecasting
- Recommendation systems
- Predictive analytics

---

# Dashboard Preview

The dashboard provides a complete overview of customer shopping trends, purchasing behavior, and sales performance using interactive visual analytics.

---

# Author

Developed as part of a Customer Shopping Behavior Analysis project using Python, MySQL, and Power BI.
