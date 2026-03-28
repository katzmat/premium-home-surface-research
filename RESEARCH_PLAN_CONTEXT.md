# Yahoo Mail Premium — Home Surface Research Plan
## Claude Code Project Context

> **Purpose of this document:** Planning and context document for Claude Code sessions. Captures the full research strategy, design principles, technical requirements, and open questions. Load as project context when working on any component of the research infrastructure.

---

## 1. Strategic Context

### What we're building
Yahoo Mail Premium (~$20/mo) — subscription built on AI-powered features that make the inbox understand the user's life. Core technology: **Life Graph** — frontier LLM-powered model of the user's life built from email content and behavioral signals.

### What we're researching
The **Home Surface** — new primary email screen replacing the chronological list view. Must handle:
- **Incoming**: New emails, triaged and prioritized by life context
- **Upcoming**: Obligations, deadlines, events extracted from email history
- **The middle space**: Lifting select incoming items into upcoming

### Target archetype
The overwhelmed millennial parent — someone whose email system has gotten away from them. Permission slips mixed with mortgage alerts mixed with soccer carpool. If the Home Surface works for this person, it works for everyone.

### Core thesis requirements
- Low cognitive lift
- Radically improved signal-to-noise
- Leverages intelligent context graph (Life Graph)
- Designed for rapid processing
- Creates sense of low-lift completion
- Diverges from sender/subject/snippet chronological inbox
- One surface that intuitively flexes (not linked network of surfaces)
- Comprehensive enough to replace inbox, not sit alongside it

### Established principles (validated — do NOT re-test)
1. **Cognitive chunking works**: Bite-sized chunks provide emotional and cognitive relief
2. **Whole-picture upshot is non-negotiable**: "Since you were last here" required to avoid FOMO
3. **Privacy is secondary to value**: Users accept Life Graph privacy if value delivers
4. **Upcoming ≥ incoming**: Tracking upcoming obligations at least as important as triaging new mail
5. **Replacement, not addition**: Must become primary experience

---

## 2. Open Research Questions — The Full Design Space

### Information Architecture
How is the surface organized? Primary structural units — categories, priority tiers, temporal groupings? Where does incoming end and upcoming begin — boundary, gradient, or fluid? How does "since you were last here" relate spatially to the rest?
- *Range*: Distinct sections ↔ fully integrated by relevance ↔ category-first with mixed incoming/upcoming

### Content Density
How much shown at once? Context per item — micro-brief replace or augment sender/subject? Grouping depth before drill-down? Density shift between light and heavy days?
- *Range*: Headline-only ↔ full micro-briefs inline ↔ category summaries with counts

### Interaction Patterns & Triage Mechanics
Interaction grammar? System-decided vs. user-confirmed vs. spectrum? Gestures for surface action vs. drill-in? How does "lifting" incoming→upcoming feel?
- *Range*: Per-item approve/defer/dismiss ↔ batch by category ↔ system pre-triaged, user reviews

### Behavior Patterns
How do people move through this? Scan pattern? What triggers drill-down vs. surface action? Quick check-in vs. dedicated session?
- *Captured via*: Lab observation, scroll/tap instrumentation, Express self-report

### Cognitive Framing & Mental Model
What mental model adopted? Briefing? Dashboard? Assistant? Does framing create calm or anxiety?
- *Range*: Briefing you read ↔ dashboard you monitor ↔ assistant reports to you ↔ canvas you scan

### Completion Model
What replaces unread count? State, progress signal, absence of urgency? Reset daily or accumulate?
- *Range*: Explicit state ↔ progressive depletion ↔ ambient calm ↔ summary receipt

### Temporal Dynamics
Surface change throughout day? Post-triage behavior — contract, rearrange, celebrate? Hours away vs. minutes?
- *Range*: Static snapshot ↔ morning/evening modes ↔ continuous adaptation

### User Agency Spectrum
How much triage agency wanted? Varies by email type, trust level, tenure. Default posture and evolution?

---

## 3. Research Architecture — Three Components

### Pre-Phase: The Concept Gauntlet

**Goal**: Go wide before going deep. Take 4 distinct experience visions, run through rapid evaluation, identify which 2-3 deserve full prototype builds. Test with two cohorts to balance contextual realism against intelligence output quality.

**The Two-Lens Stimulus Package**: Each concept expressed through two complementary lenses:

1. **Value Prop Landing Page with Embedded Motion**: The promise in plain language + animated sections showing surface dynamics. Headline, description, key screens with motion that hints at behavior. Tests "would I want this?" and "does it feel right?" in a single artifact. Built as standalone HTML/React, deployable for dScout embedding or linking.

2. **Narrated Video Walkthrough**: Screen-recorded walkthrough of realistic scenario with voiceover. Full morning email processing session with sample data. Tests logic and flow — does the sequence make sense? ~60-90 seconds each. Claude Code builds the visual substrate; Matt records voiceover.

**Why two lenses**: They test different things and may produce divergent signal:
- Landing page resonance ≠ walkthrough clarity (communication problem, not concept problem)
- Walkthrough clarity ≠ landing page resonance (positioning problem, not design problem)
- These divergences tell you what to *fix* as concepts become prototypes

#### Two-Cohort Structure

The Gauntlet runs as **two parallel cohorts**, both unmoderated dScout Express missions:

1. **"Live Data Cohort"** — users port their actual email data into each prototype. Provides contextual realism and data quality insights from testing with real user data. However, the intelligence output will have quirks, flaws, and breaks reflecting the current calibration state. Ideally both cohorts would see high-intelligence versions, but the reality of development timing means this cohort's output will be rougher.

2. **"Real but Anonymized Sample Data Cohort"** — uses real, anonymized email data to simulate real-life messiness, but NOT the users' actual real-time data. This cohort's intelligence output can be better curated into a high-quality "eventual state" version — mimicking where we're striving to get the concept, not where the intel is currently calibrated.

**Why two cohorts:** We want to balance (a) contextual realism + data quality insights from testing with actual user data, with (b) the ability to show users a version with high-level intelligence output that represents the aspirational target, not the current calibration state.

**Evaluation**: Both cohorts run as dScout Express unmoderated missions. 2 concepts/day over 2 days. After each concept:
- After landing page: "Would you want this? What excites you? What worries you? How does it feel?"
- After walkthrough: "Does this make sense? Where lost? Could you do this every morning?"
- After full package: "Compared to real inbox, better? Would this replace current email? Single biggest thing to change?"

Cross-cohort comparison reveals how much intelligence quality affects concept preference and whether rougher live-data output changes which concepts resonate.

**Gauntlet output feeds Track B**:
- 2-3 concepts advanced to full prototype builds
- Design dimension priorities (which dimensions mattered most to participants)
- Concept refinement briefs (what worked, what needs to change per advancing concept)
- Cross-cohort signal on intelligence quality impact

**Timing**: Weeks 1-2.

---

### Track A — Intelligence Calibration

**Goal**: Calibrate Life Graph judgment quality through ongoing real-inbox research with dedicated dogfooders who fit our target audience.

**Participants**: 5-7 dedicated dogfooders who match our target archetype — overwhelmed, high-volume email users whose inboxes have gotten away from them. Weekday cadence.

**Recruitment criteria** (each participant is high-value — choose carefully):
- Fits the target audience: high volume, email chaos, mix of personal + professional
- Genuine email diversity across the group (not 5 PMs with identical inboxes)
- Reliable — will actually show up and engage every day
- Internal credibility — their eventual advocacy carries weight

---

#### The 7 Key Questions

1. **Does the system know what matters to *this person* — not just what's objectively urgent?** The permission slip due Friday matters more to the busy parent than the LinkedIn notification, even though both are "time-sensitive." Can it distinguish personal importance from generic urgency?

2. **How well does it connect dots across messages?** The contractor email from Monday + the payment reminder from Wednesday + the scheduling email from today = "your kitchen renovation needs three things from you this week." Can it synthesize across messages, or does it treat each email as standalone?

3. **Does the "since you were last here" summary create confidence that nothing was missed?** Too vague and people don't trust it. Too detailed and it's just another inbox. Can the intelligence produce a summary at the right altitude — complete enough to feel safe, concise enough to feel like relief?

4. **Can we get meaningfully better over time, or does accuracy plateau?** If Day 1 is 50% and Day 10 is 75% with the curve still rising, we have a path. If Day 10 is 55%, we know exactly where to focus. The trajectory matters more than any single day's score.

5. **Does it feel like it knows you, or like a machine that read your email?** Two systems can be equally accurate but feel completely different. One feels like a trusted assistant who understands your life, the other feels like an algorithm. The difference is in the tone, the small details (calling your kid's school by name vs. "a school-related email").

6. **How gracefully does it handle what it gets wrong?** The system will never be 100%. Does a missed priority feel catastrophic or minor? Does a miscategorized email erode confidence in the whole surface? Confident and wrong is far worse than humble and slightly off.

7. **Does quality hold up across different visit frequencies and volumes?** Checking in after 2 hours with 4 new emails is a different challenge than returning Monday morning to 60 weekend emails. The intelligence needs to scale both directions, and the "since you were last here" framing needs to feel appropriate whether the gap is 90 minutes or 48 hours.

---

#### Learning Areas

**Intelligence Accuracy**: Priority detection, incoming/upcoming separation, urgency vs. importance, miss rate, false alarm rate.

**Context Graph Depth**: Sender knowledge (who is this person to me?), cross-message connections (same project, same life thread), accumulated knowledge over multiple days, cold start vs. Day 5 quality.

**Aggregation & Synthesis**: Summarizing across related messages, category-level summaries, topline brief quality, handling volume spikes (12 emails vs. 60).

**Brief & Display Quality**: Micro-brief length and usefulness, tone (helpful assistant vs. robotic), visual hierarchy clarity, does it feel like a product or a report.

**Prompt & Instruction Tuning**: Which prompt structures produce best results, sensitivity to framing, value of accumulated life context, minimum viable context.

**Temporal Sensitivity**: Different visit frequencies (2 hours vs. overnight vs. weekend), morning vs. evening, deprioritizing passed events, "since you were last here" scaling.

**Personalization & Tone**: Does it feel like it knows *you*, warmth vs. clinical feel, right level of personality, trust-building through language.

**Edge Cases & Failure Modes**: Ambiguous emails, "gray zone" importance, forwarded/shared emails, context the system can't see, graceful vs. confident failure.

---

#### Method Toolkit

Track A uses a flexible toolkit of methods — not a single ossified plan. We pick 2-3 per week based on what we need to learn, and shift as the intelligence evolves.

**Method 1: Shadow Inbox**
We create the "ideal" version of what the Home Surface would show them, based on their real inbox. They compare it to their actual email and rate accuracy. Best for: measuring accuracy baseline, tracking improvement over time, testing the topline summary. Use throughout as a recurring pulse check.

**Method 2: Side-by-Side Model Comparison**
Show 2-3 different AI outputs for the *same* inbox snapshot. Different context graph versions, different prompt strategies, different levels of life context. Participant sees them together and judges: which one got it right? Which one feels like it knows you? Best for: choosing between competing intelligence approaches. Use when we have hypotheses about prompt structure or context depth and need a tiebreaker.

**Method 3: Display Variation Testing**
Same intelligence output, different presentations. Vary structure (category groups vs. priority list vs. narrative), length (one-liners vs. full briefs), tone (warm vs. efficient). Separates intelligence quality from presentation quality — a participant might hate an output because the *display* felt wrong, not because the AI was wrong. Best for: after intelligence stabilizes and we need to nail the presentation layer.

**Method 4: Real-Time Walkthrough & Annotation**
Show them a Shadow Inbox output and walk through it together, live. They narrate: "This is right... this is wrong... this one matters because you don't know my kid is allergic and this is actually from the allergist, not spam..." The richest signal — surfaces invisible context and the *why* behind failures. Best for: when stuck on accuracy gaps. Even 2-3 sessions can be more illuminating than a week of structured ratings.

**Method 5: Build-Your-Own Briefing**
Give participants their raw inbox data and ask *them* to create the ideal Home Surface view. What would you prioritize? How would you group these? What would the summary say? Establishes the "gold standard" and reveals mental models — do they think in categories, timelines, or priority tiers? Best for: early baseline before they've seen any AI output, and again after exposure to see if their sense of ideal has shifted.

**Method 6: Stress Test Scenarios**
Deliberately throw hard days at the system — 60 emails after a weekend, one urgent item buried in 30 routine ones, a day where the most important thing came from a verbal conversation the system can't see. The system probably works fine on an average Tuesday — the question is what happens on hard days, when users need it most. Best for: mid-to-late sprint, and opportunistically whenever a participant has a naturally unusual day.

---

#### Intelligence Readiness Gate

Track A produces clear evidence of where the intelligence stands and what it needs to reach product quality. Key outputs:
- Priority accuracy trajectory (improving? plateauing? stuck?)
- Failure mode breakdown (missing context? wrong categories? bad prioritization?) — determines if gaps are solvable with tuning or require a different approach
- Clear picture of which capabilities are strong and which need focused investment

This is ongoing research — learnings continuously inform the intelligence approach and get baked into the prototypes that the external panel evaluates.

---

### Track B — Experience Design Exploration

**Goal**: Build 2-3 Gauntlet winners as full interactive prototypes. Each is a complete experience with positions across ALL design dimensions. These are research-owned, instrumented web apps — the "pre-TestFlight" version.

**Relationship to Gauntlet**: Gauntlet determines what enters and what to emphasize. High value-prop but too-dense? Prototype solves density. Great walkthrough but confusing landing page? Prototype clarifies positioning.

**Intelligence is pre-calibrated**: What we learned from the dogfood WoZ group in Track A gets baked into the prototypes. The external panel never does Shadow Inbox — they experience the refined product directly.

**Testing methods** (fresh dScout panel — external recruits, clean eyes):
- dScout Express (behavioral + attitudinal, real-inbox grounding)
- Moderated labs (8-10 sessions, micro-observation, think-aloud)
- Behavioral instrumentation (taps, scroll, time, drill-down, triage speed, return frequency)

**Measurement by dimension**:

| Dimension | Signal | Method |
|-----------|--------|--------|
| IA | Intuitive? Find what needed? | First-look labs, time-to-action |
| Density | Informed or overwhelmed? | Drill-down rate, satisfaction |
| Interaction | Learnable? Fast? Complete? | Triage rate/time, observation |
| Behavior | Scan path? First look? | Observation, heatmaps |
| Framing | Mental model? Calm/anxiety? | Lab probes, trust ratings |
| Completion | When "done"? Earned? | Confidence ratings, return freq |
| Temporal | Time-appropriate? Post-triage? | Multi-day Express, probes |

---

### Convergence (Simplified)

WoZ learnings from Track A are baked into Track B prototypes before the external panel sees them. Cross-track insights emerge through the prototype testing itself: Do people tolerate less detail when intelligence is accurate? Does trust build faster in certain frames? Which completion signal works when triage is reliable?

**Quality gate**: If Track A calibration isn't sufficient by Week 3, prototypes ship with curated data instead of WoZ-informed data. Track B is not blocked.

---

### Deployment & Infrastructure

- **Platform**: Vercel (personal account initially, work account when available)
- **Structure**: Single repo, each stimulus piece and prototype as its own route
- **Prototype delivery**: Mobile-first web apps running in mobile Safari via URL. Phone-only with viewport lock for Track B prototypes. Gauntlet stimulus (landing pages + walkthrough videos) viewable on any device.
- **dScout integration**: Missions link to Vercel-hosted URLs

---

## 4. Participant Structure — Three Groups

### Gauntlet cohorts (two parallel groups, dScout Express)

**Live Data Cohort:**
- Recruited via dScout, screened for email overwhelm
- Port their actual email data into the prototypes
- Provides contextual realism and data quality insights
- Intelligence output reflects current calibration state (rougher)

**Anonymized Sample Data Cohort:**
- Recruited via dScout, screened for email overwhelm
- Uses real, anonymized email data (not their own real-time data)
- Intelligence output curated to high-quality "eventual state"
- Represents the aspirational target for model performance

### Internal dogfood group (5 people)
- Handpicked, diverse email lives (parents, managers, ICs, subscription-heavy)
- Weekday cadence, 1-2 weeks
- Participate in Shadow Inbox WoZ
- Calibrate intelligence, build internal conviction
- Roll off after Track A completes

### External dScout panel (5-8 people)
- "Cold read" validation — no product vision knowledge
- Recruited via dScout, screened for email overwhelm
- Evaluate experience prototypes with pre-calibrated intelligence
- Signal: does this make sense to someone encountering it fresh?

**Screening criteria** (all dScout cohorts): High unread (1K+), multiple accounts, inbox stress, high daily volume, personal + professional mix

---

## 5. What Needs to Be Built in Claude Code

### Priority 0: Concept Gauntlet Stimulus Packages (4 concepts, two-cohort setup)

For each concept, two deliverables — configured to support both Gauntlet cohorts:

**A. Value Prop Landing Pages with Embedded Motion**
- Clean, compelling single-page sites with animated sections
- Headline + value prop description + 2-3 key screens with motion hints
- Animated sections show surface dynamics: transitions, breathing, density shifts
- Must communicate both the experience vision and the *feel* without full interaction
- Should feel like a real product launch page
- Built as standalone HTML/React, deployable for dScout embedding or linking

**B. Narrated Video Walkthroughs**
- Screen recordings of prototype or animated mockup with voiceover script
- Walk through a realistic morning email processing scenario
- All walkthroughs use the same persona (Busy Parent) for concept comparability
- ~60-90 seconds each
- Claude Code builds the visual substrate; Matt records voiceover

**Two-cohort data requirements:**
- **Live Data Cohort**: Prototypes must support importing/porting users' actual email data. Intelligence output runs against real data at current calibration state — expect rougher output with quirks and breaks.
- **Anonymized Sample Data Cohort**: Prototypes use pre-loaded real but anonymized email data. Intelligence output is curated to represent a high-quality "eventual state" — the aspirational target, not current calibration.

**Total Gauntlet deliverables: 8** (4 landing pages + 4 walkthroughs), each supporting two data modes

### Priority 1: WoZ Prompt Template System

**Input format**: Structured inbox description
- Email list (sender, subject, snippet, time)
- Participant priorities
- Accumulated life context
- Day/time context

**Output format**: Structured JSON for rendering
- Prioritized emails with micro-briefs
- Category assignments with category briefs
- Incoming/upcoming classification
- Topline "since last visit" brief
- Completion signal (parameterized by treatment condition)
- Reasoning layer (operator review only)

**Treatment variation support**: Parameter-driven across agency, completion, density, temporal framing. No operator judgment required for what to vary.

**Must be stress-tested in Week 1 before participants start.** Target: ≤10 min per participant processing time.

### Priority 2: Shadow Inbox Renderer

High-fidelity static view from WoZ output.
- Looks like a real product
- Personalized with participant email content
- Consistent visual language across participants
- Supports visual treatments for all WoZ variation dimensions
- Generatable quickly (within 1-2 hours of input)

### Priority 3: Interactive Prototypes (2-3 Gauntlet winners)

Full interactive prototypes for Track B. Research-owned, pre-TestFlight web apps.
- Curated sample data, 3-4 personas
- Deliberate positions across ALL design dimensions
- Mobile-first web app (runs in mobile Safari)
- Realistic volumes (30-50 emails/day)
- Completion state/signal included
- Self-contained for Express missions
- Instrumented: taps, scroll, time, drill-down, triage speed, return frequency
- Analytics baked in from day one — lightweight backend (Firebase/Supabase) or similar
- Serves as reference implementation for eventual eng handoff to native

### Priority 4: dScout Mission Design

**Gauntlet Express mission**:
- 2 concepts per day, full two-lens package each
- Post-landing-page: desire, excitement, concerns, feel
- Post-walkthrough: comprehension, confusion points, daily viability
- Post-package: real-inbox comparison, replacement viability, single biggest change needed

**Track A morning input**:
- Screenshot capture
- Voice narration: "Walk me through what's here. What's important? What's coming up?"
- Structured: top 3 priorities, upcoming this week, worried about missing

**Track A afternoon reaction**:
- Shadow Inbox presented
- Priority accuracy (scale + open)
- Misses (Y/N + what)
- Miscategorization (Y/N + what)
- Completion confidence (scale)
- Real-inbox comparison (open)
- Optional voice

**Track B Express**:
- Prototype interaction
- Real-inbox comparison narration
- Multi-dimensional: framing probe, density check, IA clarity, completion timing, open reaction, replacement viability

### Priority 5: Data & Analysis Infrastructure
- Participant tracking (submissions, compliance)
- WoZ accuracy over time
- Treatment variation log
- Behavioral instrumentation dashboards
- Design dimension signal matrix
- Gauntlet results dashboard (two-lens signal per concept)

---

## 6. Concept Directions (4 Gauntlet Candidates)

### The Morning Brief
Narrative-first. Reads like a personalized briefing. High density, low interaction demand. Incoming + upcoming woven by relevance. Completion = reaching the end. Frame: document you read.

### The Living Canvas
Spatial, visual. Category tiles/zones breathe by urgency. Priority via visual weight + position. Lower per-item density, higher spatial info. Triage through manipulation. Completion = visual calm. Frame: landscape you survey.

### The Two-Stack
Maximum simplicity. Two buckets: incoming + upcoming. Satisfying "lift" interaction. High density within stacks. Categories subordinate. Completion = incoming acknowledged. Frame: desk trays.

### The Chief of Staff
Maximum delegation. Handled / Needs You / FYI. System already decided. User reviews + overrides. Low interaction demand, high trust. Completion = "Needs You" cleared. Frame: assistant reporting.

---

## 7. Sample Data Architecture

### Gauntlet walkthroughs — single persona for comparability

All four walkthrough videos use **Persona 1: The Busy Parent** so participants compare the *concept*, not the *data*. Landing pages can be more generic.

### For Track B prototypes — full persona set

Each persona needs **incoming** (today's new) and **upcoming** (extracted obligations). Include realistic messiness.

**Persona 1: The Busy Parent**
- School (permission slips, teacher notes, PTA), activities (soccer, music), household (contractor, utilities), deliveries, medical, spouse-forwarded
- ~35 emails/day
- Upcoming: permission slip due Friday, dentist Tuesday, soccer carpool, mortgage auto-draft, contractor Thursday

**Persona 2: The Job Hunter**
- Recruiters, application status, interviews, current job (meetings, projects), LinkedIn, references
- ~40 emails/day
- Upcoming: phone screen Wednesday, reference deadline, project review Friday, benefits enrollment

**Persona 3: The Professional Manager**
- Direct reports, cross-functional threads, meeting agendas, HR/benefits, travel, clients
- ~50 emails/day
- Upcoming: all-hands prep, client deliverable, travel next week (hotel pending), perf review cycle

**Persona 4: The Life-in-Transition**
- Home purchase (mortgage, inspection, attorney), wedding, job transition, insurance, moving
- ~45 emails/day
- Upcoming: inspection report due, venue payment, first day new job, insurance deadline, moving truck

---

## 8. Timeline

| | Week 1 | Week 2 | Week 3 | Week 4 | Week 5 |
|---|---|---|---|---|---|
| **Gauntlet** | Build 8 stimulus pieces + two-cohort data setup (live data integration + curated anonymized data) | Two-cohort dScout Express runs (live data + anonymized sample data), synthesize cross-cohort, refinement briefs | — | — | — |
| **Track A** | Build + stress-test WoZ prompt template, recruit 5 dogfooders | Begin daily WoZ (weekdays, 5 participants) | WoZ continues, vary treatments, roll off | — | — |
| **Track B** | — | — | Build prototypes from Gauntlet winners + WoZ learnings | dScout panel + moderated labs | Refine, synthesize, conviction deck |

---

## 9. Week 5 Deliverables — Two Distinct Outputs

1. **Experience direction deck**: "Here are the 2 strongest directions and what each needs to become a product." Funnel narrowing with data for cross-functional leadership (research, design, eng, PM, leadership).
2. **Intelligence readiness assessment**: "Can our team build this, or do we need vendor help?" Go/no-go on capability with accuracy trajectory, failure mode analysis, and build-vs-vendor recommendation.

The prototype itself is a deliverable for eng — a working reference implementation with analytics schema, not a Figma file to interpret.

---

## 10. Key Decisions Still Needed

- [ ] Final concept definitions for 4 Gauntlet candidates (detailed enough to build from)
- [ ] Which 5 internal dogfooders?
- [ ] External panel budget and screening criteria
- [ ] Design dimension matrix — positions per prototype
- [ ] Eng handoff model (pre-TestFlight web proto → native port)
- [ ] Instrumentation spec for behavioral capture

---

## 11. Reference: Mail Premium Feature Strategy

- **Life Graph**: LLM model of user's life powering everything
- **Briefs**: AI context at every scale (micro, thread, category, daily)
- **Dynamic Categories**: Personal groupings, appear/fade dynamically
- **Home Surface**: New primary screen — THIS IS WHAT WE'RE RESEARCHING
- **Generative Search**: Natural language search
- **Inbox Rescue**: One-time cleanup, a la carte, on-ramp to Premium
- **Chief of Staff Agent**: Agentic assistant (long-term, patent pending)
