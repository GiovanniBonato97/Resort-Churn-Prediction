# Compliance-Aware Customer Churn Prediction – Integrated Resorts

## Business problem
Australian integrated resorts must retain valuable customers while meeting strict responsible-gambling obligations. Sending retention offers to at-risk gamblers is ineffective and non-compliant, and can lead to fines and licence risk.

**Question:** How can a resort keep customers who are likely to leave, while identifying at-risk gamblers who should get support instead of promotions?

## Approach
A two-stage classification framework:
1. **Stage 1 – Churn vs retained:** predicts which customers are likely to disengage.
2. **Stage 2 – Voluntary disengagement vs at-risk gambling:** separates the cause of churn so each group gets the right action.

## Data
- **Customer_data** (Roy & Pandit, 2024): 2,000 resort customers with behavioural features such as booking frequency, revenue, meals and loyalty status.
- **Online_casino_DIB** (Ghaharian, 2023): 138,928 casino transactions (deposits, bets, withdrawals).

**Data preparation**
- Removed names and emails so individuals can't be identified.
- Checked for missing values and removed 72 duplicate transactions.
- Aggregated transactions per account into features: total transactions, average transaction amount, weekly transactions, monthly amount, declined transaction rate, night-time activity ratio.
- Labelled the data using behavioural thresholds and an 80/20 train/test split.

## Models and results
| Stage | Best model | Key metric |
|---|---|---|
| 1 – Churn prediction | Logistic Regression | F1 = 0.906, ROC-AUC = 0.916 |
| 2 – At-risk gambling detection | Decision Tree | Recall = 0.993 |

Logistic Regression, Decision Tree and Random Forest were compared. F1 was used for Stage 1 to balance wasted retention spend against lost customers; recall was used for Stage 2 because missing an at-risk gambler is the costliest error.

## Key insights (SHAP)
- **Churn drivers:** low booking frequency, low revenue and no loyalty membership.
- **Gambling-risk drivers:** high monthly spend, high average transaction size, frequent declined transactions and late-night activity.

## Recommendations
- **Voluntary churners:** targeted offers (accommodation, dining, loyalty rewards) instead of blanket promotions, to cut wasted marketing spend.
- **At-risk gamblers:** no promotions; route them to self-exclusion options, deposit limits and human compliance review.
- Use model outputs to support staff decisions, not replace them.

## Limitations
- The two public datasets share no customer IDs, so the stages can't be linked end to end.
- Near-perfect Stage 2 results may reflect overfitting from threshold-based labels; validation on real resort data is needed.

## Tools
Python · pandas · scikit-learn · SHAP · Power BI · Google Colab


## Files
| File | Description |
|---|---|
| [churn_prediction.ipynb](churn_prediction.ipynb) | Full analysis: data prep, models, SHAP |
| [Elevator_Pitch.pdf](Elevator_Pitch.pdf) | 7-slide project summary |
| [Project_Report.pdf](Project_Report.pdf) | Detailed project report |
| [customer_data_clean.xlsx](customer_data_clean.xlsx) | Cleaned and aggregated datasets |
