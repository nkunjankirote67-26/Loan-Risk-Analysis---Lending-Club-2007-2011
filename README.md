# Loan Risk Analysis — Lending Club (2007–2011)

Analysis of 39,717 real consumer loans, cleaned in Python/pandas and visualized in Tableau to find what actually predicts default.

**Data source:** Kaggle ([`imsparsh/lending-club-loan-dataset-2007-2011`](https://www.kaggle.com/datasets/imsparsh/lending-club-loan-dataset-2007-2011), CC0-1.0) — real Lending Club loan data.

## Live dashboard

**[View on Tableau Public →](https://public.tableau.com/app/profile/hellen.nkunja8438/viz/ConsumerLoanRiskAnalysisLendingClub2007-2011/Dashboard1?publish=yes)**

## Summary

Starting from a raw 111-column export, this project narrows to the columns that matter, cleans what actually needs fixing, and analyzes what predicts default while checking every finding against sample size before trusting it.

**Key takeaway:** most loan purposes look similar once you check sample size — except small business loans, which default at nearly double the rate of every other well-sampled category. That's the standout, defensible finding of the project.

## Findings

1. **Grade predicts default risk cleanly, with no exceptions.** A fully monotonic increase from grade A (6.0%) to grade G (32.0%)  every grade well-sampled (minimum 316 loans).
2. **Income matters, but the real effect is modest.** A $7,600 gap between defaulted and repaid borrowers ($62,427 vs. $70,049) — a real but subtle effect, since actual default risk is driven by many interacting factors, not one dominant signal.
3. **Small business loans default at nearly double the rate of other purposes.** 26.0% vs. 10–16% for most other well-sampled categories, backed by 1,828 loans — genuinely trustworthy, not small-sample noise. Likely explanation: business loans carry venture risk (the business itself can fail), while purposes like debt consolidation are backed by steadier personal income.
4. **Loan volume grew ~2,000x in four years**, from $7,500/month (June 2007) to $31.5M/month (December 2011), with a visible contraction during the 2008 financial crisis — a real macroeconomic event showing up directly in the data.
5. **Overall default rate: 14.2%** across 39,717 loans and $445.6M in issued volume (14.6% if still-active "Current" loans are excluded — a negligible difference, so the simpler definition was kept).

## Data cleaning

| Issue | Column(s) | Fix |
|---|---|---|
| Wrong data type | `int_rate` | Removed `%` symbol, converted text to numeric |
| Inconsistent whitespace | `term` | Stripped leading/trailing spaces |
| Missing categorical data (~2.7%) | `emp_length` | Filled with an explicit `"Unknown"` category rather than the mode ("10+ years"), which was already 23% of all values and would have been exaggerated further by mode-filling |
| Default definition | `loan_status` | Defined as `"Charged Off"` only; checked that excluding still-active `"Current"` loans didn't meaningfully change the rate (14.2% → 14.6%) before deciding to keep the simpler definition |

## Repo contents

- `lendingclub_real_cleaned.csv` — cleaned dataset with engineered flag columns
- `loan_portfolio_summary_real_data.docx` — one-page findings summary
- `notebook.ipynb` — full cleaning and analysis workflow, step by step
- Tableau workbook — published directly to [Tableau Public](https://public.tableau.com/app/profile/hellen.nkunja8438/viz/ConsumerLoanRiskAnalysisLendingClub2007-2011/Dashboard1?publish=yes) rather than stored as a repo file

## Tools used

Python, pandas, Google Colab, Kaggle API, Tableau Public


