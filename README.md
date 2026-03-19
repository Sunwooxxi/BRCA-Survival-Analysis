# 🧬 Survival Analysis of Breast Cancer Using GAN-Generated Synthetic Clinical Data

> Evaluating whether GAN-generated synthetic clinical data can reliably replicate real-world survival patterns and risk structures.

---

## Overview

This project investigates the validity of synthetic medical data in survival analysis.  
Using GAN-generated breast cancer datasets, we apply classical survival analysis methods to assess whether synthetic data can reproduce real-world survival behavior and clinical risk structures.

---

## Motivation

- Medical data silos limit access to high-quality clinical datasets  
- Synthetic data is emerging as a scalable alternative  
- However, its reliability in time-to-event (survival) analysis remains unclear  

This project aims to **evaluate whether synthetic data preserves statistical validity in survival modeling**

---

## Dataset

- **Source**: National Cancer Data Center (NCDC)  
- **Type**: GAN-generated synthetic breast cancer dataset  
- **Original Variables**: 57 → **Final Variables**: 29 (after preprocessing)

### Outcome Variables
- `Death`: 1 = Deceased, 0 = Alive / Censored  
- `Survival_period`: Time-to-event (days)

---

## Methodology

1. **Data Preprocessing and Variable Reduction**  
2. **Kaplan–Meier Survival Curves & Cumulative Hazard Analysis**  
3. **Log-Rank Test for Group Comparison**  
4. **Cox Proportional Hazards Model**
   - Univariate Cox Analysis  
   - Full Model vs. Null Model Comparison (C-index, AIC)  
   - Backward Elimination Based on AIC  
5. **Final Model**
   - Incorporation of Clinical Relevance  
   - Interaction Effect Assessment  
   - Proportional Hazards Assumption Diagnostics  

---

## Key Findings

- Synthetic data captures overall survival trends but fails to distinguish fine-grained prognostic effects  
- Predictive performance is limited (low C-index)  
- Risk structure distortion and information loss are observed during data generation  
- Careful interpretation is required when applying synthetic data to survival modeling  

---

## Tech Stack

- **Python**: pandas, numpy, lifelines, scikit-survival, matplotlib  
- **Environment**: Jupyter Notebook

---

## Repository Structure
```
├── data/           # Raw and processed datasets (NCDC Synthetic Data)
├── docs/           # Research papers, presentation slides, and data dictionaries
├── figures/        # Visualization plots (KM-curves, Hazard functions, etc.)
├── notebooks/      # Jupyter notebooks for preprocessing, modeling, and diagnostics
└── README.md       # Project overview and key findings
```
---

## Documents

- `합성데이터기반_유방암_생존분석.pdf`  
- `presentation.pptx`  

---

## Contact

For questions or collaboration, feel free to reach out.
