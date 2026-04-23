## 📊 Exploratory Data Analysis (EDA) Project

This project focuses on performing **Exploratory Data Analysis (EDA)** on a cleaned dataset to uncover patterns, trends, and insights using **Python** and **pandas**.

---

## 📌 Overview

After completing data cleaning in Project 1, this project analyzes the dataset to better understand its structure and extract meaningful insights. The goal is to transform raw data into actionable information through statistical analysis and visualization.

---

## 🎯 Objectives

* Perform descriptive statistical analysis
* Identify trends and patterns in the data
* Detect outliers and unusual observations
* Generate meaningful insights

---

## 🛠️ Tools Used

* Python
* Pandas
* NumPy
* Matplotlib

---

## 🔍 Analysis Performed

### 1. Descriptive Statistics

* Used `.describe()` to calculate mean, median, min, max, and count

### 2. Categorical Analysis

* Analyzed distributions of:

  * Payment methods
  * Order status
  * Top-selling products

### 3. Trend Analysis

* Examined monthly sales trends using date-based grouping

### 4. Outlier Detection

* Identified extreme values using the **IQR (Interquartile Range)** method

### 5. Data Visualization

* Histogram for sales distribution
* Bar chart for categorical variables
* Line chart for monthly sales trends

---

## 📈 Key Insights

* Identified the most commonly used payment method
* Determined the most frequent order status
* Found top-performing products
* Observed sales trends over time
* Detected outliers in high-value transactions

---

## 📁 Output

* Visualizations (charts)
* Statistical summaries
* Insights derived from the dataset

---

## 🚀 Conclusion

The EDA process provided a deeper understanding of the dataset by revealing patterns, trends, and anomalies. These insights form the foundation for further analysis, visualization, or predictive modeling.
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# -------------------------------
# 1. Load Dataset
# -------------------------------
df = pd.read_csv("/content/Dataset for Data Analytics - Sheet1.csv")

print("🔹 First 5 rows:\n", df.head())

# -------------------------------
# 2. Basic Statistics
# -------------------------------
print("\n🔹 Basic Statistics:\n")
print(df.describe())

# -------------------------------
# 3. Categorical Analysis
# -------------------------------
print("\n🔹 Payment Method Distribution:\n")
print(df['PaymentMethod'].value_counts())

print("\n🔹 Order Status Distribution:\n")
print(df['OrderStatus'].value_counts())

print("\n🔹 Top 10 Products:\n")
print(df['Product'].value_counts().head(10))

# -------------------------------
# 4. Time-Based Trend Analysis
# -------------------------------
df['Date'] = pd.to_datetime(df['Date'])
df['Month'] = df['Date'].dt.to_period('M')

monthly_sales = df.groupby('Month')['TotalPrice'].sum()

print("\n🔹 Monthly Sales Trend:\n")
print(monthly_sales)

# -------------------------------
# 5. Outlier Detection
# -------------------------------
Q1 = df['TotalPrice'].quantile(0.25)
Q3 = df['TotalPrice'].quantile(0.75)
IQR = Q3 - Q1

outliers = df[(df['TotalPrice'] < Q1 - 1.5 * IQR) | 
              (df['TotalPrice'] > Q3 + 1.5 * IQR)]

print("\n🔹 Number of Outliers:", len(outliers))

# -------------------------------
# 6. Data Visualization
# -------------------------------

# Histogram (Distribution)
plt.figure()
df['TotalPrice'].hist()
plt.title("Total Price Distribution")
plt.xlabel("Total Price")
plt.ylabel("Frequency")
plt.show()

# Bar chart (Payment Method)
plt.figure()
df['PaymentMethod'].value_counts().plot(kind='bar')
plt.title("Payment Method Distribution")
plt.xlabel("Payment Method")
plt.ylabel("Count")
plt.show()

# Monthly Sales Line Chart
plt.figure()
monthly_sales.plot(kind='line', marker='o')
plt.title("Monthly Sales Trend")
plt.xlabel("Month")
plt.ylabel("Total Sales")
plt.show()

# -------------------------------
# 7. Key Insights (Print)
# -------------------------------
print("\n🔹 KEY INSIGHTS:")

print("- Most used payment method:",
      df['PaymentMethod'].value_counts().idxmax())

print("- Most common order status:",
      df['OrderStatus'].value_counts().idxmax())

print("- Top selling product:",
      df['Product'].value_counts().idxmax())

print("- Total revenue:",
      df['TotalPrice'].sum())

print("- Average order value:",
      df['TotalPrice'].mean())

print("- Number of outliers detected:",
      len(outliers))
