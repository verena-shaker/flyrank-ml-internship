# Capstone Report — Google Search Ranking & Discoverability

- **Author:** Intern
- **Lane:** Refresh / Content Opportunity Scoring
- **Repo:** https://github.com/verena-shaker/flyrank-ml-internship
- **Date:** 2026-08-29

---

## 0. Abstract
How can search engines optimize the re-indexing and content refresh pipeline for underperforming web pages? This project leverages real FlyRank search analytics data to evaluate organic performance metrics (CTR, position, and impressions). We established a rule-based baseline and trained a Decision Tree Classifier to predict high-impact opportunity pages. The model achieved a higher F1-score than the simple heuristic on held-out evaluation data. The final output provides a prioritized, action-scored queue to guide content editing decisions.

---

## 1. Problem framing
This decision support pipeline evaluates web pages at the `(url, date)` grain to identify content that needs optimization. The human action is for editors to rewrite, update, or re-structure content. The cost of a false positive is wasted editorial time, while a false negative leaves low-performing content unoptimized. Machine learning improves this process by capturing multi-feature interactions (e.g., high impressions paired with low CTR at top positions) far better than static threshold rules.

---

## 2. Data safety
We extracted query-level and page-level metrics from the FlyRank search database using DuckDB. Features include `impressions`, `clicks`, `ctr`, and `position`. Explicit leakage variables—such as future performance windows (`trend_direction`, `trend_pct`) and client-identifying raw domains—were excluded from feature matrices. Pseudonymized entity IDs were used solely for time-aware grouping and split validations.

---

## 3. Baseline
The baseline rule flags pages based on two explicit threshold heuristics:
- `LOW_RANK_LOW_CTR`: Position > 10 and CTR < 0.03 (Score: 0.85)
- `HIGH_RANK_LOW_CTR`: Position <= 10 and CTR < 0.02 (Score: 0.70)

This heuristic acts as a non-ML benchmark to establish minimum acceptable performance for prioritization accuracy.

---

## 4. Model / analysis
We trained a Decision Tree Classifier (`scikit-learn`) to predict action priorities. Features passed to the model include normalized `impressions`, `clicks`, `position`, `ctr`, and rolling average ratios. The target variable is binary, representing whether a page yields positive re-engagement post-refresh. Hyperparameters were tuned with max depth constraints to prevent overfitting.

---

## 5. Evaluation
We performed a time-aware train/test split (80% historical training, 20% holdout validation) to reflect real-world deployment conditions without temporal leakage. The Decision Tree outperformed the baseline rule in overall precision and recall on the test set, reducing false-positive opportunity flags by identifying low-volume edge cases.

---

## 6. Interpretation
Feature importance analysis reveals that `ctr` and `position` are the primary drivers of model decisions, followed by `impressions`. Pages with high impression counts sitting at positions 4–10 with lagging CTR were consistently flagged as highest priority for immediate content refresh.

---

## 7. Recommendation
The pipeline exports a ranked action queue saved to `work/outputs/baseline_action_score.csv` (and model recommendations). Editors should prioritize the Top-20 flagged URLs daily. Low-confidence outputs (scores < 0.50) should be monitored rather than acted upon immediately to save resources.

---

## 8. Reproducibility
To reproduce the evaluation and outputs:
1. Run `w03_data_contract.ipynb` to setup inputs.
2. Run `w04_baseline_score.ipynb` to evaluate baseline heuristics and output `work/outputs/baseline_action_score.csv`.
3. Run `w05_model.ipynb` to train the decision tree and output performance comparisons.
Environment dependencies are pinned in `requirements.txt`. Random seed is fixed at `42`.

---

## 9. Acknowledgments & data credit
Built on the [FlyRank ML Internship dataset](https://flyrank.ai).
