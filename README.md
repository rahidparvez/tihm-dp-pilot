# Pilot: privacy-preserving data quality checks on TIHM home-monitoring data

This repository contains a small pilot notebook that replicates, in Python, the Laplace-based differential privacy approach of Tomášik et al. (2026) on the open TIHM home-monitoring dataset. It is not an extension of their Java data quality agent.

## What the notebook does

1. Defines two patient-level quality checks on heart rate and body temperature data.
2. Shows why patient-level contribution bounding matters: counting gap events or individual readings instead of patients raises the sensitivity of a check.
3. Measures how differential privacy noise affects a quality metric as the cohort gets smaller.
4. Compares three ways of releasing a cumulative count every week under a fixed total privacy budget.

## Results (epsilon = 1, fixed random seed)

- A check for heart rate gaps of more than 7 days flagged 16 of 53 patients (30.2%).
- Its median absolute error was 2.8 percentage points on the full cohort and 14.0 points on random 10-patient cohorts.
- Over 13 weekly releases, summing noisy weekly counts (RMSE 3.71 patients) was more accurate than the basic binary tree mechanism (RMSE 9.85 patients). On a synthetic stream, the basic binary tree only became more accurate at around 4,096 releases.

## How to run

Open `TIHM_DP_pilot.ipynb` in Google Colab and select Runtime > Run all. The first cell downloads the data directly from Zenodo.

## Limitations

This is a small pilot, not a research result. The thresholds (7 days, 34-42 °C) are illustrative and not clinical criteria. In the weekly experiment the total number of patients is treated as public, and only the basic version of the binary tree mechanism is tested.

## Data and acknowledgement

TIHM dataset: F. Palermo et al., "TIHM: An open dataset for remote healthcare monitoring in dementia," Scientific Data, vol. 10, p. 606, 2023. Available on Zenodo (record 7622128) under CC-BY-4.0 for non-commercial research use. No data is stored in this repository. We acknowledge Surrey and Borders Partnership NHS Foundation Trust.

## References

- R. Tomášik et al., "Privacy-preserving data quality assessment for federated health data networks," BMC Medical Informatics and Decision Making, vol. 26, p. 49, 2026.
- C. Dwork, M. Naor, T. Pitassi, and G. N. Rothblum, "Differential privacy under continual observation," STOC 2010, pp. 715-724.
- T.-H. H. Chan, E. Shi, and D. Song, "Private and continual release of statistics," ACM Transactions on Information and System Security, vol. 14, no. 3, Art. 26, 2011.

## Author

Md. Rahid Parvez
