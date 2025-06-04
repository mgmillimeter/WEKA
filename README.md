# 📃 Methodology 

This section outlines the step-by-step methodology followed in this study, applying the Knowledge Discovery in Databases (KDD) process to analyze student performance using WEKA. The process included data cleaning, transformation, modeling, and interpretation using both classification (J48 decision tree) and association rule mining (Apriori). Each step is documented with clear reasoning to ensure reproducibility and clarity for beginners.

---

## 🔍 Step 1: Data Understanding

Before any analysis, the dataset (`bd_students_per_uncleaned.csv`) was manually inspected to:

* Understand the structure and number of records
* Identify missing values, duplicates, and inconsistencies
* Detect irrelevant or unusable attributes

> ✉️ *Purpose: To know what we're working with and identify problems early.*

---

## ♻️ Step 2: Data Cleaning

Cleaning was applied to remove noise and prepare the dataset for modeling:

| Task                      | Action Taken                                                      | Rationale                                                    |
| ------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------ |
| Remove irrelevant columns | Dropped `id` and `full_name`                                      | These are identifiers with no impact on academic performance |
| Handle missing values     | Removed 1 record with missing `location`                          | Minimal impact from deletion; better than guessing           |
| Remove duplicates         | Eliminated 315 duplicate rows                                     | Prevents bias and inflated accuracy in modeling              |
| Fix inconsistent values   | Standardized entries in `location`, `education`, `guardian`, etc. | Ensures WEKA treats similar entries as the same class        |
| Correct attribute names   | Fixed encoding issues (e.g., `Ã¥ge` → `age`)                      | Prevents confusion during analysis and filtering             |

Final cleaned dataset: **8296 rows × 22 attributes**

> 🔧 *Cleaning ensures that our models learn from accurate and consistent information.*

---

## 🪤 Step 3: Feature Engineering

To support performance prediction:

* Created `overall_avg_score`: average of 5 subject scores per student
* Created `performance_category`: **Low / Medium / High** labels using percentile-based discretization in Excel

  * Low: bottom 33.3%
  * Medium: middle 33.3%
  * High: top 33.3%

> 🔍 *This step transforms raw scores into understandable categories for classification.*

---

## 💡 Step 4: Dataset Preparation for Modeling

Two different dataset versions were created:

### Version A: For Classification (J48, Apriori)

* **Kept**: `performance_category`
* **Removed**: `overall_avg_score`
* Applied **Discretize** filter in WEKA for numeric attributes:

  ```
  Discretize -F -B 3 -M -1.0 -R first-last -precision 6
  ```

### Version B: For Numeric Analysis (Regression, Clustering)

* **Kept**: `overall_avg_score`
* **Removed**: `performance_category`
* Applied:

  * `Normalize`: Scales values between 0 and 1
  * `NominalToBinary`: Converts categorical values to binary (0/1)

> 🔧 *Each model has different requirements, so we prepared separate datasets to match them.*

---

## 🔢 Step 5: Modeling & Analysis

### ✍️ J48 Decision Tree (Classification)

* Purpose: Predict `performance_category` based on student features
* Accuracy: **96.08%** (10-fold cross-validation)
* Key rules from the tree:

  * `stu_group = Science AND studytime > 5` ➞ High performance
  * `stu_group = Arts AND studytime <= 3.5` ➞ Low performance
  * `attendance > 91` boosts performance even with low study time

> 🌟 *J48 gives an easy-to-follow flowchart of how student characteristics lead to performance levels.*

---

### 👉 Apriori (Association Rule Mining)

* Purpose: Discover strong, frequent patterns in student data
* Applied to **discretized dataset with nominal values only**
* Configuration:

  ```
  Apriori -N 10 -C 0.9 -M 0.1 -c 17
  ```
* Sample results:

  * If `studytime = Low AND stu_group = Arts` ➞ `performance_category = Low` (99% confidence)
  * If `studytime = High` ➞ `stu_group = Science AND performance = High` (98-99% confidence)

> ✨ *Apriori reveals human-readable if-then rules that support policy-making and intervention planning.*

---

## 🔹 Summary: Why We Used These Methods

| Method  | Purpose                  | Why We Chose It (Layman’s Terms)                     |
| ------- | ------------------------ | ---------------------------------------------------- |
| J48     | Predict outcomes         | Helps understand how different factors cause results |
| Apriori | Discover common patterns | Shows what often happens among students              |

By combining both, we get:

* **Prediction + Explanation**
* **Accuracy + Interpretability**
* **Data science + Real-world insights**

> 📆 This methodology supports data-driven education research that is easy to communicate and act on.
