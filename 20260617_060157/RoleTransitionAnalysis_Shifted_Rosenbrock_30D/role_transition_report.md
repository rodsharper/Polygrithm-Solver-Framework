# Role Transition Analysis — Shifted Rosenbrock 30D
**Batch:** `20260617_060157`  **Runs analyzed:** 30  **Successful runs:** 2 / 30  **Median time-to-zero among successful runs:** 3220 ms  
## Key visual artifacts
- `role_occupancy_heatmap.svg` — probability that each role appears in each active-time bin.
- `source_contribution_heatmap.svg` — source/base-solver share of positive improvement contribution by active-time bin.
- `role_transition_matrix.svg` — compressed role-change transition probabilities.
- `representative_run_timeline.svg` — median-like successful run with role-colored improvement events.

## Observed behavioral signature
The convergence traces exhibit a repeatable stochastic phase structure. Early active progress is dominated by **Exploiter** activity (mean occupancy 99%); middle progress is dominated by **Exploiter** activity (mean occupancy 97%); late active progress is dominated by **Refiner** activity (mean occupancy 94%).

## Dominant compressed role transitions
- `Polisher` → `Refiner`: 83%
- `Local Explorer` → `Exploiter`: 81%
- `Exploiter` → `Refiner`: 79%
- `Global Explorer` → `Local Explorer`: 70%
- `Refiner` → `Exploiter`: 61%
- `Refiner` → `Polisher`: 38%
- `Global Explorer` → `Exploiter`: 26%
- `Polisher` → `Exploiter`: 17%

## Suggested interpretation
Although individual runs differ in exact event timing, the aggregate traces show a statistically meaningful role-flow signature: broad discovery/exploration events tend to precede exploitation/refinement/polishing behavior, and successful runs reach the optimum after a small number of high-impact improvement jumps. The role occupancy and transition matrix should be presented as the statistical evidence; the representative timeline should be presented only as an intuitive example.

## Statistical framing
Use run-normalized active-time bins to handle stochastic timing differences. Role occupancy is measured as `P(role appears in bin)` across runs, preventing a single verbose run from dominating the estimate. Transition probabilities are computed from compressed role-change sequences, making the matrix a summary of phase changes rather than repeated identical events.
