---
description: Run Phase 0 data archaeology on a CSV/JSON before any downstream pipeline
argument-hint: <path/to/data.csv|json>
---

Invoke the `cortex-guardrail` subagent. Data file:

**$ARGUMENTS**

Run Phase 0 data archaeology (Framework §3.4):

1. **Locate the raw source** of every column — where did it come from? CRM, scrape, manual entry, derived field?
2. **Cross-reference each label against external reality.** Sample 20 records:
   - For company-level columns, Firecrawl the domain and confirm the claim.
   - For person-level columns, verify the LinkedIn URL resolves and matches.
   - For derived fields (engagement scores, propensity, etc.) trace the formula and verify on sample rows.
3. **Quarantine bad records.** Any record where the CRM disagrees with external reality goes into a `quarantined.csv` for human review.
4. **Apply the Cortex-specific failure modes (pre-seeded in agent prompt §2):**
   - "Head of Platform" title disambiguation (Platform Eng vs. Platform Marketing).
   - GitHub org ≠ company legal name.
   - Backstage repo presence ≠ Backstage in production (check commit recency).
   - Status page URL existing ≠ active incident reporting.
5. **Write `data_confidence.md`** with the schema: Column | Source | Confidence (H/M/L) | Known failure mode.
6. **Block downstream pipeline** if any column feeding segmentation, scoring, or messaging has unknown source or low confidence.

Produce the `data_confidence.md` and `quarantined.csv` artifacts. Do not approve downstream work until the user reviews quarantined records.
