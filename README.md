# DataPruning Official Benchmarks

Reproducible benchmark results for [DataPruning](https://datapruning.com) — a production dataset optimization system.

## What This Is

This repository contains **verified, reproducible benchmark results** generated using the same production optimization standards and evaluation methodology used by [DataPruning](https://datapruning.com).

## What This Is NOT

- ❌ Not the DataPruning backend or SDK source code
- ❌ Not an alternative implementation of the optimization algorithm
- ❌ Not simplified or benchmark-specific logic

## Benchmark Methodology

Every benchmark follows this strict protocol to ensure scientific validity:

1. **Load** original dataset
2. **Detect** target column
3. **Split** train/test (80/20 stratified, seed 42) — BEFORE any optimization
4. **Preprocess** both splits independently using standardized preprocessing and feature alignment
5. **Align** train/test feature spaces to ensure consistent dimensionality
6. **Optimize** training set ONLY using the DataPruning production optimization pipeline
7. **Safety layer**: reduction cap + class preservation (train set only)
8. **Train** Logistic Regression, Random Forest, and XGBoost on original training set
9. **Train** the same models on the optimized training set
10. **Evaluate** BOTH on the untouched test set — only variable is training data quality

### Leak-Free Design

The test set is NEVER touched by any optimization logic. By splitting FIRST and optimizing ONLY the training set, we ensure:
- The test set represents genuinely unseen data
- Any preservation (or improvement) of metrics is attributable to better training data quality
- Results are scientifically defensible for ML peer review

## Dataset Licensing

This repository does **not** redistribute original datasets. Users must:
1. Download from the original source (linked in each benchmark's REPORT.md)
2. Verify licensing terms before redistributing
3. Use the provided dataset download scripts

## Structure

```
benchmarks/
├── index.json                  # Registry consumed by datapruning.com
├── bank_marketing/
│   ├── metrics/results.json    # All metrics (consumed by website)
│   ├── charts/*.png            # Comparison charts
│   └── REPORT.md               # Full methodology + per-dataset details
├── adult_income/
│   └── ...
└── ...
```

## License

The benchmark data, metrics, and charts in this repository are licensed under CC BY 4.0.
Individual dataset licenses apply to the original data — see each dataset's source for details.
