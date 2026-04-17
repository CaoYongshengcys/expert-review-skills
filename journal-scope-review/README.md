# Journal Scope Review

> An AI agent skill that performs pre-submission scope alignment analysis for academic manuscripts, preventing desk rejections caused by journal scope mismatch.

## Why This Exists

Scope mismatch is the #1 cause of desk rejection — and it is entirely preventable.

A real example: a paper on multi-type energy storage capacity planning for AGC frequency regulation was submitted to **IEEE Transactions on Energy Conversion**. The editor's response:

> *"The contributions are primarily in using energy storage to support power system-wide dynamic performance, instead of innovations pertaining to the energy storage systems themselves. Thus, the contributions fall outside of the scope of the IEEE Transactions on Energy Conversion, which is limited to various aspects of electrical equipment used to convert energy."*

The paper itself was not bad. It was simply sent to the wrong journal. This cost the authors **3+ months** of waiting for a result that could have been predicted in 10 minutes.

This skill automates that 10-minute check.

## How It Works

The skill implements a 6-step systematic review:

```
READ MANUSCRIPT
      |
      v
EXTRACT CONTRIBUTIONS -----> What does the paper ACTUALLY do?
      |                       (not what the abstract claims)
      v
CLASSIFY CONTRIBUTION LAYER
      |
      +-- Device/Component level
      +-- System/Operation level
      +-- Planning/Optimization level
      +-- Application/Industry level
      |
      v
MAP TO JOURNAL SCOPE ------> Does the journal publish at THIS layer?
      |
      +-- MATCH ------> Quality assessment
      +-- PARTIAL ----> Reframing guidance
      +-- MISMATCH ---> Alternative recommendations
```

### Step-by-Step

| Step | What it does |
|---|---|
| 1. Extract contributions | Reads full manuscript; checks methodology, case studies, metrics, and references — not just the abstract |
| 2. Classify layer | Maps each contribution to Device / System / Planning / Application level |
| 3. Scope alignment matrix | Cross-references contributions against the target journal's scope |
| 4. Modification cost | Estimates fix effort: Reframing (1-2 wks) / Augmenting (1-2 mo) / Rebuilding (3+ mo) |
| 5. Journal recommendation | Ranked alternatives with match reasoning, required changes, and risk factors |
| 6. Technical quick-check | Flags conceptual errors, missing benchmarks, notation issues regardless of scope |

## Built-in Journal Knowledge

Scope profiles for **15+ major journals** in power systems and energy engineering:

| Publisher | Journals | Typical Layer |
|---|---|---|
| **IEEE** | Trans. Power Systems | System + Planning |
| | Trans. Energy Conversion | Device |
| | Trans. Smart Grid | System + Application |
| | Trans. Industry Applications | Application |
| | Trans. Power Delivery | Device + System |
| | Trans. Sustainable Energy | System |
| | Trans. Power Electronics | Device |
| | Trans. Industrial Electronics | Device + Application |
| **Elsevier** | IJEPES | System + Planning |
| | Journal of Energy Storage | All layers |
| | Applied Energy | System + Planning |
| | Electric Power Systems Research | System + Planning |
| **Others** | CSEE JPES (IEEE co-published) | System + Planning |
| | MPCE | System |
| | IET GTD | System |

### Common Scope Traps

The skill includes a lookup table of the most frequent mismatch patterns:

| Paper does... | Author thinks it fits... | Actually fits... |
|---|---|---|
| ES sizing + grid frequency regulation | Trans. Energy Conversion | Trans. Power Systems, IJEPES |
| Battery SOC estimation algorithm | Trans. Power Systems | Trans. Energy Conversion |
| Converter topology for ES | Trans. Power Systems | Trans. Power Electronics |
| ES in industrial microgrid | Trans. Power Systems | Trans. Industry Applications |
| Demand response optimization | Trans. Industry Applications | Trans. Power Systems |
| Renewable forecasting | Trans. Energy Conversion | Trans. Sustainable Energy |

## Installation

### Option 1: Clone directly (recommended)

```bash
git clone https://github.com/CaoYongshengcys/journal-scope-review.git ~/.agents/skills/journal-scope-review
```

### Option 2: Copy the skill file

```bash
mkdir -p ~/.agents/skills/journal-scope-review
curl -o ~/.agents/skills/journal-scope-review/SKILL.md \
  https://raw.githubusercontent.com/CaoYongshengcys/journal-scope-review/main/SKILL.md
```

The only file the agent needs is `SKILL.md`. Place it under your agent's skill directory:
- **OpenCode**: `~/.agents/skills/journal-scope-review/SKILL.md`
- **Claude Code**: `~/.claude/skills/journal-scope-review/SKILL.md`

## Usage

Once installed, the skill is loaded automatically when you:

- Ask the agent to review a paper before submission
- Ask which journal to submit a manuscript to
- Share a rejection letter and ask for diagnosis
- Ask whether a paper fits a specific journal

### Example Prompts

```
Review my main.tex and check if it's suitable for IEEE Transactions on Energy Conversion.
```

```
My paper was rejected from [journal] for scope mismatch. Analyze why and recommend alternatives.
```

```
Which journal should I target for this manuscript? I'm considering IEEE TIA or IJEPES.
```

```
I need to switch from Trans. Energy Conversion to Trans. Industry Applications. 
What modifications are needed?
```

### Example Output Structure

The skill produces a structured review:

1. **Contribution extraction** — what the paper actually does (2-3 sentences)
2. **Scope alignment matrix** — table mapping each contribution to journal scope
3. **Verdict** — Match / Partial / Mismatch with evidence
4. **Journal recommendations** — ranked table with modification estimates
5. **Technical flags** — issues that cause rejection regardless of scope
6. **Modification roadmap** — specific sections to change if reframing is needed

## Extending to Other Fields

The current journal database focuses on **power systems and energy engineering**. To extend coverage to other fields:

1. Add journal entries to the "Quick Reference" table in `SKILL.md`
2. Add field-specific scope traps to the "Common Scope Traps" table
3. The 6-step workflow and 4-layer classification framework are domain-agnostic

Contributions for other fields (e.g., control systems, communications, computer science) are welcome via pull requests.

## Project Structure

```
journal-scope-review/
  SKILL.md      # The skill itself (agent reads this)
  README.md     # This file (for humans)
  LICENSE       # MIT
```

## Contributing

Issues and pull requests are welcome. Particularly valuable contributions:

- **New journal profiles**: Add scope descriptions for journals not yet covered
- **New scope traps**: Document mismatch patterns you've encountered
- **Field extensions**: Expand coverage beyond power/energy engineering
- **Workflow improvements**: Suggest additional review steps or diagnostic criteria

## License

[MIT](LICENSE)

## Acknowledgments

Developed from a real desk-rejection case analysis. The systematic process of diagnosing scope mismatch, evaluating modification costs across multiple target journals, and providing actionable reframing guidance was generalized into this reusable agent skill.
