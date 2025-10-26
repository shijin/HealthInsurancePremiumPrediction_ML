# Health Insurance Premium Prediction
## Project Overview

This project predicts health insurance premiums based on personal and health-related factors like age, BMI, smoking status, income, medical history, etc.
To ensure accuracy and fairness, two separate models were developed:

Model	      Segment	      Algorithm	      R² Score
Model A	   Age > 25	   XGBoost Regressor	 0.997
Model B	   Age ≤ 25	   Linear Regression	 0.988

The system is deployed as a Streamlit web application so insurance underwriters can calculate premium from anywhere.

## Objective

- Build a high-accuracy premium prediction model
- Maintain fairness for younger customers by segmenting models
- Deploy the solution as an interactive and user-friendly UI
- Provide explainability for every prediction

## Exploratory Data Analysis

- Minimal missing values → safely removed
- Outliers in age, dependants, income removed using quantile rule
- Most customers:
  - Age: Balanced spread
  - Income: Majority 0–40 Lakhs
  - Smoking: ~68% non-smokers
  - Region: Mostly Southeast region
- Age and genetic health risk positively correlated with higher premiums
- No major data quality issues after cleaning

## Feature Engineering

- Converted medical history into a numeric risk score
- Applied MinMaxScaler for scaling selected features
- One-Hot Encoding for categorical features
- Removed highly correlated features based on VIF analysis
- Final data split: 70% Train / 30% Test

## Model Development

Initial single-model approach caused large errors for customers aged ≤ 25.

## Solution: Segmented modeling

- Segment	Approach	Outcome
Age > 25	XGBoost	Very high accuracy, error < 0.5%
Age ≤ 25	Linear Regression	Error reduced from 72% → 2.04%

## Final models saved as:

- `model_rest.joblib`
- `model_young.joblib`
- `scaler_rest.joblib`
- `scaler_young.joblib`

## Evaluation Metrics

- R² Score: 98% – 99%
- MAE: ~₹6100
- Over 97% predictions within ±10% threshold
- Post segmentation:
  - Fairness improved
  - Extreme errors drastically reduced

## Deployment

- App built using Streamlit
- Cloud hosted → Accessible from any browser
- Clear UI for entering customer information
- Shows which age-segment model was used

## Explainability

To maintain trust and transparency:
- SHAP used for global & local explanations
- Displays top drivers influencing premium
- Avoids "black-box" decisions for underwriters

## Ethical AI & Governance

- No personal identity details stored → Privacy preserved
- Fairness checks across:
  - Gender
  - Smoking Status
  - BMI Category
  - Region
  - Income Segment
- Human-in-the-loop recommended for high-risk predictions
- Clear disclaimers: Assistive tool, not final underwriting decision

## Tech Stack

- Python
- Pandas, NumPy
- Scikit-learn, XGBoost
- SHAP
- Streamlit
- Joblib

## How to Run Locally

- pip install -r requirements.txt
- streamlit run app/main.py

## Business Impact

- Faster and more consistent underwriting
- Enhanced customer experience
- Operational efficiency with automation
- Scalable assistive tool for pricing teams

## Future Enhancements

- Include more clinical data for better prediction
- Add uncertainty estimates in UI
- Automate retraining with updated pricing policies
- Integration with insurer’s internal systems

## AI Governance

-	Model was evaluated for its fairness & bias.
-	Residual risk evaluation was done.
-	SHAP was used to explain overall contribution of each feature to the premium prediction.

## Author

Shijin Ramesh  
Data Scientist | Machine Learning Practitioner
[Email](kshijin92@gmail.com) | [LinkedIn](https://www.linkedin.com/in/shijinramesh/) | [Portfolio](https://www.shijinramesh.co.in/)
