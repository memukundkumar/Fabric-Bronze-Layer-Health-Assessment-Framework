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
