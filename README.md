# Customer 360° Data Engineering Project

This project builds an end-to-end Customer 360 analytics pipeline on Azure & Databricks Lakehouse.

## Architecture
- Azure Data Lake Gen2 (Bronze → Silver → Gold)
- Azure Data Factory (Lookup file ingestion)
- Azure Key Vault (secret management)
- Azure SQL Database (reference data)
- Databricks (ETL, Data Modeling, Insights)
- Delta Lake (ACID + Incremental load)

## Data Sources
| Type | Files | Load Pattern |
|------|-------|--------------|
| Main (Streaming) | transactions.csv, customer_updates.csv | Autoloader / Batch |
| Lookup (DB tables) | Customers, Support Tickets, Web Activity | JDBC Full Load |

## Data Processing
### Bronze → Silver Validations
- Null checks, type casting
- Email/phone format validation
- Remove/flag duplicates
- Date validation
- Partition by `category` (valid / bad)

✅ SCD Merge on Customer Master using Delta Lake

## Silver → Gold Transformations
- RFM scoring (Recency, Frequency, Monetary)
- Engagement classification (web metrics)
- Support ticket segmentation

### Final Output ✅
`Customer_360_View` in Gold Layer

Customer classification:
- VIP
- Loyal but Low Engagement
- At Risk
- Lost Customers
- Others

## Orchestration
LakeFlow Job Pipeline:
1️⃣ ingestion.py  
2️⃣ validation.py  
3️⃣ transformations.py  
4️⃣ output.py  
+ Email notifications on completion

---

## Tech Used
Python | PySpark | Delta Lake | Azure SQL | Azure ADF | Databricks | Structured Streaming
