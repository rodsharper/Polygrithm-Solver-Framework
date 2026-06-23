# Sharing Ablation: Sharing OFF vs Sharing ON

**Sharing OFF batch:** `20260617_094355`  
**Sharing ON batch:** `20260615_140911`  
**Exact problem-name matches:** 6  

This report compares only exact problem-name matches to avoid mixing dimensions or related-but-different functions. Lower final quality is better.

| Problem | OFF Success | ON Success | Delta | OFF Median | ON Median | OFF Mean | ON Mean | Interpretation |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| Ackley 30D | 0.0% | 100.0% | +100.0% | 7.41E-04 | 0.00E+000 | 7.41E-04 | 0.00E+000 | ON dominates |
| Hybrid F2 30D | 0.0% | 13.3% | +13.3% | 3.28E+00 | 4.95E-03 | 4.41E+00 | 1.79E-01 | ON better |
| Rosenbrock 30D | 0.0% | 10.0% | +10.0% | 4.76E-03 | 1.38E-03 | 4.41E-03 | 1.29E-03 | ON better |
| Schwefel 2.22 30D | 6.7% | 86.7% | +80.0% | 8.71E-03 | 0.00E+000 | 7.84E-03 | 1.43E-09 | ON dominates |
| Shifted Rastrigin 30D | 0.0% | 93.3% | +93.3% | 9.71E-04 | 0.00E+000 | 1.17E-03 | 1.16E+00 | ON dominates |
| Shifted Rosenbrock 30D | 0.0% | 13.3% | +13.3% | 4.55E-03 | 1.44E-03 | 1.36E-01 | 1.72E-03 | ON better |

## Omitted from exact-match comparison

Present in ON batch only:

- Griewank 30D
- Shifted Ackley 30D
- Shifted Griewank 30D
- Shifted Schwefel 30D

Present in OFF baseline only:

