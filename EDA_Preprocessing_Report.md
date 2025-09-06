# EDA & Data Pre‑Processing Report

**Author:** Hayrunnisa Yavuz  
**Email:** yavuzs811@hotmail.com
**Email:** yavuzs811@hotmail.com

**Data Source:** `Talent_Academy_Case_DT_2025.xlsx`  

## 1) Dataset Overview

- Shape: **2235 rows × 18 columns**

- Numeric columns: 7  
- Categorical/Other columns: 11

### Column Dtypes (first 20)

                column   dtype
               HastaNo   int64
                   Yas   int64
              Cinsiyet  object
              KanGrubu  object
                 Uyruk  object
        KronikHastalik  object
                 Bolum  object
                Alerji  object
               Tanilar  object
             TedaviAdi  object
          TedaviSuresi  object
       UygulamaYerleri  object
        UygulamaSuresi  object
      TedaviSuresi_num float64
    UygulamaSuresi_num float64
 KronikHastalik_sayisi   int64
        Tanilar_sayisi   int64
UygulamaYerleri_sayisi   int64



## 2) Missing Values

```
                column  missing_count
                Alerji            944
              KanGrubu            675
        KronikHastalik            611
       UygulamaYerleri            221
              Cinsiyet            169
               Tanilar             75
                 Bolum             11
               HastaNo              0
      TedaviSuresi_num              0
        Tanilar_sayisi              0
 KronikHastalik_sayisi              0
    UygulamaSuresi_num              0
             TedaviAdi              0
        UygulamaSuresi              0
          TedaviSuresi              0
                   Yas              0
                 Uyruk              0
UygulamaYerleri_sayisi              0
```

## 3) Descriptive Statistics (Numeric)

```
                         count        mean      std       min       25%       50%       75%       max
HastaNo                 2235.0  145333.100  115.214  145134.0  145235.0  145331.0  145432.0  145537.0
Yas                     2235.0      47.327   15.209       2.0      38.0      46.0      56.0      92.0
TedaviSuresi_num        2235.0      14.571    3.725       1.0      15.0      15.0      15.0      37.0
UygulamaSuresi_num      2235.0      16.573    6.269       3.0      10.0      20.0      20.0      45.0
KronikHastalik_sayisi   2235.0       1.870    1.501       0.0       0.0       2.0       3.0       4.0
Tanilar_sayisi          2235.0       2.502    1.674       0.0       1.0       2.0       3.0      13.0
UygulamaYerleri_sayisi  2235.0       0.934    0.357       0.0       1.0       1.0       1.0       2.0
```

## 4) Key Visualizations

![eda_fig_age_hist.png](eda_fig_age_hist.png)

![eda_fig_top_departments.png](eda_fig_top_departments.png)

![eda_fig_corr_heatmap.png](eda_fig_corr_heatmap.png)

![eda_fig_top_diagnoses.png](eda_fig_top_diagnoses.png)

## 5) Data Pre‑Processing Summary

- Missing value handling:

  - Multi‑label columns (e.g., `Tanilar`, `UygulamaYerleri`) imputed via **KNNImputer** over multi‑hot representations.

  - `Bolum` filled using **mode** based on keys (e.g., `Tanilar`, `TedaviAdi`, `UygulamaYerleri`).

  - `Cinsiyet` imputed via KNN over numeric proxy (0/1) then mapped back to labels.

  - `Alerji` cleaned (lowercasing, typo fixes, dedup on comma‑separated items).

- Feature engineering:

  - Extracted numeric durations: `TedaviSuresi_num`, `UygulamaSuresi_num`.

  - Counts from multi‑label fields: `KronikHastalik_sayisi`, `Tanilar_sayisi`, `UygulamaYerleri_sayisi`.

- Encoding:

  - Multi‑label → multi‑hot (0/1) via **MultiLabelBinarizer**.

  - Single categorical (e.g., `Uyruk`, `KanGrubu`, `TedaviAdi`) → **One‑Hot** if modeling required.

- Scaling (optional, for distance‑based/linear models):

  - Apply **StandardScaler** to numeric features (`Yas`, durations). Store as separate columns or overwrite.

## 6) Next Steps

- Export a modeling‑ready table (e.g., `df_oh.csv`) with encodings applied.

- Train baseline models:

  - Multi‑class (`Bolum`): Logistic Regression / RandomForest; report macro‑F1.

  - Multi‑label (`UygulamaYerleri`): OneVsRest(LogReg); report micro/macro‑F1 or Jaccard.

- Add a confusion matrix and per‑class metrics to understand failure modes.
