# Refined Role Transition Comparison

Transition statistics recomputed directly from raw `convergence.csv` traces. Consecutive identical roles within each run are compressed before counting transitions.

## How to read the percentages

- **Count** = number of compressed role changes observed across all runs.
- **Overall prevalence** = `count(From → To) / count(all compressed transitions)` for that problem. This answers: *what transitions happen most often overall?*
- **Conditional probability** = `count(From → To) / count(all transitions leaving From)`. This answers: *when role From changes, where does it usually go?*

- **Mean run prevalence** = compute the transition's prevalence separately within each run, then average those 30 values. This gives each run equal weight.
- **Run StdDev** = standard deviation of those 30 per-run prevalence values. This shows whether the transition is consistently present or concentrated in a few high-switching runs.
- **Mean phase** = average normalized within-run position of that transition, where 0.0 is early active improvement and 1.0 is late active improvement.

Role labels: **Global Explorer**, **Local Explorer**, **Exploiter**, **Refiner**, and **Polisher**.

## Schwefel 2.22 30D

Runs: **30**  
Successes: **30 / 30**  
Total compressed transitions: **791**

### Top 10 transitions by overall prevalence

| Rank | Transition | Count | Pooled prevalence | Mean run prevalence | Run StdDev | Conditional P(to \| from) | Mean phase |
|---:|---|---:|---:|---:|---:|---:|---:|
| 1 | `Local Explorer` → `Exploiter` | 195 | 24.7% | 22.7% | 10.7% | 82.6% | 0.51 |
| 2 | `Exploiter` → `Local Explorer` | 172 | 21.7% | 18.5% | 9.5% | 50.7% | 0.53 |
| 3 | `Exploiter` → `Refiner` | 138 | 17.4% | 12.9% | 8.9% | 40.7% | 0.45 |
| 4 | `Refiner` → `Exploiter` | 137 | 17.3% | 12.7% | 8.7% | 81.5% | 0.46 |
| 5 | `Global Explorer` → `Local Explorer` | 35 | 4.4% | 12.9% | 16.8% | 97.2% | 0.19 |
| 6 | `Refiner` → `Local Explorer` | 27 | 3.4% | 2.5% | 2.9% | 16.1% | 0.60 |
| 7 | `Local Explorer` → `Refiner` | 27 | 3.4% | 2.5% | 3.1% | 11.4% | 0.52 |
| 8 | `Exploiter` → `Global Explorer` | 18 | 2.3% | 3.3% | 6.7% | 5.3% | 0.96 |
| 9 | `Local Explorer` → `Global Explorer` | 14 | 1.8% | 9.0% | 17.5% | 5.9% | 0.89 |
| 10 | `Exploiter` → `Polisher` | 11 | 1.4% | 1.2% | 2.6% | 3.2% | 0.44 |

### Top 10 transitions by conditional probability

| Rank | Transition | Count | Pooled prevalence | Mean run prevalence | Run StdDev | Conditional P(to \| from) | Mean phase |
|---:|---|---:|---:|---:|---:|---:|---:|
| 1 | `Global Explorer` → `Local Explorer` | 35 | 4.4% | 12.9% | 16.8% | 97.2% | 0.19 |
| 2 | `Local Explorer` → `Exploiter` | 195 | 24.7% | 22.7% | 10.7% | 82.6% | 0.51 |
| 3 | `Refiner` → `Exploiter` | 137 | 17.3% | 12.7% | 8.7% | 81.5% | 0.46 |
| 4 | `Exploiter` → `Local Explorer` | 172 | 21.7% | 18.5% | 9.5% | 50.7% | 0.53 |
| 5 | `Polisher` → `Exploiter` | 6 | 0.8% | 0.6% | 1.2% | 50.0% | 0.42 |
| 6 | `Exploiter` → `Refiner` | 138 | 17.4% | 12.9% | 8.9% | 40.7% | 0.45 |
| 7 | `Polisher` → `Refiner` | 3 | 0.4% | 0.2% | 0.7% | 25.0% | 0.23 |
| 8 | `Polisher` → `Local Explorer` | 2 | 0.3% | 0.1% | 0.6% | 16.7% | 0.68 |
| 9 | `Refiner` → `Local Explorer` | 27 | 3.4% | 2.5% | 2.9% | 16.1% | 0.60 |
| 10 | `Local Explorer` → `Refiner` | 27 | 3.4% | 2.5% | 3.1% | 11.4% | 0.52 |

### Phase-ordered view of prevalent transitions

This table takes the same high-prevalence transitions and orders them by **mean phase**. It is a useful approximation of a typical temporal flow, but cyclic transitions mean it should not be read as a clean deterministic sequence.

| Phase order | Transition | Mean phase | Count | Pooled prevalence | Mean run prevalence | Run StdDev |
|---:|---|---:|---:|---:|---:|---:|
| 1 | `Global Explorer` → `Local Explorer` | 0.19 | 35 | 4.4% | 12.9% | 16.8% |
| 2 | `Exploiter` → `Polisher` | 0.44 | 11 | 1.4% | 1.2% | 2.6% |
| 3 | `Exploiter` → `Refiner` | 0.45 | 138 | 17.4% | 12.9% | 8.9% |
| 4 | `Refiner` → `Exploiter` | 0.46 | 137 | 17.3% | 12.7% | 8.7% |
| 5 | `Local Explorer` → `Exploiter` | 0.51 | 195 | 24.7% | 22.7% | 10.7% |
| 6 | `Local Explorer` → `Refiner` | 0.52 | 27 | 3.4% | 2.5% | 3.1% |
| 7 | `Exploiter` → `Local Explorer` | 0.53 | 172 | 21.7% | 18.5% | 9.5% |
| 8 | `Refiner` → `Local Explorer` | 0.60 | 27 | 3.4% | 2.5% | 2.9% |
| 9 | `Local Explorer` → `Global Explorer` | 0.89 | 14 | 1.8% | 9.0% | 17.5% |
| 10 | `Exploiter` → `Global Explorer` | 0.96 | 18 | 2.3% | 3.3% | 6.7% |

## Rosenbrock 30D

Runs: **30**  
Successes: **3 / 30**  
Total compressed transitions: **8777**

### Top 10 transitions by overall prevalence

| Rank | Transition | Count | Pooled prevalence | Mean run prevalence | Run StdDev | Conditional P(to \| from) | Mean phase |
|---:|---|---:|---:|---:|---:|---:|---:|
| 1 | `Refiner` → `Exploiter` | 2307 | 26.3% | 24.1% | 8.3% | 63.1% | 0.42 |
| 2 | `Exploiter` → `Refiner` | 2269 | 25.9% | 23.8% | 8.0% | 76.7% | 0.41 |
| 3 | `Polisher` → `Refiner` | 1389 | 15.8% | 14.7% | 6.6% | 83.4% | 0.73 |
| 4 | `Refiner` → `Polisher` | 1325 | 15.1% | 14.0% | 6.2% | 36.3% | 0.73 |
| 5 | `Local Explorer` → `Exploiter` | 365 | 4.2% | 7.4% | 11.7% | 86.5% | 0.23 |
| 6 | `Exploiter` → `Local Explorer` | 343 | 3.9% | 7.1% | 11.7% | 11.6% | 0.24 |
| 7 | `Exploiter` → `Polisher` | 341 | 3.9% | 3.5% | 1.5% | 11.5% | 0.56 |
| 8 | `Polisher` → `Exploiter` | 273 | 3.1% | 2.7% | 1.3% | 16.4% | 0.52 |
| 9 | `Global Explorer` → `Local Explorer` | 55 | 0.6% | 1.0% | 1.2% | 73.3% | 0.01 |
| 10 | `Local Explorer` → `Global Explorer` | 39 | 0.4% | 0.9% | 1.7% | 9.2% | 0.10 |

### Top 10 transitions by conditional probability

| Rank | Transition | Count | Pooled prevalence | Mean run prevalence | Run StdDev | Conditional P(to \| from) | Mean phase |
|---:|---|---:|---:|---:|---:|---:|---:|
| 1 | `Local Explorer` → `Exploiter` | 365 | 4.2% | 7.4% | 11.7% | 86.5% | 0.23 |
| 2 | `Polisher` → `Refiner` | 1389 | 15.8% | 14.7% | 6.6% | 83.4% | 0.73 |
| 3 | `Exploiter` → `Refiner` | 2269 | 25.9% | 23.8% | 8.0% | 76.7% | 0.41 |
| 4 | `Global Explorer` → `Local Explorer` | 55 | 0.6% | 1.0% | 1.2% | 73.3% | 0.01 |
| 5 | `Refiner` → `Exploiter` | 2307 | 26.3% | 24.1% | 8.3% | 63.1% | 0.42 |
| 6 | `Refiner` → `Polisher` | 1325 | 15.1% | 14.0% | 6.2% | 36.3% | 0.73 |
| 7 | `Global Explorer` → `Exploiter` | 16 | 0.2% | 0.3% | 0.6% | 21.3% | 0.04 |
| 8 | `Polisher` → `Exploiter` | 273 | 3.1% | 2.7% | 1.3% | 16.4% | 0.52 |
| 9 | `Exploiter` → `Local Explorer` | 343 | 3.9% | 7.1% | 11.7% | 11.6% | 0.24 |
| 10 | `Exploiter` → `Polisher` | 341 | 3.9% | 3.5% | 1.5% | 11.5% | 0.56 |

### Phase-ordered view of prevalent transitions

This table takes the same high-prevalence transitions and orders them by **mean phase**. It is a useful approximation of a typical temporal flow, but cyclic transitions mean it should not be read as a clean deterministic sequence.

| Phase order | Transition | Mean phase | Count | Pooled prevalence | Mean run prevalence | Run StdDev |
|---:|---|---:|---:|---:|---:|---:|
| 1 | `Global Explorer` → `Local Explorer` | 0.01 | 55 | 0.6% | 1.0% | 1.2% |
| 2 | `Local Explorer` → `Global Explorer` | 0.10 | 39 | 0.4% | 0.9% | 1.7% |
| 3 | `Local Explorer` → `Exploiter` | 0.23 | 365 | 4.2% | 7.4% | 11.7% |
| 4 | `Exploiter` → `Local Explorer` | 0.24 | 343 | 3.9% | 7.1% | 11.7% |
| 5 | `Exploiter` → `Refiner` | 0.41 | 2269 | 25.9% | 23.8% | 8.0% |
| 6 | `Refiner` → `Exploiter` | 0.42 | 2307 | 26.3% | 24.1% | 8.3% |
| 7 | `Polisher` → `Exploiter` | 0.52 | 273 | 3.1% | 2.7% | 1.3% |
| 8 | `Exploiter` → `Polisher` | 0.56 | 341 | 3.9% | 3.5% | 1.5% |
| 9 | `Refiner` → `Polisher` | 0.73 | 1325 | 15.1% | 14.0% | 6.2% |
| 10 | `Polisher` → `Refiner` | 0.73 | 1389 | 15.8% | 14.7% | 6.6% |

## Verified side-by-side interpretation

| Feature | Schwefel 2.22 30D | Rosenbrock 30D |
|---|---|---|
| Success rate | 30/30 = 100% | 3/30 = 10% |
| Most prevalent transition | `Local Explorer` → `Exploiter`: count 195, prevalence 24.7%, conditional 82.6% | `Refiner` → `Exploiter`: count 2307, prevalence 26.3%, conditional 63.1% |
| Global-to-local exploration | count 35, pooled 4.4%, mean-run 12.9% ± 16.8%, conditional 97.2%, mean phase 0.19 | count 55, pooled 0.6%, mean-run 1.0% ± 1.2%, conditional 73.3%, mean phase 0.01 |
| Local exploration to exploitation | count 195, pooled 24.7%, mean-run 22.7% ± 10.7%, conditional 82.6%, mean phase 0.51 | count 365, pooled 4.2%, mean-run 7.4% ± 11.7%, conditional 86.5%, mean phase 0.23 |
| Exploiter to local exploration | count 172, pooled 21.7%, mean-run 18.5% ± 9.5%, conditional 50.7%, mean phase 0.53 | count 343, pooled 3.9%, mean-run 7.1% ± 11.7%, conditional 11.6%, mean phase 0.24 |
| Exploiter to refinement | count 138, pooled 17.4%, mean-run 12.9% ± 8.9%, conditional 40.7%, mean phase 0.45 | count 2269, pooled 25.9%, mean-run 23.8% ± 8.0%, conditional 76.7%, mean phase 0.41 |
| Refiner to exploitation | count 137, pooled 17.3%, mean-run 12.7% ± 8.7%, conditional 81.5%, mean phase 0.46 | count 2307, pooled 26.3%, mean-run 24.1% ± 8.3%, conditional 63.1%, mean phase 0.42 |
| Refiner to polishing | count 1, pooled 0.1%, mean-run 0.1% ± 0.6%, conditional 0.6%, mean phase 0.29 | count 1325, pooled 15.1%, mean-run 14.0% ± 6.2%, conditional 36.3%, mean phase 0.73 |
| Polisher back to refinement | count 3, pooled 0.4%, mean-run 0.2% ± 0.7%, conditional 25.0%, mean phase 0.23 | count 1389, pooled 15.8%, mean-run 14.7% ± 6.6%, conditional 83.4%, mean phase 0.73 |
| Landscape framing | Trap-heavy / large jumps useful | Smooth curved valley / careful local following useful |

## Refined interpretation

The earlier clean phrase `Global Explorer → Local Explorer → Exploiter` is a useful shorthand for part of the Schwefel behavior, but the full transition table shows a more cyclic process. Schwefel has strong global-to-local discovery and local-explorer-to-exploiter movement, while also showing a meaningful `Exploiter → Local Explorer` return path. That supports an interpretation of repeated basin probing rather than a one-way pipeline.

Rosenbrock shows stronger exploitation/refinement coupling in overall prevalence. Its most common transitions are dominated by `Refiner → Exploiter` and `Exploiter → Refiner`. The high conditional `Polisher → Refiner` probability is real, but it should be interpreted carefully: it is strong **when polishing occurs**, not necessarily the dominant behavior overall. This correction avoids overstating a Refiner ⇄ Polisher loop as the main global pattern.

Sequencing the transitions into a single typical path is only partially valid. The phase-ordered tables approximate temporal flow using mean within-run position, but both problems show feedback loops. Therefore, the most defensible presentation is: **phase tendencies plus cyclic transition motifs**, not a single fixed role pipeline.

The best-supported conclusion is that the same Polygrithm hierarchy exhibits different stochastic transition tendencies by problem. Schwefel emphasizes discovery/probing cycles; Rosenbrock emphasizes exploitation/refinement cycling consistent with navigating a smooth curved basin.
