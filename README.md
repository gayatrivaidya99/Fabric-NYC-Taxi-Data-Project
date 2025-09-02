# Fabric-NYC-Taxi-Data-Project

# NYC Taxi Data Pipeline

A data pipeline for processing NYC taxi trip data using Microsoft Fabric and Azure Data Factory.

## Overview

Automated ETL solution that processes NYC taxi data through a three-layer architecture:
- **Bronze Layer**: Raw data staging
- **Silver Layer**: Cleaned and validated data warehouse
- **Gold Layer**: Aggregated data for reporting

## Architecture

```
NYC Taxi Data → Azure Data Factory → Staging → Data Warehouse → Power BI
```

### Key Components
- **Data Source**: NYC Taxi & Limousine Commission data
- **Processing**: Azure Data Factory pipelines
- **Storage**: Azure Data Lake Storage (Parquet format)
- **Warehouse**: Microsoft Fabric
- **Reporting**: Power BI semantic model

## Data Model

### Fact Table
- `fact_trips`: Trip data with metrics (revenue, passenger count, distance)

### Dimension Tables  
- `dim_date`: Date dimension
- `dim_vendor`: Vendor information
- `dim_location`: Geographic data
- `dim_payment_method`: Payment types

### KPIs Tracked
- Total revenue by date/payment method
- Trip count and passenger metrics
- Vendor performance
- Geographic journey patterns

## Pipeline Workflows

### Pipeline 1: Data Ingestion
```
Raw Data → Staging (nyctaxi-yellow) → Basic Validation
```

### Pipeline 2: Data Transformation
```
Staging → Data Cleansing → Business Rules → Data Warehouse
```

### Pipeline 3: Data Aggregation
```
Data Warehouse → Aggregations → Presentation Layer → Power BI
```

## Key Stored Procedures

```sql
-- Process staging to warehouse
EXEC sp_process_staging_data @start_date, @end_date

-- Data quality checks
EXEC sp_data_quality_check @table_name, @validation_date

-- Remove outliers
EXEC sp_remove_outliers @table_name

-- Archive old data
EXEC sp_archive_processed_data @retention_months
```

## Setup

### Prerequisites
- Azure subscription
- Microsoft Fabric workspace
- Power BI Pro license

### Quick Start
1. Clone repository
2. Deploy ARM templates
3. Configure linked services
4. Run initial data load
5. Schedule pipelines

## Processing Schedule
- **Daily Ingestion**: 2:00 AM UTC
- **Data Transformation**: 3:00 AM UTC
- **Quality Checks**: Hourly
- **Monthly Aggregation**: 1st of each month

## Data Retention
- Bronze Layer: 90 days
- Silver Layer: 2 years  
- Gold Layer: 7 years

## Monitoring

### Key Metrics
- Pipeline execution status
- Data quality scores
- Processing performance
- Cost optimization

### Alerts
- Pipeline failures
- Data quality issues (< 95% score)
- Processing delays (> 2 hours)

## Features

- ✅ Automated daily processing
- ✅ Data quality validation
- ✅ Error handling and retry logic
- ✅ Performance optimization
- ✅ Incremental data loading
- ✅ Automated archival
- ✅ Real-time monitoring

## Technology Stack

- **Orchestration**: Azure Data Factory
- **Processing**: Microsoft Fabric Spark
- **Storage**: Azure Data Lake Gen2
- **Analytics**: Power BI
- **Security**: Azure AD, RBAC

## License

MIT License - see LICENSE file for details.

## Support

- Technical Issues: Create GitHub issue
- Questions: data-eng@company.com
- Emergency: On-call team

---
**Version**: 1.0 | **Last Updated**: September 2025
