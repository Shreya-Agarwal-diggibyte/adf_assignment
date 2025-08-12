# ADF Assignment

##  Overview

This project demonstrates a **data pipeline architecture** following the **medallion approach** (Bronze → Silver → Gold) using Azure Data Factory (ADF) and Databricks notebooks.

The pipeline consists of:

* **Bronze Layer**: Raw data ingestion.
* **Silver Layer**: Data cleaning, transformation, and standardization.
* **Gold Layer**: Aggregated and business-ready datasets.

##  Project Structure

```
src/
├── bronze_to_silver/
│   ├── drivers.ipynb        # Logic to transform raw 'drivers' data from Bronze to Silver
│   ├── utils.ipynb          # Utility functions shared across transformation steps
└── silver_to_gold/
    ├── gold_aggregations.ipynb  # Business-level aggregations for analytics
```

##  How It Works

1. **ADF Orchestration**
   Azure Data Factory orchestrates the execution of Databricks notebooks for each stage of the pipeline.

2. **Bronze to Silver**

   * Cleans and validates raw driver datasets.
   * Applies schema enforcement and basic transformations.
   * Saves processed data to the Silver zone.

3. **Silver to Gold**

   * Reads curated Silver datasets.
   * Performs aggregations, joins, and KPIs required for analytics.
   * Outputs Gold datasets for reporting and BI tools.

## Prerequisites

* Azure Subscription with:

  * Azure Data Factory
  * Azure Databricks Workspace
* Databricks cluster with appropriate runtime (Spark + Python support)
* Access to input datasets in Azure Data Lake Storage (ADLS)
* Configured **linked services** in ADF for Databricks and ADLS

## Usage

1. **Clone the repository**

   ```bash
   git clone <repo_url>
   cd adf_assignment
   ```

2. **Upload notebooks to Databricks**

   * Navigate to your Databricks workspace.
   * Import the `.ipynb` files under `src/` into corresponding workspace folders.

3. **Set up ADF pipelines**

   * Create ADF pipelines to run:

     * `bronze_to_silver/drivers.ipynb`
     * `silver_to_gold/gold_aggregations.ipynb`
   * Use **Databricks Notebook** activities and pass parameters if required.

4. **Run the Pipeline**
   Trigger the ADF pipeline manually or schedule it for automation.

## Notes

* `utils.ipynb` contains shared functions that must be available to other notebooks (import or `%run` in Databricks).
* Ensure ADLS paths and configurations match your environment.
* If using Git integration in Databricks, prefer SSH authentication for secure access.
