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

**Goal**: Go wide before going deep. Take 4 distinct experience visions, run through rapid evaluation, identify which 2-3 deserve full prototype builds.

**The Two-Lens Stimulus Package**: Each concept expressed through two complementary lenses:

1. **Value Prop Landing Page with Embedded Motion**: The promise in plain language + animated sections showing surface dynamics. Headline, description, key screens with motion that hints at behavior. Tests "would I want this?" and "does it feel right?" in a single artifact. Built as standalone HTML/React, deployable for dScout embedding or linking.

2. **Narrated Video Walkthrough**: Screen-recorded walkthrough of realistic scenario with voiceover. Full morning email processing session with sample data. Tests logic and flow — does the sequence make sense? ~60-90 seconds each. Claude Code builds the visual substrate; Matt records voiceover.

**Why two lenses**: They test different things and may produce divergent signal:
- Landing page resonance ≠ walkthrough clarity (communication problem, not concept problem)
- Walkthrough clarity ≠ landing page resonance (positioning problem, not design problem)
- These divergences tell you what to *fix* as concepts become prototypes

**Evaluation**: dScout Express mission. 2 concepts/day over 2 days. After each concept:
- After landing page: "Would you want this? What excites you? What worries you? How does it feel?"
- After walkthrough: "Does this make sense? Where lost? Could you do this every morning?"
- After full package: "Compared to real inbox, better? Would this replace current email? Single biggest thing to change?"

**Gauntlet output feeds Track B**:
- 2-3 concepts advanced to full prototype builds
- Design dimension priorities (which dimensions mattered most to participants)
- Concept refinement briefs (what worked, what needs to change per advancing concept)

**Timing**: Weeks 1-2.

---

### Track A — Intelligence Calibration (Shadow Inbox + WoZ)

**Goal**: Calibrate Life Graph judgment quality through daily WoZ simulation. This is a calibration sprint (1-2 weeks), not an extended study.

**Method**: The Shadow Inbox — participants keep real inbox, receive daily simulated Home Surface view for comparison.

**Participants**: 5 internal dogfooders, weekdays only.

**Recruitment criteria for the 5** (each participant is high-value — choose carefully):
- Genuine email diversity (not 5 PMs with identical inboxes)
- High daily volume (enough signal for WoZ to work with)
- Reliable — will actually screenshot and narrate every morning
- Internal credibility — their eventual advocacy carries weight

**Daily cycle**:
1. **Morning input** (participant, ~5 min): dScout diary — screenshots, voice narration, structured priority/upcoming fields
2. **WoZ processing** (Matt, ~8-15 min/participant): Claude prompt template → simulated output → rendered mockup. Batch all participants after a morning cutoff to minimize context-switching.
3. **Shadow Inbox delivery** (within 1-2 hours): Personalized view while morning context fresh
4. **Afternoon reaction** (participant, ~3-5 min): dScout evaluation — accuracy, misses, categorization, completion

**WoZ treatment variations** (within-subjects, varied on select days):
- **Agency**: Aggressive (handled + receipts) vs. Conservative (everything + priority tiers)
- **Completion**: Progress indicator vs. affirmative statement vs. countdown vs. no signal
- **Density**: Full micro-briefs per item vs. category summaries only
- **Temporal**: Morning-optimized vs. catch-up vs. unified

**Metrics**: Priority accuracy (~80% target), miss rate, trust trajectory, completion effectiveness, density preference

**Intelligence readiness gate**: Track A isn't just tuning the prompt — it produces evidence about whether the intelligence layer is feasible in-house. Key outputs:
- Priority accuracy trajectory over the 1-2 weeks (improving? plateauing? stuck?)
- Failure mode breakdown (missing context? wrong categories? bad prioritization?) — determines if gaps are solvable with tuning or fundamental
- Honest comparison: what a well-prompted frontier LLM can do today vs. what the product needs
- **Recommendation: build in-house vs. bring in vendor consultation**

If after 1-2 weeks of daily iteration accuracy is stuck well below threshold, that's the alarm bell for bringing in outside help.

**This group rolls off after 1-2 weeks.** Their purpose is to calibrate the intelligence and build internal conviction. WoZ learnings get baked into the prototypes that the external panel evaluates.

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

## 4. Participant Structure — Two Groups, Sequential

### Internal dogfood group (5 people)
- Handpicked, diverse email lives (parents, managers, ICs, subscription-heavy)
- Weekday cadence, 1-2 weeks
- Participate in Gauntlet reactions + Shadow Inbox WoZ
- Calibrate intelligence, build internal conviction
- Roll off after Track A completes

### External dScout panel (5-8 people)
- "Cold read" validation — no product vision knowledge
- Recruited via dScout, screened for email overwhelm
- Evaluate experience prototypes with pre-calibrated intelligence
- Signal: does this make sense to someone encountering it fresh?

**Screening criteria**: High unread (1K+), multiple accounts, inbox stress, high daily volume, personal + professional mix

---

## 5. What Needs to Be Built in Claude Code

### Priority 0: Concept Gauntlet Stimulus Packages (4 concepts)

For each concept, two deliverables:

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

**Total Gauntlet deliverables: 8** (4 landing pages + 4 walkthroughs)

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
| **Gauntlet** | Build 8 stimulus pieces (4 landing pages + 4 walkthroughs) | dScout Express runs, synthesize, refinement briefs | — | — | — |
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
