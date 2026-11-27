# Quality Control (QC) Batch Pass/Fail Classifier

A Machine Learning proof-of-concept using a **Decision Tree Classifier** to predict Quality Control (QC) pass/fail outcomes for gluten-free food production batches and identify the primary process parameters driving defects.

---

## Project Overview

In food manufacturing and chemical processing, ensuring every production batch meets strict safety and quality standards is critical. This project demonstrates an end-to-end data science workflow—from exploratory data analysis (EDA) to model tuning and interpretability—using **500 simulated production batches** (`68.6%` Pass / `31.4%` Fail, with `~3%` realistic sensor/lab noise).

### Monitored QC Parameters

| Parameter | Target Pass Window | QC Relevance |
| :--- | :--- | :--- |
| **`Gluten_Trace_ppm`** | `< 20.0 ppm` | International legal threshold for gluten-free labeling |
| **`Moisture_Pct`** | `9.0% – 13.5%` | Shelf life, microbial stability, and product texture |
| **`pH`** | `5.6 – 7.0` | Acidity control, taste, and ingredient reactivity |
| **`Oven_Temp_C`** | `172°C – 198°C` | Proper baking/drying without scorching or undercooking |
| **`Mixing_Time_min`** | `10.5 – 19.5 min` | Dough uniformity and structural consistency |

> **Engineering Note:** For fixed, independent thresholds like the ones used to generate this synthetic dataset, simple rule-based checks are sufficient. This project serves as a **scalable proof-of-concept pipeline** designed to be applied to real historical plant logs, where batch failures often stem from complex, non-obvious multi-variable interactions that manual spreadsheets miss.

---

## Model & Results

A **Decision Tree Classifier** (`criterion="entropy"`, `max_depth=9`) was trained on an 80/20 train-test split (`400` training batches, `100` unseen test batches):

* **Test Accuracy:** `95.0%`
* **Fail Class Recall:** `93.0%` (`25 / 27` defective batches correctly caught)
* **False Positives:** Only `2` out of `100` test batches—minimizing the highest-risk error in food safety (approving a defective batch).

### Top Drivers of QC Decisions (Feature Importance)
1. **Oven Temperature (`Oven_Temp_C`)** — `23.5%`
2. **Moisture Percentage (`Moisture_Pct`)** — `21.4%`
3. **pH Level (`pH`)** — `21.1%`
4. **Mixing Time (`Mixing_Time_min`)** — `19.5%`
5. **Gluten Trace (`Gluten_Trace_ppm`)** — `14.5%`

---

## Repository Structure

```text
Quality-Control-Batch-ML/
├── qc_batch_data.csv              # Simulated dataset (500 production batches)
├── qc_batch_classifier_en.ipynb   # Full Jupyter Notebook (EDA, training, evaluation)
├── qc_batch_classifier_en.pdf     # Exported visual report with code and charts
└── README.md                      # Project documentation
```

---

## Tech Stack

* **Python 3**
* **Pandas & NumPy** — Data handling and manipulation
* **Scikit-learn** — Train/test splitting, Decision Tree modeling, and evaluation metrics
* **Matplotlib** — Exploratory charts, Confusion Matrix, and Feature Importance plots

---

## How to Run Locally

1. Clone this repository:
   ```bash
   git clone https://github.com/shafiepour-chem/Quality-Control-Batch-ML.git
   cd Quality-Control-Batch-ML
   ```
2. Install the required libraries:
   ```bash
   pip install pandas numpy matplotlib scikit-learn jupyter
   ```
3. Launch Jupyter Notebook and open `qc_batch_classifier_en.ipynb`:
   ```bash
   jupyter notebook
   ```
