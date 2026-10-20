# 🏎️ Formula 1 Azure Data Engineering Project

## 📋 Project Overview
End-to-end data engineering pipeline that ingests Formula 1 race data from the API into Azure Data Lake Storage Gen2 using Azure Data Factory, transforms it through Bronze/Silver/Gold medallion layers in Azure Databricks with PySpark and SQL, and delivers actionable race insights via Power BI dashboards.

---

## 🏗️ Architecture
```
Formula 1 API (Ergast)
        ↓
Azure Data Factory (Ingestion)
        ↓
ADLS Gen2 - Bronze Layer (Raw Data)
        ↓
Azure Databricks - Silver Layer (Cleaned & Transformed)
        ↓
Azure Databricks - Gold Layer (Aggregated & Business Ready)
        ↓
Power BI (Insights & Dashboards)
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **Azure Data Factory** | Data ingestion & pipeline orchestration |
| **Azure Data Lake Gen2** | Scalable cloud storage (Bronze/Silver/Gold) |
| **Azure Databricks** | Data transformation using PySpark & SQL |
| **Apache Spark** | Distributed data processing |
| **Delta Lake** | ACID transactions & time travel |
| **Unity Catalog** | Data governance & access control |
| **Power BI** | Business intelligence & dashboards |
| **Azure Key Vault** | Secrets & credentials management |

---

## 🥉🥈🥇 Medallion Architecture

### Bronze Layer (Raw)
- Raw data ingested as-is from Ergast Formula 1 API
- Stored in original JSON/CSV format
- No transformations applied
- Full historical data retained

### Silver Layer (Cleaned)
- Data cleaned and standardized
- Schema enforced
- Null values handled
- Data types corrected
- Duplicate records removed
- Joined across related datasets

### Gold Layer (Business Ready)
- Aggregated metrics computed
- Race standings calculated
- Driver & constructor analytics
- Optimized for Power BI consumption
- Delta format for fast querying

---

## 📊 Data Sources

Data sourced from **Ergast Formula 1 API** (http://ergast.com/mrd/):

| Dataset | Description |
|---------|-------------|
| `races` | Race schedule, circuit, date |
| `drivers` | Driver details, nationality |
| `constructors` | Team/constructor details |
| `results` | Race results per driver |
| `qualifying` | Qualifying session results |
| `pit_stops` | Pit stop timings |
| `lap_times` | Individual lap times |
| `standings` | Driver & constructor standings |

---

## 📈 Power BI Insights

- 🏆 Driver Championship Standings
- 🏎️ Constructor Championship Standings  
- ⏱️ Fastest Lap Analysis
- 🔄 Pit Stop Strategy Analysis
- 📍 Circuit Performance Comparison
- 📅 Season-by-Season Trends
- 🌍 Driver Nationality Distribution
- 📊 Points Progression Over Season

---

## 📁 Project Structure

```
formula1-azure-project/
│
├── ingestion/                  # ADF pipeline JSONs
│   ├── bronze_pipeline.json
│   └── linked_services/
│
├── databricks/
│   ├── bronze/                 # Raw ingestion notebooks
│   │   └── ingest_races.py
│   ├── silver/                 # Transformation notebooks
│   │   ├── transform_races.py
│   │   ├── transform_drivers.py
│   │   └── transform_results.py
│   ├── gold/                   # Aggregation notebooks
│   │   ├── race_standings.py
│   │   └── driver_analytics.py
│   └── utils/                  # Shared utilities
│       └── common_functions.py
│
├── powerbi/                    # Power BI report files
│   └── formula1_insights.pbix
│
├── setup/                      # Infrastructure setup
│   └── mount_adls.py
│
└── README.md
```

---

## ⚙️ Setup & Configuration

### Prerequisites
- Azure Subscription
- Azure Data Factory instance
- Azure Databricks workspace
- Azure Data Lake Storage Gen2
- Azure Key Vault
- Power BI Desktop

### Step 1 — Clone Repository
```bash
git clone https://github.com/vidyakinjarapu/formula1-azure-project.git
cd formula1-azure-project
```

### Step 2 — Configure Azure Resources
```
1. Create Resource Group
2. Create ADLS Gen2 with bronze/silver/gold containers
3. Create Azure Databricks workspace
4. Create Azure Data Factory
5. Create Azure Key Vault
```

### Step 3 — Mount ADLS in Databricks
```python
# Run setup/mount_adls.py in Databricks notebook
configs = {
    "fs.azure.account.auth.type": "OAuth",
    "fs.azure.account.oauth.provider.type": "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
    "fs.azure.account.oauth2.client.id": "<client-id>",
    "fs.azure.account.oauth2.client.secret": dbutils.secrets.get("kv-scope", "client-secret"),
    "fs.azure.account.oauth2.client.endpoint": "https://login.microsoftonline.com/<tenant-id>/oauth2/token"
}

dbutils.fs.mount(
    source="abfss://bronze@<storage-account>.dfs.core.windows.net/",
    mount_point="/mnt/formula1/bronze",
    extra_configs=configs
)
```

### Step 4 — Run ADF Pipelines
```
ADF Studio → Author → Pipelines
→ Run bronze ingestion pipeline
→ Trigger silver transformation
→ Trigger gold aggregation
```

### Step 5 — Connect Power BI
```
Power BI Desktop
→ Get Data → Azure Databricks
→ Connect to Gold layer tables
→ Build dashboards
```

---

## 🔐 Security

- Azure Key Vault for secrets management
- Service Principal authentication
- ADLS Gen2 ACLs for access control
- Unity Catalog for data governance
- No hardcoded credentials in code

---

## 🚀 Key Features

- ✅ Fully automated end-to-end pipeline
- ✅ Medallion architecture (Bronze/Silver/Gold)
- ✅ Delta Lake format for ACID transactions
- ✅ Time travel capability on all layers
- ✅ Parameterized & reusable ADF pipelines
- ✅ PySpark & Spark SQL transformations
- ✅ Unity Catalog governance
- ✅ Power BI real-time insights

---

## 📚 Learning Outcomes

- Azure Data Factory pipeline design
- Azure Databricks & PySpark
- Medallion architecture implementation
- Delta Lake & Unity Catalog
- ADLS Gen2 storage management
- End-to-end data engineering workflow
- Power BI dashboard creation

---

## 👤 Author

**Vidya Kinjarapu**  
Senior Azure/Cloud Data Engineer  
Azure | Databricks | ADF | PySpark | Power BI

---

## 📄 License
MIT License — feel free to use and modify for your own learning projects.
