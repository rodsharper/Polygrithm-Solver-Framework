# Reviewer Data — Polygrithm Solver Framework

This bundle contains the experimental data behind the paper. It is self‑contained: this single README documents the methodology and **every artifact type** in the bundle, so each table, figure, and CSV can be interpreted without external context.

## Methodology at a glance

- **Same single Polygrithm.** Every problem was solved by one fixed, automatically‑constructed solver configuration — `L3-HardNdGreedyUiRun-OrthogonalGeneralist8-SharingOn-Generalist` — applied uniformly to all problems with **no per‑problem tuning**. The framework composes the solver from each problem's definition using this one recipe; the specialist roster is identical across problems (visible as the `HOG8-…` source identifiers in the convergence logs).
- **Dimensionality.** All problems are **30‑dimensional**, except one ablation problem that is 50‑D (noted in the Ablation section).
- **Repetitions and budget.** Each problem was run **30 independent times**, each run under a fixed **10‑second (10,000 ms)** compute budget.

## Success criterion (identical to the paper)

A run is **successful** when its final objective value `f(x)` satisfies

> `| f(x) − f* | ≤ ε`,  with  `ε = 1 × 10⁻⁸`

where `f*` is the known global optimum of the benchmark. Values reported as `0.0` indicate convergence within numerical precision limits. **Lower objective values are better.**

## Outliers, and why the median is reported

**No runs are discarded** — all 30 runs contribute to every statistic. A run is flagged as an **outlier** using the standard Tukey rule: its final objective value falls outside

> `[ Q1 − 1.5 · IQR ,  Q3 + 1.5 · IQR ]`

where `Q1`/`Q3` are the first/third quartiles and `IQR = Q3 − Q1` of the 30 final objective values. The per‑problem outlier count is the `Outliers` column in `batch_summary.csv`. Because a small number of failed runs can stagnate far from the optimum and inflate the mean under heavy‑tailed failure modes, the **median is reported alongside the mean** as a robust summary (e.g., a problem can show a high success rate yet a relatively large mean if a few runs stagnate).

## Start here

➡️ **[Main results — `20260615_140911/batch_summary.csv`](20260615_140911/batch_summary.csv)** — the per‑problem summary behind the paper's main results table.

The paper itself contains the convergence figure, so it is not duplicated here.

## Role names

The five specialist roles are **Global Explorer**, **Local Explorer**, **Exploiter**, **Refiner**, and **Polisher** — identical to the names used in the paper.

## What each artifact contains

### Per‑problem results — `<batch>/batch_summary.csv`

One row per problem; all statistics are computed over the 30 final objective values (scientific notation, e.g. `1.788451E-001`). Columns:

| Column | Meaning |
| --- | --- |
| `Problem` | Benchmark name. |
| `Mean`, `Median`, `StdDev` | Central tendency and spread of the 30 final objective values (lower is better). |
| `Success` | Success rate — percentage of the 30 runs meeting the `ε` criterion above. |
| `Runs` | Number of runs (30). |
| `Best`, `Worst` | Best and worst final objective value across the 30 runs. |
| `Q1`, `Q3`, `IQR` | First quartile, third quartile, and inter‑quartile range. |
| `Outliers` | Count of runs outside the Tukey `1.5 · IQR` fences (see *Outliers* above). |
| `CILower`, `CIUpper` | Lower/upper bound of the 95% confidence interval for the mean. |

### Per‑run convergence traces — `<batch>/<Problem>/Run_k/convergence.csv`

One row per **accepted improvement** during a single run, in time order. Columns:

| Column | Meaning |
| --- | --- |
| `TimeMs` | Elapsed milliseconds when the improvement was accepted. |
| `BestQuality` | Best objective value after this improvement. |
| `Source` | The specialist/strategy that produced the improvement (e.g. `HOG8-ML06-H1-GPS-Spray-Specialist-Global Explorer`). |
| `Role` | The role that source was acting in (one of the five roles). |
| `DeltaPct` | Percentage improvement over the previous best. |

Each run folder also contains **`run.log`** (the raw solver log for that run). Each problem folder contains a **`summary.txt`** with that problem's aggregate run summary, and the 30 run folders `Run_1 … Run_30/`.

### Role‑transition analysis — `<batch>/RoleTransitionAnalysis_<Problem>/`

Characterises how the five roles hand off control over the course of a run. Run progress is divided into twenty 5% bins (`0-5%`, `5-10%`, … `95-100%`).

- **`role_transition_matrix.csv`** (+ `role_transition_matrix.svg`) — row‑stochastic matrix of role→role transition probabilities (rows = *from* role, columns = *to* role; each row sums to 1). The SVG renders it as a heatmap.
- **`role_occupancy_by_bin.csv`** (+ `role_occupancy_heatmap.svg`) — fraction of activity attributed to each role within each 5% progress bin (rows = role, columns = bins).
- **`source_contribution_by_bin.csv`** (+ `source_contribution_heatmap.svg`) — fraction of accepted improvements contributed by each source/strategy within each 5% progress bin (rows = source, columns = bins).
- **`run_features.csv`** — one row per run with summary features: `Run`, `FinalBest`, `Success` (True/False), `TimeToSuccessMs` (blank if never reached), `ActiveDurationMs`, `EventCount`, `LargeJumpCount`, `RoleEntropy`, `SourceEntropy`, and `RoleShare_<role>` (share of events per role).
- **`representative_run_timeline.svg`** — timeline of role/source activity for a representative run.
- **`role_transition_report.md`** — narrative summary of the role‑transition behaviour for that problem.

### Cross‑problem transition tables — `<batch>/RoleTransition_Refined_Tables/<Problem>_transitions_all.csv`

Aggregated role‑transition statistics, one row per *from→to* role pair. Columns: `FromRoleLabel`, `ToRoleLabel`, `Count`, `OverallPrevalence`, `ConditionalProbability`, `MeanRunPrevalence`, `StdDevRunPrevalence`, `MeanPhase`. The companion **`<batch>/RoleTransition_Refined_Comparison.md`** discusses these results.

### Ablation — `AblationSummary_SharingOn_vs_SharingOff/`

The paper's ablation isolating the effect of enabling vs. disabling **solution sharing** between strategies. With sharing **OFF**, strategies operate independently and consistently fail to converge under the strict success criterion (0% success across these problems); with sharing **ON**, success rises substantially, often from 0% to near 100%.

- **`ablation_success_rate_table.csv`** — per‑problem ON‑vs‑OFF comparison. Columns: `Problem`, `OffSuccessPct`, `OnSuccessPct`, `DeltaSuccessPct` (percentage points), `OffMedian`, `OnMedian`, `OffMean`, `OnMean`, `OffStdDev`, `OnStdDev`. Median/mean values are final objective values (lower is better). One problem is 50‑D (`Schwefel 2.22+R 50D`).
- **`ablation_table.md`** — the same table rendered in Markdown.

The sharing‑OFF baseline runs used for this comparison are preserved under `20260617_094355/`.

## Batches

- **`20260615_140911/`** — the main results batch: 10 problems (`batch_summary.csv` + per‑problem run folders) plus role‑transition analysis for Rosenbrock 30D and Schwefel 2.22 30D. Solver configuration: `L3-HardNdGreedyUiRun-OrthogonalGeneralist8-SharingOn-Generalist`.
- **`20260617_060157/`** — additional role‑transition analysis across five problems (per‑problem run folders, four `RoleTransitionAnalysis_<Problem>/` folders, the refined transition tables, and a `PresentationArtifacts/` folder of per‑problem presentation outputs).
- **`20260617_094355/`** — the **sharing‑OFF baseline** used in the ablation (per‑problem run folders + `batch_summary.csv` + `PresentationArtifacts/`).

The original batch‑run IDs are preserved so the paper's tables, figures, and analysis notes can be traced back to the generated logs.

## File manifest

A complete file index with byte sizes and SHA‑256 hashes is provided in **[`FILE_MANIFEST.tsv`](FILE_MANIFEST.tsv)** (tab‑separated, with columns `relative_path`, `bytes`, `sha256`).