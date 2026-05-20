# The Jordan Crawford GTM Engineering Framework

A working framework for builds, decisions, and mindset, synthesized from Cannonball GTM and *On the Edge by Blueprint*. The order matters: mindset shapes decisions, decisions shape builds. Read top to bottom the first time.

-----

## Part 1 — Mindset

### 1.1 You are not in the assembly line anymore

Old GTM moves like a relay race: product marketing → demand gen → SDRs → AE, everybody owning 11% of the journey, nobody owning the outcome. That structure exists because the work used to require specialists. It doesn't anymore. One operator with Claude Code, the right skills, and access to public data does the work that used to require five people.

The implication is not "AI saves time." That framing is wrong and it makes you build the wrong things. The implication is **margin expansion and revenue per employee**. Automation isn't a convenience wrapper on a job that still exists. It's infrastructure that compounds. The old role doesn't get faster. It gets replaced.

If you are still writing job descriptions for "GTM Engineer at $85K to support the demand gen team," you are solving last year's problem. The role that matters is the one that does strategy through execution in the same Tuesday afternoon.

### 1.2 The three stages of GTM maturity

There are three eras of AI in GTM. Most teams are in stage 2 and think they're at the top.

- **Stage 1 — One-off LLMs.** ChatGPT in a browser tab. Task efficiency. Faster at single tasks, but the system has amnesia. Every new window starts from zero. Your team is still the memory layer.
- **Stage 2 — Workflows.** Clay, n8n, Zapier, Make. Process efficiency. Deterministic pipelines that work exactly as designed and snap when reality changes. You automated the assembly line but it is still an assembly line.
- **Stage 3 — Claude Code + LLMs.** Personal efficiency and compounding judgment. The system remembers context, evaluates its own output, and improves the plan based on what happened last time. Next week is easier than last week.

Smart teams skip stage 2 entirely and go from stage 1 straight to stage 3. The middle stage is a trap that turns operators into mechanics.

### 1.3 You are not the main character

Nobody wakes up thinking about your product. They wake up in a situation. Messaging is the art of describing someone's situation so precisely that replying feels easier than ignoring. If your message could have been written for anyone, it gets deleted before they finish the subject line.

You are not targeting people. You are targeting conditions. Problem before person. Personalization isn't "I saw you went to Michigan." Personalization is "we've seen this exact constraint in teams like yours, and it creates this predictable failure mode."

### 1.4 Plausible is the enemy of correct

A derived foreign key field at one client was wrong on 42.6% of records. 37,000 calls attributed to the wrong accounts. Every dossier looked plausible. Nobody noticed for weeks.

Wrong gets caught. Plausible gets acted on. The work of GTM engineering is mostly the discipline of distrusting your own data first. Phase 0 of every build is sitting on the data and not believing it.

### 1.5 Claude cannot tell you what Claude costs

A four-month Anthropic bill rendered as $256,409 in a deck. The actual number was $2,564. Anthropic's API returns cost in cents and labels the currency USD. The deck-generation code, written with Claude, dutifully rendered cents as dollars and never flinched.

Two operating rules fall out of this:

- **If you are about to spend money on a Claude job, compute the cost yourself against published rates before you send a request.** Claude has no internal sense of what API calls cost or what magnitudes are plausible.
- **Build pre-flight cost gates into every agent loop.** Under $100, log and proceed. $100–$1,000, prompt for `y`. $1,000–$10,000, require the dollar amount as a flag. Above $10,000, require a second flag like `--i-mean-it`. Put the rule in three places — your home folder, the repo, the specific tool — so nobody can override it quietly.

The bill that didn't happen today is the same bill that ends careers the next time the workload is a hundred times larger.

### 1.6 What this all means for the work

You are not selling time savings. You are not selling automation. You are building a system that codifies judgment, holds onto context, and gets better next week. The thing you ship is not the campaign. It's the apparatus that runs the campaign.

-----

## Part 2 — Decisions

The decisions framework answers four questions in order. Most teams skip questions one and two and start at three. That's why their campaigns don't work.

### 2.1 Decision 1 — Is your segment dead-center on your solution?

The Concentric Circle Test. Three rings: segment, company, person. At every layer, ask one question: how close is my solution to their core challenge?

Markets are too big to message. *Healthcare* is a market. *Orthodontists* is a segment. The segment has a single core challenge — the thing the people in it wake up worrying about. Your job is to find a segment whose core challenge **is** your solution.

If you sell dishwashing automation to restaurants, you are selling into a segment whose core challenge is filling seats. You will get meetings. You will not win many. Every word out of your mouth is "I know you don't care about this, but I'm going to convince you that you should." That is not a hard sell. That is a difficult sell.

Sell dishwashing automation to outsourced commercial dishwashing facilities (Dish Hubs) and the segment's core challenge **is** your product. Send the worst possible LinkedIn message and get seven replies out of ten. Same message. Different segment. Easy mode versus difficult mode.

Segment size matters: roughly 100 to 2,000 companies. Over 50,000, it's a market. Under 50, it's an account list. And the obvious cut isn't always right — "orthodontists" might be three different segments (PE roll-ups, mom-and-pop, practice groups) with three different cores.

### 2.2 Decision 2 — Is this a pain-qualified segment or a firmographic list?

Apollo filters are not segments. "50 to 1,000 employees in vertical X" is a description of a list of companies, not a description of pain.

The customers who write you the biggest checks and stay the longest don't share a headcount band. They share a situation — an operational thing that happened to them six to eighteen months before they bought, that almost nobody else on the filter is going through right now. That's the actual segment.

Build ICP the other direction. Start with outcomes you already have (won, lost, healthy, churned), enrich each account with public-data signals (Firecrawl, LinkedIn, state portals, GitHub activity), and reconstruct what those companies looked like *before* they bought. The signals that survive a held-out 20% sample are real. The ones that collapse on holdout were coincidences.

Examples of real signals that came out of this kind of work:

- Two state professional registrations in the prior 18 months (state SoS portal)
- A compliance/GRC role posted in the prior 6 months (Firecrawl careers page)
- A compliance-tagged GitHub repo that went quiet for nine months

None of those are on an Apollo filter. None of them are firmographic. Each one reflects an operational event that preceded buying behavior.

### 2.3 Decision 3 — Are you targeting moments, not profiles?

Only about 5% of your market is in a buying cycle right now. Budget allocated, authority identified, need confirmed, timing now. Those buyers are fully qualified. Every competitor is fighting for them. There aren't enough of them to hit your growth number.

You have two options:

- **TAM spam.** Volume-based outbound across a large addressable market. Works if you have the budget to sustain volume across tens of thousands of accounts. Most companies don't.
- **Needs-based outbound.** Find buyers who have a need but haven't started looking yet. Roughly 15% of accounts experiencing pain. Smaller TAM, different motion.

Both motions need signals. Licensed signal data (funding, headcount, job postings, intent) is becoming commoditized — every competitor has it. Public data is where the asymmetry lives. Permits filed, budgets approved, contracts awarded, state filings, regulatory submissions. Nobody is selling it as a feed. You have to assemble it. That assembly is the moat.

The buyer journey changed. Buyers used to make ~70% of the decision before contacting you. Now it's closer to 90%, driven by ChatGPT, reviews, and peer conversations. By the time they fill out your form, they've already decided. Signals are how you reach them before that point.

### 2.4 Decision 4 — Is the meeting booked rate telling you to pivot?

One metric resolves every internal argument about whether a campaign is working: **Meeting Booked Rate (MBR) = meetings booked / total activities (emails + calls) against a given list**.

Open rates, reply rates, positive reply rates — these are metrics teams use to keep dying campaigns alive. The campaign is either booking meetings or it isn't.

87% of cold email replies arrive within 24 hours. You don't need 30 days. You don't need to "let the sequence play out." If somebody tells you on day three "we just need to wait a few more days," they're wrong. By the end of week one you have rolling data across enough batches to read MBR with confidence.

What takes time is downstream: meetings to SQOs, deal velocity, conversion. That's weeks. MBR is days.

The persona decision is the only one that has to be discovered, not pre-computed. The founder picks the segment and the company filter. The salesperson tests four personas across the segment with 500–1,000 dials over 2–4 days. If all four fail, the segment is wrong (founder error, try again). If one pops, lock it.

### 2.5 Decision 5 — Ladder of escalation on cost

For every tool decision in a build, ask: what is the cheapest workable method, and what is the trigger to escalate?

- Free local methods first — scrapers you run yourself
- Cheap paid methods next — marketplace actors, batch APIs
- Expensive APIs only when the cheaper layer demonstrably fails the quality or coverage bar

Premium model calls and high-tier enrichment are the last resort, not the default. If you start at the top of the ladder, you've decided that cost discipline isn't part of the build.

-----

## Part 3 — Builds

The build framework is operational. It assumes you've made the decisions above. If you haven't, the build is going to be wrong no matter how clean the code is.

### 3.1 Three building blocks: Tools, Skills, MCP

The Claude Code ecosystem has three layers. Most operators conflate them and that's why their outputs are generic.

- **Tools** are capabilities — actions that execute and return a result. Built-in (read file, run bash, search web) or external (Exa for AI search, Firecrawl for crawls, a Gong API client). Tools are the hands. They do stuff.
- **Skills** are written instructions — markdown files — that teach Claude how to think about a category of work. Methodology encoded. Your playbook for case studies, your pain-qualified segmentation process, your editorial standards. Skills are the brain.
- **MCP** is the integration layer that connects Claude to external systems. CRM, Slack, Drive, vertical databases. MCP is the eyes into your world.

Most companies skip straight to asking Claude to do things without providing context. Then they're shocked when the output is generic. That's not an AI problem. That's an onboarding problem. You wouldn't hand a new SDR a phone and say "go." You give them playbooks, an ICP, methodology. Skills are how you do that for Claude.

### 3.2 Define output before input

The mental model that separates fast operators from stuck ones: can you describe a clear output given a set of inputs? "Pull all Gong recordings for this account, pull the Salesforce record, fill the case-study template, format like this" — you know the inputs, you know the output, you know what good looks like.

Compare to "go do my sales job for me." No clear inputs, no clear outputs, no measure of quality. Every session restarts from scratch.

If you can't articulate the output, you don't yet have a problem fit for Claude Code. You have a confusion fit for a whiteboard.

### 3.3 The eight tool categories for GTM pipelines

Real GTM work is a chain of dependent steps where a bad decision early contaminates everything downstream. The minimum viable version is the first three. Add the others as the workflow gets complex.

1. **Data source discovery for TAM building.** A formal research pass per client, industry, geography. Rank candidate sources by coverage, quality, cost, durability. Output a primary/fallback/gap-filler plan. Authoritative sources first — government databases, licensing boards, Secretary of State filings, vertical directories. The "source stack" mindset usually beats the "one big API" mindset.
1. **Web scraping / bulk capture.** Capture test on a small sample before a production run. Prove access, measure failure rates, understand cost profile.
1. **Email verification.** Catch bad addresses before they hit your sender reputation.
1. **Enrichment.** LinkedIn, firmographic, technographic. Not firmographic *as a discriminator* — only as enrichment.
1. **CRM integration.** Read in, write out. The audit trail lives here.
1. **Outreach orchestration.** Sequencing, sending, tracking.
1. **Analytics and attribution.** What's the MBR by segment, by message variant, by persona?
1. **Cost monitoring.** Pre-flight checks (see 1.5) and post-hoc reconciliation against published rates.

### 3.4 Phase 0 of every build is data archaeology

Before building any pipeline that depends on CRM data, cross-reference every CRM label against external reality. Firecrawl on the domain. LinkedIn enrichment. Web presence check. Anything where the CRM says "$50K healthy customer" but the company has one employee and a dead website gets quarantined.

Quarantined records get reviewed by a human and either reinstated or excluded. Build a `data_confidence.md` artifact and require operator approval before downstream work runs.

Skip this and you'll build downstream conclusions on records that are fiction. The CRM is third in the trust hierarchy, not first.

### 3.5 The trust hierarchy

When two systems disagree about an account, prefer in this order:

1. **Customer actions** — product events, logins, payments, feature usage. They voted with their behavior.
1. **Customer voice** — call transcripts, support tickets, emails they wrote. They said it themselves.
1. **CRM-derived state** — opportunity stages, account types, lead-source classifications. This is what reps entered when commission triggered. One step removed from reality.

A rep marks a deal "Customer" when commission triggers. Product data shows that account never logged in. Product is right.

### 3.6 Identity linking, three hard rules

Identity linking is where joins go wrong and downstream artifacts become fiction. Three rules, learned the hard way:

- **Never join by email domain without stripping the company's own domain first.** Internal employees dialing on behalf of customers will produce hundreds of false matches.
- **Never join on a single key.** Require at least two of: ID match, domain match, name fuzzy match at 0.92+. Numeric IDs collide. A wealth management firm in Missouri got joined to a thermal engineering firm in New York because a customer ID matched.
- **Surface a 100-record random spot-check to a human.** Don't trust the aggregate. Tiebreakers from the human go into the artifact as audit trail.

### 3.7 Hold out 20%

Any pipeline that generates hypotheses — discriminators, signals, segments, scoring rubrics — must hold out 20% of the source data from the start. Never let hypothesis generation see it. At the end, re-test every surviving hypothesis on the holdout.

The vowel-name failure mode: a hypothesis with great training lift and ~1.0 holdout lift is a coincidence. Kill it. The real signals hold their lift on the holdout because they reflect operational reality, not training-set artifacts.

### 3.8 Forbidden columns in pain-segmentation work

When clustering customers to find pain segments, the following columns must be stripped before clustering or they'll dominate the result and produce a firmographic ICP dressed up in new clothes:

- Headcount
- Revenue / ARR
- Industry / vertical
- Close date
- Anything that exists because the customer bought (deal size, opportunity stage, contract value)

If you cluster on these, you're predicting the past, not finding the segment.

### 3.9 Messaging build pattern

The format that performs. Subject 2–5 words. Three lines, structured as Situation → Insight → Inquisition.

```
Subject: [2–5 words, sharp label for the situation]

You're probably dealing with [specific situation] right now.

Most teams get stuck because [specific constraint or tradeoff].

Am I close, or is it different on your side?
```

- **Subject** earns the open. Not understanding, not pitching. Curiosity.
- **Situation** names their reality, not yours. If you describe yourself instead of them, the whole email collapses.
- **Insight** is one unique take that signals you've seen this movie before.
- **Inquisition** asks for truth, not time. "Book a call" is a CTA. "Did I get this right?" is an inquisition. Replies are the win condition.

Two high-performing patterns sit on top of this format:

- **Pain-Qualified Segment (PQS)** — lead with a specific operational fact that only applies to this segment ("Filed on May 23, 2024, your El Dorado Hills location is scheduled to take three years for permit approval"). The fact does the work. No "we are a leading provider."
- **Permissionless Value Proposition (PVP)** — deliver something valuable in the email itself. Interview their customers, write the case study, do the research. The email isn't "please." It's "I already did the work."

### 3.10 Pre-flight cost gates

Every agent loop ships with a cost gate. The gate computes estimated cost from token counts and published rates before any expensive call goes out.

- < $100: log estimate, proceed
- $100–$1,000: prompt for `y` confirmation
- $1,000–$10,000: require dollar amount as a CLI flag (so typos can't authorize four-figure spend)
- $10,000+: require a second confirmation flag

Put the rule in three places: `~/CLAUDE.md`, the repo, the specific tool. Override has to happen in three places to bypass it.

Cache system prompts by default. Anthropic charges full price first time, ~10% on repeats. An agent swarm that sends the same prompt thousands of times without caching is paying ten times more than it should.

### 3.11 The critique trio

For any high-stakes generated artifact — a dossier, a segment definition, a scoring rubric — run three independent reviewers in parallel before shipping:

- **Statistician** — checking distributions, outliers, sample sizes, lift significance
- **RevOps perspective** — checking operational coherence. Does this match how the business actually runs?
- **Outlier hunter** — checking individual records for paradoxes. An account paying $45K/month with zero calls in a year is either extraordinary or a linking failure.

The trio produces a unified list of things that must be resolved before the artifact ships. The operator resolves each one. The artifact doesn't ship until the list is empty.

### 3.12 What ships, what gets reverted

When you find a bug late, fix the bug. Don't unfix the discipline.

The $67K bill that wasn't was a unit conversion error — cents rendered as dollars. The cost forensic deck got reverted. The safety check, the prompt caching, the three copies of the rule, the twenty-three commits in forty-seven minutes — those stayed. The misread was wrong. The infrastructure built in response to it was still correct.

The bill that didn't happen today is the same bill that ends careers the next time the workload is a hundred times larger.

-----

## Quick reference

**Before you build anything**

- Is my segment dead-center on my solution? (Concentric Circle Test)
- Is this a pain-qualified segment or an Apollo filter?
- Am I targeting a moment or a profile?
- What's my MBR target and pivot threshold?
- What's the cheapest workable method at each layer?

**Before you ship anything**

- Did Phase 0 quarantine the bad records?
- Did I hold out 20%?
- Did I strip headcount/revenue/industry/close-date columns?
- Did the critique trio agree?
- Is the pre-flight cost gate in place?

**Before you spend a dollar on Claude**

- Did I compute the cost myself against published rates?
- Is the system prompt cached?
- Is the cost rule in all three CLAUDE.md files?

**When the campaign is two days old**

- What's the MBR?
- If it's not on track, the segment is probably wrong. Pivot in week one, not week four.

-----

*Synthesized from Cannonball GTM (cannonballgtm.substack.com) and On the Edge by Blueprint (edge.blueprintgtm.com), 2026 archive.*
