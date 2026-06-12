---
description: Compute MBR for a campaign and decide pivot per Cortex thresholds
argument-hint: <campaign or segment name>
---

Invoke the `cortex-strategy-build` subagent. Campaign to read:

**$ARGUMENTS**

Compute and decide:

1. **MBR = meetings booked / (emails sent + dials made)** for this campaign, per persona.
2. State activity count — discipline applies only at ≥1,000 activities (Framework §2.4).
3. State the read window — 24h after first send for early read, rolling 5-day for stable read. 87% of cold-email replies arrive in 24h.
4. Compare against Cortex thresholds:
   - PQS / warm: ≥0.8% MBR target.
   - Cold with signal: ≥0.3% MBR target.
   - **Pivot trigger: below 0.2% MBR by end of week 1 across ≥1,000 activities.**
5. **Decide:** continue, swap persona, or pivot segment. If 3 of 4 personas flatline, the segment is wrong — pivot the segment, not the copy.
6. Output the decision with the data that justifies it.

If activity count is below threshold, say so explicitly and ask for more time, not a decision.
