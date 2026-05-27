# Spar Nord ATM Transaction ETL Project

## Project Overview

An ETL (Extract, Transform, Load) data engineering project processing ATM transaction data for Spar Nord Bank. The project extracts transactions from source systems, transforms data for analytics, and loads into Amazon Redshift data warehouse.

## Objective

- Extract ATM transaction data
- Transform for analytics and reporting
- Load into Redshift for BI tools
- Enable transaction analytics and fraud detection

## Architecture

```
Source Systems → Data Ingestion → Spark ETL → Redshift → Analytics
                  (Sqoop)        (PySpark)    Data Lake
```

## Components

### 1. Data Ingestion (Sqoop)
- Extracts transaction data from relational databases
- Loads into HDFS landing zone
- Supports incremental updates

### 2. Data Transformation (Spark)
- PySpark ETL jobs clean and transform data
- Aggregations and feature engineering
- Data quality validation
- Deduplication and enrichment

### 3. Data Loading (Redshift)
- Loads transformed data into Redshift
- Creates analytics tables
- Implements data retention policies
- Supports incremental loads

## Technologies

- **Ingestion**: Apache Sqoop
- **Processing**: Apache Spark, PySpark
- **Storage**: Amazon Redshift
- **Workflow**: Airflow (if applicable)

## Installation & Setup

### Prerequisites

- Java 8+
- Spark 2.4+
- Sqoop 1.4+
- Python 3.7+
- AWS credentials for Redshift

### Configuration

```bash
# Configure Sqoop connection
vi $SQOOP_HOME/conf/sqoop-site.xml

# Set Spark configuration
vi spark/conf/spark-defaults.conf

# Configure Redshift connection
vi config/redshift_config.yaml
```

### Running ETL

```bash
# Extract data using Sqoop
sqoop import --connect jdbc:mysql://source_db:3306/transactions \
  --table atm_transactions --target-dir /data/raw/transactions

# Run Spark transformation
spark-submit src/transform_atm_data.py --input /data/raw/transactions \
  --output /data/transformed/transactions

# Load to Redshift
python src/load_to_redshift.py --input /data/transformed/transactions
```

## ETL Pipeline

1. **Extract** - Daily incremental load from source DB
2. **Validate** - Data quality checks
3. **Transform** - Aggregations, deduplication, enrichment
4. **Validate** - Post-transform validation
5. **Load** - Batch load to Redshift
6. **Reconcile** - Record counts and checksums

## Query Examples

See `RedshiftQueries.pdf` for sample analytical queries.

## Performance

- Daily volume: [X million transactions]
- Processing time: [X hours]
- Redshift query performance: [X seconds for standard queries]

## Documentation

- `RedshiftSetup.pdf` - Redshift cluster setup guide
- `RedshiftQueries.pdf` - Example analytical queries
- `SqoopDataIngestion.pdf` - Data ingestion documentation
- `SparkETLCode.ipynb` - PySpark transformation code

## Monitoring & Alerts

- Job status monitoring
- Data quality metrics
- SLA compliance tracking

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Sqoop connection failure | Verify JDBC connection string |
| Spark job timeout | Increase executor memory |
| Redshift load errors | Check table schema compatibility |

## Files

- `SparkETLCode.ipynb` - Transformation code
- `Spar_Nord_Atm_Trans_ETL_Project_Abhilasha.zip` - Complete project
- PDF documentation files

## Author

Abhilasha Garg

## License
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)
[![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=flat&logo=jupyter)](https://jupyter.org/)

[License]
