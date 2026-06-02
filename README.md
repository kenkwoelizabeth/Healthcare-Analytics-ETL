
# 🏥 Healthcare Analytics ETL Pipeline

**End-to-end data engineering pipeline analyzing COVID-19 vaccination trends, FDA adverse events, and clinical trial data using Databricks.**

[![Databricks](https://img.shields.io/badge/Databricks-Powered-red)](https://databricks.com/)
[![PySpark](https://img.shields.io/badge/PySpark-3.5-orange)](https://spark.apache.org/)
[![Delta Lake](https://img.shields.io/badge/Delta%20Lake-ACID-blue)](https://delta.io/)

---

## 📊 Project Overview

Production-grade **Medallion Architecture (Bronze-Silver-Gold)** ETL pipeline that:

✅ Ingests data from **3 public healthcare APIs** (CDC, OpenFDA, ClinicalTrials.gov)  
✅ Processes **COVID-19 vaccination, adverse events, and clinical trials data**  
✅ Uses **Delta Lake** for ACID transactions and time travel  
✅ Powers an **AI/BI Dashboard** with 8+ visualizations  
✅ Runs **automated daily jobs** for continuous refresh  

---

## 🏗️ Architecture

### Medallion Data Flow

```
APIs (CDC, OpenFDA, ClinicalTrials.gov)
    ↓
🥉 BRONZE LAYER (Raw Data)
    • bronze_cdc, bronze_openfda, bronze_trials
    • Schema-on-read, as-is ingestion
    ↓
🥈 SILVER LAYER (Cleaned & Validated)
    • Type casting & standardization
    • Deduplication & null handling
    ↓
🥇 GOLD LAYER (Business Metrics)
    • State-level aggregations
    • Pre-calculated KPIs
    ↓
AI/BI DASHBOARD (Lakeview)
```

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|-----------|
| **Platform** | Databricks |
| **Processing** | PySpark |
| **Storage** | Delta Lake |
| **Catalog** | Unity Catalog |
| **Orchestration** | Databricks Jobs |
| **Visualization** | AI/BI Dashboard |
| **Languages** | Python, SQL |

---

## 📈 Key Insights

### Dashboard Metrics
- 📋 **FDA Adverse Event Reports**: 100
- 💉 **Average Vaccination Rate**: 58%
- 🧪 **Clinical Trials Analyzed**: 100

### Geographic Analysis
- **Highest**: Massachusetts (79%)
- **Lowest**: South Dakota (12%)
- **Gap**: 67 percentage points

### Urban-Rural Divide
- **Metropolitan**: 58% vaccinated
- **Non-Metropolitan**: 47.4% vaccinated
- **Disparity**: 10.6 percentage points

### Age Demographics
- **65+ Years**: 79.4% (highest)
- **18+ Years**: 61.1%
- **All Ages**: 52.4%

### Safety Profile
- **Non-Serious Cases**: 66%
- **Serious Cases**: 34%

---

## 🚀 Pipeline Workflow

### 1️⃣ Bronze Layer: Raw Ingestion

```python
import requests
import pandas as pd

# Ingest CDC COVID-19 data
response = requests.get("https://data.cdc.gov/resource/8xkx-amqh.json?$limit=100")
data = response.json()
spark_df = spark.createDataFrame(pd.DataFrame(data))

spark_df.write \
    .format("delta") \
    .mode("overwrite") \
    .saveAsTable("etl_healthcare_project.healthcare.bronze_cdc")
```

### 2️⃣ Silver Layer: Transformation

```python
from pyspark.sql.functions import *

silver_cdc = bronze_cdc \
    .withColumn("state", upper(col("recip_state"))) \
    .withColumn("vaccination_rate", col("series_complete_pop_pct").cast("double")) \
    .dropDuplicates() \
    .filter(col("state").isNotNull())

silver_cdc.write.saveAsTable("silver_cdc")
```

### 3️⃣ Gold Layer: Aggregation

```python
gold_vaccination = silver_cdc \
    .groupBy("state") \
    .agg(
        avg("vaccination_rate").alias("avg_rate"),
        sum("total_vaccinated").alias("total_vaccinated")
    )
```

---

## 📂 Project Structure

```
Healthcare-Analytics-ETL/
├── notebooks/
│   └── etl_healthcare_pipeline.ipynb   # Main ETL pipeline
├── dashboards/
│   └── screenshots/                    # Dashboard images
├── README.md                           # This file
├── .gitignore                          # Git ignore rules
└── LICENSE                             # MIT License
```

---

## ⚙️ Setup & Deployment

### Prerequisites
- Databricks workspace
- Unity Catalog enabled
- Python 3.10+

### Installation

1. **Clone repository**
```bash
git clone https://github.com/kenkwoelizabeth/Healthcare-Analytics-ETL.git
```

2. **Import notebook**
   - Open Databricks workspace
   - Import `notebooks/etl_healthcare_pipeline.ipynb`

3. **Create catalog**
```sql
CREATE CATALOG IF NOT EXISTS etl_healthcare_project;
CREATE SCHEMA IF NOT EXISTS etl_healthcare_project.healthcare;
```

4. **Run pipeline**
   - Attach to cluster
   - Execute all cells

### Automated Scheduling
- **Job Name**: ETL Healthcare
- **Schedule**: Daily at 2:00 AM (America/New_York)
- **Compute**: Serverless
- **Notifications**: Email alerts on failure

---

## 📊 Data Sources

| API | Endpoint | Records | Frequency |
|-----|----------|---------|----------|
| **CDC COVID-19** | `data.cdc.gov/resource/8xkx-amqh.json` | 100 | Daily |
| **OpenFDA** | `api.fda.gov/drug/event.json` | 100 | Real-time |
| **ClinicalTrials** | `clinicaltrials.gov/api/v2/studies` | 100 | Weekly |

---

## 🎓 Skills Demonstrated

✅ **Data Engineering**: ETL design, medallion architecture  
✅ **Big Data**: PySpark, distributed computing, Delta Lake  
✅ **Data Quality**: Validation, deduplication, cleansing  
✅ **Automation**: Job scheduling, monitoring, alerting  
✅ **API Integration**: RESTful APIs, JSON parsing  
✅ **Visualization**: Dashboard design, storytelling  

---

## 🔮 Future Enhancements

- [ ] Implement incremental loading (CDC pattern)
- [ ] Add data quality tests (Great Expectations)
- [ ] Build ML model for vaccination prediction
- [ ] Migrate to real-time streaming
- [ ] Add dbt for transformation orchestration
- [ ] Deploy REST API for queries
- [ ] Implement CI/CD with GitHub Actions

---



## 📄 License

MIT License - Free to use for learning and portfolio purposes.

---

<div align="center">

### ⭐ If you found this project helpful, please give it a star! ⭐

**Made with ❤️ using Databricks**

</div>
