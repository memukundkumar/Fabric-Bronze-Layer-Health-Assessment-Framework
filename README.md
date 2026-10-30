# Fabric Bronze Layer Health Assessment Framework

A reusable Microsoft Fabric notebook framework designed to assess the operational health, structural integrity, data completeness, and historical volume stability of your Bronze layer tables **without requiring direct access to original source systems**.

---

## 🚀 Features
- **Structural Validation:** Automatically detects missing tables and schema drift against user-defined expectations.
- **Ingestion Monitoring:** Verifies ingestion timestamps and data freshness.
- **Completeness Profiling:** Computes null percentages against configurable quality thresholds.
- **Historical Tracking:** Persists assessment runs into a Delta history table (`bronze_health_history`) to detect volume drops or schema anomalies over time.
- **Operational Monitoring:** Integrates with Power BI Direct Lake and Fabric Data Activator for automated alerts.

---

## 📂 Repository Structure
```text
fabric-bronze-health-assessment/
├── Fabric_Bronze_Health_Assessment.ipynb
├── README.md
├── LICENSE
├── powerbi/
│   └── bronze_health_report.md
└── alerts/
    └── fabric_data_activator_rules.md

⚙️ Step-by-Step Execution Guide in Microsoft Fabric
Follow these steps to deploy and execute the health check notebook in your Fabric workspace:

Step 1: Import the Notebook
Log in to Microsoft Fabric.

Navigate to your target workspace and select Data Engineering or Data Science experience.

Click Import > Notebook from the top ribbon or workspace home.

Upload the Fabric_Bronze_Health_Assessment.ipynb file downloaded from this repository.

Step 2: Attach Your Lakehouse
Open the imported notebook in Microsoft Fabric.

On the left-hand side panel, locate the Lakehouses section in the Explorer pane.

Click Add Lakehouse > Existing Lakehouse and select your target Bronze layer Lakehouse.

Ensure it is set as the default workspace Lakehouse so PySpark can easily resolve table names.

Step 3: Configure Expected Tables & Columns
In the first cell of the notebook, modify the CONFIG dictionary to match your specific ingestion schema:

CONFIG = {
    "expected_tables": ["your_table_bronze_1", "your_table_bronze_2"],
    "expected_columns": {
        "your_table_bronze_1": ["ColumnID", "ColumnName", "IngestionTimestamp"],
        "your_table_bronze_2": ["RecordID", "IngestionTimestamp"]
    },
    "max_acceptable_null_pct": 5.0,
    "volume_anomaly_threshold_pct": 50.0,
    "history_table_name": "bronze_health_history"
}

Step 4: Run the Assessment
Click Run All from the top notebook toolbar (or run cells sequentially).

Review Output: The notebook will display a Pandas DataFrame scorecard showing structural checks, null percentages, and freshness statuses (PASS, WARNING, FAIL).

Audit Log: Results are automatically appended to the bronze_health_history Delta table in your Lakehouse for historical trend analysis.

📊 Operational Monitoring & Dashboards
Power BI Integration: Connect Power BI in Direct Lake mode to the bronze_health_history table using the guide in powerbi/bronze_health_report.md.

Automated Alerts: Configure Microsoft Fabric Data Activator rules using alerts/fabric_data_activator_rules.md to notify your team via Microsoft Teams or email when a structural check fails.

📄 License
This project is licensed under the Apache License 2.0 - see the LICENSE file for details.
