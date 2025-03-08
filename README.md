# Data Engineering Project on Zomato database:
## Objective

This project is a data engineering solution built on Microsoft Azure, designed to process Zomato sales data following the Medallion Architecture (Bronze, Silver, and Gold layers). It automates data workflows by enabling incremental data loading and transforming the data using PySpark. The transformed data is then stored in Azure Synapse, where it’s analyzed and visualized through Power BI.

## Project Architecture:

![image](https://github.com/user-attachments/assets/c29b2a9a-d883-4164-9402-ce8a667c7e96)

**Medallion Architecture:** 
The Medallion Architecture in Azure Data Factory (ADF) 
structures data into three layers for better data management and analytics:\
**Bronze Layer (Raw Data - Landing Zone)**\
• Stores raw, unprocessed data from GitHub, CSV, etc. 

• Stored in: Azure SQL Database.

• ADF Activity: Copy Activity (loads raw data as Parquet), Incremental Data loading and stored in ADLS Gen2.

**Silver Layer (Cleansed Data - Curated Zone)**\
• Data is cleaned & removes duplicates, null values, and incorrect records.

• Processed using: Azure Databricks. 

• Stored in: ADLS Gen2 (Parquet).

**Gold Layer (Aggregated Data - Consumption Zone)**\
• Final business-ready data for reporting & analytics in Azure Synapse and Power BI. 

## Project Overview:
•	Based on the architecture, first step is to migrate the Zomato data from GitHub repository to SQL Database.

• The ingested data is then stored in Azure Data Lake Storage Gen2, where it is initially placed in the raw data store, referred to as the bronze layer. This layer contains an unprocessed copy of the source data and the data is incrementally loaded in Azure SQL Database through Azure Data Factory (ADF).

•	Next, the data is transformed using Databricks. These initial transformations enhance data quality and structure, forming the transformed data layer, also known as the silver layer.

• The data is then moved to the silver layer, where initial data transformations are applied to enhance quality and structure. 

• Next, the data is transferred to the gold layer, where final data transformations and optimizations are performed to prepare it for reporting and analytics.

• The processed data is then loaded into Azure Synapse analytics for structured querying and storage.

•	Finally, data from Azure Synapse analytics is connected to Power BI, where further data analysis and visualization are performed to generate business insights.

## Required Azure Services:
To implement the project, the following Azure services need to be created:

• Azure Data Lake Storage Gen 2 – For scalable and secure data storage.

• Azure Data Factory – For orchestrating data movement and transformation.

• Azure SQL Database – For structured data storage and querying. 

•	Databricks – For transforming the data according to the requirement

• Azure Synapse Analytics – For scalable data warehousing and advanced analytics to connect with Power BI.

•	Power BI – For data visualization and reporting.

## Pipeline Details
### Pipeline 1: Data Ingestion
This pipeline fetches data from GitHub and loads it into the Azure SQL Database.
Here the source is GitHub Repo and sink is Azure SQL DB

![image](https://github.com/user-attachments/assets/8dc79bde-c537-45c9-95ff-5375d2799c9a)

### Pipeline 2: Incremental Data Loading

This pipeline ensures that only new data is appended to the Bronze layer in Azure Data Lake Gen 2.

![image](https://github.com/user-attachments/assets/e9f49718-a098-43eb-a3df-9f11ca227e8c)

The incremental data loading pipeline in Azure Data Factory (ADF) uses two Lookup activities, one Copy Data activity, and one Stored Procedure activity. The first Lookup retrieves the last processed Restaurant_ID from the watermark table, while the second fetches the current maximum Restaurant_ID from the ZomatoData table. The Copy Data activity transfers only new records by filtering data between these two values. Finally, the Stored Procedure updates the watermark table with the latest processed ID, ensuring efficient and optimized incremental data loading for future pipeline runs.

## Data Transformation

After storing the incremental data in the bronze layer, a Databricks notebook was created within the ZomatoData resource group and connected to the database using an SAS token.
Some of the below transformation has been performed
![image](https://github.com/user-attachments/assets/77e81f0e-0d84-4045-b539-708bfdd1dcd4)

Merged two dataset using Inner join and save the data in silver layer
![image](https://github.com/user-attachments/assets/0f9d4ad6-aa75-44ad-a4cc-152a59a89e0b)
![image](https://github.com/user-attachments/assets/491950f3-7faf-4d2e-9163-8823379ca5b3)



