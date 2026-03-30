# 🧬 Breast Cancer Survival Analysis Using GAN-Generated Synthetic Data

> Evaluating whether GAN-generated synthetic clinical data can reliably replicate real-world survival patterns and prognostic risk structures.

---

## Overview

This project performs survival analysis on GAN-generated breast cancer data provided by the National Cancer Data Center (NCDC), assessing the extent to which synthetic data preserves clinically meaningful prognostic structures. The analysis follows a stepwise pipeline from Kaplan–Meier estimation through Cox proportional hazards modeling, with a focus on interpreting both statistical and clinical validity.

---

## Background & Motivation

Breast cancer is among the most prevalent malignancies in Korean women. Accurate identification of prognostic factors — including tumor stage, hormone receptor status, lymph node involvement, and histological type — requires access to large-scale, high-quality clinical data. However, increasing restrictions on personal health data have limited the use of real patient records. GAN-based synthetic data has emerged as a potential alternative, as it can learn and reproduce statistical distributions from real clinical datasets while protecting sensitive information.

Despite this promise, it remains unclear whether GAN-generated data can faithfully replicate the complex causal and structural relationships between clinical variables and survival outcomes. This project empirically evaluates that question.

---

## Dataset

- **Source**: National Cancer Data Center, South Korea
- **Type**: GAN-generated synthetic breast cancer dataset
- **Original Variables**: 59 → **Final Variables**: 29 (after preprocessing)
- **Sample Size**: 10,000 patients / 3,476 observed deaths

### Key Outcome Variables

| Variable | Description |
|----------|-------------|
| `Death` | Event indicator (1 = deceased, 0 = alive/censored) |
| `Survival_period` | Time-to-event in days |

### Selected Covariates

Clinical variables included after preprocessing: `AGE`, `BMI`, `Stage` (TNM-based), `T_stage`, `N_stage`, `M_stage`, `Diagnosis`, `BRCA_status`, `ER_clean`, `PR_clean`, `AR_clean`, `Hormone_status`, `Chemotherapy`, `Radiation_Therapy`, `Hormone_therapy`, `Surgery_type`, `Menopause_status`, `Has_birth`, `Smoke`, and others.

---

## Preprocessing

The raw dataset contained 59 variables with non-standard missing codes, redundant clinical constructs, and logical inconsistencies. Preprocessing included:

- Consolidating duplicate histological diagnosis variables into a single `Diagnosis` variable
- Reconstructing TNM staging from individual T/N/M columns using AJCC criteria
- Merging BRCA1/BRCA2 pathogenic variant and VUS flags into a unified `BRCA_status`
- Combining ER and PR receptor status into a composite `Hormone_status`
- Converting age and BMI into clinically meaningful categorical groups
- Handling missing values through median imputation or category consolidation
- Integrating treatment types (surgery, chemotherapy, radiotherapy, hormone therapy) into a single `treat` variable

---

## Methodology

1. **Kaplan–Meier Survival Estimation & Cumulative Hazard Analysis**
   - Overall survival curve: 1-yr 92.7%, 2-yr 83.3%, 3-yr 66.4%
   - Stratified KM curves and Nelson–Aalen cumulative hazard by T-stage, Diagnosis, BRCA status, and parity

2. **Log-Rank Test**
   - Applied to all categorical covariates
   - No variable reached statistical significance (all p > 0.10)
   - Highest chi-square: `Diagnosis` (χ² = 8.46, p = 0.133)

3. **Univariate Cox Proportional Hazards Model**
   - `Diagnosis` (lobular carcinoma): HR = 0.77, p = 0.029 ✓ significant
   - `BMI` and `BRCA_status` (Pathogenic): borderline significance at α = 0.20

4. **Full Multivariable Cox Model**
   - All candidate covariates included simultaneously
   - C-index: 0.528 / AIC: 57,248.88
   - Most covariates non-significant in the multivariate setting

5. **Backward Elimination (AIC-based)**
   - 13-step elimination from 14 initial covariates
   - Final AIC-selected variable: **BMI only** (C-index: 0.507, AIC: 57,206.41)
   - AIC nearly identical to null model (57,206.30), indicating minimal predictive gain

6. **Final Model Selection**
   - Combining statistical criteria with clinical reasoning
   - Final model covariates: **BMI** + **Diagnosis** + **BRCA_status**
   - C-index: 0.518 / AIC: 57,209.70

7. **Interaction Effect Testing**
   - Three candidate interactions evaluated via likelihood ratio test (LRT)
   - BRCA × Diagnosis: LRT p = 0.087 (borderline), but AIC increased (+7.11)
   - No interaction term improved model fit; main-effects model retained

8. **Proportional Hazards Assumption Diagnostics**
   - Schoenfeld residual test: no violation detected for any covariate
   - Log–log survival curves: curves approximately parallel across categories
   - Nelson–Aalen log cumulative hazard: no crossing or nonlinear pattern
   - Martingale / Deviance residuals: no influential outliers, stable fit

---

## Key Findings

| Finding | Detail |
|--------|--------|
| Overall survival trend | Reasonably reproduced by GAN model |
| Group-level prognostic separation | Limited — KM curves largely overlapping |
| Log-rank test | No variable significant at α = 0.05 |
| Best univariate predictor | Lobular carcinoma (HR = 0.77, p = 0.03) |
| Full model C-index | ~0.53 (marginally above random) |
| AIC-selected model | BMI only — near null model performance |
| PH assumption | Satisfied across all final model covariates |

---

## Conclusions & Limitations

GAN-generated data successfully reproduced the **overall shape** of the survival function, but **failed to preserve the fine-grained prognostic structure** associated with individual clinical variables. The near-null predictive performance (C-index ≈ 0.52) across all model specifications suggests that the synthetic data generation process did not adequately capture the complex causal relationships between covariates and survival outcomes.

**Limitations:**
- Synthetic, not real, clinical data — limits clinical generalizability
- AIC-selected model (BMI only) conflicts with known clinical evidence
- Findings underscore the need to combine statistical criteria with clinical judgment when analyzing synthetic survival data

This work provides a rigorous analytical **template** that can be directly applied to real patient data in future studies.

---

## Tech Stack

- **Language**: Python 3
- **Libraries**: `pandas`, `numpy`, `lifelines`, `scikit-survival`, `matplotlib`, `scipy`
- **Environment**: Jupyter Notebook

---

## Project Structure

```
BRCA-Survival-Analysis/
├── data/
│   ├── Adjusted_synbreast_trainset.csv
│   ├── 합성데이터설명(유방암).csv
│   └── 암임상+라이브러리+합성데이터(폐암,유방암,대장암)+설명서.pdf
├── notebook/
│   └── 합성데이터 기반 유방암 생존분석.ipynb
├── report/
│   └── 합성데이터 기반 유방암 생존분석.pdf
└── README.md
```

---

## Authors

- 김서윤 (Seoyun Kim)
- 정선우 (Sunwoo Jung)

*Capstone Design — Practical Survival Analysis with Medical Data*

---

## References

- 김재희. (2025.). R을 이용한 생존분석 기초. 자유아카데미.
- 공경엽. (2006). 유방암에 있어서 예후 및 치료 예측인자. Journal of the Korean Society for Breast Screening, 3(1), 5–12.
- 윤성욱, 우혜경, 김정은. (2021-06-23). 유방암 생존 예측: 특성 선택 및 예측 모델 비교, 그리고 유전적 특성의 효과. 한국정보과학회 학술발표논문집, 제주.
