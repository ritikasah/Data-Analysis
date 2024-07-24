# Amazon Sales Report Analysis

## Introduction
This project involves analyzing sales data from Amazon to gain insights into customer behavior, sales distribution across different states, and product demand. The analysis is performed using various Python libraries for data manipulation, visualization, and statistical analysis.

## Prerequisites
To run the code in this project, you need to have Python installed along with the following libraries:
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Installation

### You can install the required libraries using pip:
``` pip install pandas numpy matplotlib seaborn ```

## Dataset
The dataset used in this analysis contains information about Amazon sales, including order dates, ship dates, order IDs, product IDs, customer information, product categories, sales amounts, and shipping states.

## Analysis Steps
### 1. Data Loading
The dataset is loaded into a Pandas DataFrame for analysis.
```import pandas as pd
df = pd.read_csv('amazon_sales.csv')```

### 2. Data Cleaning
The data is cleaned by handling missing values, converting data types, and extracting relevant columns.
``` # Dropping rows with missing values
df.dropna(inplace=True)
# Converting date columns to datetime format
df['order-date'] = pd.to_datetime(df['order-date'])
df['ship-date'] = pd.to_datetime(df['ship-date'])
```

### 3. Data Analysis
Various analyses are performed to understand sales trends and customer behavior.

a. Monthly Sales Trend
A line plot is created to visualize the sales trend over time.
```
import matplotlib.pyplot as plt

df['month'] = df['order-date'].dt.to_period('M')
monthly_sales = df.groupby('month')['sales'].sum()

plt.figure(figsize=(12,6))
monthly_sales.plot(kind='line')
plt.title('Monthly Sales Trend')
plt.xlabel('Month')
plt.ylabel('Sales')
plt.show()
```

b. Top Products
The top-selling products are identified by calculating the total sales for each product.
```
top_products = df.groupby('product-id')['sales'].sum().nlargest(10)

plt.figure(figsize=(12,6))
top_products.plot(kind='bar')
plt.title('Top 10 Products by Sales')
plt.xlabel('Product ID')
plt.ylabel('Sales')
plt.show()
```

c. Sales Distribution by State
A bar plot is created to show the distribution of sales across different states.
```
import seaborn as sns

top_states = df['ship-state'].value_counts().head(10)

plt.figure(figsize=(12,6))
sns.countplot(x='ship-state', data=df[df['ship-state'].isin(top_states.index)])
plt.title('Sales Distribution by State')
plt.xlabel('State')
plt.ylabel('Count')
plt.xticks(rotation=90)
plt.show()
```
## 4. Observations and Conclusion
The following observations are made from the analysis:

* Most buyers are from Maharashtra.
* T-shirts in M-size are in high demand.
* The business has a significant impact on customers in Maharashtra and mainly serves retailers.
  
## Conclusion
This analysis provides valuable insights into the sales performance and customer behavior of the business on Amazon. By understanding these trends, the business can make informed decisions to improve sales and customer satisfaction.

## Author
This analysis was performed by~
### Ritika Sah
