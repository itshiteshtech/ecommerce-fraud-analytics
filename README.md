# E-Commerce Fraud & Return Analytics Dashboard

An executive-level Power BI dashboard designed to monitor shipping losses, detect AI fraud risk scores, and manage scam patterns.

### Key DAX Measures Used:

• Avg Risk Score:
Avg_Risk = AVERAGE(final_ai_fraud_predictions[average ai risk])

• Total Frauds Count:
Total_Frauds = COUNTROWS(FILTER(final_ai_fraud_predictions, final_ai_fraud_predictions[Fraud Order] > 0))

### Dashboard Highlights:
• Executive KPI Cards: Shipping Loss, Total Orders, AI Risk Score, and Fraud Orders with trend lines and live alerts.
• Scam Pattern Analysis: Custom visual categorization covering Product Swapping, Genuine Issues, COD Fake Orders, and UPI Scams.
• AI Control Room: Real-time action recommendations with conditional risk formatting (CRITICAL, HIGH, SAFE).
