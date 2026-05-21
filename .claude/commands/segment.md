---
description: Walk the Concentric Circle Test for a Cortex outbound segment hypothesis
argument-hint: <hypothesis segment description>
---

Invoke the `cortex-strategy-build` subagent. The hypothesis segment is:

**$ARGUMENTS**

Walk the Concentric Circle Test (Framework §2.1) anchored to Cortex's three pillars (centralize data / unlock insights / continuously improve). Output:

1. Ring-by-ring count estimate (bullseye → outer), with explicit company-count target at each ring.
2. Whether the bullseye satisfies the **100–2,000 company** rule. If under, segment is an account list. If over, it's a market.
3. Which ring this hypothesis actually sits in.
4. A pillar-tagged signal stack table (per §4 of the agent prompt) for the bullseye.
5. Flag if this is firmographic-dressed-as-pain (Apollo filter) vs. a real pain-qualified segment.

Do not propose any scrape or list build yet. Stop after the segment is locked.
