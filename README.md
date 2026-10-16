# Which Prepaid Plan Is Better? (Megaline: Surf vs. Ultimate)

A statistical analysis of the two prepaid plans of the telecom operator Megaline, **Surf** and **Ultimate**, to find out which one generates more revenue. The commercial department wants this answer to adjust its advertising budget.

The analysis uses the 2018 usage of 500 customers (calls, messages and internet sessions) and follows the full workflow of a small data project: data cleaning, aggregation, feature engineering, exploratory analysis and hypothesis testing.

## Main findings

* **Ultimate brings in more revenue per user:** 71.82 USD per month on average, against 58.19 USD for Surf, even though Surf has the lower monthly fee (20 USD vs. 70 USD).
* **The difference is statistically significant.** Welch's t-test gives p ≈ 5.7e-08, so the null hypothesis of equal average revenue is rejected at α = 0.05.
* **Ultimate revenue is far more predictable.** Standard deviation of monthly revenue per user: about 7 USD for Ultimate and about 44 USD for Surf. Surf's tight allowances (500 minutes, 50 messages, 15 GB) and expensive overage (10 USD per extra GB) make its bills vary a lot.
* **Usage is similar across plans for calls and internet,** but Ultimate users send more messages (38.5 vs. 32.4 per month on average).
* **No regional effect:** the average revenue of users in the NY-NJ area is not significantly different from the other regions (p ≈ 0.48).

## What the notebook does

1. Loads and checks the five datasets (plans, users, calls, messages, internet), fixing data types and checking duplicated rows and keys.
2. Converts minutes and megabytes following the billing rules (calls rounded up per call, internet summed per month and then rounded up to whole GB).
3. Aggregates calls, minutes, messages and internet usage per user and month, and merges everything with the plan conditions.
4. Calculates the monthly revenue of each user (monthly fee + overage costs).
5. Compares the behavior of both plans with bar charts, histograms (normalized, because the groups have different sizes), box plots and descriptive statistics.
6. Tests two hypotheses with `scipy.stats.ttest_ind`: Surf vs. Ultimate average revenue, and NY-NJ vs. other regions.

The notebook also keeps the comments of the AI reviewer from the TripleTen program. After each point that asked for a change there is a short note saying how it was addressed.

## Repository structure

```
best_mobile_plan/
├── dataframes/
│   ├── megaline_calls.csv
│   ├── megaline_internet.csv
│   ├── megaline_messages.csv
│   ├── megaline_plans.csv
│   └── megaline_users.csv
├── best_mobile_plan.ipynb
├── README.md
└── requirements.txt
```

## Run locally

```
git clone https://github.com/<your-username>/best_mobile_plan.git
cd best_mobile_plan
python -m venv .venv
.venv\Scripts\activate          # Windows
source .venv/bin/activate       # macOS / Linux
pip install -r requirements.txt
pip install ipykernel           # to run the notebook in VS Code or Jupyter
```

Then open `best_mobile_plan.ipynb` and run all cells. The notebook reads the data from the `dataframes/` folder, so it must be opened from the project root.

## Tech stack

Python, pandas, NumPy, SciPy, Matplotlib, Seaborn, Jupyter Notebook.
