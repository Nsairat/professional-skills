# Startup Playbook — Zero to Scale

## Stage 0: Idea & Validation

### Idea Evaluation Framework

**Market Factors**
| Factor | Question | Score (1-5) |
|--------|----------|-------------|
| Market Size | Is TAM > $1B? | |
| Growth | Is market growing >20% YoY? | |
| Timing | Why now? (Technology, regulation, behavior shift) | |
| Competition | Is it fragmented or dominated? | |

**Team Factors**
| Factor | Question | Score (1-5) |
|--------|----------|-------------|
| Founder-Market Fit | Do you have unique insight/experience? | |
| Technical Capability | Can you build this? | |
| Sales Capability | Can you sell this? | |
| Commitment | All-in for 7-10 years? | |

**Product Factors**
| Factor | Question | Score (1-5) |
|--------|----------|-------------|
| Problem Severity | Hair on fire problem? | |
| Frequency | Daily/weekly use case? | |
| Monetization | Clear path to revenue? | |
| Defensibility | Can you build a moat? | |

### Customer Discovery (4 Weeks)

**Week 1-2: Problem Interviews (20+)**
```
Goal: Validate the problem exists and matters

Questions:
- "Tell me about [problem domain]..."
- "What's the hardest part about [activity]?"
- "How are you solving this today?"
- "How much time/money does this cost you?"
- "If you could wave a magic wand..."

Signals to look for:
✓ Emotional response (frustration, pain)
✓ Active workarounds
✓ Spending money on bad solutions
✓ Multiple people mention same problem
```

**Week 3-4: Solution Interviews (10+)**
```
Goal: Validate solution concept resonates

Show:
- Concept description (not prototype)
- Value proposition
- How it works (high level)

Questions:
- "Does this solve your problem?"
- "What would you expect it to do?"
- "What's missing?"
- "Would you pay for this?"
- "What would you pay?"
```

---

## Stage 1: Pre-Product Market Fit (0-1)

### Building the MVP

**MVP Checklist**
- [ ] Solves ONE core problem
- [ ] Measurable value delivered
- [ ] Can be built in 4-8 weeks
- [ ] Users can onboard without help
- [ ] Core metrics can be tracked
- [ ] Path to monetization visible

**MVP Scope Decision**
```
Start with:
"What is the MINIMUM we need to test our core hypothesis?"

NOT:
"What's a basic version of our full vision?"

Cut:
- Nice-to-have features
- Edge cases
- Polish and design details
- Scalability concerns
- Most integrations

Keep:
- Core value loop
- Essential onboarding
- Basic analytics
- Feedback mechanism
```

### Finding Early Adopters

**Ideal Early Adopter Profile**
1. Has the problem acutely
2. Knows they have the problem
3. Actively seeking solutions
4. Has budget/authority to buy
5. Willing to give feedback
6. Forgiving of rough edges

**Where to Find Them**
- Communities (Reddit, Discord, Slack groups)
- Industry events and conferences
- LinkedIn outreach
- Existing networks
- Adjacent product users
- Content marketing
- Product Hunt, Hacker News

**Outreach Template**
```
Subject: Quick question about [their problem domain]

Hi [Name],

I noticed you're [relevant context from their profile].

I'm working on [one-sentence description of what you're building].
We're looking for early feedback from people who [describe their situation].

Would you be open to a 20-minute call this week? 
I'd love to understand how you currently handle [problem].

No pitch - just learning.

[Your name]
```

### Measuring PMF Progress

**Weekly Tracking Dashboard**
```
┌────────────────────────────────────────────────────────────────┐
│                   Pre-PMF Metrics                               │
├────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Acquisition           │  Activation           │  Engagement   │
│  ───────────           │  ──────────           │  ──────────   │
│  Signups: X            │  Completed onboard: X%│  DAU: X       │
│  Source: Y             │  Time to value: X min │  WAU/MAU: X%  │
│  WoW growth: X%        │  Aha moment: X%       │  Retention: X%│
│                        │                       │               │
│  Qualitative           │  Revenue              │  NPS          │
│  ───────────           │  ───────              │  ───          │
│  User calls: X         │  MRR: $X              │  Score: X     │
│  Key feedback themes   │  Paying users: X      │  Promoters: X%│
│  - Theme 1             │  Conversion: X%       │  Detractors: X│
│  - Theme 2             │                       │               │
└────────────────────────────────────────────────────────────────┘
```

**Sean Ellis Test**
```
"How would you feel if you could no longer use [product]?"

A) Very disappointed
B) Somewhat disappointed  
C) Not disappointed
D) N/A - no longer use

PMF threshold: >40% "Very disappointed"

Track weekly and segment by:
- Activation status
- Usage frequency
- Customer segment
```

### Iteration Cadence

**Weekly Cycle (Pre-PMF)**
```
Monday:    Review metrics, plan sprint
Tuesday:   Build
Wednesday: Build  
Thursday:  Ship, start user testing
Friday:    User interviews, analyze, plan

Key rules:
- Ship something every week
- Talk to users every week
- Review metrics every week
- Make one bet per sprint
```

---

## Stage 2: Post-PMF Scaling (1-N)

### Signs You've Hit PMF

**Strong Signals**
- Organic growth (word of mouth)
- Demand exceeds capacity
- Users find new use cases
- Low churn (<5% monthly)
- High NPS (>50)
- Competition copying you
- Inbound investor interest

**Weak Signals**
- Growth only from paid acquisition
- High churn requiring constant replacement
- Users need convincing
- Features don't move metrics
- Flat or declining engagement

### Scaling the Product

**What Changes Post-PMF**

| Aspect | Pre-PMF | Post-PMF |
|--------|---------|----------|
| Goal | Find what works | Scale what works |
| Speed | Fast, scrappy | Fast, sustainable |
| Quality | Good enough | Production-grade |
| Tech Debt | Acceptable | Must address |
| Team | Small, generalist | Growing, specialized |
| Process | Minimal | Structured |
| Features | Test many | Double down on winners |

### Growth Model

**Growth Equation**
```
Growth = Acquisition × Activation × Retention × Monetization × Referral

Focus on highest-leverage factor:
- Leaky bucket? → Fix retention first
- Low conversion? → Fix activation
- Great retention? → Scale acquisition
```

**Growth Loops**

**Viral Loop**
```
User → Invites Others → Others Join → Invite More
           │                              │
           └──────────────────────────────┘

Metrics: Viral coefficient (K), cycle time
K > 1 = exponential growth
```

**Content Loop**
```
User → Creates Content → Content Indexed → New User Finds → User
           │                                                  │
           └──────────────────────────────────────────────────┘

Metrics: Content created, SEO ranking, conversion from content
```

**Paid Loop**
```
Acquire User → User Pays → Reinvest Revenue → Acquire More
      │                                            │
      └────────────────────────────────────────────┘

Metrics: CAC, LTV, payback period
LTV/CAC > 3 = healthy
```

### Scaling the Team

**Product Team Growth**

| Users | Product Team Size | Structure |
|-------|-------------------|-----------|
| 0-10K | 1-2 PMs | Founders + first PM |
| 10K-100K | 3-5 PMs | Add specializations |
| 100K-1M | 5-10 PMs | Feature teams |
| 1M+ | 10-20+ PMs | Multiple product lines |

**When to Hire**

| Role | Trigger | What to Look For |
|------|---------|------------------|
| First PM | Founder can't do it all | Generalist, startup DNA |
| Growth PM | Acquisition is priority | Data-driven, experimentation |
| Platform PM | Platform emerging | Technical, ecosystem thinking |
| PM Manager | 4+ PMs | Coaching, scaling experience |

---

## Stage 3: Market Leadership

### Expanding the Product

**Expansion Strategies**

| Strategy | Description | Risk | Example |
|----------|-------------|------|---------|
| **Go Deeper** | More features for same users | Low | Slack → Workflows |
| **Go Broader** | Same product, adjacent segments | Medium | Zoom → Enterprise |
| **Go Adjacent** | New product for same users | Medium | Shopify → Payments |
| **Go New** | New product, new market | High | Amazon → AWS |

### Platform Evolution

**Product to Platform Journey**
```
Stage 1: Single Product
- One product, one segment
- Direct value creation

Stage 2: Product Suite  
- Multiple products
- Integrated experience
- Cross-sell opportunities

Stage 3: Platform
- Third-party integrations
- Developer ecosystem
- Network effects

Stage 4: Ecosystem
- Multiple business models
- Partner revenue sharing
- Industry standard
```

### Competitive Strategy

**Porter's Generic Strategies**

```
                    Strategic Advantage
                Uniqueness    Low Cost
           ┌─────────────┬─────────────┐
   Broad   │Differentiation│ Cost       │
   Target  │              │ Leadership │
           ├─────────────┼─────────────┤
   Narrow  │   Focus     │   Focus     │
   Target  │(Differentiation)│ (Cost)  │
           └─────────────┴─────────────┘
```

**Competitive Response Framework**

| Their Move | Our Response Options |
|------------|---------------------|
| Copy our features | Innovate faster, focus on UX |
| Lower prices | Add value, focus on segments that value quality |
| Enter our market | Double down on strengths, raise switching costs |
| Acquire competitor | Partner with others, accelerate roadmap |

---

## Fundraising & Investor Relations

### Stage-Appropriate Metrics

**Pre-Seed / Seed**
- Qualitative: User interviews, feedback themes
- Early signals: Waitlist size, prototype engagement
- Team: Founder backgrounds, commitment

**Series A**
- PMF evidence: Retention, NPS, Sean Ellis test
- Early traction: MRR/ARR, growth rate
- Unit economics: Early LTV/CAC signals

**Series B**
- Growth: ARR, MoM/YoY growth rate
- Efficiency: Burn multiple, magic number
- Market: TAM penetration, competitive position

**Series C+**
- Scale: Revenue, growth, market share
- Profitability path: Margins, efficiency
- Moat: Network effects, switching costs

### Pitch Deck Structure

**10-15 Slides**
1. **Title**: Company name, one-liner
2. **Problem**: Pain point (make it feel real)
3. **Solution**: How you solve it
4. **Demo/Product**: Show, don't tell
5. **Traction**: Metrics and growth
6. **Market**: TAM, SAM, SOM
7. **Business Model**: How you make money
8. **Competition**: Why you win
9. **Team**: Why you're the ones
10. **Roadmap**: Where you're going
11. **Financials**: Revenue, burn, projections
12. **Ask**: How much, for what

### Board Management

**Board Meeting Cadence**
- Frequency: Monthly (early) to Quarterly (later)
- Duration: 2-4 hours
- Materials: Sent 3-5 days ahead

**Board Deck Template**
```
1. Highlights & Lowlights (1 slide)
2. Key Metrics Dashboard (1-2 slides)
3. Product Update (2-3 slides)
4. Go-to-Market Update (2-3 slides)
5. Team & Org (1 slide)
6. Financial Update (2-3 slides)
7. Strategic Discussion Topic (2-3 slides)
8. Asks / Decisions Needed (1 slide)
```

**Investor Updates (Monthly)**
```
Subject: [Company] Monthly Update - [Month Year]

🎯 Key Metrics
- ARR: $X (+Y% MoM)
- Customers: X
- Burn: $X/month
- Runway: X months

✅ Wins
- [Highlight 1]
- [Highlight 2]

⚠️ Challenges
- [Challenge 1 + what we're doing]

🙏 Asks
- [Specific ask with context]

📅 Next Month Focus
- [Priority 1]
- [Priority 2]
```
