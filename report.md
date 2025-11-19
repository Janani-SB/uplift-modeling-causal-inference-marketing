# Uplift Modeling Project - Executive Summary

Date: 2025-11-19T10:18:10.397339Z

Dataset: Hillstrom E-mail analytics (uploaded)

Models implemented:
- S-Learner (LightGBM)
- T-Learner (LightGBM - separate treated & control)

Evaluation (uplift metrics):
- AUUC (S-Learner): 30.757072
- AUUC (T-Learner): -30.446441

Model comparison:
The S-Learner was preferred because it achieved higher AUUC, indicating better ordering of customers by estimated incremental conversion. This suggests that pooled modeling with treatment as a feature provided more stable CATE estimates for this dataset.

Segmentation:
A segmentation summary (segmentation_summary.csv) includes the counts and characteristics of four groups: Takers, Sure Things, Lost Causes, Sleeping Dogs. The segmentation logic uses uplift quantiles and baseline probability thresholds to ensure all groups are represented and actionable.

Feature importance:
Global feature importance (LightGBM gain) is saved to `global_feature_importance.csv`. Top features include historical spend and recency indicators which explain both baseline and incremental responses.

Local explanations:
Local model reports for sampled customers (p0, p1, uplift and top contributing features) are provided in `local_model_reports.json`.

Recommendation:
- Target the 'Takers' group for campaign delivery to maximize incremental conversions.
- Exclude 'Sleeping Dogs' (negative uplift) to avoid harming conversion.
- Avoid spending on 'Sure Things' (convert regardless) and 'Lost Causes' (unlikely to convert).
- For production, run k-fold AUUC validation and implement cost-aware thresholds.

Files included in outputs directory: preprocessor.joblib, best_model_lgb.joblib, global_feature_importance.csv, local_model_reports.json, segmentation_summary.csv, qini.png, roc.png, pr.png, confusion_matrix.png, report.md, credit_project_outputs.zip.

