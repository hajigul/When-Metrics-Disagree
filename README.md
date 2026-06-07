
# When Metrics Disagree: A Meta-Analysis of KGC Model Benchmarking
**Analyzing Trade-offs in MCDM Consistency, Stability, Robustness, and Generalizability in KGC **

**Anonymous Author(s)**  
KDD 2026 Submission (under review)


Evaluating Knowledge Graph Completion (KGC) models has reached a critical impasse due to fragmented performance assessment. Traditional rank-based metrics (MRR, Hits@k, MR) frequently produce inconsistent or contradictory rankings across datasets and metrics. We reframe KGC evaluation as a Multi-Criteria Decision Making (MCDM) problem and conduct the first comprehensive meta-evaluation of seven aggregators (EDAS, TOPSIS, VIKOR, WASPAS, Borda, MOORA, Z-Score) across ten models, five benchmarks, and two tasks: relation (h,?,t) and tail (h,r,?) prediction.

We rigorously analyze five desiderata:

- **Consistency** — alignment with individual metrics  
- **Stability** — cross-dataset ranking consistency  
- **Metric Independence** — robustness to metric removal  
- **Robustness** — stability under noise injection  
- **Generalizability** — performance prediction on unseen benchmarks  

Results reveal a clear **No Free Lunch** trade-off: **no single aggregator dominates all dimensions**. Pareto analysis identifies **Z-Score** as the jointly optimal aggregator for holistic KGC evaluation. The framework resolves longstanding contradictions in model rankings and establishes a principled, reproducible standard for KGC benchmarking.


This notebook reproduces the core experiments and visualizations presented in the paper:

- Relation prediction analysis (consistency, correlations, and ranking plots)  
- Tail prediction analysis (same dimensions)  
- Stability (cross-dataset variance + boxplots)  
- Robustness / metric dependency (leave-one-metric-out + noise injection)  
- Consensus analysis (average ranking + lollipop plots)  
- No-Free-Lunch visualization suite:  
  - Critical Difference diagrams  
  - Radar charts (trade-off overview)  
  - Horizontal desiderata bars  
  - Overall performance ranking  

## Required Input Files

Place these two CSV files in the following path **before running**:  
- r_pred_main_file.csv     # Relation prediction metrics (all datasets)  
- t_pred_main_file.csv     # Tail prediction metrics (all datasets)
