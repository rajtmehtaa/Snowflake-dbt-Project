# Snowflake-dbt Project: E-commerce Data Analysis

---

## Introduction

This repository documents my learning journey through two different yet interconnected projects that focus on **Snowflake** and **dbt**, applied to an E-commerce dataset. These projects allowed me to explore:
1. **Snowflake OLAP & Batch Processing**: Understanding data ingestion, transformation, and visualization workflows.
2. **dbt Data Transformation**: Creating dimensional models, a **One Wide Table (OWT)**, and performing **RFM Analysis** for actionable business insights.

The dataset used is an **e-commerce dataset** from Kaggle: https://www.kaggle.com/datasets/carrie1/ecommerce-data or you can download the archive.zip file frome Snowflake/Python/archive.zip , which contains the dataset.

---

## Technologies Used

- **Snowflake**: Cloud Data Warehouse for OLAP and Batch Processing.
- **dbt Core**: Transformations and data modeling.
- **Power BI**: Business Intelligence and visualization.
- **SQL**: Developed SQL worksheets and models for data ingestion, transformation, and querying within Snowflake.
- **Python**: Implemented pre-processing on raw data and performed RFM Analysis by creating Python-based models.
---

## Part A: Snowflake OLAP and Batch Processing

### Objective:
Learn how to process and transform E-commerce data using Snowflake to enable efficient OLAP operations.

### Architecture:
![Image](https://github.com/user-attachments/assets/49e356ff-3830-4dac-95cf-c209476ebceb)

### Workflow:
1. **Data Ingestion**:
   - Loaded raw e-commerce data from a CSV file into **Snowflake stages**.
2. **Preprocessing**:
   - Cleaned and prepared data externally before loading it into Snowflake tables. Use "simplify.py" from Snowflake/Python/ for pre-preprocessing.
3. **Data Loading**:
   - Stored raw data in a **Snowflake Warehouse**.
   - Transformed the data into **invoice** and **items** tables for further analysis.
4. **BI Integration**:
   - Connected **Power BI** to Snowflake to create insightful dashboards for data visualization.

### Setup

#### 1. Snowflake Account Setup
To start using Snowflake, follow these steps:
- Sign up for a **Snowflake Free Trial Account** [here](https://signup.snowflake.com/).
- Once registered, log in to the **Snowflake Web Interface**.
- Choose the region and cloud provider you want to use (AWS, Azure, or GCP).
- Note down your **Account Identifier**, which will be required for SnowSQL and connecting other tools like Power BI.

---

#### 2. Creating the Warehouse and Setting Up a Snowflake Database
1. **Create a Warehouse**:
   - Navigate to the **Warehouses** section in Snowflake.
   - Click **Create Warehouse**, provide a name (e.g., `SMALLWAREHOUSE`), and set the size (e.g., `X-SMALL`) for testing.
   - Click **Finish** to create the warehouse.

2. **Create a Database**:
   - Navigate to the **Databases** section.
   - Click **Create Database** and provide a name (e.g., `ECOMMERCE_DB`).
   - Your database is now ready for use.
  
3. **Before Loading CSV to create Schema**
   - Use "1_Before_Loading_CSV.sql" file from Snowflake/Sql/ and run it on Snowflake worksheet.

---

#### 3. Using Internal Stages with SnowSQL
1. **Install SnowSQL**:
   - Download and install **SnowSQL** from the [official Snowflake documentation](https://docs.snowflake.com/en/user-guide/snowsql.html).
     
2. **Configure SnowSQL**:
   - Open the terminal and configure SnowSQL with your account details:
     ```bash
     snowsql -a <account_identifier> -u <username>
     ```
3. **Create an Internal Stage & Upload Files to Stage**:
   - In the Snowflake worksheet run the "2_Load with snowsql.sql" file from Snowflake/Sql/
---

#### 4. Splitting Data into Two Tables
3. **Split Data into Invoices and Items Tables**:
   - In the Snowflake worksheet run the "3_Split_table.sql" file from Snowflake/Sql/
4. **Visualize**:
   - In the Snowflake worksheet run the "4_Visualize.sql" file from Snowflake/Sql/
5. **Dashboard in Snowflake**:
  - In the Snowflake worksheet run the "5_Dashboard.sql" file from Snowflake/Sql/
---

#### 5. Visualizing Data with Power BI
1. **Install Power BI Desktop**:
   - Download and install **Power BI Desktop** from [here](https://powerbi.microsoft.com/).

2. **Connect Power BI to Snowflake**:
   - Open Power BI and click on **Get Data**.
   - Choose **Snowflake** as the data source.
   - Enter your Snowflake account details:
     - Server: `<account_identifier>.snowflakecomputing.com`
     - Warehouse: `SMALLWAREHOUSE`
     - Database: `ECOMMERCE_DB`
     - Schema: `ECOMMERCE_SCHEMA`
   - Click **OK** and sign in with your Snowflake credentials.

3. **Load Data**:
   - Select the tables (e.g., `INVOICE_TABLE`, `ITEMS_TABLE`) and click **Load**.

4. **Create Dashboards**:
   - Use the data to create visualizations eg: Count of Distinct Countries.
  
## Project B: dbt and Dimensional Modeling in Snowflake

---

### Objective:
Leverage **dbt** to transform raw E-commerce data into dimensional models, data marts, and a unified **One Wide Table (OWT)** for advanced analytics.

---

### Architecture:

#### 1. dbt-Snowflake Architecture:
![dbt-Snowflake Architecture](https://github.com/user-attachments/assets/2e9824bf-5ecd-4aee-a807-b24f93e0d1d2)

#### 2. Tables:
![Tables Overview](https://github.com/user-attachments/assets/97ce45ca-68f9-417d-9801-84c7d0a95f90)

---

### Workflow:

1. **Data Ingestion**:
   - Followed the Snowflake preparation steps to load the raw E-commerce data (CSV file) into **Snowflake Staging Tables**.

2. **Data Transformation with dbt**:
   - Configured and set up **dbt Core** to work with the Snowflake instance.
   - Built **SQL models**, custom schemas, and Python models to transform the raw data into structured data.
   - Worked with **dbt source files** and **seed files** to integrate auxiliary data like `countries.csv`.

3. **Pushing to Snowflake**:
   - Used **dbt CLI commands** to push transformations and models to Snowflake.
   - Modified the `ecommerce_dbt` repository created using `dbt init` by adding:
     - Models: For staging, marts, and OWT creation.
     - Seeds: For auxiliary data ingestion (e.g., `countries.csv`).
     - Targets: To specify the destination schema and database in Snowflake.
   - Implemented and validated transformations with **generic tests** in dbt.

4. **Dimensional Modeling**:
   - Created dimensional tables for **invoices**, **items**, and **countries**.
   - Designed a unified **One Wide Table (OWT)** to aggregate data marts for BI tools like Power BI.

5. **RFM Analysis**:
   - Performed **RFM Analysis** using dbt Python models to segment customers based on:
     - **Recency**: Time since the last order.
     - **Frequency**: Number of orders.
     - **Monetary Value**: Total value of purchases.
   - Example output:
     ![Image](https://github.com/user-attachments/assets/6e96c312-9495-4ab9-8d09-ec2cb042f888)

---

### Key Deliverables:

1. **SQL Models**:
   - Designed robust SQL transformations for Snowflake tables.
   - Ensured data consistency and accuracy with tests in dbt.

2. **Custom Schemas and Seed Files**:
   - Added `countries.csv` seed file to integrate country data and enrich dimensional models.

3. **One Wide Table (OWT)**:
   - Aggregated key insights from multiple tables into a single, query-ready structure for downstream analytics.

4. **RFM Analysis**:
   - Identified high-value customers through a detailed segmentation analysis.

---

### Setup:

#### 1. Setting Up dbt Core:
- Installed dbt Core locally and configured it to connect to Snowflake.
- Initialized the project with:
  ```bash
  dbt init ecommerce_dbt
- Updated `dbt_project.yml` file to specify the database, schema, and Snowflake profile.

### 2. Adding Models and Seeds:
- Added `countries.csv` to the 'model' folder as a seed file and updated the dimension scripts.
  
  ```bash
  dbt seed
- Created mart models and defined transformations for invoices, items, and the One Wide Table (OWT).

### 3. Running dbt Commands: 
- Executed transformation with:
  ```bash
  dbt run
- Tested Models using:
  ```bash
  dbt test
- Validated data with custom and generic tests in dbt.

## Conclusion
Together, these projects highlight expertise in end-to-end data engineering workflows, including data ingestion, transformation, and visualization. They also emphasize the integration of scalable tools like Snowflake and dbt to derive valuable business intelligence from raw datasets, bridging the gap between raw data and decision-making. These projects serve as a foundation for handling large-scale data engineering tasks in real-world scenarios.
