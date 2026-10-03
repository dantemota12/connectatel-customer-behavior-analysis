# ConnectaTel Customer Behavior Analysis: Usage Segmentation & Churn Insights
Analyzed 4,000 customers and 40,000 usage events from a Latin American telecom with Python: data cleaning, usage and age segmentation, outlier detection, and churn insights with plan recommendations.

## Objective
Evaluate the behavior of ConnectaTel customers (2024 data) to build a statistical profile, detect atypical behavior, create customer segments, and recommend retention strategies and plan improvements.

## Datasets
| File | Description | Rows |
|---|---|---|
| plans.csv | Current plans (price, included minutes, messages and GB, extra costs) | 2 |
| users_latam.csv | Customers (age, city, registration date, plan, churn date) | 4,000 |
| usage.csv | Real usage of calls and text messages | 40,000 |

## Tools
Python · Pandas · NumPy · Seaborn · Matplotlib · Jupyter Notebook

## Process
1. Loaded and explored the three datasets (structure, data types, nulls).
2. Identified data quality problems: sentinel values, impossible dates and missing values.
3. Cleaned the data: replaced the age sentinel with the median, converted unknown cities to nulls, and flagged future dates.
4. Verified that nulls in `duration` and `length` depend on the event type (calls vs. messages), so they were kept as logical nulls.
5. Built usage metrics per user (messages, calls and call minutes) and merged them with the customer table.
6. Visualized distributions by plan with histograms and detected outliers with boxplots and the IQR method.
7. Segmented customers by usage level (low, medium, high) and by age (young, adult, older adult).
8. Translated the findings into an executive summary with recommendations.

## Data Quality Issues Found
| Column | Issue | Records |
|---|---|---|
| `age` | Sentinel value -999 | 55 (1.38%) |
| `city` | Sentinel "?" (plus missing values) | 96 (2.4%) |
| `reg_date` | Impossible future dates (year 2026) | 40 (1.0%) |
| `usage.date` | Missing values | 50 (0.13%) |

Nulls in `duration` (55.2%) and `length` (44.7%) are expected: duration only applies to calls and length only to messages.

## Key Findings
1. **Usage segments:** Medium use is the largest segment (73.6%, 2,943 users), followed by Low use (19.4%) and High use (7.0%, 279 users).
2. **Age does not drive usage:** The share of each usage level is almost the same across young, adult and older adult customers, so usage level, not age, is what differentiates customer behavior.
3. **High-use customers consume more than double** the low-use group (9.6 vs. 3.1 messages, 5.9 vs. 2.8 calls, and 30.1 vs. 14.9 call minutes on average).
4. **High-use customers also show the highest churn** (14.0% vs. about 11.5% in the other groups). The gap is small and based on a small group, so it should be confirmed before acting on it.
5. **Outliers are plausible heavy usage, not errors**, so they were kept. The Basic plan concentrates 60.6% of the call-minute outliers.

## Recommendations
- Design a high-consumption plan for the high-use segment, which may be paying extra charges under the current plans.
- Review the Basic plan: include a more generous minutes package or encourage migration of heavy users to Premium.
- Prioritize retention of the high-use segment (loyalty discounts or proactive plan upgrades).
- Do not use age as a commercial segmentation criterion; focus campaigns on actual usage level.

## How to Run
1. Open the notebook in Google Colab or Jupyter.
2. Install the requirements: `pandas`, `numpy`, `seaborn`, `matplotlib`.
3. Place `plans.csv`, `users_latam.csv` and `usage.csv` in a `/datasets/` folder (or change the paths in the loading cell).
4. Run all cells in order.

## Files
- `sprint_7_-_cuaderno_de_jupiter_-_S7_Version-Estudiante-Project-ConnectaTel.ipynb`: full analysis notebook (cleaning, segmentation, visualization and executive summary).
- `images/`: screenshots of the charts.
- [Download the notebook from Google Drive](https://drive.google.com/file/d/1CXO7xKcUKCEmqAmG6IcPniGZu2fgQSv4/view?usp=sharing)
