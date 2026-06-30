# WHO Global Life Expectancy Prediction

A Stacking Ensemble Framework with Novel Feature Engineering and GroupKFold Validation for Global Life Expectancy Prediction

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)

## Overview

This repository contains the complete code, models, and results for a machine learning research study predicting global life expectancy using the WHO Global Health Observatory (GHO) dataset. The proposed Stacking Ensemble achieves **R²=0.9873**, surpassing the current published state-of-the-art (R²=0.9423) by **4.76%**, while reducing prediction error (MAE) by **50.4%** compared to the best published benchmark.

This work addresses a critical methodological gap in prior research on this dataset: the absence of country-grouped cross-validation, which causes temporal data leakage and inflated performance estimates in all previously published studies.

## Key Results

| Model | R² | MAE (years) | RMSE (years) |
|---|---|---|---|
| Linear Regression | 0.8532 | 2.7032 | 3.7030 |
| Random Forest | 0.9091 | 2.0661 | 2.9140 |
| MLP Neural Network | 0.8793 | 2.5446 | 3.3583 |
| LightGBM | 0.9215 | 2.0320 | 2.7078 |
| XGBoost | 0.9235 | 1.9406 | 2.6730 |
| **Stacking Ensemble (Proposed)** | **0.9873** | **0.7698** | **1.0873** |
| SOTA — Dolgopolyi et al. (2025) | 0.9423 | — | — |
| SOTA — Omondi et al. (2023) | — | 1.554 | 2.402 |

All results evaluated under **GroupKFold (k=5)** cross-validation — countries never split across train/test folds, eliminating data leakage present in all prior published work on this dataset.

## Key Contributions

1. **Country-grouped cross-validation** (GroupKFold, k=5) — first application on this dataset, preventing temporal data leakage
2. **Three novel composite features** — Composite Immunization Index, Socioeconomic Score, and Mortality Burden Index
3. **Stacking Ensemble** combining XGBoost, LightGBM, Random Forest, and MLP via a Bayesian-optimised Ridge meta-learner
4. **First SHAP interpretability analysis** on this dataset, identifying HIV/AIDS prevalence as the dominant predictor

## Dataset

- **Source:** [WHO Life Expectancy Dataset (Kaggle)](https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who)
- **Size:** 2,938 observations, 193 countries, 2000–2015
- **Target:** Life expectancy at birth (years)

Download the dataset CSV from Kaggle and place it in the project root before running the notebook.

## Repository Structure

```
who-life-expectancy-prediction/
├── README.md
├── LICENSE
├── requirements.txt
├── who_life_expectancy_prediction.ipynb
├── figures/
│   └── (24 publication-quality figures, 300 DPI)
└── paper/
    └── WHO_LifeExpectancy_Paper.pdf
```

## Installation

```bash
git clone https://github.com/sandeshkumar/who-life-expectancy-prediction.git
cd who-life-expectancy-prediction
pip install -r requirements.txt
```

## Usage

1. Download the dataset from Kaggle and place `LifeExpectancyData.csv` in the project root
2. Open `who_life_expectancy_prediction.ipynb` in Jupyter or Google Colab
3. Run all cells sequentially — the notebook is organised by research day (Day 1–8)
4. Trained models and figures are saved automatically to local directories

## Methodology Summary

- **Preprocessing:** Two-stage grouped country-level median imputation (handles 44% feature missingness), log transformation of 6 skewed features, Winsorization at 1.5×IQR
- **Validation:** GroupKFold (k=5) — countries never appear in both train and test folds
- **Models:** Linear Regression, Ridge, Lasso, Decision Tree, Random Forest, XGBoost, LightGBM, MLP, Stacking Ensemble
- **Hyperparameter Tuning:** Optuna Bayesian optimisation (150 trials for XGBoost, 50 for LightGBM and Random Forest)
- **Interpretability:** SHAP (SHapley Additive exPlanations) analysis on best single model

## Citation

If you use this code or findings in your research, please cite:

```bibtex
@article{kumar2026lifeexpectancy,
  author  = {Kumar, Sandesh},
  title   = {Beyond Conventional Benchmarks: A Stacking Ensemble Framework
             with Novel Feature Engineering and GroupKFold Validation
             for Global Life Expectancy Prediction},
  year    = {2026},
  institution = {Sukkur Institute of Business Administration},
  url     = {https://github.com/sandeshkumar/who-life-expectancy-prediction}
}
```

## Author

**Sandesh Kumar**
Department of Computer Science (Artificial Intelligence)
Sukkur Institute of Business Administration (Sukkur IBA University)
[sandeshkumar.bscsaif24@iba-suk.edu.pk](mailto:sandeshkumar.bscsaif24@iba-suk.edu.pk)

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

## Acknowledgements

Dataset originally compiled by Deeksha Russell and Duan Wang. Kaggle distribution by [Kumar, A. (2017)](https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who).
