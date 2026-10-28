# E-Commerce Fraud & Return Analytics Dashboard

An executive-level Power BI dashboard designed to monitor shipping losses, detect AI fraud risk scores, and manage scam patterns.

### Key DAX Measures Used:

- **Avg Risk Score:**
```dax
Avg_Risk = AVERAGE(final_ai_fraud_predictions[average ai risk])
