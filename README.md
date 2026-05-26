# Atlicon Consolidated Pipeline

A production-grade data pipeline implementing the medallion architecture (Bronze → Silver → Gold) for FMCG (Fast-Moving Consumer Goods) analytics on Databricks.

## 🎯 Project Overview

This pipeline processes customer, product, pricing, and order data from CSV files stored in S3, applying data quality transformations and producing analytics-ready datasets in Unity Catalog.

## 🏗️ Architecture

### Medallion Layers

* **Bronze Layer** (`fmcg.bronze.*`): Raw data ingestion from S3 with minimal processing
* **Silver Layer** (`fmcg.silver.*`): Cleaned and validated data with quality checks
* **Gold Layer** (`fmcg.gold.*`): Business-level aggregated tables optimized for analytics

### Technology Stack

* **Compute**: Databricks (PySpark)
* **Storage**: Delta Lake with Change Data Feed enabled
* **Catalog**: Unity Catalog (`fmcg` catalog)
* **Source**: AWS S3 (`s3://sportsbar-eio/`)
* **Format**: CSV files with header

## 📁 Project Structure

```
atlicon_consolidated_pipeline/
├── consolidated_pipeline/
│   ├── 1_setup/
│   │   └── utilities              # Shared configuration and helper functions
│   ├── 2_dimension_data_processing/
│   │   ├── 1_customer_data_processing
│   │   ├── 2_products_data_processing
│   │   └── 3_pricing_data_processing
│   └── 3_fact_data_processing/
│       ├── 1_full_load_fact       # Initial full data load
│       └── 2_incremental_load_fact # Ongoing incremental updates
└── README.md
```

## 🔄 Pipeline Components

### 1. Setup & Utilities

* **Shared Variables**: `bronze_schema`, `silver_schema`, `gold_schema`
* **Widget Configuration**: Parameterized notebooks for `catalog` and `data_source`
* **Common Functions**: Reusable transformation and validation logic

### 2. Dimension Processing

#### Customer Dimension
* **Source**: `s3://sportsbar-eio/customers/*.csv`
* **Transformations**:
  - Duplicate removal based on `customer_id`
  - Trim whitespace from `customer_name`
  - Add file metadata (`read_timestamp`, `file_name`, `file_size`)
* **Output**: `fmcg.gold.dim_customers`

#### Product Dimension
* **Source**: `s3://sportsbar-eio/products/*.csv`
* **Transformations**: Data quality checks and standardization
* **Output**: `fmcg.gold.dim_products`

#### Pricing Dimension
* **Source**: `s3://sportsbar-eio/pricing/*.csv`
* **Transformations**: Price validation and formatting
* **Output**: `fmcg.gold.dim_pricing`

### 3. Fact Processing

#### Orders Fact Table
* **Source**: `s3://sportsbar-eio/orders/landing/*.csv`
* **Processing Modes**:
  - **Full Load**: Initial bulk data load
  - **Incremental Load**: Process only new arrivals using staging table
* **Transformations**:
  - Cast `order_qty` to double for schema consistency
  - Add file metadata for lineage tracking
* **Output**: `fmcg.gold.sb_fact_orders`

#### Key Features
* **Staging Table**: `fmcg.bronze.staging_orders` for incremental processing
* **File Management**: Automated movement from `landing/` to `processed/` directories
* **Change Data Feed**: Enabled for downstream CDC consumers

## 🚀 Usage

### Running Dimension Processing

```python
# Example: Customer dimension processing
dbutils.widgets.text("catalog", "fmcg", "Catalog")
dbutils.widgets.text("data_source", "customers", "Data Source")

# Execute the notebook
%run ./consolidated_pipeline/2_dimension_data_processing/1_customer_data_processing
```

### Running Fact Processing

```python
# Initial full load
%run ./consolidated_pipeline/3_fact_data_processing/1_full_load_fact

# Subsequent incremental loads
%run ./consolidated_pipeline/3_fact_data_processing/2_incremental_load_fact
```

## 📊 Data Quality Checks

The pipeline implements multiple data quality validations:

* **Deduplication**: Primary key uniqueness enforcement
* **Whitespace Trimming**: Clean string fields
* **Schema Validation**: Type casting and consistency checks
* **Null Handling**: Missing value detection and handling

## 🔧 Configuration

### Required Widgets

Each processing notebook accepts the following parameters:

* `catalog`: Unity Catalog name (default: `fmcg`)
* `data_source`: Source data identifier (e.g., `customers`, `products`, `orders`)

### S3 Path Structure

```
s3://sportsbar-eio/
├── customers/
│   └── *.csv
├── products/
│   └── *.csv
├── pricing/
│   └── *.csv
└── orders/
    ├── landing/    # New files arrive here
    └── processed/  # Processed files moved here
```

## 📈 Pipeline Patterns

### Incremental Processing Pattern

1. **Read** new files from `landing/` directory
2. **Write** to staging table with `mode("overwrite")`
3. **Append** to main bronze table
4. **Move** processed files to `processed/` directory
5. **Transform** and promote to silver/gold layers

### Change Data Capture

All Delta tables have Change Data Feed enabled:

```python
.option("delta.enableChangeDataFeed", "true")
```

This allows downstream systems to track inserts, updates, and deletes.

## 🎯 Next Steps

* [ ] Add data validation tests
* [ ] Implement error handling and logging
* [ ] Create orchestration job/workflow
* [ ] Add monitoring and alerting
* [ ] Document data lineage
* [ ] Add incremental processing for dimension tables

## 👥 Contributors

Data Engineering Team

## 📄 License

See LICENSE file for details.
