# 🧩 Imputation

Imputation means filling in missing values to allow downstream statistical analysis.

## Examples:
- **Mean/Median Imputation**: Fill missing values with the average/median of non-missing ones.
- **KNN Imputation**: Estimate missing values using similar proteins.
- **Regression Imputation**: Predict missing values using other protein signals.
- **Expectation Maximization (EM)**: Iteratively estimates missing values.
- **Single Imputation**: Any of the above applied once.
- **Zero Imputation**: Fill NA with 0 (not recommended for most cases).

### Example Table Before Imputation:

| Protein | Sample 1 | Sample 2 | Sample 3 | Sample 4 |
|---------|----------|----------|----------|----------|
| P001    | 10000    | 9800     | 10200    | NA       |
| P002    | 500      | NA       | NA       | 490      |
| P003    | NA       | NA       | NA       | NA       |