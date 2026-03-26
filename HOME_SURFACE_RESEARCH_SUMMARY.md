# Yahoo Mail Premium — Home Surface Research Strategy
## One-Pager for Planning & Alignment

---

### What We're Answering
The Home Surface replaces the chronological inbox with an intelligent, life-organized screen powered by the Life Graph. We need to answer two questions simultaneously:

1. **Is the intelligence good enough?** Can the system correctly prioritize, categorize, and brief a user's email life? And critically — can our intelligence team build this, or do we need vendor help?
2. **What should the experience feel like?** Of the many possible ways to organize and present this — which ones actually work?

These questions are interdependent. A great experience with bad intelligence feels broken. Great intelligence in a confusing experience gets ignored. So we run them in parallel and merge them when both are ready.

**Target archetype:** The overwhelmed millennial parent — someone whose email system has gotten away from them. Permission slips mixed with mortgage alerts mixed with soccer carpool. If the Home Surface works for this person, it works for everyone.

---

### How the Research Works

#### Phase 0: Concept Gauntlet (Weeks 1–2)
**Purpose:** Go wide, then narrow. Start with 4 distinct visions for what the Home Surface could be. Kill the weak ones fast.

**Four concepts, each representing a different design philosophy:**

| Concept | Metaphor | What it uniquely tests |
|---|---|---|
| **Morning Brief** | Document you read | Narrative density, passive consumption, completion = finishing reading |
| **Living Canvas** | Landscape you survey | Spatial organization, visual priority, ambient completion |
| **Two-Stack** | Desk trays | Maximum simplicity, incoming/upcoming as the primary split |
| **Chief of Staff** | Assistant reporting | Maximum delegation, trust, system-decided triage |

**Two lenses per concept (8 deliverables total):**
- **Landing page with embedded motion** — tests desirability *and* feel in one artifact. "Would I want this? Does it feel right?" Built as polished single-page sites with animated sections that hint at surface dynamics.
- **Narrated video walkthrough** — tests comprehension and flow. Screen-recorded walkthrough of a realistic morning email session with voiceover. "Does this make sense? Could I do this every day?"

**How we test:** dScout Express — participants see 2 concepts/day over 2 days, react after each lens.

**What comes out:** 2–3 concepts advance to full prototype builds, with refinement notes on what worked and what to fix.

---

#### Track A: Intelligence Calibration (Ongoing)
**Purpose:** Calibrate the Life Graph's judgment quality through ongoing research with 5–7 dedicated dogfooders who fit our target audience — overwhelmed, high-volume email users whose inboxes have gotten away from them.

**The 7 key questions we need to answer:**
1. Does the system know what matters to *this person* — not just what's objectively urgent?
2. How well does it connect dots across messages to surface the real picture?
3. Does the "since you were last here" summary create confidence nothing was missed?
4. Can we get meaningfully better over time, or does accuracy plateau?
5. Does it feel like it knows you, or like a machine that read your email?
6. How gracefully does it handle what it gets wrong?
7. Does quality hold up across different visit frequencies and volumes?

**Method toolkit** (pick 2–3 per week based on what we need, not a fixed script):
- **Shadow Inbox** — create the ideal AI output, participant rates accuracy. Recurring pulse check.
- **Side-by-Side Comparison** — 2–3 different AI outputs for the same inbox. Which approach wins?
- **Display Variations** — same intelligence, different presentations. Separate AI quality from display quality.
- **Real-Time Walkthrough** — walk through output together live. Surfaces the *why* behind failures.
- **Build-Your-Own Briefing** — participant creates their ideal version. Establishes the gold standard.
- **Stress Tests** — hard days: 60 emails after a weekend, one urgent item buried in 30 routine ones.

**What we're targeting:** ~80% priority accuracy, plus qualitative signal on personalization, warmth, aggregation quality, and temporal sensitivity.

**The intelligence readiness gate:** Track A produces clear evidence of where the intelligence stands and what it needs:
- Priority accuracy trajectory (improving? plateauing? stuck?)
- Failure mode breakdown — which capabilities are strong, which need focused investment
- Clear picture of what's working and where to double down

**Who to recruit — the 5–7 matter a lot:**
- Fits the target audience: high volume, email chaos, mix of personal + professional
- Genuine email diversity across the group (not 5 PMs with identical inboxes)
- Reliable — will actually show up and engage every day
- Internal credibility — their eventual advocacy carries weight

**This is ongoing research.** Learnings continuously inform the intelligence approach and get baked into the prototypes that the external panel evaluates.

---

#### Track B: Experience Prototypes (Weeks 3–5)
**Purpose:** The 2–3 Gauntlet winners become full interactive prototypes — rich, instrumented web apps with realistic data. These are the "pre-TestFlight" versions: research owns them, analytics are baked in from day one.

**Each prototype takes a deliberate position on:**
- Information architecture (categories vs. priority tiers vs. timeline)
- Content density (headlines only vs. full micro-briefs vs. category summaries)
- Interaction/triage model (per-item actions vs. batch vs. system-handled)
- Cognitive framing (briefing vs. dashboard vs. assistant vs. canvas)
- Completion signal (progress bar vs. calm state vs. receipt vs. countdown)
- Temporal behavior (static vs. time-of-day modes vs. continuous adaptation)

**Intelligence is pre-calibrated.** What we learned from the dogfood WoZ group gets baked into the prototypes. The panel never does Shadow Inbox — they experience the refined product directly.

**Prototypes are mobile-first web apps** (run in mobile Safari via URL — no TestFlight, no App Store). Phone-only with viewport lock. Participants get a link; Gauntlet stimulus can be viewed on any device.

**How we test (fresh dScout panel — external recruits, clean eyes):**
- dScout Express (use prototype → go to real inbox → narrate comparison)
- Moderated labs (8–10 sessions, think-aloud, scan pattern observation)
- Built-in analytics (taps, scroll, time, drill-down, triage speed, return frequency)

---

### Who Participates — Two Groups, Sequential

| Group | Who | When | Purpose |
|---|---|---|---|
| **Internal dogfood (5)** | Handpicked Yahoo Mail team, diverse email lives | Weeks 1–3 (Gauntlet reactions + Shadow Inbox) | Calibrate intelligence, test concepts, build internal advocacy |
| **External dScout panel (5–8)** | Recruited via dScout, screened for email overwhelm | Weeks 3–5 (prototype testing) | Clean-read validation on experience prototypes with calibrated intelligence |

---

### What Gets Built (in rough priority order)
1. **Gauntlet stimulus packages** — 4 landing pages with embedded motion + 4 video walkthroughs
2. **WoZ prompt template** — structured input/output for Shadow Inbox simulation, stress-tested before participants start
3. **Shadow Inbox renderer** — high-fidelity static views from WoZ output
4. **Interactive prototypes** — 2–3 Gauntlet winners as instrumented web apps (pre-TestFlight, research-owned)
5. **dScout mission structures** — question flows for Gauntlet, Track A daily cycles, Track B evaluation
6. **Analytics + tracking** — behavioral instrumentation baked into prototypes, WoZ accuracy tracking

---

### Week 5 Deliverables — Two Distinct Outputs

1. **Experience direction deck:** "Here are the 2 strongest directions and what each needs to become a product." Funnel narrowing with data — feeds design/eng/PM.
2. **Intelligence readiness assessment:** "Can our team build this, or do we need vendor help?" Go/no-go on capability with accuracy trajectory, failure mode analysis, and build-vs-vendor recommendation.

**Audience:** Cross-functional leadership (research, design, eng, PM, leadership).

---

### Infrastructure
- **Deployment:** Vercel (personal account initially, work account when available)
- **Single repo**, each stimulus piece and prototype as its own route
- **dScout missions** point to Vercel URLs

---

### Key Decisions Still Needed
1. Final concept definitions for the 4 Gauntlet candidates (Week 1 sprint)
2. Which 5 internal dogfooders? (Recruit by end of Week 1)
3. External panel budget and screening criteria
4. Eng handoff model (pre-TestFlight web proto → native port)

---

### Timeline at a Glance

| | Week 1 | Week 2 | Week 3 | Week 4 | Week 5 |
|---|---|---|---|---|---|
| **Gauntlet** | Build 8 stimulus pieces | dScout Express runs, synthesize | — | — | — |
| **Track A** | Build + stress-test prompt template, recruit 5 dogfooders | Begin daily WoZ (weekdays) | WoZ continues, vary treatments, roll off | — | — |
| **Track B** | — | — | Build prototypes from Gauntlet winners + WoZ learnings | dScout panel + moderated labs | Refine, synthesize, conviction deck |
