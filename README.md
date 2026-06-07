# When Metrics Disagree: A Meta-Analysis of Knowledge-Graph-Completion Model Benchmarking

> **ICDM submission** — code for the paper *"When Metrics Disagree: A Meta-Analysis of Knowledge-Graph-Completion Model Benchmarking"*

[![Python 3.8+](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

---

## Overview

Evaluating Knowledge Graph Completion (KGC) models is hindered by fragmented assessment. Relying on isolated rank-based metrics (MRR, Hits@k, MR) yields conflicting model rankings, complicating comparisons, enabling selective reporting, and obscuring genuine progress.

This repository reframes KGC evaluation as a **Multi-Criteria Decision-Making (MCDM)** problem and provides a meta-analysis evaluating **seven aggregators** across **five tests**:

| Test | Description |
|---|---|
| **Consistency** | Alignment with individual base metrics |
| **Stability** | Cross-dataset ranking variance |
| **Independence** | Robustness under leave-one-metric-out |
| **Robustness** | Resilience to noise injection (5%–30%, 1,000 trials) |
| **Generalizability** | Predictive accuracy on unseen benchmarks (leave-one-dataset-out) |

Pareto-optimal analysis identifies **Z-score** as the most balanced aggregator, with **DualE** and **FMS** as top-performing models for tail and relation prediction, respectively.

---

## Repository Structure

```
.
├── 1__Tail_Analysis_Main_File.ipynb                          # Main tail prediction (h,r,?) analysis
├── 2__Relation_analysis_Main_File.ipynb                      # Main relation prediction (h,?,t) analysis
├── 3__Tail_prediction_sensitivity_analysis.ipynb             # LOMO/LOGO sensitivity — tail
├── 4__Relation_prediction_sensitivity_analysis.ipynb         # LOMO/LOGO sensitivity — relation
├── 5__Tail_prediction_base_analysis_code__Supplementary_.ipynb   # Supplementary tail analysis
├── 6__Relation_prediction_base_analysis__Supplementary_.ipynb    # Supplementary relation analysis
├── data/
│   ├── t_pred_main_file.csv     # Tail prediction metrics across all datasets
│   └── r_pred_main_file.csv     # Relation prediction metrics across all datasets
└── README.md
```

> **Note:** The `data/` CSV files are not included in this repository. See [Data](#data) below.

---

## Requirements

### Python version

Python 3.8 or higher.

### Install dependencies

```bash
pip install -r requirements.txt
```

Or install manually:

```bash
pip install numpy pandas scipy matplotlib seaborn tqdm scikit-posthocs
```

### `requirements.txt`

```
numpy>=1.21
pandas>=1.3
scipy>=1.7
matplotlib>=3.4
seaborn>=0.11
tqdm>=4.62
scikit-posthocs>=0.7
```

> The notebooks were originally developed in **Google Colab**. They contain `google.colab` drive mount cells — these can be skipped or replaced with local file paths when running locally (see [Running Locally](#running-locally)).

---

## Data

The experiments require two CSV input files:

| File | Description |
|---|---|
| `t_pred_main_file.csv` | Tail prediction (h,r,?) metrics — MR, MRR, H@1, H@3, H@10 per model per dataset |
| `r_pred_main_file.csv` | Relation prediction (h,?,t) metrics — same format |

The data covers **20 KGC models** across **5 benchmark datasets**: FB15k, WN18, FB15K-237, WN18RR, and YAGO3-10. Source results are from published papers (see References in the paper).

Place the CSV files in the `data/` folder (or update the path variables at the top of each notebook).

---

## How to Run

### Option A — Google Colab (recommended)

1. Upload the repository to your Google Drive.
2. Open any notebook in Colab.
3. Run the drive mount cell and update the data path if needed:
   ```python
   ORIGINAL_DATA_PATH = '/content/drive/MyDrive/<your_folder>/t_pred_main_file.csv'
   ```
4. Run all cells (`Runtime → Run all`).

### Option B — Running Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/when-metrics-disagree.git
   cd when-metrics-disagree
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. In each notebook, **skip or comment out** the Google Drive mount cell:
   ```python
   # from google.colab import drive
   # drive.mount('/content/drive', force_remount=True)
   ```

4. Update the data path variable to a local path, e.g.:
   ```python
   ORIGINAL_DATA_PATH = 'data/t_pred_main_file.csv'
   ```

5. Launch Jupyter and run:
   ```bash
   jupyter notebook
   ```

### Notebook execution order

For full reproduction of paper results, run in this order:

| Step | Notebook | Purpose |
|---|---|---|
| 1 | `1__Tail_Analysis_Main_File.ipynb` | Core tail prediction MCDM analysis + Pareto |
| 2 | `2__Relation_analysis_Main_File.ipynb` | Core relation prediction MCDM analysis + Pareto |
| 3 | `3__Tail_prediction_sensitivity_analysis.ipynb` | LOMO/LOGO sensitivity for tail task |
| 4 | `4__Relation_prediction_sensitivity_analysis.ipynb` | LOMO/LOGO sensitivity for relation task |
| 5 | `5__Tail_prediction_base_analysis_code__Supplementary_.ipynb` | Full-Set / LOMO-only / LOGO-only supplementary results |
| 6 | `6__Relation_prediction_base_analysis__Supplementary_.ipynb` | Same, for relation prediction |

---

## MCDM Aggregators

Seven aggregators are evaluated:

| ID | Aggregator | Description |
|---|---|---|
| ZS | **Z-score** | Standardizes metrics; Pareto-optimal aggregator |
| ED | **EDAS** | Distance from average solution |
| MO | **MOORA** | Multi-objective ratio analysis |
| TP | **TOPSIS** | Similarity to ideal solution |
| BS | **Borda Count** | Ordinal rank aggregation |
| WA | **WASPAS** | Weighted sum + weighted product hybrid |
| VQ | **VIKOR** | Compromise ranking under group utility |

---

## Key Results

- **Z-score** is the Pareto-optimal aggregator for both tail and relation prediction tasks.
- **DualE** ranks first for tail prediction (h,r,?).
- **FMS** ranks first for relation prediction (h,?,t).
- Consistency and Stability are robust to model removal; Generalizability and Independence are highly sensitive.
- LOGO removal impacts exceed LOMO, as removing architectural families disrupts transferable rankings more than single-model removal.

---

## Citation

If you use this code or framework, please cite:

```bibtex
@inproceedings{whenmetricsagree2025,
  title     = {When Metrics Disagree: A Meta-Analysis of Knowledge-Graph-Completion Model Benchmarking},
  booktitle = {IEEE International Conference on Data Mining (ICDM)},
  year      = {2025}
}
```

---

## License

This project is released under the [MIT License](LICENSE).
