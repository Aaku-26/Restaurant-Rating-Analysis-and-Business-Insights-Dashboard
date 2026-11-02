# Dataset Information & Acquisition Guide

This directory documents the raw source datasets used in the **Zomato vs Swiggy – Restaurant Rating & Performance Analysis** project.

---

## 1. Raw Datasets Overview

| Dataset | Filename | Raw Size | Records | GitHub Tracking Status |
| :--- | :--- | :--- | :--- | :--- |
| **Zomato India Restaurants** | `zomato_restaurants_in_India.csv` | ~114.85 MB | 211,944 rows, 26 columns | **Excluded from Git** (Exceeds GitHub's 100 MB hard limit) |
| **Swiggy Bangalore & Metros** | `swiggy.csv` | ~0.88 MB | 8,680 rows, 10 columns | Retained locally / Documented |

---

## 2. Why is the raw Zomato dataset excluded from Git?
GitHub enforces a strict **100.00 MB maximum file size limit** on repositories. Because `zomato_restaurants_in_India.csv` is ~114.85 MB, pushing it directly to GitHub results in rejection (`error: GH001: Large files detected`).

To comply with GitHub repository best practices without requiring paid Git LFS bandwidth, the raw Zomato dataset is preserved locally on the analyst's machine and excluded from version control via `.gitignore`.

> **Note:** The final cleaned and deduplicated datasets:
> - `outputs/cleaned_zomato.csv` (~20.8 MB, 55,568 rows)
> - `outputs/cleaned_swiggy.csv` (~1.16 MB, 8,680 rows)
> - `outputs/restaurant_performance.csv` (~12.1 MB, 64,248 rows)
> 
> **Are fully tracked in this repository!** Anyone who clones this repository can immediately launch the Streamlit dashboard and run all analysis scripts without having to re-download the raw data.

---

## 3. How to Obtain the Raw Datasets (If Re-Running from Scratch)

If you wish to re-execute the raw data cleaning pipeline (`notebooks/clean_data.py`), you can download the original raw datasets from public data repositories:

1. **Zomato Restaurants in India:**
   - **Source:** Kaggle (Zomato Restaurants in India Dataset)
   - **Original Filename:** `zomato_restaurants_in_India.csv`
   - **Search Query:** `kaggle datasets download -d nilesh789/zomato-restaurants-in-india` or search "Zomato Restaurants in India" on Kaggle.
   - **Placement:** Place the downloaded CSV file in the root project folder:
     ```
     Rating Analysis/zomato_restaurants_in_India.csv
     ```

2. **Swiggy Restaurants Dataset:**
   - **Source:** Kaggle (Swiggy Restaurant Dataset for Top Indian Metros)
   - **Original Filename:** `swiggy.csv`
   - **Placement:** Place the downloaded CSV file in the root project folder:
     ```
     Rating Analysis/swiggy.csv
     ```

---

## 4. Re-Generating Cleaned Datasets
Once the raw files are placed in the root directory, simply run:
```bash
python notebooks/clean_data.py
```
This will automatically:
- Remove 156,376 duplicate records.
- Handle artificial zero ratings and missing cost values.
- Engineer derived rating, price, and popularity tiers.
- Generate `outputs/cleaned_zomato.csv`, `outputs/cleaned_swiggy.csv`, and `outputs/data_cleaning_report.txt`.
