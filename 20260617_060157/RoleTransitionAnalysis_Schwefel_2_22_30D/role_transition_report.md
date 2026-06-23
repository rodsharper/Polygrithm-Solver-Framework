# Role Transition Analysis — Schwefel 2.22 30D
**Batch:** `20260617_060157`  **Runs analyzed:** 30  **Successful runs:** 30 / 30  **Median time-to-zero among successful runs:** 3026 ms  
## Key visual artifacts
- `role_occupancy_heatmap.svg` — probability that each role appears in each active-time bin.
- `source_contribution_heatmap.svg` — source/base-solver share of positive improvement contribution by active-time bin.
- `role_transition_matrix.svg` — compressed role-change transition probabilities.
- `representative_run_timeline.svg` — median-like successful run with role-colored improvement events.

## Observed behavioral signature
The convergence traces exhibit a repeatable stochastic phase structure. Early active progress is dominated by **Exploiter** activity (mean occupancy 73%); middle progress is dominated by **Exploiter** activity (mean occupancy 67%); late active progress is dominated by **Exploiter** activity (mean occupancy 63%).

## Dominant compressed role transitions
- `Global Explorer` → `Local Explorer`: 88%
- `Refiner` → `Exploiter`: 87%
- `Local Explorer` → `Exploiter`: 77%
- `Polisher` → `Exploiter`: 50%
- `Exploiter` → `Local Explorer`: 49%
- `Exploiter` → `Refiner`: 41%
- `Polisher` → `Local Explorer`: 23%
- `Polisher` → `Refiner`: 18%

## Suggested interpretation
Although individual runs differ in exact event timing, the aggregate traces show a statistically meaningful role-flow signature: broad discovery/exploration events tend to precede exploitation/refinement/polishing behavior, and successful runs reach the optimum after a small number of high-impact improvement jumps. The role occupancy and transition matrix should be presented as the statistical evidence; the representative timeline should be presented only as an intuitive example.

## Statistical framing
Use run-normalized active-time bins to handle stochastic timing differences. Role occupancy is measured as `P(role appears in bin)` across runs, preventing a single verbose run from dominating the estimate. Transition probabilities are computed from compressed role-change sequences, making the matrix a summary of phase changes rather than repeated identical events.
