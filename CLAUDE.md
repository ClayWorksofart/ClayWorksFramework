# ClayWorksFramework — Repo CLAUDE.md

This repo operationalizes the **Jordan Crawford GTM Engineering Framework** for **Cortex** (cortex.io, Engineering Operations Platform).

Canonical references:
- **Framework:** `docs/framework.md` (Cannonball GTM / Blueprint, 2026)
- **Cortex Message House:** `docs/cortex-message-house.md`
- **Strategy / build agent:** `.claude/agents/cortex-strategy-build.md`
- **Guardrail agent:** `.claude/agents/cortex-guardrail.md`

## Agent invocation

Sub-agents are auto-routed by keyword:

| You say / intend | Routes to | What happens |
| --- | --- | --- |
| "pick a segment", "Concentric Circle Test", "what's the bullseye" | `cortex-strategy-build` | Walks rings, demands 100–2,000 count, outputs pillar-tagged signal stack |
| "build a list", "scrape", "pipeline" | `cortex-strategy-build` | Walks ladder of escalation, writes output schema first, then scaffolds |
| "draft messaging", "PQS", "PVP" | `cortex-strategy-build` | Produces 3 Subject 2–5 word + Situation→Insight→Inquisition bodies, pillar-tagged |
| "MBR", "pivot", "day 2" | `cortex-strategy-build` | Runs MBR = meetings / (emails+dials); applies Cortex thresholds |
| "ship it", "ready", "final", "this looks right" | `cortex-guardrail` | Critique trio + hold-out delta + forbidden-columns grep + plausibility audit |
| "run scrape_*.py", "estimate cost", "paid API" | `cortex-guardrail` | Pre-flight cost gate (Framework §3.10) |
| "merge", "join", "link" | `cortex-guardrail` | Identity-linking audit (≥2 keys, fuzzy ≥0.92, 100-record human spot-check) |
| "cluster", "score", "find pain segment" | `cortex-guardrail` | Forbidden-columns block + 20% hold-out enforcement |

## Repo cost ceilings (the second of the "three places")

This is the repo-level copy of the cost-gate rule (Framework §3.10). The other two places: `~/CLAUDE.md` (your home), and the header docstring of each `scrape_*.py`.

| Estimated spend | Required action |
| --- | --- |
| `< $100` | Log estimate to `cost_log.md`, proceed |
| `$100 – $1,000` | Prompt user for `y` confirmation |
| `$1,000 – $10,000` | Require `--i-spent <dollars>` CLI flag on the command |
| `$10,000+` | Require second `--i-mean-it` flag + rationale in commit message |

**Always:**
- Compute cost yourself against published Anthropic rates (Framework §1.5 — Claude can't tell you what Claude costs).
- Cache system prompts (~10% on repeats; uncached swarms pay 10× over).
- Assert the unit (cents vs. dollars) on every cost report. The $256,409 → $2,564 cents-as-dollars bug is the canonical lesson.

## Cortex stance (loaded into every session)

- **Tagline:** *"Code is no longer the bottleneck. Everything else is."*
- **Positioning:** Engineering Operations Platform — continuously improve operational maturity, reduce developer friction.
- **Deal drivers:** Engineering leaders (VPE, CTO, SVP Eng).
- **Primary beneficiaries:** Platform engineering, SREs, engineers.
- **Secondary beneficiaries:** Security, TPMs.
- **Three pillars:** (1) Centralize your data, (2) Unlock insights, (3) Continuously improve.
- **Proof:** ~30% incident reduction, ~50% MTTR improvement; startups → Fortune 100.

Full text: `docs/cortex-message-house.md`.

## Discipline checklists (Framework Quick Reference)

**Before you build anything**
- Is my segment dead-center on Cortex's three pillars? (Concentric Circle Test)
- Is this a pain-qualified segment or an Apollo filter?
- Am I targeting a moment or a profile?
- What's my MBR target and pivot threshold?
- What's the cheapest workable method at each layer?

**Before you ship anything**
- Did Phase 0 quarantine the bad records?
- Did I hold out 20% by account?
- Did I strip headcount / revenue / industry / close-date columns?
- Did the critique trio agree?
- Is the pre-flight cost gate in place?

**Before you spend a dollar on Claude**
- Did I compute the cost myself against published rates?
- Is the system prompt cached?
- Is the cost rule in `~/CLAUDE.md`, this `CLAUDE.md`, and the script header docstring?
- Did I assert the unit (cents vs. dollars)?

**When the campaign is two days old**
- What's the MBR?
- If it's not on track, the segment is probably wrong. Pivot in week one, not week four.

## Forbidden columns in pain-segmentation (Framework §3.8)

Block before any clustering / segmentation: `headcount`, `employees`, `revenue`, `ARR`, `MRR`, `industry`, `vertical`, `close_date`, `stage`, `amount`, `owner`, `funding_round`, `total_funding` (unless paired with an operational signal).

## Forbidden actions

- Single-key joins (always ≥2 keys, fuzzy ≥0.92).
- Email joins without stripping `cortex.io` and the customer's own domain first.
- Running any paid-API script without the cost-gate flag for `$1K+` estimates.
- Trusting LLM self-reported cost math.
- Skipping the 20% hold-out on hypothesis-generating pipelines.
- Relaxing a discipline threshold to make a build pass (Framework §3.12 — fix the bug, don't unfix the discipline).
