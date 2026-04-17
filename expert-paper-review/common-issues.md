# Common Issues Reference: Power & Energy Systems Papers

> A curated catalog of frequently encountered issues in power/energy systems manuscripts.
> Built from review experience; use as a checklist during reviews.

## 1. Novelty & Originality Issues

| ID | Issue | Frequency | Severity | How to Detect |
|----|-------|-----------|----------|---------------|
| N1 | Incremental improvement over existing method without clear advantage | Very High | Major | Compare with recent SOTA; check if improvement margin is within noise |
| N2 | "Novel combination" of two known methods without synergy analysis | High | Major | Ask: does combining A+B create insight beyond A and B separately? |
| N3 | Applying well-known ML model to power system data without domain contribution | High | Critical | Check if the "novelty" is just sklearn/PyTorch on a new dataset |
| N4 | Claiming novelty by adding unnecessary complexity | Medium | Major | Simpler baseline achieves comparable results |
| N5 | Ignoring recent publications that already solved the same problem | Medium | Critical | Check arXiv/IEEE from last 2 years on same topic |

## 2. Technical Rigor Issues

| ID | Issue | Frequency | Severity | How to Detect |
|----|-------|-----------|----------|---------------|
| T1 | Incorrect power flow equations (e.g., mixing AC/DC formulations) | Medium | Critical | Verify equations against standard textbook references |
| T2 | Ignoring reactive power in studies where it matters | High | Major | Check if Q is omitted in voltage-sensitive studies |
| T3 | Linearization without stating validity range | High | Major | Look for DC-OPF used where AC-OPF is needed |
| T4 | Confusing primary/secondary/tertiary frequency control | Medium | Critical | Check if control timescales are mixed inappropriately |
| T5 | Missing power balance constraints | Low | Critical | Verify sum of generation = sum of demand + losses |
| T6 | Battery model ignoring SOC limits, efficiency, or degradation | Very High | Major | Check if 0 <= SOC <= 1, round-trip efficiency applied |
| T7 | Claiming "optimal solution" without convexity proof | High | Major | Non-convex + heuristic solver = no optimality guarantee |
| T8 | Undefined or inconsistent notation | High | Minor | Scan nomenclature section vs. actual equation usage |
| T9 | Per-unit system errors or missing base values | Medium | Major | Check if Sbase/Vbase are specified and consistently used |
| T10 | Stochastic model with too few scenarios | Medium | Major | <100 scenarios for Monte Carlo is usually insufficient |

## 3. Methodology Issues

| ID | Issue | Frequency | Severity | How to Detect |
|----|-------|-----------|----------|---------------|
| M1 | Using metaheuristic (GA/PSO/GWO) for convex problems | High | Major | If LP/QP formulation exists, metaheuristic is unjustified |
| M2 | No comparison with mathematical programming baselines | Very High | Major | At minimum compare with CPLEX/Gurobi for optimization papers |
| M3 | Hyperparameter tuning not described for ML methods | High | Major | Check if learning rate, epochs, architecture are justified |
| M4 | Train/test data leakage in forecasting studies | Medium | Critical | Check if future data leaks into training features |
| M5 | Unjustified VMD/EMD decomposition mode number | High | Major | Mode number should be selected by analysis, not assumed |
| M6 | Multi-objective optimization without Pareto front analysis | Medium | Major | Weighted sum with fixed weights != multi-objective |
| M7 | Rolling horizon/MPC without proper receding implementation | Medium | Major | Check if re-optimization actually uses updated info |
| M8 | Deep learning with insufficient training data explanation | High | Major | Dataset size, augmentation, and split ratios must be stated |
| M9 | Deterministic planning ignoring all uncertainty | Medium | Major | Real-world planning must account for load/RES uncertainty |
| M10 | Comparing algorithms under different computational budgets | Medium | Major | PSO with 10000 iterations vs. GA with 100 is unfair |

## 4. Results & Validation Issues

| ID | Issue | Frequency | Severity | How to Detect |
|----|-------|-----------|----------|---------------|
| V1 | Test system too small for claimed system-level contribution | Very High | Major | < 30 buses for system-level claims is weak |
| V2 | No statistical significance analysis | High | Major | Single run of stochastic algorithm proves nothing |
| V3 | Cherry-picked scenarios showing only favorable results | Medium | Major | Check if worst-case or average-case is shown |
| V4 | Missing computational time comparison | High | Minor | Especially important for optimization/ML methods |
| V5 | Percentage improvement without absolute values | Medium | Minor | 50% better than a terrible baseline is meaningless |
| V6 | No sensitivity analysis on key parameters | High | Major | How robust is the result to parameter changes? |
| V7 | Comparing with outdated methods only (>5 years) | High | Major | Must include recent SOTA as baseline |
| V8 | Simulation-only for hardware-applicable claims | Medium | Major | Claims about real-time control need at least HIL validation |
| V9 | Inconsistent results between text and tables/figures | Low | Critical | Cross-check all numerical claims |
| V10 | Missing error metrics diversity (only RMSE, no MAE/MAPE) | High | Minor | Multiple metrics give fuller picture |

## 5. Literature Review Issues

| ID | Issue | Frequency | Severity | How to Detect |
|----|-------|-----------|----------|---------------|
| L1 | Missing key recent references (last 2 years) | Very High | Major | Search IEEE/Elsevier for recent papers on same topic |
| L2 | Review reads as a list without synthesis | High | Minor | Should identify gaps, not just summarize |
| L3 | Self-citation bias (>30% self-references) | Medium | Minor | Count self-citations vs. total references |
| L4 | No comparison table with existing methods | High | Major | Table showing what each prior work covers vs. this paper |
| L5 | Citing review papers instead of original sources | Medium | Minor | Go to primary sources for specific claims |

## 6. Writing Quality Issues

| ID | Issue | Frequency | Severity | How to Detect |
|----|-------|-----------|----------|---------------|
| W1 | Abstract too long or not self-contained | High | Minor | Should be <250 words with problem/method/result/conclusion |
| W2 | Conclusion merely restates abstract | Very High | Minor | Should add insights, limitations, future work |
| W3 | Figures too small or low-resolution | High | Minor | Must be readable when printed |
| W4 | Variables not defined before first use | High | Minor | Check nomenclature completeness |
| W5 | Inconsistent terminology | Medium | Minor | Same concept called different names in different sections |
| W6 | Missing figure/table captions or cross-references | Medium | Minor | Every figure must be referenced in text |
| W7 | Paper structure not following target journal convention | Medium | Minor | Check journal author guidelines |
| W8 | Overly long paper without proportional content | Medium | Minor | Check if content justifies page count |

## Issue Cross-Reference Template

When persisting issues to the knowledge base, use this format in `reviews/issues/*.md`:

```markdown
## [Issue ID]: [Issue Title]

### Occurrences
| Date | Paper | Severity | Notes |
|------|-------|----------|-------|
| YYYY-MM-DD | [Paper title](../YYYY-MM-DD_short-title.md) | C/M/m/S | [Brief context] |

### Pattern Analysis
[After 3+ occurrences, analyze: Why does this keep happening? Common root cause?]

### Best Practice
[What should authors do instead?]
```
