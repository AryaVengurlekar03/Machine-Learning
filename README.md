# Position-Aware Search Intelligence

Evaluating Heuristic Rules vs. Gradient Boosting for Content Refresh Opportunity Scoring

---

## 1. What This Project Does

This project identifies organic search content pieces with significant Click-Through Rate (CTR) underperformance relative to their position-tier peers and ranks them as high-priority content refresh opportunities.

By evaluating both baseline position-peer heuristics and position-aware Machine Learning (ML) models, the system produces actionable rankings and diagnostics to help teams systematically recover missed search traffic.

---

## 2. Who It Is For

This framework is built for two core audiences:
- **Content & SEO Teams:** Content strategists and digital marketers who need a transparent, data-driven way to prioritize content refresh candidates without relying on manual intuition or uncalibrated raw metrics.
- **ML & Data Practitioners:** Search intelligence engineers and data scientists interested in ranking formulations, position-aware feature engineering, leakage prevention, and honest unseen-client validation for organic search datasets.

---

## 3. Problem

Organic search content frequently degrades over time or fails to capture expected search impressions due to outdated titles, snippets, or sub-optimal relevance. However, evaluating raw CTR in isolation is misleading because organic CTR is heavily governed by SERP position. A page at position 8 with a 2% CTR may perform normally, while a page at position 2 with a 2% CTR is severely underperforming its peers.

### Research Question
> “Can a position-aware machine learning model identify organic search content pieces with significant CTR underperformance relative to position-tier peers, and how does its ranking performance compare with a fixed heuristic baseline under an unseen-client validation design?”

---

## 4. Approach

The methodology processes organic search performance and web analytics data across portfolio domains to discover underperforming URLs:

- **Dataset Scale:** 28,795 valid content pieces across 31 anonymized client domains.
- **Feature Space:** 47 safe, non-leakage features incorporating search visibility metrics, position tiers, content metadata (e.g., word count, title length), and GA4 engagement signals (e.g., bounce rate, session duration).
- **Target Formulation:** Modeled in log space as \(\log(1 + \text{missed\_clicks})\) to compress heavy-tailed traffic distribution skew while maintaining numerical stability.
- **Model Framework:** `HistGradientBoostingRegressor` (gradient boosted decision trees with native missing-value handling).
- **Baseline Comparison:** A fixed position-peer heuristic rule that calculates CTR deficit relative to position-tier benchmark averages.

---

## 5. Architecture

```text
Data
  ↓
Validation / Cleaning
  ↓
Feature Engineering
  ↓
Leakage Audit
  ↓
Client-Grouped Train/Test Split
  ↓
Heuristic Baseline + ML Model
  ↓
Ranking Evaluation
  ↓
Action Playbook
  ↓
Content Refresh Recommendations
```

---

## 6. Validation Design

To prevent domain-level data leakage and evaluate real-world generalization to new sites, the project enforces a client-grouped validation split:

- **Split Strategy:** `GroupShuffleSplit` grouped strictly by anonymized client domain IDs.
- **Data Partitioning:** 25 training clients (22,974 rows) and 6 unseen test clients (5,821 rows).
- **Leakage Controls:** Client domain identifiers are strictly excluded from the feature set. Target-derived metrics and sibling leakage variables are audited and removed prior to model training.

---

## 7. Setup

### Prerequisites
- Python 3.10 or higher
- `git`

### Repository Setup
```bash
git clone https://github.com/AryaVengurlekar03/Machine-Learning.git
cd Machine-Learning
```

### Dependency Installation
Install the required packages using standard `pip`:
```bash
pip install -r requirements.txt
```

*(Dependencies include: `pandas>=2.2`, `numpy>=1.26`, `scikit-learn>=1.4`, `matplotlib>=3.8`, `reportlab>=4.0`, `duckdb>=1.0`, `huggingface_hub>=0.24`)*

### Dataset Requirements
The anonymized starter dataset is bundled directly within the repository at:
`data/raw/content_refresh_anonymized.csv`

No external dataset download or API key setup is required to execute the pipeline on the sample.

### Running Notebooks and Scripts
- **Execute the full Python pipeline:**
  ```bash
  python scripts/run_all.py
  ```
- **Execute individual pipeline steps:**
  ```bash
  python scripts/01_prepare_features.py
  python scripts/02_baseline_score.py
  python scripts/03_train_model.py
  python scripts/04_evaluate_and_export.py
  python scripts/05_build_pdf_report.py
  ```
- **Execute the capstone notebook programmatically:**
  ```bash
  python scripts/execute_capstone.py
  ```

---

## 8. Usage

To reproduce the analysis and examine the full end-to-end evaluation:

1. **Main Capstone Notebook:** Open and run [`work/notebooks/capstone.ipynb`](work/notebooks/capstone.ipynb).
2. **Phase Notebooks:** Detailed step-by-step experiment files are located in `work/notebooks/`:
   - [`w01_research_question.ipynb`](work/notebooks/w01_research_question.ipynb): Problem definition & domain context
   - [`w02_ml_task_framing.ipynb`](work/notebooks/w02_ml_task_framing.ipynb): Target formulation & metric selection
   - [`w03_data_contract.ipynb`](work/notebooks/w03_data_contract.ipynb) & [`w03_feature_leakage_check.ipynb`](work/notebooks/w03_feature_leakage_check.ipynb): Data cleaning & leakage audit
   - [`w04_baseline_score.ipynb`](work/notebooks/w04_baseline_score.ipynb): Heuristic baseline formulation
   - [`w05_model.ipynb`](work/notebooks/w05_model.ipynb): Model training & parameter tuning
   - [`w06_validation_audit.ipynb`](work/notebooks/w06_validation_audit.ipynb): Unseen-client evaluation audit
   - [`w07_action_playbook.ipynb`](work/notebooks/w07_action_playbook.ipynb): Action playbook & refresh recommendation queue
3. **Generated Artifacts & Figures:**
   - Evaluation figures are exported to `work/figures/` (e.g., [`w07_precision_at_k_comparison.png`](work/figures/w07_precision_at_k_comparison.png), [`w07_opportunity_score_distribution.png`](work/figures/w07_opportunity_score_distribution.png), [`w07_reason_code_distribution.png`](work/figures/w07_reason_code_distribution.png)).
   - Outputs such as [`outputs/model_report.md`](outputs/model_report.md) and [`outputs/refresh_queue_sample.csv`](outputs/refresh_queue_sample.csv) contain exported evaluation summaries and prioritized page queues.

---

## 9. V2 Evaluation Results

The models and baseline were evaluated on the 6 unseen test client domains (5,821 rows) under a strict top-K ranking protocol.

| Metric | ML Model (`HistGradientBoosting`) | Fixed Heuristic Baseline |
|---|---|---|
| **Precision@10** | 0.9000 | **1.0000** |
| **Precision@20** | 0.8500 | **1.0000** |
| **Precision@50** | 0.7200 | **1.0000** |
| **Precision@100** | 0.5400 | **0.7300** |
| **Top-50 Recoverable Clicks** | 1,627.3 | **2,283.7** |

- **Test Set Base Rate:** 1.25%

### Honest Conclusion
Under this strict unseen-client validation design, **the fixed position-peer heuristic baseline outperformed the machine learning model** across all reported precision@K tiers and recoverable click totals. The simpler, domain-calibrated heuristic rule provides tighter ranking precision for top refresh opportunities on unseen domains.

---

## 10. Practical Recommendation

Based on empirical evaluation:
- **Operational Rule:** Deploy the position-peer heuristic as the primary transparent sorter for prioritizing CTR-underperforming content in production workflows.
- **ML Role:** Retain machine learning as a multi-signal research framework for future experimentation as additional interaction features and time-series signals become available.
- **Action Playbook & Diagnostic Mapping:**
  - Primary Diagnostic Code: `CTR_BELOW_POSITION_PEER`
  - Operational Action: `OPTIMIZE_TITLE_META_SNIPPET`

---

## 11. Limitations

- **Cross-Sectional Data:** Evaluation is based on static snapshot data and does not establish causal traffic recovery post-refresh.
- **Validation Scope:** While client-grouped splitting avoids spatial domain leakage, it does not substitute for true forward-looking time-series validation.
- **Baseline Superiority:** The ML regressor currently underperforms the simpler heuristic on unseen client domains; further feature engineering and rank-specific loss functions are required before asserting ML operational superiority.
- **Traffic Opportunity vs. Guarantee:** Identified metrics represent opportunity bounds rather than guaranteed traffic outcomes.

---

## 12. Reproducibility

The analyses, models, charts, and paper claims are designed to be reproducible from the anonymized dataset and the scripts/notebooks included in this repository.

- **Live Research Paper:** [https://aryavengurlekar03.github.io/Machine-Learning/paper.html](https://aryavengurlekar03.github.io/Machine-Learning/paper.html)
- **Source Code Repository:** [https://github.com/AryaVengurlekar03/Machine-Learning](https://github.com/AryaVengurlekar03/Machine-Learning)

---

## 13. AI Transparency

I built this project with AI assistance, including Claude/ChatGPT, for coding support, debugging, documentation, and structuring. I reviewed and tested the implementation, checked the evaluation outputs, and made the final decisions about the methodology and claims.

---

## 14. Project Structure

```text
Machine-Learning/
├── data/
│   └── raw/
│       └── content_refresh_anonymized.csv   # Starter anonymized dataset (28,795 rows)
├── docs/                                    # Core documentation and data dictionary
│   └── data-dictionary.md                   # Column descriptions and schema rules
├── notebooks/                               # Starter notebooks (01 to 03)
├── outputs/                                 # Exported reports, CSVs, and charts
│   ├── charts/                              # Pipeline charts
│   ├── model_report.md                      # Pipeline Markdown report
│   └── refresh_queue_sample.csv             # Scored refresh queue sample
├── scripts/                                 # Standalone python pipeline scripts
│   ├── 01_prepare_features.py               # Feature processing & cleaning
│   ├── 02_baseline_score.py                 # Baseline heuristic calculation
│   ├── 03_train_model.py                    # Model training step
│   ├── 04_evaluate_and_export.py            # Evaluation & export script
│   ├── 05_build_pdf_report.py               # PDF generation script
│   ├── execute_capstone.py                  # Capstone headless notebook runner
│   └── run_all.py                           # Master pipeline runner
├── skills/                                  # Instruction skills and task router
├── work/                                    # Capstone development space
│   ├── figures/                             # Generated capstone charts
│   └── notebooks/                           # Capstone notebooks (w01-w07, capstone.ipynb)
├── paper.html                               # Published research paper HTML view
├── index.html                               # Project landing page HTML view
├── requirements.txt                         # Python dependencies
└── README.md                                # Project root README
```

---

## 15. Research Paper

The full technical paper detailing the research question, data contract, leakage audit, validation design, and comparative analysis is published online:

📄 **Read the Live Paper:** [https://aryavengurlekar03.github.io/Machine-Learning/paper.html](https://aryavengurlekar03.github.io/Machine-Learning/paper.html)

---

## 16. Demo

Demo video: To be added after recording.

---

## 17. Next Steps

- **Time-Aware Validation:** Incorporate multi-snapshot time-series splits to test performance across temporal shifts.
- **Learning-to-Rank Formulations:** Transition from point-wise regression target optimization to pairwise/listwise ranking objectives (e.g., LambdaMART).
- **Expanded Feature Space:** Integrate internal link architecture metrics, SERP feature presence (snippets/passages), and search intent classifications.
- **Causal Evaluation:** Conduct controlled A/B testing and quasi-experimental post-refresh traffic outcome tracking.
