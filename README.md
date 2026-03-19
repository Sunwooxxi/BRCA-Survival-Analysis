# Survival Analysis of Breast Cancer Using GAN-Generated Synthetic Data
This study utilizes the Breast Cancer Library data provided by the National Cancer Data Center, which includes clinical information of patients within five years of diagnosis. By applying an AI generative model algorithm to create synthetic data, the research performs a survival analysis and evaluates the extent to which the synthetic data replicates actual survival patterns and risk structures.

## 1. Research Background
The high degree of data silos in the medical field serves as a major barrier to data-driven research, leading to the accelerated adoption of synthetic data as a viable solution. However, there remains a lack of in-depth discussion regarding whether synthetic data can faithfully replicate the actual risk structures in survival data analysis, which inherently possesses time-dependent characteristics. This study evaluates the statistical validity of synthetic data through survival analysis modeling of breast cancer datasets and examines the limitations regarding information loss and distortion that occur during the data synthesis process

## 2. Datasets
Data Source: Breast cancer synthetic dataset provided by the National Cancer Data Center (NCDC).
Dimensionality: 57 original variables, reduced to 29 final variables after preprocessing.
Key Outcomes:
  Death: Vital status (1 = Deceased, 0 = Censored/Alive)
  Survival_period: Survival duration measured in days.

## 3. Methodology
1. Data Preprocessing and Variable Reduction
2. Kaplan–Meier Survival Curves and Cumulative Hazard Function Analysis
3. Comparison of Survival Functions Between Groups Using the Log-Rank Test
4. Cox Proportional Hazards Model
    - Univariate Cox Analysis
    - Comparison of Full Model vs. Null Model (C-index, AIC)
    - Variable Selection Using Backward Elimination Based on AIC
5. Final Model
   - Incorporation of Clinical Relevance
   - Assessment of Interaction Effects
   - Diagnostics of the Proportional Hazards Assumption

## 4. Key Findings
- Limitations in Prognostic Granularity: Synthetic data captured general survival trajectories but struggled to isolate the distinct clinical impacts of individual prognostic factors.
- Limited Predictive Accuracy: The model demonstrated constrained predictive performance, with the C-index reflecting overall limited accuracy.
- Interpretation Caution: Results underscore the need for rigorous scrutiny of statistical significance and feature selection in synthetic data-driven survival modeling.
- 
## 5. Tech Stack
- Python: pandas, numpy, lifelines, scikit-survival, matplotlib
- Jupyter Notebook

## 6. Repository Structure
- notebooks/: Jupyter notebooks for data preprocessing, survival analysis, and model diagnostics.
- docs/: Documentation, including research papers, presentation materials, and dataset descriptions.
- data/: Raw datasets (Original source data).
- 
## 7. Documents
- `합성데이터기반 유방암 생존분석.pdf` 
- Powepoint
