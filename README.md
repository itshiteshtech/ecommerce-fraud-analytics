# E-Commerce Fraud & Return Analytics Dashboard

An executive-level Power BI dashboard designed to monitor shipping losses, detect AI fraud risk scores, and manage scam patterns.

### Key DAX Measures:

• Avg Risk Score:
Avg_Risk = AVERAGE(final_ai_fraud_predictions[average ai risk])

• Total Frauds Count:
Total_Frauds = COUNTROWS(FILTER(final_ai_fraud_predictions, final_ai_fraud_predictions[Fraud Order] > 0))

### SQL Data Pipeline & Extraction:
• Return Rate & Fraud Loss Aggregation Query:
SELECT 
    Customer_ID,
    Order_ID,
    Product_Category,
    Courier_Partner,
    City_Tier,
    Order_Value_INR,
    Fraud_Order,
    Return_Reason,
    ROUND(AVG(average_ai_risk), 2) AS Avg_Risk_Score
FROM final_ai_fraud_predictions
GROUP BY Customer_ID, Order_ID, Product_Category, Courier_Partner, City_Tier, Order_Value_INR, Fraud_Order, Return_Reason;

### Python & AI/ML Pipeline:
• Model Architecture: Scikit-Learn Random Forest Classifier
• Target: Predict fraud probability and assign Risk Score (0 to 100%)

Python Code:
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

# Load Dataset
df = pd.read_csv("ecommerce_fraud_data.csv")

# Feature Selection
X = df[['Order_Value_INR', 'Customer_Past_Return_Count', 'City_Tier', 'Payment_Mode']]
y = df['Fraud_Order']
X = pd.get_dummies(X, drop_first=True)

# Train Test Split & Model Fitting
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)

# Generate AI Risk Score
df['average_ai_risk'] = model.predict_proba(X)[:, 1] * 100

### Dashboard Highlights:
• Executive KPI Cards: Shipping Loss, Total Orders, AI Risk Score, and Fraud Orders with trend lines and live alerts.
• Scam Pattern Analysis: Custom visual categorization covering Product Swapping, Genuine Issues, COD Fake Orders, and UPI Scams.
• AI Control Room: Real-time action recommendations with conditional risk formatting (CRITICAL, HIGH, SAFE).
