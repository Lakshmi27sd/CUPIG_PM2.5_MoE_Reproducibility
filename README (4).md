# CUPI-G PM2.5 Forecasting with a Peak-Weighted Mixture of Experts

This repository contains the implementation workflow accompanying the manuscript:

**Peak-Weighted Mixture of Experts for Multi-Station PM2.5 Forecasting in CUPI-G Regional Campaigns**

The public notebook provides the code used for data preprocessing, chronological data partitioning, window construction, model definition and training, ablation experiments, evaluation, statistical analysis, and manuscript-facing result generation.

## Main file

`CUPIG_PM25_MoE_Reproducibility.ipynb`

The notebook is organized as an end-to-end workflow. Run the cells in order.

## Experimental workflow

The implementation includes:

- construction and screening of hourly CUPI-G observations;
- 72-hour input windows and 24-hour PM2.5 forecasting horizons;
- chronological train/validation/test partitioning;
- training-only target transformation statistics;
- causal handling of auxiliary-covariate missingness;
- missingness indicators;
- the reference two-expert Mixture-of-Experts model;
- peak-weighted training for high-PM2.5 target hours;
- matched single-expert and capacity-matched controls;
- fixed-gate, no-station-embedding, and three-expert ablations;
- peak-weight sensitivity experiments;
- neural and deterministic comparison models;
- evaluation over random seeds 1, 7, and 21;
- overall and high-concentration performance metrics;
- gate diagnostics;
- retransformation sensitivity analysis;
- dependence-aware statistical comparisons;
- global Holm multiple-comparison correction;
- calendar-block bootstrap confidence intervals; and
- packaging of figures, tables, and numerical outputs.

## Data

The observational CUPI-G data are **not redistributed in this repository**.

Users should obtain the observational data from the original data source described in the manuscript and configure the corresponding input paths in the notebook.

Hourly PM2.5 data source:

https://aakash-rihn.org/en/data-set/

Related CUPI-G spatial analyses and meteorological maps:

https://zenodo.org/records/15702750

The repository code should not be interpreted as granting redistribution rights for third-party observational data.

## Reproducing the analysis

1. Open the notebook in Google Colab or another compatible Python environment.
2. Make the required CUPI-G source files available to the runtime.
3. Configure the data and output paths in the setup section.
4. Use the full experiment mode when reproducing manuscript results.
5. Run the notebook cells sequentially.
6. Use a fresh output directory for an independent reproduction.
7. Compare the generated experiment accounting and evaluation outputs with the corresponding manuscript tables and figures.

The complete experiment involves multiple neural configurations and random seeds and can require substantial computation. Smoke/test modes, where present, are intended only for checking the execution pipeline and should not be reported as manuscript results.

## Reproducibility safeguards

The workflow is designed so that:

- preprocessing and transformation parameters are derived from the appropriate training data;
- held-out test observations are not used for model selection;
- auxiliary missing-data handling follows the causal procedure implemented in the notebook;
- neural configurations use the predefined random seeds;
- high-concentration weighting is applied at the target-time-step level;
- statistical comparisons account for temporal dependence through daily aggregation and dependence-aware inference; and
- multiple comparisons are controlled using the global Holm procedure implemented in the analysis.

For a completely fresh reproduction, use a new output directory rather than relying on previously cached experiment artifacts.

## Software requirements

The principal Python packages are listed in `requirements.txt`.

Exact package versions can vary across compatible environments. For archival reproducibility, authors may additionally record the package versions from the final clean execution environment.

## Repository contents

- `CUPIG_PM25_MoE_Reproducibility.ipynb` — complete analysis workflow
- `README.md` — repository documentation
- `requirements.txt` — principal Python dependencies
- `.gitignore` — prevents accidental upload of raw data, model artifacts, and local runtime files
- `CITATION.cff` — citation metadata template
- `PUBLIC_RELEASE_CHECKLIST.txt` — checks to complete before making the repository public

## Results

The notebook generates the numerical outputs used for model comparison, ablation analysis, statistical testing, and manuscript figures/tables. If the uploaded notebook contains saved outputs, those outputs should be treated as execution records of that notebook. Independent reproducibility should be assessed by executing the workflow with the required source data.

## Code availability

The implementation is provided to improve transparency and reproducibility of the associated study. The observational dataset itself is not redistributed with the code.

After the GitHub repository is public, the repository URL can be inserted into the manuscript's Code Availability statement.

## Citation

Please cite the associated manuscript when using this implementation. The final journal citation should be added after publication.

## License

No software license is assigned automatically by these support files. Before public release, the authors should select a code license that is consistent with institutional requirements and any third-party data or software obligations.
