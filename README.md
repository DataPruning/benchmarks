# DataPruning Official Benchmarks

Reproducible benchmark results for [DataPruning](https://datapruning.com) — a data optimization algorithm that removes redundant training samples while preserving model performance.

## What This Repository Contains

- ✅ **Benchmark metrics** — structured JSON results for each dataset
- ✅ **Comparison charts** — accuracy, training time, reduction, class distribution
- ✅ **Full methodology** — detailed reproduction steps
- ✅ **Fairness guarantees** — verified leak-free evaluation

This repository does **not** contain any DataPruning source code, proprietary algorithms, or implementation details. It is purely an output directory for scientific validation.

## Benchmark Methodology

### Leak-Free Design

Every benchmark follows a strict split-first protocol to prevent data leakage:

1. **Dataset loaded** — from a verified public source
2. **Train/Test split** — 80/20 stratified split (random seed 42) **before any optimization**
3. **Optimization applied to training set only** — the test set is never touched
4. **Identical models trained** on both original and optimized training data
5. **Both models evaluated** on the same untouched test set
6. **Comparison** — the only variable is training data quality

### Fairness Principles

- Same train/test split for original and optimized
- Same random seed (42) for reproducibility
- Same model hyperparameters
- Same preprocessing pipeline
- No retuning after optimization
- Evaluation on untouched test data only

## Benchmark Coverage

| Category | Example Dataset | Description |
|----------|----------------|-------------|
| Binary Classification | Bank Marketing, Adult Income, Breast Cancer | Predict a binary outcome |
| Multiclass Classification | Wine Quality, Dry Bean | Predict one of several classes |
| Regression | California Housing | Predict a continuous value |
| Imbalanced Data | Adult Income | Uneven class distribution |
| Small Datasets | Breast Cancer | < 1,000 rows |
| Larger Datasets | Bank Marketing, Adult Income | > 10,000 rows |

## Repository Structure

```
benchmarks/
├── index.json                        # Registry consumed by datapruning.com
├── bank_marketing/
│   ├── metrics/results.json          # All numeric metrics
│   ├── charts/*.png                  # Comparison charts
│   └── REPORT.md                     # Full methodology + results
├── adult_income/
│   └── ...
├── wine_quality/
│   └── ...
├── dry_bean/
│   └── ...
├── breast_cancer/
│   └── ...
├── california_housing/
│   └── ...
├── README.md                         # This file
└── .gitignore
```

## Reproducing Benchmarks

To reproduce these results:

```bash
git clone https://github.com/DataPruning/benchmarks.git
# Clone the private demo_backend repo (requires access)
# Run: python -m benchmark_runner.run --config benchmark_runner/datasets.json --output ../benchmarks-public --runs 3
```

## Dataset Licensing

This repository does not redistribute original datasets. Users must download datasets from their original sources (linked in each benchmark's REPORT.md). Individual dataset licenses apply.

## License

The benchmark data, metrics, and charts in this repository are licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
