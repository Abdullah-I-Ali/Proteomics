# 🧩 Imputation in Proteomics

Imputation is the process of estimating missing values in the dataset. In proteomics, missing values are common due to detection limits, sample variability, or random instrument behavior. This step is essential to avoid losing valuable proteins and to ensure accurate downstream analysis.

---

## 🤔 Why Are Values Missing?
In proteomics datasets, not every protein is detected in every sample. This can happen for three main reasons:

- **MCAR (Missing Completely At Random)**: The missingness has no pattern; it's purely random and unrelated to the data.
- **MAR (Missing At Random)**: Missingness depends on other observed values. For example, proteins in low-concentration samples might be harder to detect.
- **MNAR (Missing Not At Random)**: Missing values are related to the unobserved value itself. This is common in proteomics, where low-abundance proteins fall below the instrument's detection limit.

Understanding the cause of missingness helps decide which imputation method to use.

---

## ⏱️ When Do We Do Imputation?
Imputation is done **after normalization and filtering**, and **before** steps like scaling, PCA, or statistical testing. We don’t impute before filtering because we don’t want to keep proteins that were never reliably detected in the first place.

---

## 🔍 Types of Imputation Methods (With Examples)

### 1. **Left-Shifted Imputation (for MNAR)**
This method assumes the missing values are due to very low abundance, below detection limit. So we replace missing values with small numbers that mimic low-intensity signals.

📌 *Example:* Imagine you have 10 samples. A protein is detected in 7 of them with very low intensity values, and missing in 3. Instead of removing it, you fill the missing cells with small numbers that are slightly lower than the smallest observed ones. This keeps the trend of the protein being low but detectable.

🧠 This is suitable when most of your missing values are **not random**, but related to protein abundance.

---

### 2. **Average-based or Similarity-based Imputation (for MAR)**
When missingness is due to technical reasons or sample variation, we can estimate missing values by looking at similar proteins or sample behavior.

📌 *Example:* Suppose a protein is missing in one sample, but present in all others. We look at proteins that behave similarly across other samples, and use their patterns to estimate the missing value.

🧠 This works well when missing values are spread randomly or when you believe the protein *should* have been detected.

---

### 3. **Fixed Value Imputation**
Some researchers simply fill missing values with a constant number, like zero or the lowest value in the dataset.

📌 *Example:* If you set all missing values to zero, you’re assuming those proteins are truly absent. But in reality, they may be present at low levels, so this can distort your analysis.

🧠 Use this method only if you're sure the missingness means "absence."

---

## ✅ Summary & Recommendations
- Use **left-shifted imputation** when values are missing because of detection limits (MNAR).
- Use **similarity-based imputation** when values are missing due to sample differences (MAR).
- Never apply imputation before filtering unreliable proteins.
- After imputation, always visualize the dataset again (like PCA or distribution plots) to make sure the imputation didn’t introduce bias.

---

## 📌 In Practice
Let’s say you started with 1500 proteins. After filtering for proteins present in at least 70% of samples, you’re left with 1100. But even those 1100 still have some scattered missing values. That’s when you apply imputation to fill in those gaps—choosing the best method based on whether those gaps are random or abundance-related.

Now your dataset is complete and ready for further analysis like scaling or statistical testing.

---

This version of imputation explanation avoids technical code and focuses on clear concepts and real-world intuition. Perfect for newcomers and documentation!

