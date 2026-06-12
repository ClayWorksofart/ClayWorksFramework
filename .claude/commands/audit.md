---
description: Run cortex-guardrail discipline audit on an artifact before shipping
argument-hint: <path/to/artifact.csv|json|md>
---

Invoke the `cortex-guardrail` subagent. The artifact to audit is:

**$ARGUMENTS**

Run the full ship-readiness audit:

1. **Phase 0 data archaeology (§3.4)** — produce / update `data_confidence.md` covering every column the artifact uses.
2. **Trust hierarchy check (§3.5)** — identify which tier each column comes from; reject Tier-3-as-primary.
3. **Identity-linking audit (§3.6)** — if joins were performed, verify ≥2 keys, fuzzy ≥0.92, and 100-record human spot-check.
4. **Hold-out 20% by account (§3.7)** — verify a hold-out was carved; produce hold-out delta report per hypothesis.
5. **Forbidden columns grep (§3.8)** — grep the artifact for headcount/revenue/ARR/industry/close_date/deal-derived; fail loudly on any hit.
6. **Critique trio (§3.11)** — Statistician, RevOps, Outlier hunter verdicts written into the audit doc. Top-10 outliers shown by hand.
7. **Plausibility check (§1.4)** — sample 20 rows; verify each claimed signal at source.

Write `audit_passed_<artifact>_<YYYY-MM-DD>.md` on green, or `audit_failed_<artifact>_<YYYY-MM-DD>.md` with fix list on red. Do NOT declare the artifact shippable on red.
