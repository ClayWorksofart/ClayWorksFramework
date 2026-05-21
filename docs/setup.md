# Cortex GTM Engineering Setup — What It Is, How To Use It, Where It Can Go

> One-page guide to the two-agent Cortex GTM apparatus installed in this repo. Read top-to-bottom the first time. Bookmark for daily reference.

---

## TL;DR

- This repo now runs the **Jordan Crawford GTM Engineering Framework** (Cannonball GTM / Blueprint, 2026) calibrated to **Cortex's Engineering Operations Platform** positioning.
- Two Claude Code subagents — `cortex-strategy-build` and `cortex-guardrail` — split the work the way the framework does: one drives decisions and builds, one stops the drive when discipline is broken.
- Six slash commands wrap the most-used workflows (`/segment`, `/messaging`, `/mbr`, `/phase0`, `/preflight`, `/audit`).
- Works inside the Claude Code IDE extension (Cursor / VS Code). Auto-loads when you open this repo.
- Cost-gate discipline is wired in three places per framework §3.10 — `~/CLAUDE.md` (you), repo `CLAUDE.md` (this repo), and every `scrape_*.py` header.

---

## Why this exists

Old GTM is a relay: product marketing → demand gen → SDR → AE, each owning 11% of the journey, nobody owning the outcome. That structure exists because the work used to require specialists. It doesn't anymore.

The same operator, with Claude Code and public data, can do **strategy through execution in the same Tuesday afternoon**. But only if the working surface enforces the discipline that prevents the failure modes the framework was written to prevent:

- **Apollo-filter-dressed-as-segment** ("VPE at 200+ engineers" is a list, not a pain segment).
- **Plausible-is-not-correct** errors (the 42.6% wrong-FK case — 37,000 calls attributed to wrong accounts because every dossier looked reasonable).
- **Cents-as-dollars cost bugs** (the $256,409 Anthropic bill that was actually $2,564).
- **Identity-link collisions** (a wealth management firm joined to a thermal engineering firm because customer IDs matched).
- **Vowel-name hypothesis traps** (great training lift, ~1.0 hold-out lift, all coincidence).

The two agents make those failure modes *expensive to commit*. The discipline rules are inline in the agent prompts, in `CLAUDE.md`, in slash commands, and in script headers. There are three copies of every rule because one copy is one revert away from gone.

---

## What got built

### The two subagents (`.claude/agents/`)

| Agent | Model | Role | What triggers it |
| --- | --- | --- | --- |
| `cortex-strategy-build` | sonnet | **Driver.** Picks segments, builds pipelines, drafts messaging, reads MBR, decides pivots. | "segment", "list build", "scrape", "messaging", "PQS", "PVP", "MBR", "pivot", "outbound" |
| `cortex-guardrail` | opus | **Gate.** Phase 0 archaeology, identity-link audits, hold-out checks, forbidden-column blocks, cost gates, critique trio, plausibility review. | "ship", "final", "ready", "run", "join", "merge", "cluster", "score", "estimate cost", "paid API", "audit" |

The two agents know about each other and **hand off explicitly** when discipline kicks in. Strategy/build won't run a paid script — it stops and calls guardrail for the cost gate. Guardrail won't return control until its audit writes either `audit_passed_*.md` or `audit_failed_*.md`.

### Slash commands (`.claude/commands/`)

These appear in the Claude Code panel when you type `/`:

| Command | What it does |
| --- | --- |
| `/segment <hypothesis>` | Walks Concentric Circle Test on a hypothesis segment — bullseye → outer rings, counts at each, pillar-tagged signal stack. |
| `/messaging <segment> \| <pillar>` | Three Subject 2–5-word + Situation → Insight → Inquisition variants, anchored to a Cortex value pillar. |
| `/mbr <campaign>` | MBR read + pivot decision against Cortex-tuned thresholds. |
| `/phase0 <data.csv>` | Data archaeology, writes `data_confidence.md`, quarantines bad records. |
| `/preflight <script> against <N>` | Cost-gate audit before a paid run — estimates, applies the gate, verifies caching. |
| `/audit <artifact>` | Full ship-readiness audit — critique trio + hold-out delta + forbidden-columns grep + plausibility check. |

### Supporting docs (`docs/`)

| File | Purpose |
| --- | --- |
| `framework.md` | Crawford framework verbatim — single source of truth referenced by rule number throughout the agents. |
| `cortex-message-house.md` | Cortex positioning, pillars, ICP — pulled from Cristina's Notion export. |
| `setup.md` | This file. |

### Repo-root files

| File | Purpose |
| --- | --- |
| `CLAUDE.md` | Auto-loaded into every session. Cortex stance, agent routing table, cost ceilings, discipline checklists. Second of three places the cost-gate rule lives. |
| `.claude/settings.json` | Permission allowlist (no prompt on safe reads); `ask` list for destructive bash; prompt caching on by default. |
| `.gitignore` | Adds `.claude/settings.local.json` (personal overrides), audit artifacts, `data_confidence.md`, `quarantined.csv`, `cost_log.md` — per-build outputs that shouldn't pollute source control. |
| `scrape_*.py` headers | Cost-gate docstring on each. Third of three places the rule lives. |

---

## The framework, distilled

Three parts. Order matters: mindset shapes decisions, decisions shape builds.

### Mindset (the lens before any keystroke)

| Rule | One-line statement |
| --- | --- |
| §1.1 | You are not in the assembly line. One operator does strategy through execution. |
| §1.2 | Skip Stage 2 of GTM maturity. Don't build a Zapier stack. Build the apparatus. |
| §1.3 | You are not the main character. Target conditions, not people. |
| §1.4 | **Plausible is the enemy of correct.** Distrust your own data first. |
| §1.5 | Claude can't tell you what Claude costs. Compute it yourself against published rates. |
| §1.6 | What ships is the apparatus, not the campaign. |

### Decisions (answer in order — don't skip)

| # | Decision | What it forces |
| --- | --- | --- |
| 2.1 | **Concentric Circle Test** | Is the segment dead-center on Cortex's three pillars? Bullseye 100–2,000 cos. |
| 2.2 | **Pain-qualified vs. firmographic** | Is "VPE at 200+ engineers" pain or an Apollo filter? Force an observable event. |
| 2.3 | **Moments not profiles** | 5% in-cycle, 15% in pain, 80% nothing. Cortex's zone is the 15%. |
| 2.4 | **MBR-driven pivots** | One metric: `meetings / (emails + dials)`. 87% of replies in 24h. Pivot the segment in week one, not the copy in week four. |
| 2.5 | **Ladder of escalation on cost** | Free public → cheap paid → expensive APIs → premium LLM last. |

### Builds (assumes decisions are right)

| Rule | Discipline |
| --- | --- |
| §3.1 | Tools (do) / Skills (think) / MCP (eyes). Skills are how you onboard Claude. |
| §3.2 | Define output before input. No schema → no build. |
| §3.3 | Eight tool categories: source discovery → scrape → email verify → enrichment → CRM → outreach → analytics → cost monitoring. |
| §3.4 | **Phase 0 data archaeology.** Cross-reference every CRM label against external reality. Quarantine the bad ones. |
| §3.5 | **Trust hierarchy.** Customer actions > customer voice > CRM-derived state. |
| §3.6 | **Identity linking.** Strip own domain before email join. ≥2 keys. Fuzzy ≥0.92. 100-record human spot-check. |
| §3.7 | **Hold out 20% by account.** Vowel-name failure mode — kill hypotheses that don't hold lift on hold-out. |
| §3.8 | **Forbidden columns** in pain segmentation: headcount, revenue/ARR, industry, close_date, deal-derived. |
| §3.9 | Messaging: Subject 2–5 words; Situation → Insight → Inquisition. PQS (the fact does the work) + PVP (deliver value before the ask). |
| §3.10 | **Cost gate.** `<$100` log; `$100–1K` prompt y; `$1K–10K` `--i-spent <dollars>`; `$10K+` `--i-mean-it`. Rule in three places. |
| §3.11 | **Critique trio.** Statistician + RevOps + Outlier hunter on every shippable artifact. |
| §3.12 | Fix the bug, don't unfix the discipline. |

---

## Cortex calibration

The Crawford framework is generic. The agents are not — they're pre-anchored to Cortex specifically.

### Cortex stance (loaded into every session via `CLAUDE.md`)

- **Tagline:** *"Code is no longer the bottleneck. Everything else is."*
- **Positioning:** Engineering Operations Platform that helps engineering organizations continuously improve operational maturity and reduce developer friction.
- **Deal drivers:** Engineering leaders (VPE, CTO, SVP Eng).
- **Primary beneficiaries:** Platform engineering, SREs, engineers.
- **Secondary beneficiaries:** Security, TPMs.
- **Three value pillars:** (1) Centralize your data, (2) Unlock insights, (3) Continuously improve.
- **Proof:** ~30% incident reduction, ~50% MTTR improvement; startups → Fortune 100.

### Cortex bullseye (pre-anchored Concentric Circles)

- **Bullseye (~150–400 cos):** Post-incident orgs that hired a Head of Platform / Staff Platform Eng / VP Platform Engineering in the last 6 months; 100–2,000 engineers; multi-service architecture; public evidence of operational maturity gap.
- **Ring 2 (~500–1,500 cos):** Orgs with a stalled Backstage POC or a competitor eval signal (OpsLevel / Port / Roadie mentioned in RFP, RFC, or eng blog).
- **Ring 3 (~1,500–4,000 cos):** Orgs publicly hiring SREs / DevEx / Platform Engineers with "service catalog", "golden paths", "SLO management", or "developer portal" in the JD.
- **Outer:** Firmographic-only ("200+ engineers"). Flagged as Apollo filter, not segment.

### Cortex pain-qualified signal stack

| Signal | Source | Pillar | Freshness | Confidence |
| --- | --- | --- | --- | --- |
| New Head of Platform / VP Platform hire | LinkedIn, careers, press | All 3 | <6mo | High |
| Public post-mortem citing ownership / MTTR | Eng blog, status page archive | 1+3 | <12mo | High |
| Backstage repo went quiet 6mo+ | GitHub | 1 | live | Med-High |
| OpsLevel / Port / Roadie review or RFP | G2, Reddit, public RFPs | All 3 | <12mo | Med |
| "Service catalog" / "golden paths" / "SLO" in JD | LinkedIn Jobs, careers | 1+3 | <90d | High |
| SOC2 / FedRAMP / ISO27001 hiring push | Job boards, trust center | 1 | <6mo | Med |
| Conference talk on DevEx / platform team | YouTube, KubeCon archive | 2 | <12mo | Med |
| Public DORA metric / RFC doc | Eng blog, GitHub | 2 | <12mo | Med |
| Acquisition / merger (tool-sprawl trigger) | Press, SEC | 1 | <12mo | High |

### Cortex MBR benchmarks (provisional — refine with RevOps Day 5)

- PQS / warm list: **≥0.8% MBR**.
- Cold list with strong signal: **≥0.3% MBR**.
- **Pivot trigger:** below **0.2% MBR** by end of week 1 across ≥1,000 activities → pivot the segment, not the copy.

### Cortex messaging examples (pillar-anchored)

**Pillar 1 — Centralize**
- Subject: *Ownership after merge*
- Body: *"You're probably reconciling service ownership across Snyk, PagerDuty, and three Confluence pages right now. Most platform teams stall because automated mapping breaks the moment a repo gets renamed. Am I close, or is it different on your side?"*

**Pillar 2 — Unlock insights**
- Subject: *MTTR drift this quarter*
- Body: *"You're probably watching MTTR creep up post-merger and can't tell which team is dragging the median. Most leaders get stuck because the dashboard shows the *what* but not the *why*. Did I get this right?"*

**Pillar 3 — Continuously improve**
- Subject: *Scorecard month three*
- Body: *"You're probably running a scorecard initiative in Notion and chasing teams by Slack DM. Most orgs lose momentum at month three because enforcement isn't in the workflow. Am I close?"*

---

## How to use it day-to-day

### The default loop

```
Hypothesis → /segment → /messaging → /preflight → run → /mbr (day 2) → /audit → ship
                                          ↓                              ↑
                                       guardrail blocks ←→ strategy fixes
```

### Six concrete sessions

**1. Pick a segment (10 minutes)**

In the Claude Code panel: `/segment post-incident orgs that hired a Head of Platform in the last 6 months`

The strategy agent walks Concentric Circles, demands a count at each ring, produces a pillar-tagged signal stack, and flags if it's really an Apollo filter in disguise. Output goes in your next message — nothing is written to disk until you say so.

**2. Build a target list (30 minutes – 2 hours)**

In chat: *"Build a target list for the bullseye segment using public GitHub + LinkedIn signals. Start with the source-stack ladder."*

Strategy agent walks the cost ladder (free public → cheap paid → expensive APIs → premium LLM), writes the output schema first (per §3.2), then scaffolds a new `scrape_postincident.py` from the existing `scrape_companies.py` template. Before any execution that estimates >$100, **it auto-hands off** to guardrail.

**3. Pre-flight a paid run (2 minutes)**

`/preflight scrape_postincident.py against 1,800 domains`

Guardrail computes cost (token count × Anthropic rate × call count + Firecrawl page cost), asserts the unit (dollars not cents), applies the gate, verifies prompt caching is on, verifies the rule is in three places. Only on green does control return.

**4. Draft messaging (10 minutes)**

`/messaging Backstage-stall segment | pillar 1`

Three Subject + body variants pillar-anchored to "Centralize your data." Self-critique runs before output — any variant that talks about Cortex instead of the prospect gets killed.

**5. Day-2 MBR read (5 minutes)**

`/mbr segment_v3 campaign`

MBR computed, threshold applied, decision returned. If you're under 0.2% across ≥1,000 activities by end of week 1, the agent says **pivot the segment, not the copy** — and tells you which persona swap to try first if 3 of 4 personas have flatlined.

**6. Ship-readiness audit (15 minutes)**

`/audit segment_v3_final.csv`

Guardrail runs: Phase 0 archaeology → trust hierarchy check → identity-link audit → hold-out delta → forbidden-columns grep → critique trio (Statistician + RevOps + Outlier hunter) → plausibility (sample 20 rows, verify each signal at source). Writes `audit_passed_*.md` or `audit_failed_*.md` with required fixes.

### Hand-off in the wild — what it looks like

You: *"Run scrape_companies.py against the 5,000 domains in segment_v3.csv."*

`cortex-strategy-build`: *"Estimating cost... 5,000 domains × ~2,500 input + ~1,000 output tokens × Anthropic Sonnet rate ≈ $42 if cached, ≈ $420 uncached. **Delegating to cortex-guardrail for cost-gate audit. Resuming on green light.**"*

`cortex-guardrail`: *"Cost estimate $42 cached / $420 uncached (unit: USD, not cents — verified). Caching: `scrape_companies.py` line 87 uses cache_control: ✓. Rule placement: `~/CLAUDE.md` ✓, `./CLAUDE.md` ✓, script header docstring ✓. Gate: estimate is in `$100–1K` band — **prompt: confirm with `y` to proceed.**"*

You: *"y"*

`cortex-guardrail`: *"Approved. Logging to `cost_log.md`. Returning to strategy-build for execution."*

That's the apparatus. It's slow on purpose. The bill that didn't happen today is the same bill that ends careers when the workload is 100× larger.

---

## What's possible next

What's installed today is the floor. The framework's eight tool categories — and the apparatus that connects them — go a lot deeper.

### Immediate next builds (this quarter)

| Capability | What it unlocks |
| --- | --- |
| **MCP for Salesforce / HubSpot** | Agents read pipeline state directly. `/mbr` pulls live activity counts instead of you pasting them. Hand-off includes "this account has an open opp — pause outbound" checks. |
| **MCP for Gong / Chorus** | Trust-hierarchy Tier-2 (customer voice) comes from call transcripts automatically. Agents draft case studies from won-deal transcripts via PVP pattern. |
| **MCP for LinkedIn (Sales Nav)** | Persona discovery in week 1 swaps from manual to scripted. 3–4 personas × 500–1,000 activities each, automated. |
| **Email verification step** | Closes the "missing tool category 3" gap before the first send hits sender reputation. |
| **Outreach / SalesLoft / Apollo orchestration** | Tool category 6. Closes the loop so `/mbr` reads actual sequenced data. |
| **Cost monitoring service** | Tool category 8 promoted from policy-in-docs to code-that-runs. Post-hoc reconciliation against published Anthropic rates every Friday. |
| **Subscribe / babysit loops** | `/loop 1h /mbr segment_v3` — auto-reads MBR every hour during business hours, pings you if it crosses pivot threshold. |

### Mid-term extensions (next 2 quarters)

- **Per-segment skill files** — `.claude/skills/post-incident-segment.md`, `.claude/skills/backstage-stall.md`, each encoding the playbook for one Cortex sub-segment. Skills are how you onboard Claude (§3.1); right now we have one playbook. We should have a dozen.
- **PVP generator agent** — third agent that produces the one-page "Cortex Operational Maturity Read" from public GitHub + post-mortems + status pages, on demand per prospect.
- **Case-study factory** — automated case study draft from Salesforce won-deal record + Gong transcripts + customer review URLs.
- **Competitive intelligence subagent** — tracks OpsLevel / Port / Roadie product releases, RFP wins, and customer attrition signals.
- **Eng-leader newsletter scraping** — KubeCon talks, Platform Engineering Conference, monthly post-mortem aggregators feed the signal stack daily.

### Long-term — the apparatus pattern

The two-agent split (driver + gate) is a **pattern**, not a one-off. The same pattern works for:

- **Product marketing** — `pmm-build` drafts, `pmm-guardrail` enforces brand voice + claims that pass legal.
- **Customer marketing** — `cm-build` produces case studies, `cm-guardrail` enforces the trust-hierarchy + permission-to-publish + numbers-verified rules.
- **Renewals / CS** — `renewal-build` drafts QBR decks from product-usage data, `renewal-guardrail` enforces the actions > voice > stage hierarchy on health scoring.

Each domain copies the pattern and re-anchors. The framework rules are universal; the calibration is per-domain.

### What this is *not* trying to do

- **Not replacing the AE / SDR org.** The apparatus changes what they spend their day on (high-judgment work, not list-pulling).
- **Not a Clay / n8n replacement.** This is Stage 3 (compounding judgment), not Stage 2 (deterministic workflows). Different category.
- **Not a forever-fork.** When Crawford updates the framework, you update `docs/framework.md` and the agents inherit it.

---

## File map

```
/
├── CLAUDE.md                              # Auto-loaded discipline doc, agent routing, checklists
├── .claude/
│   ├── settings.json                      # Permission allowlist, prompt caching default
│   ├── agents/
│   │   ├── cortex-strategy-build.md       # Driver agent (sonnet)
│   │   └── cortex-guardrail.md            # Gate agent (opus)
│   └── commands/
│       ├── segment.md                     # /segment
│       ├── messaging.md                   # /messaging
│       ├── mbr.md                         # /mbr
│       ├── phase0.md                      # /phase0
│       ├── preflight.md                   # /preflight
│       └── audit.md                       # /audit
├── docs/
│   ├── framework.md                       # Crawford framework verbatim
│   ├── cortex-message-house.md            # Cortex positioning + pillars
│   └── setup.md                           # This file
├── scrape_companies.py                    # Cost-gate header docstring (third place)
├── scrape_batch3.py                       # Cost-gate header docstring
├── scrape_batch4.py                       # Cost-gate header docstring
├── scrape_with_webfetch.py                # Cost-gate header docstring
└── blueprint-framework-template.md        # Pre-existing PQS/PVP methodology
```

Plus one file on your Mac (not in this repo):

```
~/CLAUDE.md                                # Third place: global discipline doc
```

---

## Glossary

| Term | Meaning |
| --- | --- |
| **PQS** | Pain-Qualified Segment. List defined by an observable operational event, not firmographics. "The list is the message." |
| **PVP** | Permissionless Value Proposition. Deliver value (a custom dossier, a maturity read) inside the email, before any ask. |
| **MBR** | Meeting Booked Rate. `meetings booked / (emails + dials)`. The only metric that matters in week 1. |
| **Concentric Circle Test** | Three rings (bullseye → outer) at every layer (segment → company → person). Bullseye is 100–2,000 cos. |
| **Phase 0** | Data archaeology. Cross-reference every CRM label against external reality before any pipeline runs. |
| **Trust hierarchy** | Customer actions > customer voice > CRM-derived state. CRM is third, not first. |
| **Hold-out 20%** | Carve 20% of source data by account, never let hypothesis generation see it, re-test on hold-out before shipping. |
| **Forbidden columns** | Headcount, revenue / ARR, industry, close_date, deal-derived. Blocked in pain segmentation. |
| **Critique trio** | Statistician + RevOps + Outlier hunter. Three reviewers on every shippable artifact. |
| **Cost gate** | `<$100` log; `$100–1K` prompt; `$1K–10K` flag; `$10K+` two flags. In three places. |
| **Ladder of escalation** | Free public → cheap paid → expensive APIs → premium LLM, last to first. |
| **Subject 2–5 words** | Email subject rule: 2–5 words, curiosity-earning, not pitching. |
| **Situation → Insight → Inquisition** | Three-line body format. Their reality, your unique take, ask for truth not time. |
| **Plausible is not correct** | Wrong gets caught. Plausible gets acted on. Distrust your own data first. |
| **Cents-as-dollars** | The $256,409 vs $2,564 lesson. Anthropic API returns cost in cents labeled USD. Always assert unit. |
| **Vowel-name failure** | Hypothesis with great training lift and ~1.0 hold-out lift. Coincidence. Kill it. |
| **Apparatus** | What ships. Not the campaign — the system that runs the campaign and gets better next week. |

---

*Built on the Jordan Crawford GTM Engineering Framework (Cannonball GTM / Blueprint, 2026). Calibrated to Cortex's Message House (March 2026).*
