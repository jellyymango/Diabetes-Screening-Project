# Diabetes Risk Screening Tool

**Evaluating Machine Learning Classification Models for Diabetes Risk Screening**

SJSU CMPE 257 — Machine Learning

🔗 **Live app:** https://diabetes-screening.streamlit.app/

\---

## Overview

Diabetes is one of the most prevalent chronic diseases worldwide, and early
screening is a critical step in reducing long-term complications and healthcare
costs. This project evaluates four supervised classification models — Logistic
Regression, Random Forest, XGBoost, and Support Vector Classification (SVC) — for
diabetes risk screening, and deploys the best-performing models as an interactive
Streamlit web application.

The application supports a **two-stage screening workflow**:

* A low-barrier **Self Assessment** that uses only self-reportable, accessible
inputs to produce a preliminary risk indication.
* A higher-accuracy **Clinical Assessment** that additionally accepts laboratory
measurements (fasting blood sugar, HbA1c, blood pressure) for a more reliable
estimate.

> ⚠️ \*\*Disclaimer:\*\* This tool is for \*\*educational purposes only\*\* and is \*\*not a
> medical diagnosis\*\*. It should not be used as a substitute for professional
> medical advice, diagnosis, or treatment. Always consult a qualified healthcare
> provider regarding any medical concern.

\---

## Features

* **Two screening modes** selectable from a single interface:

  * *Self Assessment* — accessible demographic, lifestyle, symptom, and history
inputs, scored with the accessible-feature **SVC** model.
  * *Clinical Assessment* — all of the above plus lab measurements, scored with
the full-feature **XGBoost** model.
* **Probability output** rendered numerically and as a progress bar.
* **Binary risk decision** using a 0.40 prediction threshold
("Diabetic" / "Not Diabetic").
* **Borderline warning** for results between 0.30 and 0.40, prompting the user to
seek further evaluation.
* **Mode-specific confidence note** communicating the lower reliability of
accessible-only inference.

\---

## Getting Started

### Prerequisites

* Python 3.9+
* `pip`

### Installation \& Local Run

```bash
# Clone the repository
git clone https://github.com/jellyymango/Diabetes-Screening-Project.git
cd Diabetes-Screening-Project

# (Optional) create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\\Scripts\\activate

# Install dependencies
pip install -r requirements.txt

# Launch the app
streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`.



### Dependencies

`streamlit`, `pandas`, `scikit-learn`, `xgboost`, `joblib` — exact pinned
versions are listed in [`requirements.txt`](requirements.txt).

\---

## Dataset

The models were trained on the public
[Diabetes Health Dataset](https://www.kaggle.com/datasets/rabieelkharoua/diabetes-health-dataset-analysis)
by R. El Kharoua (Kaggle, 2024): 1,879 patient records and 46 columns, reduced to
43 predictors after removing the non-informative identifier and a constant
column. The dataset is synthetic, so reported metrics should be interpreted as
upper-bound estimates under idealized conditions.

\---

## Results

Stratified 5-fold cross-validation on the **full feature set**:

|Model|F1|ROC-AUC|
|-|:-:|:-:|
|Logistic Regression|0.7927|0.9053|
|Random Forest|0.8742|0.9554|
|**XGBoost**|**0.9156**|**0.9579**|
|SVC (RBF)|0.7999|0.9094|

XGBoost is the strongest performer on the full feature set. When restricted to
the 25 accessible (self-reportable) features, performance collapses across all
models (best ROC-AUC ≈ 0.599), which is why the Self Assessment mode is presented
only as a low-fidelity prompt to seek clinical follow-up rather than as a
diagnostic.

\---

## Authors

* **Aaron Yalong** — Department of Computer Engineering, San José State University
* **Joseph Manivong** — Department of Computer Engineering, San José State University
* **Serey Roth** — Department of Computer Engineering, San José State University

\---

## License

This project was developed as academic coursework for SJSU CMPE 257 and is
intended for **educational use only**. If you wish to reuse or extend this work,
please contact the authors. Consider adding a formal open-source license (e.g.,
MIT) if you intend to distribute it more broadly.

