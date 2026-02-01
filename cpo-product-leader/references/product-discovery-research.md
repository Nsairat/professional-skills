# Product Discovery & User Research

## Discovery Framework

### Continuous Discovery Habits

```
┌─────────────────────────────────────────────────────────────────┐
│                   Continuous Discovery                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│                    Weekly Customer Touchpoint                    │
│                              │                                   │
│         ┌────────────────────┼────────────────────┐             │
│         │                    │                    │             │
│    ┌────▼────┐         ┌─────▼────┐        ┌─────▼────┐        │
│    │ Customer│         │ Prototype│        │ Assumption│        │
│    │ Interview│        │ Testing  │        │ Testing   │        │
│    └─────────┘         └──────────┘        └──────────┘        │
│         │                    │                    │             │
│         └────────────────────┼────────────────────┘             │
│                              │                                   │
│                     ┌────────▼────────┐                         │
│                     │ Update Opportunity│                        │
│                     │ Solution Tree    │                         │
│                     └─────────────────┘                         │
└─────────────────────────────────────────────────────────────────┘
```

### Opportunity Solution Tree

```
                         ┌─────────────┐
                         │   Desired   │
                         │   Outcome   │
                         └──────┬──────┘
                                │
           ┌────────────────────┼────────────────────┐
           │                    │                    │
    ┌──────▼──────┐     ┌───────▼──────┐    ┌───────▼──────┐
    │ Opportunity │     │ Opportunity  │    │ Opportunity  │
    │      A      │     │      B       │    │      C       │
    └──────┬──────┘     └──────────────┘    └──────────────┘
           │
    ┌──────┼──────┐
    │      │      │
┌───▼──┐ ┌─▼───┐ ┌▼────┐
│Sol 1 │ │Sol 2│ │Sol 3│
└──────┘ └─────┘ └─────┘
    │
┌───▼──────┐
│Experiment│
└──────────┘
```

---

## User Research Methods

### Research Method Selection

| Method | Best For | Time | Fidelity |
|--------|----------|------|----------|
| **User Interviews** | Deep understanding, why | 1-2 weeks | High |
| **Surveys** | Quantitative validation | 1-2 weeks | Medium |
| **Usability Testing** | UX problems | Days | High |
| **A/B Testing** | Optimization | 1-4 weeks | Very High |
| **Analytics** | Behavior patterns | Ongoing | Very High |
| **Card Sorting** | Information architecture | Days | Medium |
| **Diary Studies** | Long-term behavior | Weeks | High |
| **Field Studies** | Context understanding | Days | Very High |

### User Interview Guide

**Structure (60 minutes)**

```
1. Introduction (5 min)
   - Thank you, context, permission to record
   - "There are no wrong answers"
   - Explain you want to learn, not sell

2. Background (10 min)
   - Role, responsibilities
   - Current tools and processes
   - Day in the life

3. Problem Exploration (20 min)
   - "Tell me about the last time you..."
   - "What's the hardest part about..."
   - "How do you currently solve..."
   - Follow the energy, dig deeper

4. Solution Exploration (15 min)
   - Show prototype/concept (if applicable)
   - "What would you expect to happen..."
   - "How would this fit into your workflow..."
   - Note confusion, delight, skepticism

5. Wrap-up (10 min)
   - "Is there anything I should have asked?"
   - "Who else should I talk to?"
   - Thank you, next steps
```

**Interview Best Practices**
- Shut up and listen (aim for 80% them, 20% you)
- Ask "why" 5 times
- Follow their language, not yours
- Watch for body language and emotion
- Don't pitch or defend
- Record (with permission) and transcribe

### Jobs to Be Done (JTBD) Framework

**Job Statement Format**
```
When [situation], I want to [motivation], so I can [expected outcome].

Example:
When I'm onboarding a new customer,
I want to quickly set up their account correctly,
So I can get them to value fast and reduce churn risk.
```

**JTBD Interview Questions**
1. When did you first realize you needed something like this?
2. What were you doing/using before?
3. What made you start looking for alternatives?
4. What did you Google? Who did you ask?
5. Walk me through the moment you decided to try [solution]
6. What almost stopped you from switching?
7. What's better now? What's worse?

**Forces Diagram**
```
┌─────────────────────────────────────────────────────────────────┐
│                    Forces of Progress                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│                    ┌─────────────────┐                          │
│     PUSH           │                 │         PULL             │
│  (Current Pain)    │     CHANGE      │    (New Solution)        │
│       ───────────► │                 │ ◄───────────             │
│                    │                 │                          │
│     ANXIETY        │                 │        HABIT             │
│  (Fear of New)     │                 │   (Status Quo)           │
│       ◄─────────── │                 │ ───────────►             │
│                    └─────────────────┘                          │
│                                                                  │
│  Change happens when Push + Pull > Anxiety + Habit              │
└─────────────────────────────────────────────────────────────────┘
```

---

## Validation Methods

### Fake Door Testing

**How It Works**
1. Create UI for feature that doesn't exist
2. Measure clicks/signups/interest
3. Show "coming soon" message
4. Collect email for waitlist
5. Validate demand before building

**Use Cases**
- New feature validation
- Pricing page options
- Market segment testing
- Partnership interest

### Concierge MVP

**How It Works**
1. Manually deliver the service/value
2. No (or minimal) technology
3. Learn exactly what users need
4. Validate willingness to pay
5. Discover edge cases

**Example**
- Food delivery: Founder personally delivers
- Marketplace: Manually match buyers/sellers
- SaaS tool: Spreadsheet + human process

### Wizard of Oz

**How It Works**
1. Users interact with "product"
2. Behind the scenes: humans do the work
3. Users think it's automated
4. Test the experience, not the technology

**When to Use**
- AI/ML features (can a human do it first?)
- Complex automation
- Expensive to build, need to validate

### Smoke Test

**How It Works**
1. Landing page describing product
2. Clear call-to-action (signup, pre-order, pay)
3. Measure conversion
4. Validate market demand

**Success Metrics**
- Page visit → Signup: >10% = strong signal
- Signup → Waitlist email open: >50%
- Pre-order with payment: Ultimate validation

---

## User Personas

### Persona Template

```
┌─────────────────────────────────────────────────────────────────┐
│  Persona: [Name]                               [Photo/Avatar]   │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Demographics                     Psychographics                 │
│  ├── Role: [Title]               ├── Goals: [What they want]    │
│  ├── Company size: [X]           ├── Frustrations: [Pain points]│
│  ├── Industry: [Y]               ├── Motivations: [Why]         │
│  └── Tech savviness: [1-5]       └── Values: [What matters]     │
│                                                                  │
│  Day in the Life                                                 │
│  "Describe a typical day for this persona..."                   │
│                                                                  │
│  Key Quote                                                       │
│  "[Something they said in research that captures them]"         │
│                                                                  │
│  Jobs to Be Done                                                 │
│  1. [Primary JTBD]                                              │
│  2. [Secondary JTBD]                                            │
│  3. [Tertiary JTBD]                                             │
│                                                                  │
│  Current Solutions                Product Requirements           │
│  ├── [Tool 1]                    ├── Must have: [X]             │
│  ├── [Tool 2]                    ├── Should have: [Y]           │
│  └── Workarounds                 └── Nice to have: [Z]          │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Persona Anti-Patterns

**Avoid**
- Too many personas (max 3-4)
- Personas based on demographics only
- Personas no one uses
- Personas without real research backing
- Static personas never updated

**Instead**
- Focus on behaviors and jobs
- Base on actual user interviews
- Refer to them in decision-making
- Update as you learn more
- Make them memorable and specific

---

## Usability Testing

### Usability Test Script

**Introduction (5 min)**
```
"Thanks for being here today. I'm [name], and I'm going to 
show you something we're working on. I want to emphasize:
- We're testing the design, not you
- There are no wrong answers
- Please think out loud
- I may ask 'what are you thinking?' a lot
- Your honest feedback helps us improve
Any questions before we start?"
```

**Tasks (30-40 min)**
```
Task format:
"Imagine you want to [scenario]. Using this prototype,
please try to [specific action]. Remember to think out loud."

Good tasks:
- Realistic scenarios
- Specific but not leading
- Achievable (most should succeed)
- Ordered by flow

Track:
- Task success (yes/no/partial)
- Time to complete
- Errors made
- Assistance needed
- Verbal feedback
```

**Debrief (10 min)**
```
"Now that you've tried everything..."
- What was your overall impression?
- What was most confusing?
- What was easiest?
- Would you use this? Why/why not?
- On a scale of 1-10, how easy was this to use?
```

### Usability Metrics

| Metric | Description | Target |
|--------|-------------|--------|
| Task Success Rate | % who complete task | >80% |
| Time on Task | Seconds to complete | Depends on task |
| Error Rate | Mistakes per task | <1 |
| SUS Score | System Usability Scale | >68 (above average) |
| Satisfaction | Post-task rating | >4/5 |

### System Usability Scale (SUS)

**10 Questions (Agree 1-5)**
1. I would use this frequently
2. It's unnecessarily complex (-)
3. It was easy to use
4. I'd need tech support (-)
5. Functions well integrated
6. Too much inconsistency (-)
7. Most would learn quickly
8. Very cumbersome (-)
9. I felt confident using it
10. Steep learning curve (-)

**Scoring**
- Odd questions: Score - 1
- Even questions: 5 - Score
- Sum all, multiply by 2.5
- Result: 0-100 scale

**Interpretation**
- <50: Unacceptable
- 50-70: Marginal
- 70-85: Good
- 85+: Excellent

---

## Analytics & Quantitative

### Key Behavioral Metrics

**Engagement**
- DAU / MAU ratio (stickiness)
- Session frequency
- Session duration
- Feature adoption %
- Depth of engagement

**Retention**
- D1, D7, D30 retention
- Cohort retention curves
- Resurrection rate
- Churn rate

**Conversion**
- Funnel conversion rates
- Time to convert
- Conversion by segment
- Free to paid rate

### Cohort Analysis

```
          Week 0   Week 1   Week 2   Week 3   Week 4
Jan Cohort  100%     65%      45%      40%      38%
Feb Cohort  100%     70%      50%      45%      43%
Mar Cohort  100%     75%      55%      50%      48%

Reading: Mar cohort retains better at every stage
Signal: Something improved in product/onboarding
```

### Event Tracking Best Practices

**Naming Convention**
```
[Object]_[Action]_[Context]

Examples:
- user_signup_completed
- article_viewed_homepage
- checkout_abandoned_payment
- feature_activated_onboarding
```

**Properties to Capture**
- User ID (if logged in)
- Timestamp
- Session ID
- Device/platform
- Relevant context (page, referrer)
- Feature-specific properties

**Key Events to Track**
1. Signup / Account creation
2. Onboarding completion
3. Core action (aha moment)
4. Conversion (upgrade, purchase)
5. Retention actions (return visits, repeat purchase)
6. Churn signals (downgrade, cancel)
