# Configuring Automated Alerts for Bronze Health Failures

When a health check notebook run identifies a structural failure, missing table, or severe data drop, your team should be notified immediately.

## Method: Microsoft Fabric Data Activator
1. Open your workspace in Microsoft Fabric.
2. Select the **`bronze_health_history`** table and choose **Set up alert** (Data Activator).
3. Define the alert condition:
   - **When:** `Status` equals `FAIL`
   - **And:** `AssessmentTimestamp` is within the last 1 hour.
4. Set up the action:
   - Send an alert notification via **Microsoft Teams** or **Email** to the data engineering distribution list.
   - Include dynamic fields in the notification: `TableName`, `CheckName`, and `Details`.
