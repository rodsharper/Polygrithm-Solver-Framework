# Reviewer Data — Polygrithm Solver Framework

This bundle contains the experimental data behind the paper. Each solver was automatically constructed from its problem definition. All problems are 30‑dimensional, and each was run **30 times** with a **10,000 ms** time budget per run.

## Start here

➡️ **[Results summary (CSV)](20260615_140911/batch_summary.csv)** — per‑problem **Mean, Median, StdDev, and Success Rate** across 30 runs. This is the data behind the paper's main results table.

The paper itself contains the convergence figure, so it is not duplicated here.

## Role names

Throughout this data the five specialist roles are **Global Explorer**, **Local Explorer**, **Exploiter**, **Refiner**, and **Polisher** — identical to the names used in the paper.

## Optional supporting detail

- **Ablation (solution sharing ON vs OFF):** [`AblationSummary_SharingOn_vs_SharingOff/ablation_success_rate_table.csv`](AblationSummary_SharingOn_vs_SharingOff/ablation_success_rate_table.csv), plus the bar‑plot SVGs in that same folder. A per‑problem exact‑match comparison report lives in each run's `PresentationArtifacts/` folder.
- **Role‑transition analysis:** [`20260615_140911/RoleTransition_Refined_Comparison.md`](20260615_140911/RoleTransition_Refined_Comparison.md) and the `20260615_140911/RoleTransitionAnalysis_<Problem>/` folders (transition matrices, occupancy/contribution heatmaps, representative‑run timelines, and their backing CSVs).
- **Raw per‑run traces:** `20260615_140911/<Problem>/Run_1` … `Run_30/convergence.csv` (every accepted improvement, with its contributing source and role) — e.g., `20260615_140911/Ackley 30D/Run_1/convergence.csv`.
- **Additional batches:** `20260617_060157/` (role‑transition analysis across five problems) and `20260617_094355/` (the sharing‑OFF baseline used in the ablation).
- **Full file index with sizes and SHA‑256 hashes:** [`FILE_MANIFEST.tsv`](FILE_MANIFEST.tsv).

## Provenance

- Main results batch (`20260615_140911`) solver configuration: `L3-HardNdGreedyUiRun-OrthogonalGeneralist8-SharingOn-Generalist`.
- AblationSummary_SharingOn_vs_SharingOff/

These directories preserve the original batch-run IDs so that paper tables, figures, and analysis notes can be traced back to the generated logs.

## Batch-run index

The source experiment archive contained the following batch-run directories:

- 20260613_125015
- 20260613_125231
- 20260613_132059
- 20260613_211451
- 20260613_212721
- 20260613_220522
- 20260614_033715
- 20260614_034231
- 20260614_035915
- 20260614_080249
- 20260614_082426
- 20260614_082532
- 20260614_111721
- 20260614_113130
- 20260614_113159
- 20260614_113307
- 20260614_113350
- 20260614_113521
- 20260614_121435
- 20260614_122329
- 20260614_124240
- 20260614_130108
- 20260614_130455
- 20260614_200755
- 20260614_223825
- 20260614_223911
- 20260614_223947
- 20260614_224007
- 20260614_224028
- 20260614_224050
- 20260614_225253
- 20260614_225552
- 20260614_232318
- 20260615_000438
- 20260615_071856
- 20260615_072139
- 20260615_072608
- 20260615_073127
- 20260615_073816
- 20260615_130953
- 20260615_140911
- 20260615_140911 - Copy
- 20260616_052439
- 20260617_060157
- 20260617_094355
- 20260617_125442
- 20260617_173245
- 20260617_173714
- 20260617_174113
- 20260617_174626
- 20260617_181554
- 20260617_201748
- 20260617_201907
- 20260617_204543
- 20260618_085938
- 20260618_090059
- 20260618_112427
- 3D Cube Decomposition
- AblationSummary_SharingOn_vs_SharingOff
- Himmelblau's Function (Quadrant Decomposition)
- Rosenbrock 30D
- Schwefel 2.22 30D
- Shifted Ackley 30D
- Shifted Griewank 30D
- Shifted Rastrigin 30D
- Shifted Rosenbrock 30D


## File manifest

A complete file manifest with byte sizes and SHA-256 hashes is provided in FILE_MANIFEST.tsv.

