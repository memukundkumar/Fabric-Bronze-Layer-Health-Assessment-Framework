# Bronze Layer Health Monitoring - Power BI Setup Guide

This guide details how to connect Power BI in **Direct Lake Mode** to your Fabric Lakehouse and build the operational health dashboard.

## 1. Connect to the Lakehouse
1. Open Power BI Desktop and select **OneLake data hub** or **Microsoft Fabric Lakehouse**.
2. Select your Lakehouse and choose the `bronze_health_history` table.

## 2. Essential DAX Measures
Create a new measure table named `_Health_Measures` and add the following DAX calculations:

```dax
// Total number of health check runs executed
Total_Runs = DISTINCTCOUNT(bronze_health_history[RunID])

// Total number of failing checks across all tables
Failed_Checks = CALCULATE(
    COUNTA(bronze_health_history[Status]), 
    bronze_health_history[Status] = "FAIL"
)

// Overall health compliance percentage
Compliance_Rate = 
VAR PassedChecks = CALCULATE(
    COUNTA(bronze_health_history[Status]), 
    bronze_health_history[Status] = "PASS"
)
VAR TotalChecks = COUNTA(bronze_health_history[Status])
RETURN DIVIDE(PassedChecks, TotalChecks, 0) * 100
