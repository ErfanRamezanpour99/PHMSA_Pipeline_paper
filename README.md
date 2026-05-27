# Statistical Modeling of the Probability and Duration of Hazardous Liquid Pipeline Shutdowns

Code and data for:

> Ramezanpour, E. & Hainen, A. (2026). *Statistical Modeling of the Probability and Duration of Hazardous Liquid Pipeline Shutdowns: A Hurdle Regression Approach.* Infrastructures, 11(5), 177. https://doi.org/10.3390/infrastructures11050177

## What this is

A two-stage hurdle model applied to PHMSA hazardous liquid pipeline incident data (January 2010 – May 2025):

- **Stage 1** — logistic regression for the probability of a shutdown, using pre-decision predictors only (variables observable at the time the operator decides whether to shut down).
- **Stage 2** — lognormal OLS for the duration of a shutdown, conditional on a shutdown occurring.

Final analytical sample: 4,171 incidents (Stage 1), 2,346 shutdowns (Stage 2).

## Repository layout

```
.
├── Final_code_clean.ipynb              # main analysis notebook
├── requirements.txt
├── data/
│   ├── accident_hazardous_liquid_jan2010_present.txt   # raw PHMSA dataset
│   ├── Feature name Dictionary.csv                     # column → description map
│   ├── numeric_column_summary.csv                      # numeric column metadata
│   └── categorical_uner80null_uniqueValues_imputation.csv
└── output/                             # populated by the notebook
```

The full data archive is also available on FigShare: https://doi.org/10.6084/m9.figshare.30688115

## How to run

```bash
git clone https://github.com/<your-user>/<repo-name>.git
cd <repo-name>
python -m venv .venv && source .venv/bin/activate     # or conda
pip install -r requirements.txt
jupyter notebook Final_code_clean.ipynb
```

Run the cells top-to-bottom. The MICE blocks in Section 10 each take several minutes; everything else runs in under a minute.

## What the notebook produces

All outputs land in `./output/`.

### Main text

| Output file | Paper reference |
|---|---|
| `fig1_duration_raw.pdf` | Figure 1 |
| `fig2_duration_log.pdf` | Figure 2 |
| `fig3_correlation_matrix.pdf` | Figure 3 |
| `fig4_residuals.pdf` | Figure 4 |
| `table2_categorical_descriptives.csv` | Table 2 |
| `table3_numerical_descriptives.csv` | Table 3 |
| `table4_model_fit.csv` | Table 4 |
| `table5_hurdle_coefficients.csv` | Table 5 |

### Supplementary material

| Output file | Paper reference |
|---|---|
| `tableS1_MICE_combined_stage1.csv` | Table S1 (CC vs BR vs PMM, Stage 1) |
| `tableS2_MICE_combined_stage2.csv` | Table S2 (CC vs BR vs PMM, Stage 2) |
| `tableS3_yearFE_stage1.csv` | Table S3 (year fixed-effects, Stage 1) |
| `tableS4_yearFE_stage2.csv` | Table S4 (year fixed-effects, Stage 2) |
| `tableS5_GPD_fits.csv` | Table S5 (Generalized Pareto upper-tail fits) |
| `figS1_qq_lognormal_vs_burr12.pdf` | Figure S1 (Q–Q plots) |

### Other

- `final_models.pkl` — pickled `statsmodels` result objects for both stages, both the no-FE and with-FE versions, plus the selected feature lists and Youden-J classification threshold.

## Notebook section map

| Section | Content |
|---|---|
| 0 | Imports, font setup, paths |
| 1 | Load data |
| 2 | Build the shutdown duration response variable |
| 3 | Predictor selection and pre-processing (pre/post-decision taxonomy) |
| 4 | Build model frames (encoding, log-transforms, complete-case filter) |
| 5 | Stage 1: LASSO → forward selection → final logistic fit, VIF check |
| 6 | Stage 2: LASSO → forward selection → final lognormal fit, VIF check |
| 7 | Descriptive statistics (Tables 2 and 3) |
| 8 | Hurdle coefficient table (Table 5) and model fit summary (Table 4) |
| 9 | Figures 1–4 |
| 10 | Supplementary robustness checks (year FE, heavy-tail diagnosis, MICE BR + PMM) |
| 11 | Save model artifacts |

## Environment

- Python 3.13.2
- Key packages: `pandas`, `numpy`, `scipy`, `statsmodels`, `scikit-learn`, `matplotlib`, `seaborn`

See `requirements.txt` for pinned versions.

## Data source

Raw PHMSA hazardous liquid pipeline incident data: https://www.phmsa.dot.gov/data-and-statistics/pipeline/pipeline-incident-20-year-trends

The version used in the paper covers reports through May 2025.

## Citation

```bibtex
@article{Ramezanpour2026Hurdle,
  author  = {Ramezanpour, Erfan and Hainen, Alexander},
  title   = {Statistical Modeling of the Probability and Duration of Hazardous Liquid Pipeline Shutdowns: A Hurdle Regression Approach},
  journal = {Infrastructures},
  volume  = {11},
  number  = {5},
  pages   = {177},
  year    = {2026},
  doi     = {10.3390/infrastructures11050177}
}
```

## License

Code: MIT.
Paper: CC BY 4.0 (MDPI open access).
Data: U.S. government public domain (PHMSA).

## Contact

Erfan Ramezanpour — eramezanpour1@ua.edu
