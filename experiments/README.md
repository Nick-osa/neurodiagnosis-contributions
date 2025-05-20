## 🧪 General Experiment Overview

This repository presents a series of machine learning experiments for the **early prediction of Alzheimer's Disease (AD)** using **non-invasive features**. The aim is to identify scalable biomarkers and high-performing models that minimize reliance on invasive or subjective measures such as CSF tests or clinical scores.

### 🎯 Objectives
- Classify cognitive stages (CN, MCI, Dementia) using non-invasive data  
- Benchmark shallow ANNs and classical ML models  
- Ensure clinical relevance and interpretability (via SHAP)

### 🔁 Experiment Roadmap

| Experiment | Description           | Features Used                             |
|-----------:|------------------------|--------------------------------------------|
| 1          | Baseline ANN           | Age, APOE4, MMSE, CDRSB, Hippocampus/ICV   |
| 2          | Non-invasive only      | Age, APOE4, MRI biomarkers only            |
| 3          | Expanded MRI features  | Cortical thickness, ventricular volume, etc. |
| 4+         | Model comparisons      | Classical ML models (RF, SVM, etc.)        |

### 📊 Evaluation
- Accuracy, confusion matrix, class-wise performance  
- Feature importance via SHAP for explainability



# 🧠 ANN Model – Experiment 1

Baseline experiment using a shallow Artificial Neural Network (ANN) to classify Alzheimer's stages (CN, MCI, Dementia) from the cleaned ADNIMERGE dataset.

## 🔍 Features Used
- **Age** (Demographic)
- **APOE4** status (Genetic risk factor)
- **MMSE**, **CDRSB** (Clinical scores)
- **Hippocampus/ICV** (MRI biomarker)

## 🧱 Model Architecture
- Shallow ANN with 2 hidden layers
- Output: 3-class softmax
- Loss: Categorical crossentropy
- Optimizer: Adam

## 📊 Results
- **Accuracy**: ~91%
- **Key drivers** (via SHAP): MMSE, Hippocampal volume
- Establishes baseline for future experiments with expanded features and model depth

---------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🧠 ANN Model – Experiment 2

Follow-up experiment focused on addressing class imbalance and improving interpretability. SMOTE was applied to improve classification of underrepresented classes (e.g., Dementia), and SHAP was introduced to explain model predictions. A Logistic Regression baseline was added for comparison.

## 🔍 Features Used
- **Age** (Demographic)
- **APOE4** status (Genetic risk factor)
- **MMSE**, **CDRSB** (Clinical scores)
- **Hippocampus/ICV** (MRI biomarker)

## 🧱 Model Architecture
- Shallow ANN with 2 hidden layers + dropout
- Output: 3-class softmax
- Loss: Categorical crossentropy
- Optimizer: Adam
- Compared with Logistic Regression

## ⚖️ Class Imbalance Handling
- Applied **SMOTE** to oversample Dementia cases
- Improved recall and precision for minority class, though still room for improvement

## 📊 Results
- **ANN Accuracy**: ~91%
- **Logistic Regression**: Comparable accuracy but lower performance in non-linear class boundaries
- **Key drivers** (via SHAP): CDRSB, MMSE, Hippocampus/ICV
- **APOE4**: Least impactful feature

## 🧠 Interpretability
- Applied **SHAP** for feature attribution
- Validated clinical relevance of top features
- Helped build trust in model decisions

## 🔄 Next Steps
- Expand MRI biomarkers (e.g., Cortical Thickness, Ventricular Volume)
- Test more complex ANN architectures and classical models (e.g., Random Forest)
- Apply cross-validation for robustness

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 🧠 ANN Model – Experiment 3

This experiment explores the predictive power of non-invasive features—MRI biomarkers, age, and APOE4 status—for classifying Alzheimer's Disease stages (CN, MCI, Dementia). The goal is to assess how well models perform **with and without clinical scores** (MMSE, CDRSB) and to interpret key contributors using SHAP.

## 🔍 Features Used

### Base Feature Set (non-invasive):
- **Age** (Demographic)
- **APOE4** (Genetic)
- **MRI Volumes** (normalized):
  - Hippocampus
  - Entorhinal
  - MidTemporal
  - Ventricles
  - Fusiform
  - WholeBrain

### Extended Feature Set:
- **MMSE**, **CDRSB** (Clinical scores)

## 🧱 Model Architecture
- Shallow and moderately deep ANN models
- Output: 3-class softmax (CN, MCI, Dementia)
- Loss: Categorical crossentropy
- Optimizer: Adam
- Compared with Logistic Regression

## 📊 Results
- **Accuracy**: ~90–91% with clinical scores
- **Performance dropped** when MMSE and CDRSB were removed
- All models, including logistic regression, showed **strong dependence on cognitive scores**

## 🧠 SHAP Insights

### Cognitively Normal (CN)
- High MMSE, low CDRSB, large hippocampus and whole brain volume
- Younger age and APOE4-negative status also supported CN predictions

### Mild Cognitive Impairment (MCI)
- Moderate CDRSB and MMSE levels
- MRI biomarkers had modest contribution; more sensitive features may be needed

### Dementia
- High CDRSB, low MMSE
- Smaller hippocampus, larger ventricles had strong impact
- SHAP showed limited MRI feature influence when clinical scores were excluded

## 🔄 Next Steps
- Add **non-invasive biomarkers** (e.g., blood-based, extended demographic and polygenic scores)
- **Improve MRI feature engineering**:
  - Create region-based ratios (e.g., hippocampus/ventricles)
  - Compute brain asymmetry scores
  - Normalize by age or ICV, use z-scores for volumetric deviations
- Evaluate models trained **without cognitive scores** to test potential for early, non-invasive prediction


