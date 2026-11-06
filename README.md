# Telco Customer Churn Analysis

End-to-end churn analysis of 7,043 telecom customers using **Python, SQL (SQLite), pandas, Matplotlib/Seaborn and scikit-learn**: who churns, why, how much revenue it costs, and which active customers to contact first.

## Business Questions
1. What is the overall churn rate and how much revenue does it cost?
2. Which contracts, tenure groups, services and payment methods are linked to the highest churn?
3. Which active customers should a retention team prioritise?
4. Can churn be predicted on customers the model has not seen?

## Key Results
| Metric | Result |
|---|---|
| Churn rate | 26.5% (1,869 of 7,043 customers) |
| Monthly revenue lost to churn | 30.5% of total (churners pay about 21% more than retained customers) |
| Month-to-month vs two-year contract churn | 42.7% vs 2.8% |
| Churn in first 12 months vs 49-72 months | 47.4% vs 9.5% |
| Fiber optic share of lost revenue | about 82% |
| Electronic check customers | 45.3% churn, 57% of all churners |
| High-risk tier (6-factor score) | 36% of customers, about 74% of churners |
| Active high-risk revenue at risk | 1,182 customers, about 28% of active monthly revenue |
| Logistic regression (held-out test set) | ROC-AUC 0.842 (simple risk score: 0.818) |

Findings show associations, not proven causes: factors such as fiber optic and month-to-month contracts overlap.

## Workflow
1. **Load**: CSV into a SQLite database; raw table kept unchanged
2. **Clean**: `TotalCharges` text to numeric (11 blanks = new customers with tenure 0), churn flag, consistent Yes/No values
3. **Feature engineering**: tenure groups, charge groups, number of add-ons, internet and auto-pay flags
4. **Analysis**: KPIs and churn by segment, calculated in both SQL and pandas (results match)
5. **Visualisation**: churn by contract, tenure, internet service, payment method, add-ons; charge distributions
6. **Risk score**: 6 points (month-to-month, tenure up to 12 months, fiber optic, electronic check, no tech support, no online security); exported a ranked priority retention list
7. **Model**: logistic regression, 80/20 stratified split, threshold trade-off (0.5 vs 0.3)

## Recommendations
- Offer incentives to move month-to-month customers to longer contracts
- Run a first-year retention programme
- Investigate fiber optic pricing and service quality
- Encourage automatic payment instead of electronic check
- Offer tech support and online security trials to internet customers who lack them
- Contact the high-risk tier first, ordered by monthly charges

## Limitations
- Single snapshot with no dates, so no time trends or churn reasons
- No currency stated; revenue is in dataset units
- Risk score factors were chosen from the same data they were measured on; the test-set model result is the fairer measure
- Basic model with no tuning or cross-validation

## Project Structure
```
├── data/            raw CSV, SQLite database, cleaned and feature CSVs
├── outputs/         charts (PNG) and priority_retention_list.csv
├── notebooks/       Jupyter notebook (or the .ipynb in the repo root)
└── README.md
```

## How to Run
```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
jupyter notebook
```
Download the **Telco Customer Churn** dataset (`WA_Fn-UseC_-Telco-Customer-Churn.csv`) from Kaggle into `data/`, then run the notebook top to bottom.

## Tools
Python, pandas, NumPy, SQL (SQLite), Matplotlib, Seaborn, scikit-learn, Jupyter

## Author
Amish Raut
