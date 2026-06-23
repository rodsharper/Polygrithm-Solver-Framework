# Refined Role Transition Comparison

Transition statistics recomputed directly from raw `convergence.csv` traces. Consecutive identical roles within each run are compressed before counting transitions.

## How to read the percentages

- **Count** = number of compressed role changes observed across all runs.
- **Overall prevalence** = `count(From → To) / count(all compressed transitions)` for that problem. This answers: *what transitions happen most often overall?*
- **Conditional probability** = `count(From → To) / count(all transitions leaving From)`. This answers: *when role From changes, where does it usually go?*

- **Mean run prevalence** = compute the transition's prevalence separately within each run, then average those 30 values. This gives each run equal weight.
- **Run StdDev** = standard deviation of those 30 per-run prevalence values. This shows whether the transition is consistently present or concentrated in a few high-switching runs.
- **Mean phase** = average normalized within-run position of that transition, where 0.0 is early active improvement and 1.0 is late active improvement.

Canonical role labels used here: **Global Explorer**, **Local Explorer**, **Exploiter**, **Refiner**, and **Polisher**.

## Schwefel 2.22 30D

Runs: **30**  
Successes: **30 / 30**  
Total compressed transitions: **938**

### Top 10 transitions by overall prevalence

| Rank | Transition | Count | Pooled prevalence | Mean run prevalence | Run StdDev | Conditional P(to \| from) | Mean phase |
|---:|---|---:|---:|---:|---:|---:|---:|
| 1 | `Local Explorer` → `Exploiter` | 208 | 22.2% | 23.2% | 9.6% | 77.0% | 0.50 |
| 2 | `Exploiter` → `Local Explorer` | 196 | 20.9% | 16.9% | 9.7% | 49.2% | 0.55 |
| 3 | `Refiner` → `Exploiter` | 173 | 18.4% | 14.0% | 9.3% | 86.9% | 0.43 |
| 4 | `Exploiter` → `Refiner` | 164 | 17.5% | 13.3% | 8.8% | 41.2% | 0.39 |
| 5 | `Global Explorer` → `Local Explorer` | 43 | 4.6% | 12.0% | 14.8% | 87.8% | 0.34 |
| 6 | `Local Explorer` → `Refiner` | 31 | 3.3% | 2.5% | 2.4% | 11.5% | 0.61 |
| 7 | `Local Explorer` → `Global Explorer` | 27 | 2.9% | 5.3% | 12.4% | 10.0% | 0.93 |
| 8 | `Refiner` → `Local Explorer` | 26 | 2.8% | 2.1% | 3.0% | 13.1% | 0.58 |
| 9 | `Exploiter` → `Global Explorer` | 20 | 2.1% | 6.9% | 11.6% | 5.0% | 0.90 |
| 10 | `Exploiter` → `Polisher` | 18 | 1.9% | 1.3% | 2.4% | 4.5% | 0.50 |

### Top 10 transitions by conditional probability

| Rank | Transition | Count | Pooled prevalence | Mean run prevalence | Run StdDev | Conditional P(to \| from) | Mean phase |
|---:|---|---:|---:|---:|---:|---:|---:|
| 1 | `Global Explorer` → `Local Explorer` | 43 | 4.6% | 12.0% | 14.8% | 87.8% | 0.34 |
| 2 | `Refiner` → `Exploiter` | 173 | 18.4% | 14.0% | 9.3% | 86.9% | 0.43 |
| 3 | `Local Explorer` → `Exploiter` | 208 | 22.2% | 23.2% | 9.6% | 77.0% | 0.50 |
| 4 | `Polisher` → `Exploiter` | 11 | 1.2% | 0.9% | 1.5% | 50.0% | 0.51 |
| 5 | `Exploiter` → `Local Explorer` | 196 | 20.9% | 16.9% | 9.7% | 49.2% | 0.55 |
| 6 | `Exploiter` → `Refiner` | 164 | 17.5% | 13.3% | 8.8% | 41.2% | 0.39 |
| 7 | `Polisher` → `Local Explorer` | 5 | 0.5% | 0.4% | 1.0% | 22.7% | 0.48 |
| 8 | `Polisher` → `Refiner` | 4 | 0.4% | 0.3% | 0.9% | 18.2% | 0.51 |
| 9 | `Refiner` → `Local Explorer` | 26 | 2.8% | 2.1% | 3.0% | 13.1% | 0.58 |
| 10 | `Global Explorer` → `Exploiter` | 6 | 0.6% | 0.4% | 0.9% | 12.2% | 0.69 |

### Phase-ordered view of prevalent transitions

This table takes the same high-prevalence transitions and orders them by **mean phase**. It is a useful approximation of a typical temporal flow, but cyclic transitions mean it should not be read as a clean deterministic sequence.

| Phase order | Transition | Mean phase | Count | Pooled prevalence | Mean run prevalence | Run StdDev |
|---:|---|---:|---:|---:|---:|---:|
| 1 | `Global Explorer` → `Local Explorer` | 0.34 | 43 | 4.6% | 12.0% | 14.8% |
| 2 | `Exploiter` → `Refiner` | 0.39 | 164 | 17.5% | 13.3% | 8.8% |
| 3 | `Refiner` → `Exploiter` | 0.43 | 173 | 18.4% | 14.0% | 9.3% |
| 4 | `Local Explorer` → `Exploiter` | 0.50 | 208 | 22.2% | 23.2% | 9.6% |
| 5 | `Exploiter` → `Polisher` | 0.50 | 18 | 1.9% | 1.3% | 2.4% |
| 6 | `Exploiter` → `Local Explorer` | 0.55 | 196 | 20.9% | 16.9% | 9.7% |
| 7 | `Refiner` → `Local Explorer` | 0.58 | 26 | 2.8% | 2.1% | 3.0% |
| 8 | `Local Explorer` → `Refiner` | 0.61 | 31 | 3.3% | 2.5% | 2.4% |
| 9 | `Exploiter` → `Global Explorer` | 0.90 | 20 | 2.1% | 6.9% | 11.6% |
| 10 | `Local Explorer` → `Global Explorer` | 0.93 | 27 | 2.9% | 5.3% | 12.4% |

## Rosenbrock 30D

Runs: **30**  
Successes: **2 / 30**  
Total compressed transitions: **9738**

### Top 10 transitions by overall prevalence

| Rank | Transition | Count | Pooled prevalence | Mean run prevalence | Run StdDev | Conditional P(to \| from) | Mean phase |
|---:|---|---:|---:|---:|---:|---:|---:|
| 1 | `Refiner` → `Exploiter` | 2633 | 27.0% | 25.6% | 5.8% | 62.6% | 0.40 |
| 2 | `Exploiter` → `Refiner` | 2548 | 26.2% | 25.1% | 4.6% | 79.6% | 0.39 |
| 3 | `Polisher` → `Refiner` | 1662 | 17.1% | 16.5% | 5.4% | 83.7% | 0.71 |
| 4 | `Refiner` → `Polisher` | 1557 | 16.0% | 15.6% | 4.5% | 37.0% | 0.72 |
| 5 | `Exploiter` → `Polisher` | 431 | 4.4% | 4.2% | 1.4% | 13.5% | 0.58 |
| 6 | `Polisher` → `Exploiter` | 320 | 3.3% | 3.0% | 1.3% | 16.1% | 0.57 |
| 7 | `Local Explorer` → `Exploiter` | 233 | 2.4% | 3.9% | 6.9% | 84.4% | 0.14 |
| 8 | `Exploiter` → `Local Explorer` | 209 | 2.1% | 3.5% | 6.2% | 6.5% | 0.15 |
| 9 | `Global Explorer` → `Local Explorer` | 51 | 0.5% | 0.7% | 0.9% | 71.8% | 0.02 |
| 10 | `Local Explorer` → `Global Explorer` | 28 | 0.3% | 0.4% | 0.7% | 10.1% | 0.08 |

### Top 10 transitions by conditional probability

| Rank | Transition | Count | Pooled prevalence | Mean run prevalence | Run StdDev | Conditional P(to \| from) | Mean phase |
|---:|---|---:|---:|---:|---:|---:|---:|
| 1 | `Local Explorer` → `Exploiter` | 233 | 2.4% | 3.9% | 6.9% | 84.4% | 0.14 |
| 2 | `Polisher` → `Refiner` | 1662 | 17.1% | 16.5% | 5.4% | 83.7% | 0.71 |
| 3 | `Exploiter` → `Refiner` | 2548 | 26.2% | 25.1% | 4.6% | 79.6% | 0.39 |
| 4 | `Global Explorer` → `Local Explorer` | 51 | 0.5% | 0.7% | 0.9% | 71.8% | 0.02 |
| 5 | `Refiner` → `Exploiter` | 2633 | 27.0% | 25.6% | 5.8% | 62.6% | 0.40 |
| 6 | `Refiner` → `Polisher` | 1557 | 16.0% | 15.6% | 4.5% | 37.0% | 0.72 |
| 7 | `Global Explorer` → `Exploiter` | 19 | 0.2% | 0.5% | 1.4% | 26.8% | 0.06 |
| 8 | `Polisher` → `Exploiter` | 320 | 3.3% | 3.0% | 1.3% | 16.1% | 0.57 |
| 9 | `Exploiter` → `Polisher` | 431 | 4.4% | 4.2% | 1.4% | 13.5% | 0.58 |
| 10 | `Local Explorer` → `Global Explorer` | 28 | 0.3% | 0.4% | 0.7% | 10.1% | 0.08 |

### Phase-ordered view of prevalent transitions

This table takes the same high-prevalence transitions and orders them by **mean phase**. It is a useful approximation of a typical temporal flow, but cyclic transitions mean it should not be read as a clean deterministic sequence.

| Phase order | Transition | Mean phase | Count | Pooled prevalence | Mean run prevalence | Run StdDev |
|---:|---|---:|---:|---:|---:|---:|
| 1 | `Global Explorer` → `Local Explorer` | 0.02 | 51 | 0.5% | 0.7% | 0.9% |
| 2 | `Local Explorer` → `Global Explorer` | 0.08 | 28 | 0.3% | 0.4% | 0.7% |
| 3 | `Local Explorer` → `Exploiter` | 0.14 | 233 | 2.4% | 3.9% | 6.9% |
| 4 | `Exploiter` → `Local Explorer` | 0.15 | 209 | 2.1% | 3.5% | 6.2% |
| 5 | `Exploiter` → `Refiner` | 0.39 | 2548 | 26.2% | 25.1% | 4.6% |
| 6 | `Refiner` → `Exploiter` | 0.40 | 2633 | 27.0% | 25.6% | 5.8% |
| 7 | `Polisher` → `Exploiter` | 0.57 | 320 | 3.3% | 3.0% | 1.3% |
| 8 | `Exploiter` → `Polisher` | 0.58 | 431 | 4.4% | 4.2% | 1.4% |
| 9 | `Polisher` → `Refiner` | 0.71 | 1662 | 17.1% | 16.5% | 5.4% |
| 10 | `Refiner` → `Polisher` | 0.72 | 1557 | 16.0% | 15.6% | 4.5% |

## Verified side-by-side interpretation

| Feature | Schwefel 2.22 30D | Rosenbrock 30D |
|---|---|---|
| Success rate | 30/30 = 100% | 3/30 = 10% |
| Most prevalent transition | `Local Explorer` → `Exploiter`: count 208, prevalence 22.2%, conditional 77.0% | `Refiner` → `Exploiter`: count 2633, prevalence 27.0%, conditional 62.6% |
| Global-to-local exploration | count 43, pooled 4.6%, mean-run 12.0% ± 14.8%, conditional 87.8%, mean phase 0.34 | count 51, pooled 0.5%, mean-run 0.7% ± 0.9%, conditional 71.8%, mean phase 0.02 |
| Local exploration to exploitation | count 208, pooled 22.2%, mean-run 23.2% ± 9.6%, conditional 77.0%, mean phase 0.50 | count 233, pooled 2.4%, mean-run 3.9% ± 6.9%, conditional 84.4%, mean phase 0.14 |
| Exploiter to local exploration | count 196, pooled 20.9%, mean-run 16.9% ± 9.7%, conditional 49.2%, mean phase 0.55 | count 209, pooled 2.1%, mean-run 3.5% ± 6.2%, conditional 6.5%, mean phase 0.15 |
| Exploiter to refinement | count 164, pooled 17.5%, mean-run 13.3% ± 8.8%, conditional 41.2%, mean phase 0.39 | count 2548, pooled 26.2%, mean-run 25.1% ± 4.6%, conditional 79.6%, mean phase 0.39 |
| Refiner to exploitation | count 173, pooled 18.4%, mean-run 14.0% ± 9.3%, conditional 86.9%, mean phase 0.43 | count 2633, pooled 27.0%, mean-run 25.6% ± 5.8%, conditional 62.6%, mean phase 0.40 |
| Refiner to polishing | not observed | count 1557, pooled 16.0%, mean-run 15.6% ± 4.5%, conditional 37.0%, mean phase 0.72 |
| Polisher back to refinement | count 4, pooled 0.4%, mean-run 0.3% ± 0.9%, conditional 18.2%, mean phase 0.51 | count 1662, pooled 17.1%, mean-run 16.5% ± 5.4%, conditional 83.7%, mean phase 0.71 |
| Landscape framing | Trap-heavy / large jumps useful | Smooth curved valley / careful local following useful |

## Refined interpretation

The earlier clean phrase `Global Explorer → Local Explorer → Exploiter` is a useful shorthand for part of the Schwefel behavior, but the full transition table shows a more cyclic process. Schwefel has strong global-to-local discovery and local-explorer-to-exploiter movement, while also showing a meaningful `Exploiter → Local Explorer` return path. That supports an interpretation of repeated basin probing rather than a one-way pipeline.

Rosenbrock shows stronger exploitation/refinement coupling in overall prevalence. Its most common transitions are dominated by `Refiner → Exploiter` and `Exploiter → Refiner`. The high conditional `Polisher → Refiner` probability is real, but it should be interpreted carefully: it is strong **when polishing occurs**, not necessarily the dominant behavior overall. This correction avoids overstating a Refiner ⇄ Polisher loop as the main global pattern.

Sequencing the transitions into a single typical path is only partially valid. The phase-ordered tables approximate temporal flow using mean within-run position, but both problems show feedback loops. Therefore, the most defensible presentation is: **phase tendencies plus cyclic transition motifs**, not a single fixed role pipeline.

The best-supported conclusion is that the same Polygrithm hierarchy exhibits different stochastic transition tendencies by problem. Schwefel emphasizes discovery/probing cycles; Rosenbrock emphasizes exploitation/refinement cycling consistent with navigating a smooth curved basin.
