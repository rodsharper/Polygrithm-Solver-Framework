# Role Transition Analysis — Hybrid F2 30D
**Batch:** `20260617_060157`  **Runs analyzed:** 30  **Successful runs:** 7 / 30  **Median time-to-zero among successful runs:** 5600 ms  
## Key visual artifacts
- `role_occupancy_heatmap.svg` — probability that each role appears in each active-time bin.
- `source_contribution_heatmap.svg` — source/base-solver share of positive improvement contribution by active-time bin.
- `role_transition_matrix.svg` — compressed role-change transition probabilities.
- `representative_run_timeline.svg` — median-like successful run with role-colored improvement events.

## Observed behavioral signature
The convergence traces exhibit a repeatable stochastic phase structure. Early active progress is dominated by **Refiner** activity (mean occupancy 99%); middle progress is dominated by **Refiner** activity (mean occupancy 92%); late active progress is dominated by **Refiner** activity (mean occupancy 87%).

## Dominant compressed role transitions
- `Polisher` → `Refiner`: 88%
- `Global Explorer` → `Local Explorer`: 85%
- `Local Explorer` → `Exploiter`: 81%
- `Exploiter` → `Refiner`: 64%
- `Refiner` → `Polisher`: 61%
- `Refiner` → `Exploiter`: 36%
- `Exploiter` → `Local Explorer`: 25%
- `Global Explorer` → `Exploiter`: 13%

## Suggested interpretation
Although individual runs differ in exact event timing, the aggregate traces show a statistically meaningful role-flow signature: broad discovery/exploration events tend to precede exploitation/refinement/polishing behavior, and successful runs reach the optimum after a small number of high-impact improvement jumps. The role occupancy and transition matrix should be presented as the statistical evidence; the representative timeline should be presented only as an intuitive example.

## Statistical framing
Use run-normalized active-time bins to handle stochastic timing differences. Role occupancy is measured as `P(role appears in bin)` across runs, preventing a single verbose run from dominating the estimate. Transition probabilities are computed from compressed role-change sequences, making the matrix a summary of phase changes rather than repeated identical events.
