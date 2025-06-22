# 💪 Understanding Normalization Techniques in Omics Data Analysis
## From TIC to PQN – Choosing the Right Method for Reliable Results

**Author:** Abdallah Ibrahim  
**Tags:** proteomics, normalization, bioinformatics, data-cleaning, TIC, PQN, VSN

---

## 🔍 Introduction

When working with **omics datasets** such as **proteomics** or **metabolomics**, raw intensity values are often misleading due to various sources of technical noise: variation in sample preparation, instrument sensitivity, or biological concentration differences. To address this, **normalization** becomes an essential preprocessing step — and choosing the *right* normalization method can significantly impact your downstream results.

This article summarizes four commonly used normalization strategies:
- **Total Ion Current (TIC)**
- **Median Normalization**
- **Variance Stabilization Normalization (VSN)**
- **Probabilistic Quotient Normalization (PQN)**

---

## ⚙️ 1. Total Ion Current (TIC) Normalization

**Concept:**  
TIC assumes that the **total signal intensity** (sum of all detected intensities) in each sample should be similar. It scales each sample to the same total signal.

**How it works:**  
Each intensity in a sample is divided by the total signal for that sample, then multiplied by a common factor (like the average total signal across samples).

**Pros:**  
- Simple and fast  
- Useful when technical variation is the main concern

**Cons:**  
- Sensitive to highly abundant proteins/outliers  
- Can **mask real biological changes** if total protein content truly differs

**Use when:**  
Your samples are technically similar and differ only slightly biologically.

---

## ⚖️ 2. Median Normalization

**Concept:**  
This method assumes that **most proteins don’t change** across samples. So, it uses the **median** intensity as a reference instead of the sum.

**How it works:**  
Each sample is scaled such that its median equals the global or reference sample median.

**Pros:**  
- More robust to outliers than TIC  
- Preserves global differences if only a subset of proteins change

**Cons:**  
- Assumes symmetrical biological variation  
- Not suitable if the majority of proteins are differentially expressed

**Use when:**  
You expect small to moderate changes between samples (e.g. early disease vs healthy).

---

## 📈 3. Variance Stabilization Normalization (VSN)

**Concept:**  
VSN corrects for **heteroscedasticity** – where proteins with low intensities show more variance than high-intensity ones.

**How it works:**  
It applies a **log-like transformation** that stabilizes the variance across all intensities, making the data better suited for statistical analysis.

**Pros:**  
- Ideal for downstream statistics (e.g. t-tests, clustering)  
- Reduces noise especially in low-abundance proteins

**Cons:**  
- More complex mathematically  
- May not be intuitive for visual interpretation

**Use when:**  
You're performing **statistical differential expression** and need accurate variance modeling.

---

## 🧪 4. Probabilistic Quotient Normalization (PQN)

**Concept:**  
Developed for **metabolomics**, PQN adjusts for **sample dilution/concentration** without assuming uniform total signal or median.

**How it works:**  
1. Normalize each sample using a preliminary method (like TIC)  
2. Calculate the **quotients** of each intensity vs a reference sample  
3. Take the **median of these quotients**  
4. Scale the entire sample based on this median

**Pros:**  
- Corrects for dilution/concentration differences  
- Keeps biological variation intact  
- Very robust against outliers

**Cons:**  
- Needs a good reference sample  
- Requires more steps than TIC/Median

**Use when:**  
You're analyzing **biofluids** (like urine or plasma) where sample concentration varies widely.

---

## 🔬 Summary Table

| Method | Adjusts for Total Signal? | Handles Outliers? | Stabilizes Variance? | Best for |
|--------|----------------------------|--------------------|-----------------------|----------|
| TIC    | ✅ Yes                     | ❌ No              | ❌ No                 | Simple datasets with low variation |
| Median | ✅ Yes                     | ✅ Yes             | ❌ No                 | Balanced experiments (e.g. mild treatments) |
| VSN    | ✅ Implicitly              | ✅ Yes             | ✅ Yes                | Statistical analysis & clustering |
| PQN    | ✅ (via reference scaling) | ✅ Yes             | ❌ Partial            | Metabolomics, concentration issues |

---

## 🔬 Appendix: Worked Examples

### Example 1: Median Normalization

| Protein | Sample A | Sample B | After Median Norm (B) |
|---------|----------|----------|------------------------|
| P1      | 100      | 200      | 100                    |
| P2      | 120      | 240      | 120                    |
| P3      | 130      | 260      | 130                    |

Median of B = 240, Reference Median = 120  
Scaling factor = 120 / 240 = 0.5

📉 Sample B is scaled by 0.5

---

### Example 2: Probabilistic Quotient Normalization (PQN)

| Protein | Reference | Sample X | Quotients (X / Ref) |
|---------|-----------|-----------|----------------------|
| P1      | 100       | 150       | 1.5                  |
| P2      | 200       | 300       | 1.5                  |
| P3      | 400       | 600       | 1.5                  |

Median Quotient = 1.5  
Normalized Sample X = [150, 300, 600] / 1.5 = [100, 200, 400]

---

## 🧠 Final Thoughts

There's no one-size-fits-all approach when it comes to normalization. Always choose based on:
- The nature of your samples  
- The biological question you're asking  
- The downstream analyses you'll be applying

📌 **Rule of thumb:**
- Use **Median or VSN** for proteomics
- Use **PQN** for metabolomics or variable biofluids
- Avoid **TIC** when biological differences dominate

---

## 📁 Example Code (Coming Soon)

Stay tuned for Python and R implementations of each normalization method in `/scripts/`.

