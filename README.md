# Breast Cancer Diagnosis – Exploratory Data Analysis

> A thorough EDA using **NumPy · Pandas · Matplotlib · Seaborn** to uncover patterns in tumour morphology features that distinguish malignant from benign breast masses.

---

## Repository Structure

```
breast-cancer-eda/
├── Breast_Cancer_Diagnosis.csv   # Dataset (569 records, 32 features)
├── EDA_Breast_Cancer.py          # Full EDA script (all 5 steps)
├── plots/
│   ├── plot1_diagnosis_dist.png  # Countplot – class distribution
│   ├── plot2_radius_hist.png     # Histogram – radius mean by diagnosis
│   ├── plot3_boxplots.png        # Boxplots – 6 key mean features
│   ├── plot4_scatter.png         # Scatter – radius vs texture mean
│   ├── plot5_violin.png          # Violin – area mean by diagnosis
│   ├── plot6_heatmap.png         # Correlation heatmap (mean features)
│   └── plot7_pairplot.png        # Pairplot – 4 morphological features
└── README.md
```

---

## Dataset Overview

| Property | Value |
|---|---|
| Source | UCI Machine Learning Repository (Breast Cancer Wisconsin) |
| Records | 569 |
| Features | 30 numerical + 1 ID + 1 target (`Diagnosis`) |
| Target classes | **B** – Benign (357, 63%) · **M** – Malignant (212, 37%) |
| Missing values | None |

Features are computed from digitised images of fine needle aspirate (FNA) biopsies. For each cell nucleus, **mean**, **standard error**, and **worst** values of 10 measurements (radius, texture, perimeter, area, smoothness, compactness, concavity, concave points, symmetry, fractal dimension) are recorded.

---

## Setup & Usage

### Requirements

```bash
pip install numpy pandas matplotlib seaborn
```

### Run

```bash
# Clone / download the repo, then:
python EDA_Breast_Cancer.py
```

All 7 plots are saved as `.png` files in the working directory.

---

## EDA Steps

### Step 1 – Data Loading & Cleaning
- Loaded with `pd.read_csv()`; inspected shape, dtypes, and `isnull()` counts.
- Renamed `diagnosis` → `Diagnosis`; cast to `category` dtype.
- **No missing values** found; no imputation needed.

### Step 2 – Descriptive Statistics
- Separated numerical (30 features) vs categorical (`Diagnosis`) columns.
- Computed `.describe()`, mean, median, mode, and standard deviation.
- Identified that size/shape features (`area`, `radius`, `perimeter`) have high variance and right-skewed distributions.

### Step 3 – Data Visualisation

| Plot | Type | Key Takeaway |
|---|---|---|
| Diagnosis Distribution | Countplot | Benign majority (63 vs 37%) |
| Radius Mean | Histogram | Clear bimodal split between classes |
| 6 Mean Features | Boxplot | Malignant tumours larger across all features |
| Radius vs Texture | Scatter | Partial but visible linear class separation |
| Area Mean | Violin | Malignant distribution has heavier upper tail |
| Mean Features | Heatmap | radius/perimeter/area near-perfectly correlated |
| 4 Features | Pairplot | Strong inter-feature clustering by class |

### Step 4 – Insights & Conclusion *(see below)*

---

## Key Insights

1. **Class imbalance** is mild (63/37 split) but worth addressing with stratified sampling or SMOTE in any downstream model.
2. **Size features are the best separators** – malignant tumours consistently show larger radius, perimeter, and area.
3. **Extreme multicollinearity** – `radius_mean`, `perimeter_mean`, and `area_mean` correlate at *r > 0.99*. Using all three in a linear model will cause instability.
4. **Concavity and concave points are highly discriminative** – these shape irregularity features show the widest gap between classes.
5. **No data quality issues** – no nulls, no duplicates, numeric dtypes are already correct.
6. **Outliers exist** in `area_mean` and `perimeter_mean` among malignant samples, likely representing aggressive tumours.

