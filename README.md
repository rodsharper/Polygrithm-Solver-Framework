# Reviewer Data — Polygrithm Solver Framework

This bundle contains the experimental data behind the paper. It is **self-contained**: this single README documents the methodology and every artifact type, so each table, figure, and CSV can be interpreted without external context.

The data is grouped below **by purpose** into three areas. The files physically live in dated batch folders (`20260615_140911/`, `20260617_060157/`, `20260617_094355/`), but **you can ignore that layout** and navigate using the groups below. A complete file index is in [`FILE_MANIFEST.tsv`](FILE_MANIFEST.tsv).

## Quick navigation

- [▶️ Start here](#start-here) — the main results table
- [📊 Batch Runs](#batch-runs) — raw per-run data and per-problem summaries
- [🔁 Role Transition Artifacts](#role-transition-artifacts) — how the five solver roles hand off control
- [🧪 Ablation Data](#ablation-data) — effect of solution sharing (ON vs OFF)
- [🧭 How the data was produced](#how-the-data-was-produced) — methodology, success criterion, conventions
- [🗂️ Complete file index](#complete-file-index)

## Start here

➡️ **Main results:** [`20260615_140911/batch_summary.csv`](20260615_140911/batch_summary.csv) — the per-problem summary behind the paper's main results table.

The convergence figure is included in the paper itself, so it is not duplicated here.

---

## Batch Runs

The raw experimental runs and their per-problem summaries. **Every problem folder** (e.g. `Ackley 30D/`) contains a `summary.txt` (that problem's aggregate summary) and the 30 run folders `Run_1/ … Run_30/`. **Every batch folder** contains a `batch_summary.csv` (one row per problem).

| Batch folder | Role of this batch | Problems | Per-problem summary |
| --- | --- | --- | --- |
| [`20260615_140911/`](20260615_140911/) | **Main results** (also has role-transition analysis) | 10 | [`batch_summary.csv`](20260615_140911/batch_summary.csv) |
| [`20260617_060157/`](20260617_060157/) | **Role-transition focus** (richest role artifacts) | 5 | [`batch_summary.csv`](20260617_060157/batch_summary.csv) |
| [`20260617_094355/`](20260617_094355/) | **Sharing-OFF baseline** for the ablation | 6 | [`batch_summary.csv`](20260617_094355/batch_summary.csv) |

The dated IDs are preserved only so the paper's tables and notes can be traced back to the generated logs.

**`<batch>/batch_summary.csv`** — one row per problem; statistics computed over the 30 final objective values (scientific notation, e.g. `1.788451E-001`):

| Column | Meaning |
| --- | --- |
| `Problem` | Benchmark name. |
| `Mean`, `Median`, `StdDev` | Central tendency and spread of the 30 final objective values (lower is better). |
| `Success` | Success rate — percentage of the 30 runs meeting the `ε` criterion (see methodology). |
| `Runs` | Number of runs (30). |
| `Best`, `Worst` | Best and worst final objective value across the 30 runs. |
| `Q1`, `Q3`, `IQR` | First quartile, third quartile, and inter-quartile range. |
| `Outliers` | Count of runs outside the Tukey `1.5 · IQR` fences. |
| `CILower`, `CIUpper` | Lower/upper bound of the 95% confidence interval for the mean. |

**`<batch>/<Problem>/Run_k/convergence.csv`** — one row per **accepted improvement** within a single run, in time order:

| Column | Meaning |
| --- | --- |
| `TimeMs` | Elapsed milliseconds when the improvement was accepted. |
| `BestQuality` | Best objective value after this improvement. |
| `Source` | The specialist/strategy that produced the improvement (e.g. `HOG8-ML06-H1-GPS-Spray-Specialist-Global Explorer`). |
| `Role` | The role that source was acting in (one of the five roles). |
| `DeltaPct` | Percentage improvement over the previous best. |

Each `Run_k/` folder also contains **`run.log`** (the raw solver log for that run).

---

## Role Transition Artifacts

Everything describing **how the five solver roles hand off control** over the course of a run. The five roles are **Global Explorer**, **Local Explorer**, **Exploiter**, **Refiner**, and **Polisher** — identical to the names used in the paper.

**Entry points (start with the narrative comparisons):**

- Narrative discussion: [`20260615_140911/RoleTransition_Refined_Comparison.md`](20260615_140911/RoleTransition_Refined_Comparison.md) · [`20260617_060157/RoleTransition_Refined_Comparison.md`](20260617_060157/RoleTransition_Refined_Comparison.md)
- Refined cross-problem tables: [`20260615_140911/RoleTransition_Refined_Tables/`](20260615_140911/RoleTransition_Refined_Tables/) · [`20260617_060157/RoleTransition_Refined_Tables/`](20260617_060157/RoleTransition_Refined_Tables/)
- Per-problem analysis folders (`RoleTransitionAnalysis_<Problem>/`):
  - In `20260615_140911/`: [`Rosenbrock_30D`](20260615_140911/RoleTransitionAnalysis_Rosenbrock_30D/) · [`Schwefel_2_22_30D`](20260615_140911/RoleTransitionAnalysis_Schwefel_2_22_30D/)
  - In `20260617_060157/`: [`Hybrid_F2_30D`](20260617_060157/RoleTransitionAnalysis_Hybrid_F2_30D/) · [`Rosenbrock_30D`](20260617_060157/RoleTransitionAnalysis_Rosenbrock_30D/) · [`Schwefel_2_22_30D`](20260617_060157/RoleTransitionAnalysis_Schwefel_2_22_30D/) · [`Shifted_Rosenbrock_30D`](20260617_060157/RoleTransitionAnalysis_Shifted_Rosenbrock_30D/)

**`RoleTransitionAnalysis_<Problem>/`** — characterises role hand-offs; run progress is divided into twenty 5% bins (`0-5%`, `5-10%`, … `95-100%`):

- **`role_transition_matrix.csv`** (+ `.svg`) — row-stochastic matrix of role→role transition probabilities (rows = *from* role, columns = *to* role; each row sums to 1). The SVG renders it as a heatmap.
- **`role_occupancy_by_bin.csv`** (+ `role_occupancy_heatmap.svg`) — fraction of activity per role within each 5% progress bin.
- **`source_contribution_by_bin.csv`** (+ `source_contribution_heatmap.svg`) — fraction of accepted improvements per source/strategy within each 5% bin.
- **`run_features.csv`** — one row per run: `Run`, `FinalBest`, `Success`, `TimeToSuccessMs`, `ActiveDurationMs`, `EventCount`, `LargeJumpCount`, `RoleEntropy`, `SourceEntropy`, and `RoleShare_<role>`.
- **`representative_run_timeline.svg`** — role/source activity timeline for a representative run.
- **`role_transition_report.md`** — narrative summary for that problem.

**`RoleTransition_Refined_Tables/<Problem>_transitions_all.csv`** — aggregated transition statistics, one row per *from→to* role pair: `FromRoleLabel`, `ToRoleLabel`, `Count`, `OverallPrevalence`, `ConditionalProbability`, `MeanRunPrevalence`, `StdDevRunPrevalence`, `MeanPhase`. The companion `RoleTransition_Refined_Comparison.md` discusses these results.

---

## Ablation Data

The paper's ablation isolating the effect of enabling vs. disabling **solution sharing** between strategies. With sharing **OFF**, strategies operate independently and consistently fail to converge under the strict success criterion (0% success across these problems); with sharing **ON**, success rises substantially, often from 0% to near 100%.

**Summary tables:**

- [`AblationSummary_SharingOn_vs_SharingOff/ablation_table.md`](AblationSummary_SharingOn_vs_SharingOff/ablation_table.md) — the comparison rendered in Markdown (read this first).
- [`AblationSummary_SharingOn_vs_SharingOff/ablation_success_rate_table.csv`](AblationSummary_SharingOn_vs_SharingOff/ablation_success_rate_table.csv) — per-problem ON-vs-OFF comparison. Columns: `Problem`, `OffSuccessPct`, `OnSuccessPct`, `DeltaSuccessPct` (percentage points), `OffMedian`, `OnMedian`, `OffMean`, `OnMean`, `OffStdDev`, `OnStdDev`. Median/mean values are final objective values (lower is better). One problem is 50-D (`Schwefel 2.22+R 50D`).

**Supporting run data:**

- Sharing-OFF baseline runs: [`20260617_094355/`](20260617_094355/) (per-problem run folders + `batch_summary.csv`).
- Exact-match reconciliation vs. the main batch: [`20260617_094355/PresentationArtifacts/Ablation_vs_20260615_140911/`](20260617_094355/PresentationArtifacts/Ablation_vs_20260615_140911/) — [`manifest`](20260617_094355/PresentationArtifacts/Ablation_vs_20260615_140911/latest_ablation_artifact_manifest.md), [`report`](20260617_094355/PresentationArtifacts/Ablation_vs_20260615_140911/latest_ablation_exact_match_report.md), [`table`](20260617_094355/PresentationArtifacts/Ablation_vs_20260615_140911/latest_ablation_exact_match_table.csv).

---

## How the data was produced

**Methodology at a glance**

- **Same single Polygrithm.** Every problem was solved by one fixed, automatically-constructed solver configuration — `L3-HardNdGreedyUiRun-OrthogonalGeneralist8-SharingOn-Generalist` — applied uniformly with **no per-problem tuning**. The specialist roster is identical across problems (visible as the `HOG8-…` source identifiers in the convergence logs).
- **Dimensionality.** All problems are **30-dimensional**, except one ablation problem that is 50-D (noted in the Ablation section).
- **Repetitions and budget.** Each problem was run **30 independent times**, each under a fixed **10-second (10,000 ms)** compute budget.

**Success criterion (identical to the paper).** A run is **successful** when its final objective value `f(x)` satisfies

> `| f(x) − f* | ≤ ε`,  with  `ε = 1 × 10⁻⁸`

where `f*` is the known global optimum. Values reported as `0.0` indicate convergence within numerical precision limits. **Lower objective values are better.**

**Outliers, and why the median is reported.** **No runs are discarded** — all 30 contribute to every statistic. A run is flagged as an **outlier** using the standard Tukey rule when its final objective value falls outside

> `[ Q1 − 1.5 · IQR ,  Q3 + 1.5 · IQR ]`

(`IQR = Q3 − Q1` of the 30 final objective values; per-problem counts are the `Outliers` column in `batch_summary.csv`). Because a few failed runs can stagnate far from the optimum and inflate the mean under heavy-tailed failure modes, the **median is reported alongside the mean** as a robust summary.

---

## Complete file index

A complete file index with byte sizes and SHA-256 hashes is provided in [`FILE_MANIFEST.tsv`](FILE_MANIFEST.tsv) (tab-separated; columns `relative_path`, `bytes`, `sha256`).