# 📏 Scaling

Scaling standardizes values to the same range/unit.

## Types of Scaling:
- **Z-score Scaling**: Converts to standard normal distribution (mean = 0, std = 1).
- **Min-Max Scaling**: Rescales values between 0 and 1.
- **Log Transformation**: Reduces impact of extreme values, helps with skewed data.

## Difference vs Normalization:

| Aspect       | Normalization             | Scaling                  |
|--------------|----------------------------|---------------------------|
| Applies to   | Across samples             | Across proteins/features |
| Removes      | Sample-level variation     | Feature-level variation  |
| Goal         | Adjust sample differences  | Standardize feature size |