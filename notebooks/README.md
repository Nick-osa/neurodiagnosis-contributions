**This folder contains different python scripts for preprocessing of the ADNIMERGE and the PPMI datasets, new scripts would be added each time withouth explicit description in the README**

# Data Preprocessing

This folder contains scripts for cleaning and preparing raw data.

The ADNIMERGE has characteristic missingness of data. our plan is to progressively create models around the most available dataset.

Clinical Data
Low missingness (<3%): PTID, VISCODE, AGE, APOE4 

Moderate missingness (~30%): DX, MMSE, CDRSB 

MRI Data
High missingness (40-50%): Hippocampus/Entorhinal volumes 

PET/CSF Biomarkers
Very high missingness (75-85%): AV45, ABETA, TAU 

# Plan
Implemet the models in phases based around data availability

1. Use clinical + genetic data (AGE, APOE4, MMSE, CDRSB) with diagnosis-stratified imputation.

2. Add MRI data for reduced but richer dataset.

3. Exclude PET/CSF unless doing targeted biomarker studies.

# Workflow

## Scripts
- `ADNIMERGE_PREPROCESSING.py` - Examine data for missingness to select features
- `Visualize_neurodegenerative_biomakers.py` - Visualize how key biomakers affect AD progression and outcomes
- `ADNI_baseline_clean_csv.py` - Outputs a clean df with some selected MRI and genetic features for initial ML test model
-  ADNI_clean_data_exploration - Ouputs visualization that describes class imbalance and feature correlations


*ADNI_baseline_clean_csv.py*


Data Cleaning for ADNI

This script prepares a clean subset of the ADNIMERGE dataset (from the Alzheimer's Disease Neuroimaging Initiative) for machine learning tasks. It focuses on extracting baseline data (VISCODE == 'bl') and selecting biologically relevant features including demographics, clinical scores, imaging biomarkers, and genotype data.


Key Steps:

- Selects relevant features: AGE, APOE4, Hippocampus, ICV, MMSE, CDRSB, DX.

- Normalizes hippocampal volume using intracranial volume (Hippocampus_ICV).

- Stratified median imputation for MMSE and CDRSB by diagnosis (DX).

- Encodes missing APOE4 values using the most frequent value per diagnosis group.

- Removes rows missing critical features (DX, APOE4, Hippocampus_ICV).

- Verifies missing values and retains a clean, analysis-ready dataset.

- Exports a final .csv file for downstream ML modeling.

Output:

ADNI_baseline_clean.csv: Cleaned and preprocessed baseline data.


*ADNI_clean_data_exploration*

ADNI Baseline clean Dataset Exploratory Data Analysis (EDA)

This script performs Exploratory Data Analysis (EDA) on the ADNI baseline clean dataset to inform preprocessing and model selection for machine learning tasks.

Purpose
- Analyze dataset characteristics to identify challenges for model building.
- Understand distributions of target variable (`DX` diagnosis) and key features.
- Guide preprocessing steps and model development decisions.

Objectives
1. *Class Balance Assessment**: Visualize diagnosis distribution (CN, MCI, Dementia).
2. *Continuous Variable Exploration**: Analyze distributions/outliers in:
   - Age
   - Hippocampus_ICV
   - MMSE (Mini-Mental State Examination)
   - CDRSB (Clinical Dementia Rating Sum of Boxes)
3. *Feature Correlation Analysis**: Identify relationships between continuous variables.
4. *Diagnosis-Feature Relationships**: Visualize feature distributions across diagnoses.

 📊 Outputs Generated
| Visualization | Purpose |
|---------------|---------|
| `Count Plot` | Diagnosis class distribution |
| `Histograms` | Feature distributions & outliers |
| `Correlation Matrix` | Pairwise feature relationships |
| `Box Plots` | Feature distributions per diagnosis |



