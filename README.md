**Data Engineering Project on Zomato database**:\
**Objective**

This project is a data engineering solution built on Microsoft Azure, designed to process Zomato sales data following the Medallion Architecture (Bronze, Silver, and Gold layers). It automates data workflows by enabling incremental data loading and transforming the data using PySpark. The transformed data is then stored in Azure Synapse, where it’s analyzed and visualized through Power BI.

**Project Architecture:**

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

**Project Overview:**\
•	Based on the architecture, first step is to migrate the Zomato data from GitHub repository to SQL Database.

• The ingested data is then stored in Azure Data Lake Storage Gen2, where it is initially placed in the raw data store, referred to as the bronze layer. This layer contains an unprocessed copy of the source data and the data is incrementally loaded in Azure SQL Database through Azure Data Factory (ADF).

•	Next, the data is transformed using Databricks. These initial transformations enhance data quality and structure, forming the transformed data layer, also known as the silver layer.

• The data is then moved to the silver layer, where initial data transformations are applied to enhance quality and structure. 

• Next, the data is transferred to the gold layer, where final data transformations and optimizations are performed to prepare it for reporting and analytics.

• The processed data is then loaded into Azure Synapse analytics for structured querying and storage.

•	Finally, data from Azure Synapse analytics is connected to Power BI, where further data analysis and visualization are performed to generate business insights.
