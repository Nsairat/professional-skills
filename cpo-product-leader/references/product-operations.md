# Product Operations & Processes

## Product Development Lifecycle

### End-to-End Process

```
┌─────────────────────────────────────────────────────────────────┐
│                Product Development Lifecycle                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  DISCOVER        DEFINE         BUILD          LAUNCH           │
│  ───────         ──────         ─────          ──────           │
│                                                                  │
│  • Research      • PRD/Spec     • Development  • GTM            │
│  • Ideation      • Design       • QA           • Enablement     │
│  • Validation    • Scoping      • Beta         • Launch         │
│                  • Planning                    • Monitor        │
│                                                                  │
│      2-4 weeks    2-4 weeks      4-12 weeks    1-2 weeks       │
│                                                                  │
│  Gate: Problem   Gate: Solution Gate: Quality Gate: Success     │
│  validated       validated      approved      measured          │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Stage Gates

**Discovery → Definition Gate**
- [ ] Problem validated with user research
- [ ] Opportunity sized (potential impact)
- [ ] Strategic alignment confirmed
- [ ] Initial success metrics defined
- [ ] Stakeholder buy-in obtained

**Definition → Build Gate**
- [ ] PRD/Spec reviewed and approved
- [ ] Design completed and reviewed
- [ ] Technical design reviewed
- [ ] Scope finalized
- [ ] Sprint plan created
- [ ] Dependencies identified

**Build → Launch Gate**
- [ ] Feature complete
- [ ] QA passed
- [ ] Performance acceptable
- [ ] Security review passed
- [ ] Beta feedback addressed
- [ ] Launch plan ready
- [ ] Support trained

---

## Product Requirements Document (PRD)

### PRD Template

```markdown
# [Feature Name] PRD

## Overview
**Author**: [PM Name]
**Status**: [Draft | In Review | Approved]
**Last Updated**: [Date]

## Problem Statement
[What problem are we solving? For whom? Why now?]

## Goals & Success Metrics
| Goal | Metric | Target |
|------|--------|--------|
| [Goal 1] | [Metric] | [Target] |
| [Goal 2] | [Metric] | [Target] |

## User Stories
As a [user type], I want to [action] so that [benefit].

### Primary User Stories
1. [Story 1]
2. [Story 2]

### Secondary User Stories
1. [Story 1]

## Functional Requirements
### Must Have (P0)
- [ ] [Requirement 1]
- [ ] [Requirement 2]

### Should Have (P1)
- [ ] [Requirement 1]

### Nice to Have (P2)
- [ ] [Requirement 1]

## Non-Functional Requirements
- Performance: [Requirements]
- Security: [Requirements]
- Accessibility: [Requirements]

## Design
[Link to Figma/designs]

## Technical Considerations
[Architecture notes, API changes, migrations]

## Dependencies
| Dependency | Owner | Status |
|------------|-------|--------|
| [Dep 1] | [Team] | [Status] |

## Timeline
| Milestone | Date |
|-----------|------|
| Design complete | [Date] |
| Dev complete | [Date] |
| Beta | [Date] |
| Launch | [Date] |

## Open Questions
- [ ] [Question 1]
- [ ] [Question 2]

## Out of Scope
- [What we're NOT doing]

## Appendix
[Additional context, research, data]
```

---

## Sprint & Roadmap Planning

### Sprint Planning

**Two-Week Sprint Structure**
```
Week 1:
├── Monday: Sprint kickoff (30 min)
├── Daily: Standup (15 min)
├── Wednesday: Mid-sprint check
└── Friday: Demo prep

Week 2:
├── Daily: Standup (15 min)
├── Thursday: Sprint demo (30 min)
├── Friday AM: Retrospective (45 min)
└── Friday PM: Next sprint planning (1-2 hrs)
```

**Sprint Planning Process**
1. Review sprint goals (PM presents)
2. Review backlog items
3. Estimate and commit
4. Identify dependencies
5. Assign owners
6. Confirm capacity

### Roadmap Planning

**Quarterly Planning Process**
```
Week -4: Input gathering
├── Business goals review
├── Customer feedback synthesis
├── Technical debt assessment
└── Competitive analysis

Week -3: Strategy alignment
├── OKR draft
├── Theme identification
└── Resource assessment

Week -2: Roadmap draft
├── Initiative prioritization
├── Dependency mapping
└── Timeline estimation

Week -1: Review and approval
├── Leadership review
├── Cross-functional alignment
└── Final adjustments

Week 0: Kickoff
├── Team communication
├── Sprint planning
└── Stakeholder updates
```

### Roadmap Formats

**Timeline Roadmap (External)**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Q1           Q2           Q3           Q4    │
├─────────────────────────────────────────────────────────────────┤
│ Theme A        ▓▓▓▓▓▓▓▓▓▓                                      │
│ Theme B                    ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓                    │
│ Theme C                                    ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  │
└─────────────────────────────────────────────────────────────────┘

Note: Themes, not features. Loose timing. Sets expectations without over-committing.
```

**Now/Next/Later (Internal)**
```
NOW (This Quarter)        NEXT (Next Quarter)      LATER (Future)
─────────────────        ─────────────────        ─────────────
✓ Initiative A           • Initiative D           • Initiative G
✓ Initiative B           • Initiative E           • Initiative H
• Initiative C           • Initiative F           • Initiative I
```

---

## Agile Ceremonies

### Standup (Daily, 15 min)

**Format**
- What I did yesterday
- What I'm doing today
- Any blockers

**Anti-patterns**
- Status report to manager
- Problem-solving (take offline)
- Going over 15 minutes
- Skipping it

### Sprint Demo (Bi-weekly, 30-60 min)

**Structure**
1. Sprint goal reminder (2 min)
2. Demo working software (20-40 min)
3. Metrics update (5 min)
4. Q&A (5-10 min)
5. What's next preview (2 min)

**Best Practices**
- Show real product, not slides
- Tie back to user value
- Celebrate the team
- Invite stakeholders

### Retrospective (Bi-weekly, 45-60 min)

**Format Options**

**Start/Stop/Continue**
```
START doing:     STOP doing:      CONTINUE doing:
• [Action 1]     • [Action 1]     • [Action 1]
• [Action 2]     • [Action 2]     • [Action 2]
```

**4 L's**
```
LIKED:          LEARNED:         LACKED:         LONGED FOR:
• [Item]        • [Item]         • [Item]        • [Item]
```

**Sailboat**
```
         🏝️ Island (Goal)
              │
    Wind ☁️   │   ⚓ Anchor
  (Helping)   │   (Slowing)
              │
         ⛵ Team
```

**Action Items**
- Pick 1-2 actions per retro
- Assign owners
- Review at next retro

---

## Cross-Functional Collaboration

### PM + Engineering

**Healthy Dynamics**
- PM owns "what" and "why"
- Eng owns "how" and "when"
- Shared ownership of outcomes
- Mutual respect and trust

**Key Rituals**
| Ritual | Frequency | Purpose |
|--------|-----------|---------|
| 1:1 with Tech Lead | Weekly | Alignment, relationship |
| Backlog grooming | Weekly | Prepare upcoming work |
| Technical design review | As needed | Architecture decisions |
| Sprint planning | Bi-weekly | Commitment |
| Demo | Bi-weekly | Celebrate, align |

### PM + Design

**Collaboration Model**
```
┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│  TOGETHER          │  PM LEADS          │  DESIGN LEADS         │
│  ────────          │  ────────          │  ────────────         │
│  • User research   │  • Problem framing │  • UI design          │
│  • Journey mapping │  • Prioritization  │  • Prototypes         │
│  • Solution        │  • Requirements    │  • Usability testing  │
│    ideation        │  • Stakeholders    │  • Design system      │
│  • Success metrics │  • Go-to-market    │  • Visual polish      │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### PM + Data

**Partnership Areas**
1. Metrics definition
2. Experiment design
3. Analysis and insights
4. Dashboard creation
5. Data quality
6. Predictive modeling

**Key Questions to Data**
- What does the data say about [problem]?
- Can we build a dashboard for [metric]?
- Help me design an experiment for [hypothesis]
- What's driving the change in [metric]?
- What segments should we focus on?

---

## Launch Management

### Launch Tiers

| Tier | Description | Process |
|------|-------------|---------|
| **Tier 1** | Major launch, high visibility | Full GTM, exec review |
| **Tier 2** | Significant feature | Standard GTM, PM-led |
| **Tier 3** | Minor improvement | Lightweight, changelog |
| **Tier 4** | Bug fix/iteration | No announcement |

### Launch Checklist

**Pre-Launch (T-2 weeks)**
- [ ] Feature complete and QA'd
- [ ] Documentation written
- [ ] Support team trained
- [ ] Marketing assets ready
- [ ] Sales enablement complete
- [ ] Analytics tracking verified
- [ ] Rollout plan defined
- [ ] Rollback plan defined

**Launch Day**
- [ ] Feature flag enabled (staged rollout)
- [ ] Monitoring dashboards watched
- [ ] Support standing by
- [ ] Marketing published
- [ ] Internal announcement sent
- [ ] Social media posted

**Post-Launch (T+1 week)**
- [ ] Metrics reviewed
- [ ] User feedback collected
- [ ] Bugs triaged and fixed
- [ ] Retrospective conducted
- [ ] Success communicated

### Rollout Strategies

**Big Bang**
- All users at once
- Highest risk, fastest
- Use for low-risk changes

**Percentage Rollout**
```
Day 1: 1% of users
Day 3: 10% of users (if stable)
Day 5: 50% of users (if stable)
Day 7: 100% of users (if stable)
```

**Cohort Rollout**
- Beta users first
- Then power users
- Then all users

**Geographic Rollout**
- One region first
- Expand region by region
- Good for localization

---

## Product Metrics & Reporting

### Weekly Product Review

**Dashboard Components**
```
┌────────────────────────────────────────────────────────────────┐
│                   Weekly Product Metrics                        │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  NORTH STAR METRIC                    HEALTH METRICS           │
│  ──────────────────                   ──────────────           │
│  [Primary metric]                     DAU: X (+Y%)             │
│  Current: X                           WAU: X (+Y%)             │
│  Target: Y                            Retention: X%            │
│  WoW: +Z%                             NPS: X                   │
│                                                                 │
│  FUNNEL                               OKR PROGRESS             │
│  ──────                               ────────────             │
│  Visitors: X                          KR1: 65% ▓▓▓▓▓░░░       │
│  Signups: X (Y%)                      KR2: 40% ▓▓▓░░░░░       │
│  Activated: X (Y%)                    KR3: 80% ▓▓▓▓▓▓▓░       │
│  Paid: X (Y%)                                                   │
│                                                                 │
│  THIS WEEK                            NEXT WEEK                │
│  ─────────                            ─────────                │
│  ✓ Shipped feature A                  • Ship feature C         │
│  ✓ Ran experiment B                   • Launch beta D          │
│  • Experiment B results: +15%         • Complete research E    │
│                                                                 │
└────────────────────────────────────────────────────────────────┘
```

### Monthly Business Review

**Agenda (60-90 min)**
1. Key metrics review (15 min)
2. Product updates by area (30 min)
3. Customer insights (10 min)
4. Competitive landscape (10 min)
5. Roadmap progress (10 min)
6. Discussion / decisions (15 min)

### Quarterly Planning Review

**Template**
```
1. Last Quarter Reflection
   - What we said we'd do
   - What we actually did
   - What we learned
   - OKR scoring

2. Market & Customer Update
   - What changed in the market
   - Customer feedback themes
   - Competitive moves

3. This Quarter Plan
   - Strategic priorities
   - OKRs
   - Major initiatives
   - Resource allocation

4. Risks & Dependencies
   - Key risks
   - Cross-team dependencies
   - Asks
```
