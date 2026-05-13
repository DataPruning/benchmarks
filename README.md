# DataPruning Official Benchmarks

Reproducible machine learning benchmarks for DataPruning — an ML dataset optimization platform designed to reduce redundant training samples, improve training efficiency, and preserve predictive performance.

These benchmarks evaluate model accuracy, F1 score, regression quality, training speed, and dataset reduction across real-world machine learning datasets using a leak-free scientific methodology.

## Why These Benchmarks Matter

Machine learning performance claims are often difficult to validate.

These benchmarks are designed to transparently evaluate when dataset optimization preserves model quality, improves training efficiency, and where limitations may exist.

Our goal is scientific transparency, not cherry-picked results.

## What This Repository Contains

- ✅ Benchmark metrics — structured JSON results for every benchmark
- ✅ Comparison charts — accuracy, training time, reduction, and class distribution visualizations
- ✅ Methodology reports — detailed benchmark explanations and reproduction notes
- ✅ Fairness guarantees — leak-free evaluation methodology

This repository contains benchmark outputs only.

It does not include proprietary DataPruning implementation details, optimization logic, or private production infrastructure.

## Benchmark Methodology

### Leak-Free Evaluation Design

Every benchmark follows a strict split-first protocol to prevent train/test leakage:

1. Dataset loaded — from a verified public source
2. Train/Test split — 80/20 split (stratified for classification) using a fixed random seed (42) before optimization
3. Optimization applied to training data only — the test set is never modified or optimized
4. Identical models trained — same preprocessing, same hyperparameters, same experimental setup
5. Evaluation on untouched test data — both original and optimized models are evaluated on the exact same unseen data
6. Comparison — the only variable is training dataset quality and size

### Fairness Principles

All benchmarks follow strict fairness constraints:

- Same train/test split
- Same random seed (42)
- Same preprocessing pipeline
- Same model hyperparameters
- No retuning after optimization
- Evaluation on untouched test data only

## Benchmark Coverage

Benchmarks span multiple machine learning scenarios to evaluate robustness across different dataset characteristics.

| Category | Example Dataset | Purpose |
|----------|----------------|---------|
| Binary Classification | Bank Marketing, Adult Income | Binary prediction tasks |
| Multiclass Classification | Wine Quality, Dry Bean | Multiple target classes |
| Regression | California Housing | Continuous target prediction |
| Imbalanced Data | Adult Income, Breast Cancer | Uneven class distributions |
| Small Datasets | Breast Cancer | Low-row datasets |
| Larger Datasets | Bank Marketing, Adult Income | Higher-scale tabular data |

## Repository Structure

```
benchmarks/
├── index.json
├── bank_marketing/
│   ├── metrics/results.json
│   ├── charts/*.png
│   └── REPORT.md
├── adult_income/
├── wine_quality/
├── dry_bean/
├── breast_cancer/
├── california_housing/
├── README.md
└── .gitignore
```

## Reproducibility

All benchmark outputs are generated using the same production optimization pipeline powering DataPruning.

Each benchmark includes:
- dataset source references
- evaluation methodology
- structured metrics
- comparison charts
- reproducibility notes

Public benchmark outputs are designed for transparent independent review.

## Dataset Licensing

This repository does not redistribute original datasets.

Datasets must be obtained from their original public sources. Licensing terms vary by dataset and should be verified independently.

## Learn More

Website: https://www.datapruning.com

Explore benchmarks: https://www.datapruning.com/benchmarks

## License

All benchmark content © DataPruning. Contact us for reuse permissions.
