# Home Sales Analysis with PySpark

## Overview

This project analyzes home sales data using PySpark SQL to uncover trends and key metrics for real estate insights. The analysis focuses on calculating various metrics, creating temporary views, caching data, partitioning, and querying a large dataset to understand trends, such as average home prices based on specific attributes.

## Project Requirements

The assignment involved the following tasks:

1. **Load and Explore the Data**: Load the data from a CSV file, examine its structure, and create a temporary view.
2. **Run SQL Queries**: Perform SQL queries to answer key questions related to average home prices, sales data trends, and filters based on attributes like bedrooms, bathrooms, view ratings, and square footage.
3. **Optimize Query Performance**:
   - Cache and uncache data for faster query execution.
   - Partition data by specific attributes to facilitate efficient data retrieval.
4. **Measure Query Runtime**: Measure and compare runtimes of queries on cached and uncached data to evaluate performance improvements.

## Key Steps

1. **Data Loading**:
   - Load the `home_sales_revised.csv` file from an AWS S3 bucket into a PySpark DataFrame.
   - Create a temporary view, `home_sales`, to facilitate SQL queries.

2. **SQL Queries**:
   - Calculate average home prices based on specific criteria, such as:
     - Four-bedroom homes sold each year.
     - Homes with three bedrooms and three bathrooms built in specific years.
     - Homes with specific attributes, like floors and square footage.
   - Calculate average price per "view" rating and filter for ratings with an average price of $350,000 or more.

3. **Caching and Partitioning**:
   - **Cache the Table**: Cache the `home_sales` table in memory to optimize subsequent queries.
   - **Partition the Data**: Save the data in Parquet format partitioned by the `date_built` column to improve data access and management.

4. **Performance Comparison**:
   - Measure query runtimes on cached, uncached, and partitioned data to evaluate performance differences.

## Output Summary

### 1. Average Price for Four-Bedroom Houses Sold Per Year

| Year Sold | Average Price |
|-----------|---------------|
| 2019      | $300,263.70   |
| 2020      | $298,353.78   |
| 2021      | $301,819.44   |
| 2022      | $296,363.88   |

- **Explanation**: The results show a relatively stable average price for four-bedroom houses over the years, with slight fluctuations. The highest average price was observed in 2021 at $301,819.44, suggesting potential factors that influenced market demand or price stability.

### 2. Average Price for Three-Bedroom, Three-Bathroom Houses by Year Built

| Year Built | Average Price |
|------------|---------------|
| 2010       | $292,859.62   |
| 2011       | $291,117.47   |
| 2012       | $293,683.19   |
| 2013       | $295,962.27   |
| 2014       | $290,852.27   |
| 2015       | $288,770.30   |
| 2016       | $290,555.07   |
| 2017       | $292,676.79   |

- **Explanation**: The average prices for three-bedroom, three-bathroom homes are relatively consistent across years, with minor fluctuations around $290,000–$295,000. This consistency may indicate a steady demand for homes with these specific attributes.

### 3. Average Price for Homes with Specific Attributes (3 Beds, 3 Baths, 2 Floors, ≥ 2,000 Sq Ft) by Year Built

| Year Built | Average Price |
|------------|---------------|
| 2010       | $285,010.22   |
| 2011       | $276,553.81   |
| 2012       | $307,539.97   |
| 2013       | $303,676.79   |
| 2014       | $298,264.72   |
| 2015       | $297,609.97   |
| 2016       | $293,965.10   |
| 2017       | $280,317.58   |

- **Explanation**: The data shows an increase in average price for homes with specified attributes between 2010 and 2012, peaking at $307,539.97. Afterward, the prices remain generally stable, indicating a possible balance of supply and demand for this home type.

### 4. Average Price per "View" Rating (with Average Price ≥ $350,000)

| View Rating | Average Price |
|-------------|---------------|
| 100         | $1,026,669.50 |
| 99          | $1,061,201.42 |
| 98          | $1,053,739.33 |
| 97          | $1,129,040.15 |
| 96          | $1,017,815.92 |
| ...         | ...           |

- **Explanation**: Higher "view" ratings correlate with significantly higher average prices, suggesting that homes with premium views attract higher market values. For example, a view rating of 97 corresponds to an average price of $1,129,040.15, indicating that buyers are willing to pay a premium for homes with highly-rated views.

### Cached vs. Uncached Runtime Comparison

- **Uncached Runtime**: ~0.22 seconds
- **Cached Runtime**: ~0.12 seconds

- **Explanation**: Caching the data improved query performance, reducing the runtime from 0.21 seconds to 0.12 seconds. This highlights the efficiency gains from caching, especially valuable when working with large datasets.

## Conclusion

This analysis demonstrates the effective use of PySpark for big data processing and optimization. The analysis revealed meaningful insights into average home prices based on different attributes, and the use of caching and partitioning improved query efficiency. For further analysis, additional partitioning strategies or machine learning models could provide deeper insights and predictive capabilities.
