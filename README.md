# Cleaning and Consolidating Multi-Source Sales Data

An end-to-end ETL and data transformation project built in Power BI using Power Query to clean, profile, validate, and consolidate multi-source sales data into an analysis-ready dataset.


## Overview

This project simulates a real-world business intelligence workflow using sales data from Adventure Works.
The objective was to transform fragmented raw Excel files into a reliable dataset suitable for reporting and analysis.

The workflow included:

- importing multiple data sources
- cleaning and transforming data
- profiling columns to identify anomalies
- validating data integrity
- appending historical datasets
- merging relational tables
- creating analytical measures and visualizations


## Problem

Sales data was distributed across multiple yearly files while transactional detail records contained inconsistencies and incomplete relational coverage.

The main challenges included:
- fragmented historical datasets
- unnecessary columns
- anomalous pricing values
- incomplete relationships between tables
- unreliable results after merging datasets


## Data Sources
```
Order2022Final.xlsx -	Historical sales orders for 2022
Order2023Final.xlsx -	Historical sales orders for 2023
OrderDetailsFinal -	Product-level transaction details
```

## Objectives
1. Clean and transform raw sales data
2. Detect and remove anomalies
3. Consolidate multiple yearly datasets
4. Validate data integrity after merging
5. Create business-ready metrics and visualizations



## ETL Workflow

  
### 1. Importing Data

Excel datasets were imported into Power BI using Power Query.


### 2. Data Cleaning

The OrderDetails dataset originally contained several unnecessary fields.

The following columns were retained:
- SalesOrderID
- ProductID
- OrderQty
- UnitPrice

Three anomalous rows were identified as likely manual-entry errors and removed from the dataset to avoid skewed calculations and inaccurate reporting.

Profiling metrics reviewed:
- minimum value
- maximum value
- mean value
- distribution patterns


### 3. Appending Historical Data

The Order2022 and Order2023 datasets were appended into a unified master table named Orders.

This created a consolidated historical sales dataset suitable for time-series analysis.

Then, OrderDetails was merged with Orders using an Inner Join on the column SalesOrderID.

The merge process exposed an important data integrity issue: A significant portion of 2023 order records did not have matching entries in OrderDetails.

As a result, using an Inner Join caused many valid sales records to be excluded from the final merged dataset.

This investigation became an important part of the project and highlighted the importance of validating relational coverage before building analytical models.


### 4. Data Integrity Findings

During validation, the merged dataset produced:
- lower-than-expected revenue totals
- inconsistent temporal sales trends
- missing sales coverage for 2023

Further investigation revealed that:
- Orders contained complete transactional totals through the TotalDue field
- OrderDetails lacked matching detail records for many orders
- the Inner Join removed unmatched records entirely

To preserve reporting accuracy, revenue analysis was ultimately based on the consolidated Orders table instead of relying solely on the merged detail dataset.


### 5. Create business-ready metrics and visualizations

The visualizations were intentionally kept minimal to emphasize data quality and transformation processes rather than dashboard complexity.

<img width="662" height="693" alt="screenshot" src="https://github.com/user-attachments/assets/4493393b-90cd-47a6-abca-6b5e8fc884bc" />


## Key Learnings

This project reinforced several core business intelligence concepts:
- ETL pipeline design
- data cleaning and transformation
- anomaly detection
- append vs merge operations
- relational integrity validation
- analytical verification
- building trustworthy analytical datasets

One of the most valuable outcomes was learning how incorrect join strategies or incomplete relational coverage can significantly distort business metrics.


## Tools & Technologies
- Power BI
- Power Query
