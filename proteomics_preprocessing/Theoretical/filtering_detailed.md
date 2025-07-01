
# ✂️ Filtering in Proteomics Data Analysis  
## From Missing Values to IQR – Making Data Cleaner for Confident Interpretation

**Author:** Abdullah Ibrahim  
**Tags:** proteomics, filtering, bioinformatics, preprocessing, IQR, missing-values

---

## 🔍 Introduction

In proteomics and other omics analyses, raw data often contains unwanted noise — missing values, low-abundance proteins, or features with little variation. **Filtering** is the step where we decide *which data points to keep*, and which to discard to improve overall data quality.

This is not just a technical cleanup — filtering directly affects the sensitivity and accuracy of your downstream biological interpretations.

In this article, we explore four common filtering strategies:
- **Missing Value Filtering**
- **IQR Filtering**
- **Low Intensity Filtering**
- **Group-wise Presence Filtering**

---

## 🚫 1. Missing Value Filtering

**Concept:**  
Proteins that are not consistently detected across samples are unreliable and can introduce bias, especially during imputation.

**How it works:**  
Remove proteins that are missing in more than a set percentage (e.g. 30%) of samples overall, or per group.

**Pros:**  
- Simplifies the dataset  
- Removes weak or inconsistent signals

**Cons:**  
- May remove biologically relevant low-abundance proteins

**Use when:**  
Your dataset has many missing values and you want robust statistics.

---

### 🔧 Example:

| Protein | Sample 1 | Sample 2 | Sample 3 | % Missing |
|---------|----------|----------|----------|-----------|
| P1      | 100      | NA       | 105      | 33%       |
| P2      | NA       | NA       | 200      | 66% ❌     |
| P3      | 130      | 120      | 125      | 0% ✅     |

A common threshold is to **remove proteins with >30% missing values**.

---

## 📊 2. IQR (Interquartile Range) Filtering

**Concept:**  
Proteins that don’t vary across samples are less likely to be biologically meaningful. IQR measures the spread of the middle 50% of values.

**How it works:**  
Calculate IQR for each protein, then remove the bottom percentage (e.g. bottom 25% of proteins with lowest IQR).

**Pros:**  
- Focuses analysis on variable proteins  
- Useful before clustering and PCA

**Cons:**  
- Might remove stable but biologically relevant proteins

**Use when:**  
You want to highlight dynamic changes and remove “flat” signals.

---

### 🔧 Example:

| Protein | IQR  |
|---------|------|
| P1      | 10   |
| P2      | 2    |
| P3      | 0.5  |

You might keep only proteins with **IQR above the 25th percentile**.

---

## 📉 3. Low Intensity Filtering

**Concept:**  
Proteins with very low signal may represent background noise or stochastic detection events.

**How it works:**  
Remove proteins with an average intensity below a set threshold (e.g. log2(intensity) < 5)

**Pros:**  
- Removes background/noise  
- Speeds up downstream analysis

**Cons:**  
- May remove true low-abundance proteins

**Use when:**  
You want a cleaner dataset with strong signals only.

---

## 🧪 4. Group-wise Presence Filtering

**Concept:**  
Some filtering methods check that a protein is consistently detected *within each condition or group*, not just overall.

**How it works:**  
Keep proteins that are present in, for example, **at least 2 of 3 replicates** per condition.

**Pros:**  
- Ensures fair comparison between groups  
- Prevents bias due to uneven protein detection

**Cons:**  
- Depends on replicate count

**Use when:**  
You have multiple conditions and want reliable comparisons.

---

## 🧠 Best Practices

- Always filter **before imputation** to avoid guessing values for low-quality data.
- Combine multiple filtering steps if needed.
- Keep a record of how many proteins were removed at each step.
- Visualize before and after filtering (e.g. barplots, heatmaps, PCA).

---

## 🔬 Summary Table

| Method                  | Removes?                | Best For                          |
|-------------------------|--------------------------|------------------------------------|
| Missing Value Filtering | Incomplete proteins      | Datasets with many missing values |
| IQR Filtering           | Low-variance proteins    | Clustering & feature selection    |
| Low Intensity Filtering | Weak signal proteins     | Removing background/noise         |
| Group-wise Filtering    | Inconsistent group data  | Fair cross-condition comparisons  |

---


```
It's recommended to run filtering after normalization and before imputation or statistical testing.
---

