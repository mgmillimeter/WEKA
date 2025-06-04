# 📃 Methodology (Final Version for Research Paper)

This section outlines the step-by-step methodology followed in this study, following the **Knowledge Discovery in Databases (KDD)** process to analyze student performance using WEKA. The process included data selection, cleaning, transformation, modeling, and interpretation using both **classification (J48 decision tree)** and **association rule mining (Apriori)**.

---

## 🔁 Steps in the Knowledge Discovery in Databases (KDD) Process

### 1. Selection (Data Collection)

* Selected the dataset: `bd_students_per_uncleaned.csv`
* Defined variables of interest: demographic, academic, and family-related features
* Removed unrelated fields (e.g., student ID, full name)

> 🧠 *We only kept information useful for understanding performance.*

---

### 2. Preprocessing (Data Cleaning)

| Task                      | Action Taken                                      | Why It Matters                                          |
| ------------------------- | ------------------------------------------------- | ------------------------------------------------------- |
| Remove irrelevant columns | Dropped `id` and `full_name`                      | IDs don’t help in analysis                              |
| Handle missing values     | Deleted 1 row with missing `location`             | With just 1 missing row, deletion was simpler           |
| Remove duplicates         | Removed 315 duplicate rows                        | Prevents duplicate patterns from biasing models         |
| Standardize categories    | Cleaned `location`, `guardian`, `education`, etc. | Ensures values are consistent (e.g., "hons" → "Honors") |
| Fix attribute names       | Corrected encoding issues like `Ã¥ge` → `age`     | Makes attributes readable and usable in WEKA            |

Final dataset after cleaning: **8296 rows × 22 attributes**

> 🧼 *Clean data means reliable results.*

---

### 3. Transformation (Feature Engineering)

* Created `overall_avg_score` = average of 5 subject scores
* Generated `performance_category` (Low, Medium, High) using percentile bins in Excel:

  * Low = bottom 33.3%
  * Medium = middle 33.3%
  * High = top 33.3%

> 🔁 *We translated raw numbers into labeled categories for easier modeling.*

---

### 4. Data Mining (Modeling in WEKA)

Two versions of the dataset were prepared:

#### Version A – For Classification (J48, Apriori):

* `overall_avg_score` removed (to avoid leaking actual score into model)
* `performance_category` kept as class attribute
* Applied this Discretize filter:

  ```
  Discretize -F -B 3 -M -1.0 -R first-last -precision 6
  ```

#### Version B – For Numeric Analysis (e.g., Linear Regression):

* `performance_category` removed
* Kept `overall_avg_score`
* Applied:

  * `Normalize` to scale numeric values from 0 to 1
  * `NominalToBinary` to convert categorical data to binary form

> 🛠️ *Different tools require different formats — we prepped both.*

---

### 5. Interpretation & Evaluation (Results)

#### 📌 J48 Decision Tree (Classification)

* Accuracy: **96.08%**
* Key insights:

  * If `stu_group = Science` and `studytime > 5`, performance = High
  * If `stu_group = Arts` and `studytime <= 3.5`, performance = Low
  * High `attendance` compensates for low study time

> 🌳 *The tree shows how each factor affects student outcomes in a visual, step-by-step path.*

#### 📌 Apriori (Association Rules)

* Goal: Identify frequent, confident rules about performance
* Applied to nominal dataset using:

  ```
  Apriori -N 10 -C 0.9 -M 0.1 -c 17
  ```
* Top rules:

  * If `studytime = Low` AND `stu_group = Arts` → `performance = Low` (99% confidence)
  * If `studytime = High` → `stu_group = Science AND performance = High` (98–99%)

> 📋 *These rules are easy to explain and great for policy decisions.*

---

## ✅ Summary Table: Why These Methods Were Used

| Step             | Purpose                        | Tool Used    | Why It’s Important                                               |
| ---------------- | ------------------------------ | ------------ | ---------------------------------------------------------------- |
| Data Cleaning    | Ensure data is clean and valid | Manual/Excel | Prevents garbage in, garbage out                                 |
| Feature Creation | Add interpretable indicators   | Excel        | Allows classification and numeric modeling                       |
| J48              | Predict performance outcomes   | WEKA         | Visual and accurate classifier for decision support              |
| Apriori          | Discover frequent patterns     | WEKA         | Easy-to-read rules that help spot common risk or success factors |

> 🧩 This combined method supports clear, explainable, and actionable education insights.
