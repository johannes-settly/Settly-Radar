# Project Radar — Settly Sales Pipeline Discovery

> Find the right companies, at the right time, every week.

## What this project is

Radar is a discovery and exploration project for Settly's sales team. The goal is to find and fix the
biggest bottleneck between "a company exists in the Netherlands" and "Settly has a meeting with the right
person there." It starts as an investigation (data, tools, signals), not as a build.

Owner / facilitator: Johannes (Senior PM, AI). Decider: Marieke (CEO). Sales: Paul, Mahshad.
Pricing source of truth (adjacent project): Kimmo and Erika.

## Goal

**Primary goal (agreed in the workshop on 19 Nov 2026):** solve the top three bottlenecks for sales in
order to sign the H1 ACV target (~€2.1M, roughly 21 new companies).

**Starting point (Marieke's decision):** begin at the very front of the funnel. Establish one agreed
TAM/SAM and a reliable *weekly flow* of new, well-timed target companies for outreach.

**Principle: topline first, efficiency second.** Automation that saves time but does not add pipeline is
not the goal. Every initiative must trace back to meetings booked and ACV signed.

### Weekly pipeline math (from Marieke / Paul)

| Metric | Target |
|---|---|
| Companies prospected | 200 / week |
| New companies added | 30 / week |
| New meetings | 3 / week |
| SQLs | 9 / month |
| Positive reply rate today | ~1% (market standard) |

## Why (motivation)

- The team does not have an agreed market size. Past research landed on anything from 500 to 8,000
  companies. Mahshad regularly feels she is "running out of companies" to contact.
- Signal spotting is fragmented (Claude scheduled job, Google Alerts, Sales Navigator, Amplemarket trial)
  and only ~80% accurate. Timing matters: the same company can respond very differently a month apart.
- Generic tools under-cover Settly's niche ICP. Marieke estimates Sales Navigator showed only ~20% of the
  real market. Vendors themselves say Settly's ICP is unusually nuanced.
- Conversion *after* a meeting is strong (only one deal lost in the last 3–6 months). The constraint is
  getting enough of the right meetings.

## ICP essentials (what makes filtering hard)

- HQ in the Netherlands **and** decision-making power in the Netherlands
- FTE band matters; messaging works best per FTE cohort
- Hires internationals: non-EU (visa/IND) is only ~20% of the picture. EU movers, interns and other
  categories that don't get the 30% ruling are also in scope.
- Promising angle (Paul): use companies with 30%-ruling employees rather than only the IND recognised
  sponsor list.

## Current hypotheses to test

1. A defensible TAM/SAM can be built by combining public NL sources (IND sponsor register, 30% ruling
   signals, KvK, job posts, headcount growth) with Settly's own data, and it will be meaningfully larger
   and more accurate than what Sales Navigator / Amplemarket return out of the box.
2. Settly's own history (HubSpot meetings, call transcripts, closed-won, closed-lost, nurture) contains
   reusable timing signals (e.g. internship season → reach out in May) that generic tools cannot see.
3. Signal detection and data enrichment should mostly be **bought** (Amplemarket or similar);
   Settly-specific enrichment, scoring and the weekly account allocation are where custom work pays off.

## Constraints and guardrails

- **Tool decisions pending.** Chrono vs Amplemarket and a possible HubSpot replacement are due ~end of
  Nov 2026. HubSpot will likely stay. Do not build automations on a tool that may be replaced. Prefer
  tool-agnostic analysis and data models until the decision lands.
- **Buy vs build.** Don't rebuild scraping/signal infrastructure that Amplemarket-type tools do at scale.
  Build where Settly's niche knowledge is the edge.
- **GDPR.** Contact data must come from a certified/authorised source. Never store personal contact data
  in this repo. Work with company-level data and anonymised exports where possible.
- **Data freshness.** HubSpot data older than ~6–8 months is unreliable. Paul's cleanup is ~70–80% done.
  Start analysis from customers and recent deals (smaller, cleaner) before the 17k meetings / 20k outreaches.
- **ROI first.** Every proposed initiative needs a stated metric and expected impact before work starts.

## Out of scope (for now, see docs/06-parked-topics.md)

Pricing/proposal generation (separate pricing project landing within a month), ops handover, forecast vs
actualised revenue, a marketing-specific session (planned separately with Kimmo).

## Repo structure

```
CLAUDE.md                     ← you are here
TODO.md                       ← working to-do list, keep updated
docs/
  01-workshop-summary.md      ← 19 Nov alignment workshop: goal, risks, decision
  02-interview-mahshad.md     ← 17 Nov discovery interview
  03-interview-paul.md        ← 17 Nov discovery interview
  04-current-sales-workflow.md← funnel, tools, pain points per stage
  05-risks-and-mitigations.md ← pessimistic-hat output + how we'll address each
  06-parked-topics.md         ← valid problems we are deliberately not working on yet
  transcripts/                ← drop raw transcripts here (not committed if they contain PII)
research/                     ← findings, one file per investigation (TAM, Amplemarket, data sources…)
data/                         ← local exports only; gitignored
```

## How to work in this repo (instructions for Claude)

- This is an **exploration** phase. Default output is a written finding in `research/` with sources,
  method, numbers and a clear "so what" for the sales goal. Don't scaffold an app unless asked.
- When estimating market size, show the method and every source, give ranges, and state assumptions.
  Prefer official NL sources (IND, Belastingdienst, KvK, CBS) and cite them.
- Tie every finding back to the weekly pipeline math above.
- Flag when a conclusion depends on a pending tool decision.
- Keep `TODO.md` current: check items off, add new ones discovered during work.
- Transcripts are auto-generated and mangle names. Mapping: "Ma", "Mara", "Maria K", "America" →
  Marieke; "Michelle", "Mashad", "Mashhat" → Mahshad; "Kim", "Kimo" → Kimmo; "Erica" → Erika;
  "Hannah" → Johannes; "Chrono"/"Corona" → Chrono (outreach tool); "Apple market"/"ample market" →
  Amplemarket; "Hopspot" → HubSpot; "clot"/"cloud"/"quad" → Claude.
- If a tool is eventually built, default stack: Next.js, Supabase, Tailwind, shadcn/ui, Vercel; Claude
  Code + Langfuse for development and evals. Signal/scoring logic should get an eval set early.
