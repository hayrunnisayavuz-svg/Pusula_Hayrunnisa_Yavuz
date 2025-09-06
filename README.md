# Pusula_Name_Surname — Data Analysis Case

**Author:** Hayrunnisa Yavuz  
**Email:** yavuzs811@hotmail.com
**Email:** yavuzs811@hotmail.com

> **Repo name format:** `Pusula_Hayrunnisa_Yavuz`

A comprehensive data analysis project covering **Exploratory Data Analysis (EDA)** and **Data Pre‑Processing** for the Talent Academy case dataset. The workflow includes missing‑value handling, categorical encoding, feature engineering, (optional) scaling, and exports of reports/figures suitable for review and modeling.

---

## 🚀 Objectives
- Understand the dataset structure and quality (EDA)
- Clean and preprocess data for analysis/modeling
- Engineer useful features (durations, multi‑label counts, encodings)
- Produce a lightweight report and reproducible notebook

---

## 📦 Features

### Core
- **EDA**: shape, dtypes, missing map, descriptive stats, top‑k category frequencies
- **Visuals**: histograms, bar charts (Top Departments/Diagnoses), numeric **correlation heatmap**
- **Missing Values**:
  - `Tanilar`, `UygulamaYerleri`: **MultiLabelBinarizer + KNNImputer**
  - `Cinsiyet`: KNN (0/1 proxy) → back to labels
  - `Bolum`: Mode imputation using keys (`Tanilar`, `TedaviAdi`, `UygulamaYerleri`)
  - `Alerji`: lowercase, typo fixes, de‑dup on comma‑separated items
- **Feature Engineering**:
  - Numeric extraction: `TedaviSuresi_num`, `UygulamaSuresi_num`
  - Multi‑label counts: `KronikHastalik_sayisi`, `Tanilar_sayisi`, `UygulamaYerleri_sayisi`
- **Encoding**:
  - Multi‑label → multi‑hot (0/1)
  - Single categoricals (e.g., `Uyruk`, `KanGrubu`, `TedaviAdi`) → One‑Hot (if modeling)
- **(Optional) Scaling**:
  - `StandardScaler` for numeric features (e.g., `Yas`, durations)

### Deliverables
- `TALENTPUSULA.ipynb` — main notebook
- `EDA_Preprocessing_Report.md` — human‑readable EDA & preprocessing summary
- `figures/` — exported charts (PNG)
- (Optional) `df_processed.csv` / `df_oh.csv` — modeling‑ready tables

---

## 📊 EDA Highlights

- **Dataset size:** 2,235 rows × 18 columns
- **Top missing fields:**  
  - Alerji: 944  
  - KanGrubu: 675  
  - KronikHastalik: 611  
  - UygulamaYerleri: 221  
  - Cinsiyet: 169
- **Numeric snapshot (examples):**  
  - Age (Yas): mean ≈ 47.3  
  - TedaviSuresi_num (sessions): median = 15  
  - UygulamaSuresi_num (minutes): median = 20  
  - Tanilar_sayisi: mean ≈ 2.50
- **Key visuals:** Age histogram, Top-10 Departments, Numeric correlation heatmap, Top-20 Diagnoses
- **Full report:** see `reports/EDA_Preprocessing_Report.md`


## 🧹 Pre-processing Summary

- Missing values:  
  - `Tanilar`, `UygulamaYerleri` → MultiLabelBinarizer (multi‑hot) + **KNNImputer** (then mapped back to strings)  
  - `Cinsiyet` → KNN with 0/1 proxy, then back to labels  
  - `Bolum` → mode imputation using keys (`Tanilar`, `TedaviAdi`, `UygulamaYerleri`)  
  - `Alerji` → lowercasing, typo fixes, de‑dup on comma‑separated items
- Feature engineering: numeric durations (`TedaviSuresi_num`, `UygulamaSuresi_num`) and multi‑label counts  
- Encoding: multi‑label → multi‑hot; single categoricals (e.g., `Uyruk`, `KanGrubu`, `TedaviAdi`) → One‑Hot (if modeling)  
- (Optional) Scaling: **StandardScaler** on numeric features (e.g., `Yas`, durations)


## 🧰 Requirements
- **Python**: 3.9+ (3.10 recommended)
- Packages: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`, `xlsxwriter`, `jupyter`

Example `requirements.txt`:
```
pandas>=2.0
numpy>=1.24
scikit-learn>=1.3
matplotlib>=3.7
seaborn>=0.12
xlsxwriter>=3.1
jupyter>=1.0
```

---

## 🗂 Project Structure (suggested)
```
Pusula_Name_Surname/
├── data/
│   ├── Talent_Academy_Case_DT_2025.xlsx
│   └── Talent_Academy_Case_DT_2025_filled.xlsx   # (after preprocessing)
├── notebooks/
│   └── TALENTPUSULA.ipynb
├── reports/
│   ├── EDA_Preprocessing_Report.md
│   └── figures/
│       ├── eda_fig_age_hist.png
│       ├── eda_fig_top_departments.png
│       ├── eda_fig_corr_heatmap.png
│       └── eda_fig_top_diagnoses.png
├── src/
│   ├── preprocessing.py        # (optional) reusable functions
│   └── features.py             # (optional) feature engineering helpers
├── outputs/
│   └── df_oh.csv               # (optional) modeling-ready table
└── README.md
```

---

## 🧭 Workflow / Architecture
- **Notebook‑driven** EDA & preprocessing (MV* flavor):
  - *Views*: notebook charts (matplotlib/seaborn)
  - *Logic*: preprocessing & imputation functions (KNN/Mode)
  - *Data*: Excel input → cleaned DataFrame → exports (CSV/Excel/MD/PNG)

**Pipeline Steps**
1. Load data (`read_excel`)
2. EDA: shape/dtypes/missing/plots
3. Clean & Impute:
   - Multi‑label → multi‑hot (MLB) → **KNNImputer** → write back to string columns
   - Mode imputation for `Bolum` via key combos
   - `Cinsiyet` KNN (0/1 → label)
   - `Alerji` cleaning
4. Feature Engineering: durations (num), counts from multi‑labels
5. (Optional) Encoding & Scaling: One‑Hot; StandardScaler
6. Export: report, figures, processed tables

---

## 🛠️ Setup & Installation
1) **Clone**
```bash
git clone <your-repo-url>
cd Pusula_Name_Surname
```
2) **Create & activate venv**
```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate
```
3) **Install**
```bash
pip install -r requirements.txt
```
4) **Run notebook**
```bash
jupyter notebook notebooks/TALENTPUSULA.ipynb
```
5) **Outputs**
- `reports/EDA_Preprocessing_Report.md`
- `reports/figures/*.png`
- (optional) `outputs/df_oh.csv`

---

## 📊 Key Visuals (examples)
- Age histogram, Top‑10 Departments, Correlation heatmap, Top‑20 Diagnoses

> In this environment, sample figures were exported as:  
- `figures/eda_fig_age_hist.png`  
- `figures/eda_fig_top_departments.png`  
- `figures/eda_fig_corr_heatmap.png`  
- `figures/eda_fig_top_diagnoses.png`

---

## ✅ Quality & Reproducibility
- Set random seeds (`random_state=42`) in ML steps
- Keep **before/after missing** table in the report
- Track data versions (`data/`)

---

## 🧪 (Optional) Baseline Modeling
- **Multi‑class** (`Bolum`): Logistic Regression / RandomForest → Macro‑F1
- **Multi‑label** (`UygulamaYerleri`): One‑Vs‑Rest Logistic → Micro/Macro‑F1, Jaccard
- **Regressions** (e.g., `UygulamaSuresi_num`): MAE

---

## 🐛 Troubleshooting
- **KNNImputer leaves NaNs**: add more numeric context (age, durations, counts) or lower/adjust threshold when binarizing.
- **One‑Hot column explosion**: limit to top‑K categories or use hashing.
- **Charts not rendering**: check backend or run `%matplotlib inline` in Jupyter.

---

## 🔒 Ethics & Compliance (KVKK)
- Remove/obfuscate direct identifiers
- Use aggregated views in the report
- Keep consent & data usage documentation if required

---

## 🔮 Future Enhancements
- Automated `src/pipeline.py` to export modeling‑ready tables
- Class imbalance handling & error analysis (confusion matrix, SHAP)
- Notebook → HTML/PDF export for sharing
- Unit tests for preprocessing utilities

---

## 📧 Contact
- **Hayrunnisa Yavuz** — yavuzs811@hotmail.com

