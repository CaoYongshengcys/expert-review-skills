---
name: journal-scope-review
description: Use when reviewing a manuscript before journal submission, when a paper has been rejected for scope mismatch, or when the user asks which journal to target. Performs systematic scope-contribution alignment analysis, identifies mismatch risks, and recommends suitable journals with concrete modification guidance.
---

# Journal Scope Pre-Submission Review

## Overview

Systematic method to evaluate whether a manuscript's contributions align with a target journal's scope BEFORE submission, preventing desk rejections due to scope mismatch — the single most common and most preventable reason for rejection.

## When to Use

- User asks to review a paper before submission to a specific journal
- User asks which journal to submit to
- A paper was rejected and user wants to understand why or find alternatives
- User asks "is this paper suitable for journal X?"
- User wants to switch target journal and needs modification guidance

## When NOT to Use

- Reviewing paper quality (novelty, rigor, writing) without journal targeting
- Proofreading or formatting checks only

## Core Workflow

```
READ MANUSCRIPT
      |
      v
EXTRACT CONTRIBUTIONS --> What does this paper ACTUALLY do?
      |                    (ignore what authors CLAIM -- look at methods,
      |                     models, case studies, results)
      v
CLASSIFY CONTRIBUTION LAYER
      |
      +-- Device/Component level (materials, topology, control of a single device)
      +-- System/Operation level (dispatch, scheduling, coordination, market)
      +-- Planning/Optimization level (sizing, siting, investment)
      +-- Application/Industry level (specific use case, industrial scenario)
      |
      v
MAP TO JOURNAL SCOPE --> Does the journal publish at THIS layer?
      |
      +-- MATCH --> Proceed to quality assessment
      +-- PARTIAL --> Identify what to add/reframe
      +-- MISMATCH --> Recommend alternatives + modification cost
```

## Step 1: Extract Actual Contributions

Read the full manuscript. Do NOT rely solely on the abstract or stated contributions — authors frequently mislabel their own work's scope.

Check these sections to determine what the paper ACTUALLY contributes:

| Section | What to look for |
|---|---|
| Abstract | Claimed scope vs actual scope |
| Contributions list | Are these device-level, system-level, or planning-level? |
| Methodology | What tools/methods are used? (Optimizer = planning; Simulink device model = device; OPF = system) |
| Case study | What test system? (IEEE bus = system; lab prototype = device; factory = application) |
| Results | What metrics? (Cost/revenue = planning; efficiency/THD = device; frequency deviation = system) |
| References | Which journals dominate the bibliography? That reveals the paper's true community |

### Key Diagnostic Questions

1. Does the paper propose or improve a physical device/converter/machine? -> Device-level
2. Does the paper optimize how existing devices operate within a larger system? -> System-level
3. Does the paper decide how many/what size devices to install? -> Planning-level
4. Does the paper apply known methods to a specific industry scenario? -> Application-level

## Step 2: Build Scope Alignment Matrix

For each stated contribution, assess alignment with the target journal:

```
| Contribution | Layer | Journal Scope | Match? | Evidence |
|---|---|---|---|---|
| [contribution 1] | [layer] | [what journal covers] | Yes/No | [specific reason] |
| [contribution 2] | [layer] | [what journal covers] | Yes/No | [specific reason] |
| [contribution 3] | [layer] | [what journal covers] | Yes/No | [specific reason] |
```

A paper is scope-mismatched if ALL contributions fall outside the journal's layer.

A paper is partially matched if SOME contributions align — this is salvageable with reframing.

## Step 3: Common Scope Traps in Power/Energy Journals

These are the most frequent mismatches. Check for them explicitly:

| Paper does... | Author thinks it fits... | Actually fits... |
|---|---|---|
| ES sizing + scheduling for grid frequency regulation | Trans. Energy Conversion | Trans. Power Systems, IJEPES |
| Microgrid EMS optimization | Trans. Smart Grid | Could be, but check if it's just OPF with batteries |
| Battery SOC estimation algorithm | Trans. Power Systems | Trans. Energy Conversion, Trans. Industrial Electronics |
| Converter topology for ES | Trans. Power Systems | Trans. Power Electronics, Trans. Energy Conversion |
| ES in industrial microgrid | Trans. Power Systems | Trans. Industry Applications |
| Demand response optimization | Trans. Industry Applications | Trans. Power Systems, Trans. Smart Grid |
| Renewable forecasting | Trans. Energy Conversion | Trans. Sustainable Energy |

### Quick Reference: Major Power/Energy Journal Scopes

| Journal | Core Scope | Typical Layer | Key Signals |
|---|---|---|---|
| IEEE Trans. Power Systems | Grid operation, planning, markets, stability | System + Planning | OPF, UC, AGC, bus systems |
| IEEE Trans. Energy Conversion | Energy conversion equipment: motors, generators, converters, ES devices | Device | Machine design, converter control, device modeling |
| IEEE Trans. Smart Grid | Smart grid tech: communication, cyber-physical, DER integration | System + Application | AMI, IoT, data-driven, distribution |
| IEEE Trans. Industry Applications | Electrical equipment in industrial settings | Application | Factory, mine, data center, industrial microgrid |
| IEEE Trans. Power Delivery | Transmission and distribution equipment and systems | Device + System | Transformers, cables, insulation, protection |
| IEEE Trans. Sustainable Energy | Renewable generation and integration | System | Wind/solar forecasting, integration, variability |
| IEEE Trans. Power Electronics | Power electronic circuits and converters | Device | Topology, modulation, semiconductor |
| IEEE Trans. Industrial Electronics | Electronics/control in industrial systems | Device + Application | Drives, sensors, embedded control |
| IJEPES (Elsevier) | Broad power systems: planning, operation, control | System + Planning | Accepts engineering-application papers |
| Journal of Energy Storage (Elsevier) | All aspects of energy storage applications | All layers | Sizing, control, materials, system integration |
| Applied Energy (Elsevier) | Energy systems, efficiency, policy | System + Planning | Broad scope, accepts cross-disciplinary |
| CSEE JPES | Power and energy systems (IEEE co-published) | System + Planning | Friendly to Chinese institution authors |
| MPCE | Modern power systems, clean energy | System | Accepts ES + renewable integration |
| Electric Power Systems Research | Power system engineering | System + Planning | Lower novelty bar than TPWRS |
| IET GTD | Generation, transmission, distribution | System | Broad power engineering scope |

## Step 4: Assess Modification Cost

When scope doesn't match, estimate what it takes to fix:

### Reframing (Low cost: 1-2 weeks)
- Change narrative angle (e.g., "grid operation" -> "industrial application")
- Repackage case study scenario
- Adjust Introduction and Conclusion framing
- Add journal-relevant references
- Core model and results unchanged

### Augmenting (Medium cost: 1-2 months)
- Add new content layer (e.g., add device-level model to a system-level paper)
- Supplement with new case studies or experimental data
- Extend methodology with journal-relevant analysis

### Rebuilding (High cost: 3+ months, essentially a new paper)
- Paper's fundamental contribution is at wrong layer
- Would need entirely new models, methods, or experiments
- Better to target a different journal instead

## Step 5: Journal Recommendation

When recommending journals, provide:

1. Primary recommendation — best scope match with realistic acceptance probability
2. 2-3 alternatives — ranked by match quality
3. For each: scope match reason, estimated modification needed, risk factors

### Recommendation Template

```
| Journal | Scope Match | Modification Needed | Risk | Recommendation |
|---|---|---|---|---|
| [name] | [why it fits] | [what to change] | [what could go wrong] | Primary / Alternative |
```

### Factors Beyond Scope

After scope match is confirmed, flag these if relevant:
- Novelty bar: Is the method sufficiently novel for this journal's tier?
- Rigor bar: Does the paper meet the journal's standards for theoretical depth, case study scale, benchmarking?
- Formatting: Page limits, reference style, figure requirements
- Review timeline: How long does this journal typically take?
- Competition: How saturated is this topic in the journal?

## Step 6: Technical Quality Quick-Check

While reviewing for scope, flag obvious technical issues that would cause rejection regardless of scope:

- Conceptual errors (e.g., confusing primary and secondary frequency regulation)
- Missing benchmarks (no comparison with existing methods)
- Unjustified parameter choices (e.g., VMD mode number chosen without analysis)
- Inconsistent notation or undefined symbols
- Commented-out content that should be included or removed
- Claims not supported by results

## Common Mistakes

| Mistake | Why it happens | Fix |
|---|---|---|
| Trusting the abstract's scope claim | Authors write aspirationally | Read methodology and case study to determine actual scope |
| Recommending top journals without quality assessment | Scope match does not equal acceptance | Always assess novelty and rigor relative to journal tier |
| Suggesting only one journal | User needs options | Always provide 2-4 ranked alternatives |
| Ignoring modification cost | "Just resubmit elsewhere" | Explicitly estimate effort for each target |
| Not checking references | Bibliography reveals true community | If refs are all from TPWRS, the paper belongs in that community |
| Recommending scope change without checking feasibility | "Add device-level innovation" is easy to say | Assess whether authors can realistically do this |

## Output Format

Structure your review as:

1. Contribution extraction — what the paper actually does (2-3 sentences)
2. Scope alignment matrix — table mapping contributions to journal scope
3. Verdict — match / partial / mismatch with clear reasoning
4. Journal recommendations — ranked table with modification estimates
5. Technical flags — any issues that need fixing regardless of journal choice
6. Modification roadmap — if reframing is needed, specific sections to change
