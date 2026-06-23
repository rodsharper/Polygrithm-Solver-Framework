# Latest Ablation: Sharing OFF vs Latest Sharing ON

**Sharing OFF baseline:** `20260615_000438`  
**Sharing ON latest:** `20260617_060157`  

This report compares only exact problem-name matches to avoid mixing dimensions or related-but-different functions.

| Problem | OFF Success | ON Success | Delta | OFF Median | ON Median | Interpretation |
|---|---:|---:|---:|---:|---:|---|
| Ackley 30D | 0.0% | 100.0% | +100.0% | 7.18E-04 | 0.00E+00 | ON dominates |
| Hybrid F2 30D | 0.0% | 23.3% | +23.3% | 1.89E+00 | 4.51E-03 | ON better |
| Shifted Rosenbrock 30D | 0.0% | 6.7% | +6.7% | 2.40E-03 | 1.27E-03 | ON better |

## Omitted from exact-match comparison

Present in ON batch only:

- Rosenbrock 30D
- Schwefel 2.22 30D
- Shifted Rastrigin 10D

Present in OFF baseline only:

- Composition F2 30D
- Schwefel 2.22+R 50D
- Shifted Rastrigin 30D
