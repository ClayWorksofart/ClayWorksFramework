---
description: Pre-flight cost-gate audit before running a paid-API script
argument-hint: <script> against <N> domains/records
---

Invoke the `cortex-guardrail` subagent. Planned run:

**$ARGUMENTS**

Run the pre-flight cost gate (Framework §3.10):

1. **Estimate cost yourself** against published Anthropic + Firecrawl rates. Token count per call × rate × call count. Do NOT ask the model what it costs (§1.5).
2. **Show the math** — number of calls, tokens per call, $/1K tokens, total estimate. State the unit explicitly (dollars, not cents).
3. **Apply the gate:**
   - `<$100`: log to `cost_log.md`, proceed.
   - `$100–$1,000`: prompt user for `y` confirmation.
   - `$1,000–$10,000`: require `--i-spent <dollars>` CLI flag — verify it's present on the planned command.
   - `$10,000+`: require second `--i-mean-it` flag + commit-msg rationale.
4. **Verify prompt caching** is enabled in the script. Grep for cache_control / cached_tokens. Flag if missing — uncached is 10× more expensive.
5. **Verify the cost-gate rule lives in three places:**
   - `~/CLAUDE.md` — confirm with user (we can't read their home).
   - `./CLAUDE.md` — verify present.
   - The script's header docstring — verify present.
6. **Cents-vs-dollars regression** — assert the unit. Reference the $256,409 → $2,564 lesson.

Halt and do not approve execution until every gate item is green.
