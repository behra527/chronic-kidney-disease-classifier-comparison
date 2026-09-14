# Chronic Kidney Disease Classifier Comparison

## Logistic Regression vs Random Forest

This project compares two machine learning classifiers for **Chronic Kidney Disease (CKD) risk prediction** using the UCI Risk Factor Prediction of Chronic Kidney Disease dataset.

The main focus is on **Recall**, because missing a CKD-positive patient (False Negative) can be more concerning in a medical screening context.

---

## Project Objective

The objectives of this project are to:

* Prepare and analyze the CKD dataset.
* Check data quality and potential data leakage.
* Train Logistic Regression and Random Forest models.
* Compare model performance using classification metrics.
* Analyze False Positives and False Negatives.
* Focus on Recall for clinical evaluation.
* Use 5-Fold Stratified Cross-Validation.
* Select the better-performing model.

---

## Dataset

**Dataset:** UCI Risk Factor Prediction of Chronic Kidney Disease
**Dataset ID:** 857
**Patients:** 200
**Target Variable:** `class`

### Target Classes

* `ckd` → 1
* `notckd` → 0

The dataset contains patient information such as blood pressure, blood glucose, blood-related measurements, hypertension, diabetes, anemia, appetite, and other medical factors.

---

## Data Preparation

The following steps were performed:

1. Loaded the official UCI dataset.
2. Removed metadata rows.
3. Checked dataset structure and data types.
4. Checked missing values and duplicate records.
5. Analyzed the target distribution.
6. Converted the target into binary labels.
7. Investigated potential data leakage.

### Leakage Features Removed

The following features were excluded from modeling:

* `affected`
* `stage`
* `grf`

The `affected` feature was especially important because it directly corresponded to the target outcome.

After leakage removal, **25 features** were used for modeling.

---

## Preprocessing

A Scikit-learn preprocessing pipeline was used.

### Steps

* Most-frequent imputation
* One-Hot Encoding
* `handle_unknown="ignore"`

The same preprocessing approach was used for both models to ensure a fair comparison.

The preprocessing was included inside the model pipelines to reduce the risk of preprocessing leakage during cross-validation.

---

## Train-Test Split

A stratified 80/20 train-test split was used.

* Training set: **160 patients**
* Testing set: **40 patients**

Stratification maintained a similar CKD/notCKD distribution in both sets.

---

## Models

### 1. Logistic Regression

Logistic Regression was selected as an interpretable baseline model for binary classification.

### 2. Random Forest

Random Forest was selected because it can capture nonlinear relationships using multiple decision trees.

Configuration:

* `n_estimators = 200`
* `random_state = 42`

---

## Evaluation Metrics

The models were evaluated using:

* Accuracy
* Precision
* Recall
* F1-Score
* Confusion Matrix
* False Positives
* False Negatives
* False Negative Rate
* 5-Fold Stratified Cross-Validation

### Primary Metric: Recall

Recall was prioritized because a False Negative represents a CKD-positive patient incorrectly predicted as not having CKD.

Therefore, reducing False Negatives was the main focus of the model comparison.

---

## Test Set Results

| Model               | Accuracy | Precision | Recall | F1-Score | FP | FN |
| ------------------- | -------: | --------: | -----: | -------: | -: | -: |
| Logistic Regression |     100% |      100% |   100% |     100% |  0 |  0 |
| Random Forest       |     100% |      100% |   100% |     100% |  0 |  0 |

Both models correctly classified all 40 test patients.

### Confusion Matrix

For both models:

* True Negatives = 14
* True Positives = 26
* False Positives = 0
* False Negatives = 0

---

## 5-Fold Cross-Validation

5-Fold Stratified Cross-Validation was performed to obtain a broader comparison across multiple train-validation splits.

| Model                   |    Accuracy |   Precision |      Recall |    F1-Score |
| ----------------------- | ----------: | ----------: | ----------: | ----------: |
| **Logistic Regression** | **100.00%** | **100.00%** | **100.00%** | **100.00%** |
| Random Forest           |      99.00% |     100.00% |      98.46% |      99.22% |

### Cross-Validation Result

Logistic Regression achieved better overall performance and consistency.

Since Recall was the primary metric, **Logistic Regression was selected as the preferred model for this experiment**.

---

## Final Recommendation

**Logistic Regression** was selected as the preferred model because:

* It achieved 100% mean Recall.
* It achieved 100% mean Accuracy.
* It achieved 100% mean Precision.
* It achieved 100% mean F1-Score.
* It showed consistent performance across the five folds.

---

## Limitations

This project is not a production-ready clinical system.

Important limitations include:

* The dataset contains only 200 patients.
* Perfect performance may be influenced by strong class-separating patterns in this small dataset.
* No independent external validation was performed.
* No prospective clinical testing was performed.

Larger datasets and independent clinical validation would be required before real-world healthcare use.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Seaborn
* Google Colab
* Jupyter Notebook
  
---

## Conclusion

This project demonstrated a complete machine learning classification workflow for Chronic Kidney Disease risk prediction.

Logistic Regression and Random Forest were trained using the same dataset and preprocessing pipeline. Both models achieved perfect performance on the test set, while 5-Fold Cross-Validation showed slightly better and more consistent performance from Logistic Regression.

Therefore, **Logistic Regression was selected as the preferred model for this experiment based mainly on Recall**.

The results are promising, but further validation on larger and independent clinical datasets would be necessary before considering real-world clinical use.
