---
name: expert-paper-review
description: Use when reviewing an academic manuscript in power/energy systems domain, when simulating peer reviewer feedback, when performing pre-submission self-check, or when the user wants to build a structured review knowledge base from past reviews
---

# Expert Paper Review (Power & Energy Systems)

## Overview

Systematic expert-level manuscript review skill for power and energy systems papers. Supports two modes: (1) simulating a journal peer reviewer to produce formal review reports, and (2) pre-submission self-check to help authors identify and fix problems before submitting. Every review is persisted into a structured knowledge base for future retrieval by paper, issue type, or quality score.

## When to Use

- User asks to review a paper / manuscript
- User asks "help me check this paper before submission"
- User asks to simulate a reviewer's feedback
- User wants to find common issues from past reviews
- User asks "what problems did we find in previous papers about [topic]?"
- User provides a PDF/manuscript and asks for expert opinions

## When NOT to Use

- Purely formatting/proofreading tasks (use a grammar tool)
- Journal scope matching only (use journal-scope-review skill)
- Literature survey or citation analysis only

## Core Workflow

```
RECEIVE MANUSCRIPT
      |
      v
DETERMINE MODE ──────────────────────────────────────
      |                                              |
      v                                              v
  REVIEWER MODE                              SELF-CHECK MODE
  (formal review report)                     (author-friendly feedback)
      |                                              |
      v                                              v
FULL REVIEW (7 dimensions)              QUICK SCAN (flag top issues)
      |                                              |
      v                                              v
GENERATE REVIEW REPORT                  GENERATE IMPROVEMENT CHECKLIST
      |                                              |
      +──────────────── MERGE ───────────────────────+
                          |
                          v
              PERSIST TO KNOWLEDGE BASE
                          |
                          v
              UPDATE KNOWLEDGE BASE INDEX
```

## Review Dimensions (7 Dimensions)

Every review MUST systematically evaluate these 7 dimensions. Score each 1-5.

| # | Dimension | What to Check | Score Guide |
|---|-----------|---------------|-------------|
| 1 | **Novelty & Originality** | Is the contribution genuinely new? Does it advance the state of the art? | 5=breakthrough, 4=significant, 3=incremental, 2=marginal, 1=none |
| 2 | **Technical Rigor** | Are models correct? Derivations valid? Assumptions justified? | 5=flawless, 4=minor gaps, 3=some issues, 2=major flaws, 1=fundamentally wrong |
| 3 | **Methodology** | Is the approach appropriate? Are baselines adequate? Parameters justified? | 5=excellent, 4=good, 3=acceptable, 2=weak, 1=inappropriate |
| 4 | **Results & Validation** | Are results convincing? Sufficient case studies? Statistical significance? | 5=comprehensive, 4=adequate, 3=partial, 2=insufficient, 1=missing |
| 5 | **Literature Review** | Is related work comprehensive? Are key references included? Proper positioning? | 5=thorough, 4=good, 3=adequate, 2=gaps, 1=poor |
| 6 | **Writing Quality** | Is the paper well-organized? Clear figures/tables? Logical flow? | 5=excellent, 4=good, 3=acceptable, 2=poor structure, 1=incomprehensible |
| 7 | **Significance & Impact** | Is the problem important? Will the community benefit? Practical applicability? | 5=high impact, 4=useful, 3=moderate, 2=limited, 1=negligible |

### Overall Recommendation Mapping

| Average Score | Recommendation |
|---|---|
| 4.5 - 5.0 | Accept |
| 3.5 - 4.4 | Minor Revision |
| 2.5 - 3.4 | Major Revision |
| 1.5 - 2.4 | Reject (resubmit after major rework) |
| 1.0 - 1.4 | Reject |

## Step-by-Step Review Process

### Step 1: Read and Extract Metadata

Extract and record:
- Title, authors (if available), target journal
- Research topic and sub-field classification
- Paper type: theoretical / simulation / experimental / hybrid

### Step 2: Identify Actual Contributions

Read the FULL manuscript. Do NOT rely solely on the abstract.

| Section | What to extract |
|---|---|
| Abstract | Claimed contributions vs. actual scope |
| Introduction | Problem statement, motivation, research gap |
| Methodology | Core technical approach, models, algorithms |
| Case Study | Test system scale, scenarios, parameters |
| Results | Key metrics, comparison baselines, improvements |
| Conclusions | Claims vs. evidence, generalizability |

### Step 3: Evaluate Each Dimension

For each of the 7 dimensions:
1. State the score (1-5)
2. Provide specific evidence (quote or reference sections/equations/figures)
3. List specific issues found
4. Suggest concrete improvements

### Step 4: Classify Issues

Categorize every issue found:

| Category | Code | Description | Examples |
|---|---|---|---|
| Critical | C | Must fix; paper cannot be accepted with this | Wrong model, invalid proof, plagiarism |
| Major | M | Significantly weakens the paper | Missing baselines, unjustified assumptions, insufficient validation |
| Minor | m | Should fix but not blocking | Typos in equations, unclear figures, missing units |
| Suggestion | S | Optional improvement | Additional case studies, extended discussion, formatting |

### Step 5: Generate Review Report

Use the template in `review-template.md` to produce a structured report.

### Step 6: Persist to Knowledge Base (MANDATORY)

**Storage root:** `D:\code_cys\LLM_review\reviews\`

This step is NOT optional. After EVERY review, you MUST persist the results. Follow these sub-steps exactly:

#### 6a. Save review report

Write the completed review report to:
```
D:\code_cys\LLM_review\reviews\YYYY-MM-DD_short-title.md
```
- Use today's date in `YYYY-MM-DD` format
- `short-title` is a 2-4 word slug from the paper title, lowercase, hyphenated (e.g., `battery-degradation-scheduling`, `wind-forecast-lstm`)
- Use the template from `review-template.md` — fill in ALL sections, do not leave placeholders

#### 6b. Update INDEX.md

Read `D:\code_cys\LLM_review\reviews\INDEX.md` and update:

1. **Reviews by Date table** — add a new row:
   ```
   | YYYY-MM-DD | Paper Title | Topic | X.X | Recommendation | [link](./YYYY-MM-DD_short-title.md) |
   ```

2. **Reviews by Topic** — add an entry under the matching topic section:
   ```
   - [Paper Title](./YYYY-MM-DD_short-title.md) - X.X - YYYY-MM-DD
   ```

3. **Reviews by Issue Type** — for each major/critical issue found, add under the matching category:
   ```
   - [Paper Title](./YYYY-MM-DD_short-title.md): brief issue description
   ```

4. **Reviews by Recommendation** — add under the correct recommendation level

5. **Statistics** — increment total reviews, recalculate average score, update distribution counts, refresh most common issues

#### 6c. Update issue cross-reference files

For each issue found in the review, append a row to the matching file in `D:\code_cys\LLM_review\reviews\issues\`:

| File | When to update |
|------|---------------|
| `issues/novelty.md` | Any novelty-related issue (N1-N5 or custom) |
| `issues/technical-rigor.md` | Any technical rigor issue (T1-T10 or custom) |
| `issues/methodology.md` | Any methodology issue (M1-M10 or custom) |
| `issues/validation.md` | Any validation issue (V1-V10 or custom) |
| `issues/writing.md` | Any writing quality issue (W1-W8 or custom) |

Add a row to the **Occurrences** table in the relevant file:
```
| YYYY-MM-DD | [Paper Title](../YYYY-MM-DD_short-title.md) | Issue ID | C/M/m/S | Brief description |
```

If 3+ occurrences exist for a given issue type, update the **Pattern Analysis** section.

#### 6d. Confirm persistence

After all writes, read back INDEX.md to verify the entry was added correctly. Report to the user:
```
Review persisted to knowledge base:
- Report: reviews/YYYY-MM-DD_short-title.md
- Index updated: N total reviews, avg score X.X
- Issues cross-referenced: [list of updated issue files]
```

## Knowledge Base Structure

```
D:\code_cys\LLM_review\reviews\
  INDEX.md                          # Master index (already initialized)
  YYYY-MM-DD_short-title.md         # Individual review reports
  issues/
    novelty.md                      # Cross-reference: novelty issues (initialized)
    methodology.md                  # Cross-reference: methodology issues (initialized)
    validation.md                   # Cross-reference: validation issues (initialized)
    writing.md                      # Cross-reference: writing issues (initialized)
    technical-rigor.md              # Cross-reference: technical rigor issues (initialized)
```

## Knowledge Base Query Patterns

When the user wants to search the knowledge base:

| Query Type | How to Search |
|---|---|
| By paper title/keyword | Search INDEX.md "Reviews by Date" table |
| By topic | Search INDEX.md "Reviews by Topic" section |
| By issue type | Search `reviews/issues/*.md` cross-reference files |
| By score range | Filter INDEX.md table by "Overall Score" column |
| By recommendation | Filter INDEX.md table by "Recommendation" column |
| Common patterns | Read `reviews/issues/*.md` for recurring themes |

## Power/Energy Domain-Specific Checks

### Common Technical Issues in Power Systems Papers

| Issue | What to Check |
|---|---|
| Model validity | Is the power system model appropriate for the study scale? (node vs. bus vs. full AC) |
| Solver appropriateness | Is the optimization solver suitable? (LP vs. MILP vs. heuristic vs. metaheuristic) |
| Test system scale | Is the test system realistic enough? (3-bus toy vs. IEEE 118 vs. real grid) |
| Temporal resolution | Does the time step match the phenomenon? (seconds for frequency, hours for planning) |
| Uncertainty handling | Are stochastic/robust methods used where needed? |
| Comparison fairness | Are baselines compared under identical conditions? |
| Parameter sources | Are parameters from real data, literature, or assumed? |
| Scalability | Does the method scale to realistic problem sizes? |

### Domain-Specific Red Flags

- Using metaheuristic (GA/PSO) for convex problems solvable by LP/QP
- Frequency regulation studies without dynamic simulation
- Planning studies ignoring uncertainty (deterministic only)
- Claiming "optimal" without proving convexity or global optimality
- Comparing with outdated baselines only (>5 years old)
- Test system smaller than 30 buses for system-level claims
- Energy storage sizing without degradation modeling
- Missing per-unit or base value specifications
- Ignoring network constraints in dispatch/scheduling problems
- Renewable forecasting without proper train/test split

## Reviewer Mode vs Self-Check Mode

### Reviewer Mode Output
- Formal tone, third-person perspective
- Structured review with numbered comments
- Clear recommendation with justification
- Suitable for sharing with journal editors

### Self-Check Mode Output
- Friendly, constructive tone
- Priority-ordered improvement checklist
- Actionable suggestions with specific locations in the manuscript
- Estimated effort for each fix (quick fix / moderate / significant rework)
- Suitable for the author to work through before submission

## Common Mistakes When Reviewing

| Mistake | Fix |
|---|---|
| Being too gentle — avoiding critical feedback | Always identify the actual severity; authors need honest assessment |
| Nitpicking formatting while ignoring technical flaws | Check technical rigor FIRST, formatting LAST |
| Not reading the full paper | MUST read methodology and results, not just abstract |
| Generic comments ("needs improvement") | Always cite specific sections, equations, figures |
| Missing the forest for the trees | Start with big-picture assessment before diving into details |
| Not checking references | Verify key claims are properly cited and baselines are current |
| Ignoring reproducibility | Check if method description is sufficient to replicate results |

## Persistence Checklist

After EVERY review, complete these steps:

- [ ] Review report saved to `reviews/YYYY-MM-DD_short-title.md`
- [ ] INDEX.md updated with new entry
- [ ] Issues cross-referenced in `reviews/issues/*.md`
- [ ] Statistics in INDEX.md updated
