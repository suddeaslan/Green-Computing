# Green Computing Strategies for Healthcare Predictive Models

🌱 **A Data Science Project on Computational Sustainability in Healthcare AI**

Developed as part of the **Green Computing** course in the Master's Degree Program in Data Science at the **University of Milano-Bicocca**.

🔗 **Code Repository:** [CodeBerg - GreenEHR](https://codeberg.org/Unimib_Green_Computing_Project/GreenEHR)

---

## 👥 Authors
* **Güldeniz Güzelay** (g.guezelay@campus.unimib.it)
* **Sude Aslan** (s.aslan1@campus.unimib.it)

---

## 📌 Project Overview
As digital technologies and Artificial Intelligence grow faster than ever, their environmental footprints are expanding at an alarming rate. This project explores the crucial balance between machine learning performance and computational sustainability. Using Electronic Health Records (EHR) spanning 5 different diseases, we built baseline models, applied rigorous green computing strategies to optimize them, and evaluated the cross-platform energy efficiency of transitioning from Python to R.

### 📊 Datasets Handled
The project utilizes 5 distinct medical datasets to predict specific disease outcomes:
* **Brain Tumor:** $173 \times 31$
* **Colorectal Cancer:** $998 \times 32$
* **Heart Failure (with Depression):** $425 \times 15$
* **Sepsis/SIRS:** $1257 \times 16$
* **Neuroblastoma:** $169 \times 13$

---

## 🛠️ Methodological Workflow

### 1. Robust Preprocessing Pipeline
* **Data Cleaning:** Column standardization, duplicate removal, missing value handling using median imputation, and categorical encoding.
* **Leakage Detection:** Predefined target mapping and removal of future-informed variables (e.g., removing *"time from heart failure to death"*).
* **Feature Engineering:** Domain-specific clinical variables such as *Tumor Burden Score*, *Organ Dysfunction Indicators*, and *Disease Severity Scores*.
* **Evaluation:** Each experiment was run over **100 iterations** using different train-test splits evaluated primarily via **Matthews Correlation Coefficient (MCC)** due to class imbalances.
* **Tracking:** Environmental metrics were strictly monitored at the CPU and RAM levels via **CodeCarbon**.

---

## 🌲 Applied Green Computing Strategies

To create an energy-saving version without sacrificing predictive accuracy, the following techniques were introduced:

* **Pruning:** Feature pruning dropped elements with $< 0.3\%$ importance. Tree-structural constraints were enforced (`max_depth=6` for Random Forest; `max_depth=2`, regularizations for XGBoost) to prevent massive model structures.
* **Quantization:** Downcasted numeric features from `float64` to `float32` via custom pipeline utilities, reducing memory bandwidth and hardware heating.
* **Computation-Aware Training:** Fine-tuned estimator counts, implemented histogram-based XGBoost (`tree_method="hist"`), selected the lightweight `liblinear` solver for Logistic Regression, and relaxed convergence tolerance (`tol=1e-3`).
* **Hardware-Aware Efficiency:** Forced single-core execution (`n_jobs=1`) to eliminate multi-core context-switching overhead and thread-management waste.
* **Metric Streamlining:** Stripped out redundant evaluations (Accuracy, Precision, Recall, F1, ROC-AUC) from the internal loops, calculating only the core performance metric (MCC).

---

## 📈 Results & Key Takeaways

### Python: Baseline vs. Green-Optimized
By introducing green strategies in Python, the overall pipeline computational requirement plummeted with practically negligible impacts on accuracy:
* **Total Energy Consumption:** Decreased from **3.97 Wh to 2.05 Wh** (A massive **48.4% reduction**).
* **Total Execution Time:** Decreased from **272.2 seconds to 140.8 seconds** (**48.3% faster**).

### 🔀 Cross-Platform Comparison (Python vs. R)
Translating the optimized model into R highlighted stark architectural differences in how programming languages manage hardware loads:

| Model | Elapsed Time Change (Python → R) | Energy Consumption Change (Wh) | CO2 Emissions Change (g) | Efficiency Verdict |
| :--- | :---: | :---: | :---: | :--- |
| **Random Forest (RF)** | 📉 **-72.62%** | 📉 **-71.21%** | 📉 **-78.57%** | **R is significantly more efficient** (3.6x faster, drastically lower footprint). |
| **Logistic Regression (LR)** | 📈 +71.28% | 📈 +8.70% | 📉 -16.67% | **Marginal trade-off** (Low mathematical complexity kept them closely matched). |
| **XGBoost** | 📈 +19.60% | 📈 +48.65% | 📈 +9.09% | **Python is more efficient** (R ran slower and drew ~1.5x more energy). |

---

## 🚀 Conclusion
This research proves that **Green Computing is no longer a choice—it is a responsibility.** Sustainable tech can achieve identical performance benchmarks with significantly less harm to our planet. The choice of algorithms, hyperparameter constraints, memory handling, and even the programming language itself can drastically alter the digital carbon footprint.

---

## 📚 References
* Strubell, E., Ganesh, A., & McCallum, A. (2019). *Energy and Policy Considerations for Deep Learning in NLP*. In Proceedings of ACL.
* CodeCarbon Contributors. (2025). *CodeCarbon: Track and reduce the carbon footprint of your machine learning models*. Python Package Index.
