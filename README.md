# 🏡 Airbnb NYC Data Analysis Project

## Project 📌 Overview

**Project Title**: Airbnb Analysis Report  
**Level**: Intermediate  
**Database**: `Airbnb_Open_Data`

This project is designed to demonstrate python skills and techniques typically used by data analysts to explore, clean, and analyze Airbnb Analysis data. The project involves setting up a Airbnb open database, performing exploratory data analysis (EDA), and answering specific business questions through pyhton Libraries. This project is ideal for those who are starting their journey in data analysis and want to build a solid foundation in Pyhton in Data Analytics.

## Objectives

1. **Set up a Airbnb Open database**: Create and populate a Airbnb Booking database with the provided Aiebnb_open data.
2. **Data Cleaning**: Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis**: Use python to answer specific business questions and derive insights from the Airbnb data.

## Project Structure

### 1. Database Setup

- **Download Dataset**: The project starts by download a database  `Airbnb_open_data`.
  
#2  first we import a library to perform on data
-  import pandas as pd
-  import numpy as np
- import seaborn as sns
- import matplotlib.pyplot as plt

📊 Technologies Used

- Python (Pandas, NumPy, Matplotlib, Seaborn)
- Jupyter Notebook

📂 Dataset

- Source: Inside Airbnb Open Data
- Format: CSV file (~50,000+ records)
- Key columns: price, neighbourhood, room_type, reviews_per_month, last_review, etc.


🧹 Data Cleaning

- Converted last_review to datetime format
- Replaced missing values in key columns like reviews_per_month and last_review
- Dropped irrelevant or sparse columns (license, house_rules)
- Converted price and service fee from string to float
- Removed duplicates


```pyhton
# now we checking we a column data type and if some column have not data type are correct 
# first we correct it data type

df['last review'] = pd.to_datetime(df['last review'], errors = 'coerce')

# we use errors ='coerce' iska mtlv hota hai ki yaha pai missing vlaue ho yeah uski 
# jagah NaN fill krde meaning (Not a Number) isse humko easy hoga data pai performing krne le liyea

**  Now we fill something in missing vlaue in columns

df.fillna({'reviews per month' : 0, 'last review' : df['last review'].min()}, inplace=True)

# Now we drop a missing value in least number of missing value in column
# hum usme se missing value ko hatayenge jisme se missing value kam ho

 ** df.dropna(subset = ['NAME', 'host name'], inplace=True)

# now we delete a column thats does not need to a column

** df = df.drop(columns=['license', 'house_rules'], errors='ignore')

# remove dollar signs and convert to float
 ** df['price'] = df['price'].replace('[\$,]', '', regex=True).astype(float)
** df['service fee'] = df['service fee'].replace('[\$,]', '', regex=True).astype(float)

# Now we remove All duplicate in this this is very good thing to performing a data

 ** df.drop_duplicates(inplace = True)

```

🔍 Exploratory Data Analysis (EDA)

### 3. Data Analysis & Visualization

The following pyhton query  were developed to answer specific business questions:

1. **# what is the distribution of listing prices?
```pyhton
plt.figure(figsize=(10,5))
sns.histplot(df['price'], bins=50, kde=True, color='red')
sns.title('Distribution of listing price')
sns.xtitle('price')
sns.ytitle('Frequency')
plt.show()
```
- Most listings are under $1200
- Wide range with a long right tail

2. **# how are different room types distributed?:
```pyhton
plt.figure(figsize=(10,5))
sns.countplot(x = 'room type', data = df, color='skyblue')
plt.title('room type distribution')
plt.xlabel('Room Type')
plt.ylabel('Count')
plt.show()
```
- Entire home/apartment dominates
- Private room is the next most common
- Shared rooms and hotel rooms are minimal

3. **# How are listings distributed across different neighborhoods?**:
```python
plt.figure(figsize=(12,8))
sns.countplot(y= 'neighbourhood group', data=df, color='lightpink', order=df['neighbourhood group'].value_counts().index)
plt.title('Number of listing By Neighbourhood froup')
plt.xlabel('Count')
plt.ylabel('Neighbourhood group')
plt.show()
```
- Manhattan and Brooklyn lead in listing volume
- Queens is third
- Bronx and Staten Island have fewer listings

4. **# what is relationship Between price and room type ?**:
```python
plt.figure(figsize=(10,5))

sns.boxplot(x='room type', y='price', hue='room type', data=df, palette='coolwarm')
plt.title('Price Vs Room Type')
plt.xlabel('Room Type')
plt.ylabel('Price ($)')
plt.show()
```
- Shared rooms are the cheapest
- Entire homes and hotel rooms are higher priced

5. ** how has the number of reviews change over with time?**:
```pyhton
df['last review'] =  pd.to_datetime(df['last review'])
reviews_over_time = df.groupby(df['last review'].dt.to_period('M')).size()

plt.figure(figsize=(10,5))
reviews_over_time.plot(kind='line', color='yellow')
plt.title('Review change Over Time')
plt.xlabel('Date')
plt.ylabel('Number of Reviews')
plt.show()
```
- 2019 saw the highest activity
- Sharp decline post-2020, likely due to COVID-19

## Findings

- **Customer Demographics**: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **High-Value Transactions**: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- **Sales Trends**: Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights**: The analysis identifies the top-spending customers and the most popular product categories.

## Reports

- **Data Summary**: A detailed report summarizing total Booking, customer demographics, and category performance.
- **Trend Analysis**: Insights into sales trends across different months and shifts.
- **Customer Insights**: Reports on top customers and unique customer counts per category.

## Conclusion

This project presents a comprehensive exploratory data analysis of Airbnb listings in New York City. By cleaning the dataset, handling missing values, and visualizing key metrics, we uncovered meaningful insights into pricing trends, room type popularity, neighborhood distributions, and review patterns over time.

Key takeaways:

Manhattan and Brooklyn dominate Airbnb listings, reflecting their popularity among travelers.

Entire home/apartment listings are the most common and command higher prices.

Price ranges vary widely, but most listings are under $1200 per night.

Reviews spiked in 2019, offering clues to peak usage before the COVID-19 dip.

Room types and pricing are strongly correlated, with shared rooms being the most affordable.

This analysis not only helps hosts optimize pricing strategies but also assists potential travelers in identifying budget-friendly and popular areas. For data analysts, this project showcases proficiency in data cleaning, EDA, visualization, and storytelling — all critical skills for real-world analytical roles.

## How to Use

1. **Clone the Repository**: Clone this project repository from GitHub.
2. **Set Up the Database**: Run the pyhton scripts provided in the `Airbnb_open_data` file to create and populate the database.
3. **Run the Queries**: Use the pyhton Library provided in the `Airbnb_Analysis` file to perform your analysis.
4. **Explore and Modify**: Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.

## Author - jauwad jamal

This project is part of my portfolio, showcasing the pyhton/ Analytics skills essential for data analyst roles. If you have any questions, feedback, or would like to collaborate, feel free to get in touch!


