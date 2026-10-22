# CardioRisk â€” Cardiovascular Disease Prediction

Model-selection case study: predict cardiovascular disease (CVD) risk from patient health
records so a healthcare provider can prioritise high-risk patients and allocate doctor
consultation time.

**Stack:** Python Â· Pandas Â· scikit-learn Â· Matplotlib Â· Seaborn

---

## Problem

CardioCare wants to identify high-risk patients in advance instead of relying on
first-come-first-served consultations. Framed as binary classification on routine health
checkup data.

## Dataset

- **70,000 patient records**, 14 columns (age, gender, height, weight, blood pressure,
  cholesterol, glucose, lifestyle flags, `cardio` target)
- After cleaning: **68,648 rows**, 12 modelling features, near **50:50** class balance

## Cleaning & feature engineering

- Dropped the duplicate index column and the unique `id`.
- Removed physiologically impossible blood pressure (`ap_hi`/`ap_lo` outside 30â€“300 mmHg,
  diastolic â‰¥ systolic), height outside 100â€“250 cm, weight outside 30â€“200 kg.
- Converted age from days to years and height from cm to metres.
- Engineered **BMI** and age features for clinical interpretability.

## Models compared

| Model | Train Acc | Test Acc | Test Recall | Test AUC |
|---|---|---|---|---|
| Logistic Regression | 0.731 | 0.725 | 0.717 | 0.773 |
| Decision Tree (default) | 0.996 | 0.633 | 0.628 | 0.632 |
| **Decision Tree (tuned) â€” chosen** | 0.724 | **0.707** | **0.716** | **0.773** |
| Random Forest | 0.996 | 0.696 | 0.689 | 0.757 |

**Overfitting control:** the default tree memorised the training set (99.6% train vs 63.3%
test). Grid search with `max_depth=10`, `min_samples_leaf=20`, `min_samples_split=100`
cut the trainâ€“test gap from **36 points to 1.7 points**, with no loss in AUC.

**Insight:** the tuned non-linear model matches logistic regression at AUC 0.773, so most
of the predictive signal in these features is linear â€” non-linear BP Ã— cholesterol
interactions add limited lift.

## Files

| File | Description |
|---|---|
| `CardioRisk_Prediction.ipynb` | EDA, cleaning, feature engineering, model building and evaluation |
| `CardioRisk_Prediction_Report.pdf` | Full written report with figures and model justification |

---

**Author:** Rajat Singh Â· [LinkedIn](https://www.linkedin.com/in/rajatsingh-dataanalyst) Â· [Portfolio](https://github.com/Rajat-Singh-Source/data-analytics-portfolio) Â· [Profile](https://github.com/Rajat-Singh-Source)

