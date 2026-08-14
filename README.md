# US Stock Forecast with BERT & XGBoost

Freelance project building a stock/company credit rating forecasting pipeline that combines **BERT-based text feature extraction** (from 10-K filings) with **XGBoost classification**, further enriched with financial metrics and S&P credit ratings.

This repository consolidates three iterative development cycles, each expanding on the previous version's requirements and scope.

## Pipeline Overview

The final pipeline (v3) follows a three-stage structure, run separately on **old data** and **new data**:

Old Data ─┐
├─→ Program 1 (Preprocessing) ─→ Processed Old Data ─→ Program 2 (Training) ─→ Model
New Data ─┘ └─→ Processed New Data ───────────────────────────┘
↓
Program 3 (Testing) ─→ Result

1. **Preprocessing** — includes randomized credit rating assignment, numeric feature standardization, and BERT-based text processing
2. **Training** — trains a model using the output of Program 1
3. **Testing** — applies the trained model to new, consistently-formatted data and outputs prediction results

### Sample Output Format

| Company | Predicted Rating | Actual Rating | Correct |
|---|---|---|---|
| A | 1 | 1 | T |
| B | 1 | 2 | F |
| C | 1 | 1 | T |
| ... | ... | ... | ... |

Accuracy (Acc): 0.7

## Development History

### v1 — Proof of Concept ($6,000 TWD)
- BERT feature extraction from 10-K text combined with XGBoost classification
- Single end-to-end notebook (`run.ipynb`)

### v2 — Feature Engineering & Requirements Expansion ($6,400 TWD)
Detailed requirements included:
- Display the ratio of the four data classes
- Standardize numeric data and print standardized values
- Text preprocessing: remove HTML tags, numbers, punctuation, and non-English characters; lowercase normalization; lemmatization (converting past/future tense back to present tense)
- Experiment with tokenization methods (e.g. padding)
- Explain the function of the `[CLS]` token in BERT
- Feature selection — compare manually selected features vs. model-driven selection
- Split data into train/val/test sets
- Compare final model performance across three configurations: numeric-only, text-only, and combined numeric + text

### v3 — Final Delivery: Old vs. New Data Validation ($20,000 TWD)
- Restructured into a modular three-program pipeline (preprocessing → training → testing)
- Introduced old-vs-new dataset comparison to validate model stability on updated data
- Persisted trained features, train/test splits, and the final trained model for reproducibility
- Delivered with detailed requirement documentation (see `需求說明.png`, `需求1–3.JPG`)

## Contents

- `run_text_v3_1.ipynb`, `run_text_v3_2.ipynb`, `run_text_v3_3.ipynb` — staged pipeline: preprocessing, BERT feature extraction, and XGBoost training/evaluation
- `df_old.xlsx`, `df_new.xlsx` — old vs. new financial datasets used for model stability comparison
- `df_old_company.xlsx`, `df_new_company.xlsx`, `df_old_sample.xlsx`, `df_new_sample.xlsx` — company-level and sample-level breakdowns of each dataset
- `x_train_old/new.pickle`, `x_test_old/new.pickle`, `y_train_old/new.pickle`, `y_test_old/new.pickle` — serialized train/test splits
- `indices_train_old/new`, `indices_test_old/new` — index references for train/test splits
- `xgb_model.pkl` — final trained XGBoost model
- `report.xlsx` — output prediction report
- `標準普爾最新信用評級.xls` — S&P credit rating reference data
- `需求說明.png`, `需求1.JPG`, `需求2.JPG`, `需求3.JPG` — client requirement specifications

## References

- [Feature Extraction with BERT for Text Classification](https://towardsdatascience.com/feature-extraction-with-bert-for-text-classification-533dde44dc2f)
- [Exploring BERT: Feature extraction & Fine-tuning](https://medium.com/dataness-ai/exploring-bert-feature-extraction-fine-tuning-6d6ad7b829e7)
- [Multiclass classification with XGBoost classifier](https://stackoverflow.com/questions/57986259/multiclass-classification-with-xgboost-classifier)
- [Invalid classes inferred from unique values of `y`](https://stackoverflow.com/questions/71996617/invalid-classes-inferred-from-unique-values-of-y-expected-0-1-2-3-4-5-got) — labels must start from 0
- [Multiclass average methods: 'micro', 'macro', 'weighted', None](https://stackoverflow.com/questions/52269187/facing-valueerror-target-is-multiclass-but-average-binary)

## Total Project Value

**NT$32,400** across three delivery milestones (v1: $6,000 → v2: $6,400 → v3: $20,000)
