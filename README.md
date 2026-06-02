# Healthcare Analytics ETL Pipeline

End-to-end data pipeline analyzing COVID-19 vaccination trends, adverse events, and clinical trials using Databricks.

## 🎯 Overview
- **Medallion Architecture**: Bronze → Silver → Gold
- **Data Sources**: CDC, OpenFDA, ClinicalTrials APIs
- **Platform**: Databricks (PySpark, Delta Lake)
- **Automation**: Daily scheduled jobs

## 🛠️ Tech Stack
- Platform: Databricks
- Processing: PySpark, Delta Lake
- Storage: Unity Catalog
- Orchestration: Databricks Jobs
- Languages: Python, SQL

## 📊 Key Metrics
- 100 FDA adverse event reports
- 58% average vaccination rate
- 100 clinical trials analyzed
- 50+ states covered

## 🏗️ Architecture
## 📈 Key Insights
- MA: 79% vs SD: 12% vaccination rates
- Metro: 58% vs Non-Metro: 47.4%
- 65+ age group: 79.4% vaccinated
- 66% non-serious adverse events

## ⚙️ Setup
1. Import notebook to Databricks
2. Create catalog: `etl_healthcare_project`
3. Run all cells
4. Schedule daily job

## 📊 Data Sources
- CDC COVID-19: `data.cdc.gov/resource/8xkx-amqh.json`
- OpenFDA: `api.fda.gov/drug/event.json`
- ClinicalTrials: `clinicaltrials.gov/api/v2/studies`


# 🏥 Healthcare Analytics ETL Pipeline

**End-to-end data engineering pipeline analyzing COVID-19 vaccination trends, FDA adverse events, and clinical trial data using Databricks.**

[![Databricks](https://img.shields.io/badge/Databricks-Powered-red)](https://databricks.com/)
[![PySpark](https://img.shields.io/badge/PySpark-3.5-orange)](https://spark.apache.org/)
[![Delta Lake](https://img.shields.io/badge/Delta%20Lake-ACID-blue)](https://delta.io/)

---

## 📊 Project Overview

This project implements a production-grade **Medallion Architecture (Bronze-Silver-Gold)** ETL pipeline that processes healthcare data from multiple public APIs and delivers actionable insights through an interactive dashboard.

### What This Pipeline Does:
✅ Ingests data from **3 public healthcare APIs** (CDC, OpenFDA, ClinicalTrials.gov)  
✅ Processes **COVID-19 vaccination, adverse event, and clinical trial data**  
✅ Uses **Delta Lake** for ACID transactions and data versioning  
✅ Powers an **AI/BI Dashboard** with 8+ interactive visualizations  
✅ Runs **automated daily jobs** for continuous data refresh  



