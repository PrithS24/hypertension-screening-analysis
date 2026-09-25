# Hypertension Risk-Factor Analysis of Community Health-Screening Data

Statistical analysis of 29,999 community health-screening records to identify features significantly associated with hypertension. The analysis uses the chi-square test, Fisher's exact test and the Mann–Whitney U test, with Cramér's V effect sizes and Bonferroni correction.

This repository contains the code for Task 2 of the AIMS Lab (United International University) Research Engineer technical assessment.

## Task

> Analyze the enclosed dataset and advise features that are statistically significant by applying any standard statistical operation (such as Chi-square test). Provide the algorithm and mathematical explanation of the incorporated operation. Also, suggest possible analytic outcomes based on the provided dataset.

## Data

- 29,999 individuals from 21,449 households across 16 unions
- 27,133 adults (aged 18–100) analysed; 1,575 (5.8%) recorded as hypertensive
- **The dataset is not included** because it contains personal identifiers (see [`data/README.md`](data/README.md)).

## Method

| Step | Details |
|---|---|
| Outcomes | Recorded hypertension status (primary); measured BP ≥ 140/90 mmHg (sensitivity check) |
| Preprocessing | Removed identifiers and constant columns; kept adults only; set 59 implausible readings to missing |
| Categorical features | Pearson's chi-square test, or Fisher's exact test for sparse 2×2 tables; effect size: Cramér's V |
| Continuous features | Mann–Whitney U test; effect size: rank-biserial correlation |
| Multiple testing | Bonferroni correction across 18 tests |

$$\chi^2 = \sum_{i,j} \frac{(O_{ij} - E_{ij})^2}{E_{ij}}, \qquad E_{ij} = \frac{R_i C_j}{N}, \qquad V = \sqrt{\frac{\chi^2}{N(\min(r,c)-1)}}$$

## Key results

- **Age** (V = 0.20) and **diabetes** (V = 0.34) are the strongest associations, and both are significant for recorded and measured hypertension.
- **Gender** is unrelated to recorded hypertension but not to measured BP (men 29.5% vs women 20.3%), which suggests hypertension in men is under-recorded.
- **Differences between unions** in recorded hypertension (0.0%–25.0%) do not match measured BP, which points to differences in recording practice.
- **20.4%** of adults with a BP reading who were not recorded as hypertensive (5,003 of 24,485) had a reading of 140/90 mmHg or higher.

Full results for all 18 features are in [`results/`](results/).

## Repository structure

```
├── analysis_kaggle.ipynb              # Full analysis with outputs (run on Kaggle)
├── results/
│   ├── task2_results.csv              # Recorded hypertension
│   └── task2_results_measured_bp.csv  # Measured high BP
├── data/README.md                     # Data access note
├── requirements.txt
└── LICENSE
```

## Reproducing the analysis

1. Install the dependencies: `pip install -r requirements.txt`
2. Place `test-dataset.xlsx` in `data/`, or upload it to Kaggle as a private dataset.
3. Open `analysis_kaggle.ipynb` and run all cells.

## Limitations

- Blood pressure comes from a single screening reading.
- BMI, blood sugar and SpO₂ were measured only for a non-random subset of adults.
- There is no medication data.
- Household members are not independent observations.
- The results show associations, not causation.

## Author

**Pritha Saha**, Department of CSE, Chittagong University of Engineering & Technology (CUET)
prithasaha2022@gmail.com

## License

The code is released under the [MIT License](LICENSE). The dataset is not covered by this license.
