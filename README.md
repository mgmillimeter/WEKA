# 📊 Multivariate Analysis of Socioeconomic and Educational Factors Influencing Student Performance in Bangladesh

_Multivariate Analysis of Socioeconomic and Educational Factors Influencing Student Performance in Bangladesh: A Knowledge Discovery in Databases (KDD) Approach_  

---

## 📝 Abstract

Understanding the multifactorial influences on student academic performance is crucial for developing evidence-based educational policies. While innate ability contributes to academic success, socioeconomic and educational factors play substantial roles. This study investigates how parental education, employment, family size, geographic location, study time, attendance, tutoring, extracurricular activities, and internet access influence academic outcomes among secondary school students in Bangladesh. The Knowledge Discovery in Databases (KDD) framework was employed, involving selection, preprocessing, transformation, data mining, and interpretation phases. A structured dataset was extracted from Kaggle, followed by thorough data cleaning, outlier treatment, feature engineering, and multivariate classification using Decision Tree, Random Forest, and Support Vector Machine models. The Decision Tree classifier demonstrated superior performance with 77.7% accuracy, identifying academic group, study time, and attendance as the most significant predictors. The findings contribute to the educational data mining literature and offer practical implications for policymakers and educational institutions in tailoring targeted academic interventions.
---

## 🔑 Keywords

Student Performance, Socioeconomic Factors, Educational Data Mining, Knowledge Discovery in Databases, Bangladesh Education, Machine Learning.
---

# 1️⃣ Introduction

1.1 Background and Problem Statement
Academic performance is widely regarded as a multidimensional outcome shaped by numerous interacting factors. Beyond cognitive ability, research highlights the role of external determinants such as socioeconomic status (SES), parental education, school environment, and student habits in influencing learning outcomes (Sirin, 2005; OECD, 2019). These factors are particularly significant in developing countries, where educational inequalities often mirror broader socioeconomic disparities. Bangladesh, like many developing nations, faces challenges in ensuring equitable access to quality education. Policymakers and educators require evidence-based insights to better understand how various social, familial, and institutional factors influence student achievement. Despite numerous studies investigating individual influences, limited research explores the combined, multivariate effects of these variables. Therefore, adopting multivariate analytical approaches becomes essential to reveal complex interdependencies often missed by traditional univariate methods.
---

# 2️⃣ Literature Review

- Socioeconomic status significantly affects academic achievement ([Sirin, 2005](#references)).
- Educational data mining (EDM) reveals complex educational relationships ([Romero & Ventura, 2010](#references)).
- Prior work emphasizes the importance of parental education, school type, tutoring, and attendance ([Hanushek & Woessmann, 2011](#references)).
- The interaction between multiple variables is underexplored for Bangladesh — this study fills that gap.

---

# 3️⃣ Research Objectives

1. Investigate how socioeconomic and educational factors affect student academic performance in Bangladesh.
2. Apply multivariate models to identify the most influential predictors of academic success.
3. Provide empirical evidence to guide data-driven education policy interventions.

---

# 4️⃣ Research Significance

- Provides actionable insights for policymakers, administrators, and educational institutions.
- Contributes to the academic field of educational data mining.
- Demonstrates practical application of the Knowledge Discovery in Databases (KDD) framework on real-world educational data.

---

# 5️⃣ Methodology: Knowledge Discovery in Databases (KDD)

### 5.1 Selection (Data Collection)
- **Source:** [Kaggle - Bangladesh Student Performance EDA](https://www.kaggle.com/code/ashikshahriar/bangladesh-student-performance-eda/input)
- **Sample size:** 8,608 students
- **Variables:** academic scores, parental education and occupation, demographics, study time, attendance, tutoring, internet access, extracurricular activities.

### 5.2 Preprocessing (Data Cleaning)
- Mode imputation for missing values (location).
- Categorical inconsistencies standardized (capitalization, merging Hons→Honors).
- Outliers detected using IQR method; academic outliers retained, age filtered to 13-20 years.
- No duplicates found.

### 5.3 Transformation (Feature Engineering)
- Generated `Total Score` (sum of subject scores).
- Derived `Performance Category` (Low, Average, High) using 20th & 80th percentiles.
- Applied one-hot encoding to categorical features.

### 5.4 Data Mining (Modeling)
- Models applied:
  - Decision Tree (J48)
  - Random Forest
  - Support Vector Machine (SVM)
- 80/20 train-test split; evaluation via accuracy and F1-score.

### 5.5 Interpretation & Evaluation
- Extracted feature importance and decision rules.
- Compared findings against prior educational literature.
- Identified actionable insights for educational interventions.

---

# 6️⃣ Results and Discussion

### 6.1 Descriptive Statistics

| Variable | Mean | SD | Min | Max |
| -------- | ---- | -- | --- | --- |
| Total Score | 291 | 65 | 54 | 500 |
| Study Time (hours/day) | 4.2 | 1.8 | 0 | 10 |
| Attendance (%) | 80 | 15 | 0 | 100 |
| Age (years) | 16.5 | 1.7 | 13 | 20 |

### 6.2 Model Performance

| Model | Accuracy (%) |
| ----- | ------------- |
| Decision Tree | **77.7** |
| Random Forest | 77.6 |
| SVM | 66.3 |

### 6.3 Top Predictors (Feature Importance)

| Rank | Feature | Importance (%) |
| ---- | ------- | --------------- |
| 1 | Academic Group (Commerce/Science) | 44% |
| 2 | Study Time | 9.6% |
| 3 | Attendance | 0.4% |
| 4 | Extracurricular Participation | 0.7% |
| 5 | Guardian Type | 0.2% |
| 6 | Parental Involvement | 0.15% |
| 7 | Father’s Job | 0.09% |

### 6.4 Extracted Decision Rules

- Science students + ≥6 hours/day study + high attendance → High Performance.
- Commerce students + low study time + poor attendance → Low Performance.

---

# 7️⃣ Practical Implications

- **For schools:** Emphasize study habits, extracurricular activities, attendance monitoring.
- **For policymakers:** Implement study skill programs, parental involvement initiatives.
- **For researchers:** Demonstrate practical application of KDD + ML in education policy.

---

# 8️⃣ Limitations

- Kaggle data may not fully represent national population.
- Cross-sectional dataset limits causal inference.
- Psychological, motivational, and cognitive factors not included.

---

# 9️⃣ Future Research

- Expand to national-level longitudinal datasets.
- Include psychological, motivational, and emotional variables.
- Apply ensemble ML models and deep learning.
- Cross-country comparative studies.

---

# 🔬 Tools Used

- **WEKA 3.8.6** (J48 Decision Tree, Random Forest, SVM)
- **Python (pandas, scikit-learn, docx, matplotlib)** (Preprocessing, Reporting)
- **Excel** (Manual data cleaning and transformation)
- **WebGraphviz** (Decision Tree visualization)

---

# 📚 References

- Sirin, S. R. (2005). Socioeconomic status and academic achievement: A meta-analytic review. *Review of Educational Research, 75*(3), 417–453.
- Romero, C., & Ventura, S. (2010). Educational data mining: A review of the state of the art. *IEEE Transactions on Systems, Man, and Cybernetics, Part C*, 40(6), 601–618.
- Hanushek, E. A., & Woessmann, L. (2011). The economics of international differences in educational achievement. *Handbook of the Economics of Education*, 3, 89–200.
- Coleman, J. S., et al. (1966). *Equality of Educational Opportunity*. U.S. Dept. Health, Education, and Welfare.
- OECD. (2019). *PISA 2018 Results: What Students Know and Can Do*. OECD Publishing.
- Siemens, G., & Baker, R. S. (2012). Learning analytics and educational data mining: Towards communication and collaboration. *Proc. of the 2nd International Conf. on Learning Analytics and Knowledge*, 252–254.

---

# ⚠ License

This project is intended for academic and educational research purposes. For non-commercial use only.

---
