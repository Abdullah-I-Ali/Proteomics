# 🔍 Filtering

Filtering helps remove noise or unreliable measurements. Common filtering methods include:

- **1. 3×IQR Filtering**: Removes extreme outliers based on interquartile range.
- **2. Missing Value Filtering**: Removes proteins with too many missing values (e.g. >50% NA).
- **3. RSD Filtering**: Removes proteins with high Relative Standard Deviation (RSD).

Filtering ensures more reliable downstream statistical analysis.