# Monetization & Pricing Strategy

## Business Model Selection

### Business Model Canvas

```
┌─────────────────────────────────────────────────────────────────┐
│                    Business Model Canvas                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Key Partners     Key Activities    Value Prop     Customer     │
│  ───────────     ──────────────    ──────────     Relationships │
│                                                    ─────────────│
│  [Who helps      [What we do      [What unique   [How we        │
│   us deliver]     to deliver]      value]         engage]       │
│                                                                  │
│  Key Resources   ───────────────►  Channels                      │
│  ─────────────                     ────────                      │
│  [What we need]                    [How we reach]               │
│                                                                  │
├─────────────────────────────────────────────────────────────────┤
│  Cost Structure                    Revenue Streams               │
│  ──────────────                    ───────────────               │
│  [What we spend]                   [How we make money]          │
└─────────────────────────────────────────────────────────────────┘
```

### Common SaaS Business Models

| Model | How It Works | Best For |
|-------|--------------|----------|
| **Subscription** | Recurring fee (monthly/annual) | Most SaaS products |
| **Usage-Based** | Pay per use (API calls, storage) | Infrastructure, APIs |
| **Freemium** | Free tier + paid upgrades | PLG, large TAM |
| **Free Trial** | Full access, time-limited | Complex products |
| **Marketplace** | Take rate on transactions | Two-sided platforms |
| **Advertising** | Free product, sell attention | Consumer, media |
| **License** | One-time purchase | Enterprise software |

### Marketplace Economics

**Take Rate Benchmarks**

| Category | Typical Take Rate | Examples |
|----------|-------------------|----------|
| E-commerce | 10-20% | Amazon, Etsy |
| Services | 15-30% | Airbnb, Thumbtack |
| Food Delivery | 25-35% | DoorDash, Uber Eats |
| B2B Services | 5-15% | Upwork |
| Financial | 1-3% | Stripe, PayPal |

**Marketplace Health Metrics**

| Metric | Definition | Target |
|--------|------------|--------|
| GMV | Total transaction value | Growing |
| Net Revenue | GMV × Take Rate | Growing |
| Liquidity | % listings that transact | >15% |
| Repeat Rate | % users who transact again | >40% |
| Buyer/Seller Ratio | Balance of marketplace | Depends |

---

## Pricing Strategy

### Pricing Framework

```
┌─────────────────────────────────────────────────────────────────┐
│                    Pricing Strategy Framework                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. UNDERSTAND VALUE                                            │
│     └── What's the economic value to customer?                  │
│     └── What are alternatives and their costs?                  │
│     └── What's the willingness to pay?                          │
│                                                                  │
│  2. DEFINE PACKAGING                                            │
│     └── What features in each tier?                             │
│     └── What's the value metric?                                │
│     └── How do customers upgrade?                               │
│                                                                  │
│  3. SET PRICING                                                 │
│     └── What price points?                                      │
│     └── Annual vs monthly discount?                             │
│     └── Enterprise custom pricing?                              │
│                                                                  │
│  4. TEST & ITERATE                                              │
│     └── A/B test pricing pages                                  │
│     └── Measure conversion and revenue                          │
│     └── Gather feedback from lost deals                         │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Value-Based Pricing

**Steps to Determine Value-Based Price**

1. **Identify Economic Value**
   - Time saved × hourly cost
   - Revenue generated
   - Cost avoided
   - Risk reduced

2. **Calculate Customer ROI**
   ```
   Customer ROI = (Economic Value - Price) / Price
   
   Target: Customer gets 3-10x ROI
   Your price = Economic Value / (3 to 10)
   ```

3. **Validate with Research**
   - Van Westendorp Price Sensitivity
   - Conjoint analysis
   - Competitive comparison
   - Win/loss analysis

### Van Westendorp Price Sensitivity

**Ask 4 Questions**
1. At what price is this so cheap you'd doubt quality?
2. At what price is this a bargain—great value?
3. At what price is this getting expensive but still acceptable?
4. At what price is this too expensive to consider?

**Plot Results**
```
Price
  │
  │     ╱╲
  │    ╱  ╲     Acceptable
  │   ╱    ╲    Price Range
  │  ╱      ╲
  │ ╱        ╲
  └─────────────────────
       │    │
    Optimal  Point of
    Price    Marginal
             Cheapness
```

### Pricing Tiers

**Good/Better/Best Framework**

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────┐           │
│  │   STARTER   │   │    PRO      │   │ ENTERPRISE  │           │
│  │   $29/mo    │   │   $99/mo    │   │  Custom     │           │
│  │             │   │ MOST POPULAR│   │             │           │
│  │ ✓ Core      │   │ ✓ Everything│   │ ✓ Everything│           │
│  │ ✓ Limited   │   │   in Starter│   │   in Pro    │           │
│  │ ✓ Email     │   │ ✓ Advanced  │   │ ✓ Unlimited │           │
│  │   support   │   │ ✓ Priority  │   │ ✓ Dedicated │           │
│  │             │   │   support   │   │   support   │           │
│  │             │   │ ✓ API access│   │ ✓ Custom    │           │
│  │             │   │             │   │   integrations│         │
│  │             │   │             │   │ ✓ SLA       │           │
│  └─────────────┘   └─────────────┘   └─────────────┘           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

**Tier Design Principles**
1. **Clear differentiation**: Each tier has obvious value increase
2. **Anchor with middle**: Highlight middle tier as "best value"
3. **Decoy pricing**: Make middle tier look like best deal
4. **Feature fences**: Clear limits that drive upgrades
5. **Land and expand**: Easy entry, natural upgrade path

### Usage-Based Pricing

**Common Value Metrics**

| Product Type | Value Metric | Example |
|--------------|--------------|---------|
| Infrastructure | Compute/Storage | AWS, Snowflake |
| API | API calls | Twilio, Stripe |
| Communication | Messages/Minutes | Intercom |
| Analytics | Events/MTUs | Amplitude, Segment |
| Storage | GB stored | Dropbox |
| Seats | Users | Slack, Salesforce |

**Hybrid Model (Base + Usage)**
```
Monthly Cost = Base Fee + (Usage × Per-Unit Price)

Example:
- Base: $50/month (includes 1000 API calls)
- Overage: $0.01 per additional call

Pros: Predictable base, scales with value
Cons: More complex to understand
```

---

## Freemium Strategy

### Freemium Design

**What to Give Away Free**
- Core value (enough to hook)
- Viral features (sharing, collaboration)
- Individual use case
- Time-unlimited access

**What to Gate**
- Power features
- Team/collaboration features
- Scale (users, storage, volume)
- Support and SLAs
- Integrations
- Admin and security

### Freemium Metrics

| Metric | Definition | Benchmark |
|--------|------------|-----------|
| Free to Paid Conversion | % free users who pay | 2-5% |
| Time to Convert | Days from signup to paid | Varies |
| Paid CAC | Cost to acquire paid user | Via free → very low |
| Free User Value | Viral/content contribution | Measure it |

### Free Trial vs Freemium

| Factor | Free Trial | Freemium |
|--------|------------|----------|
| **Best for** | Complex products, high ACV | Simple products, PLG |
| **Conversion** | Higher (10-25%) | Lower (2-5%) |
| **Urgency** | Built-in (deadline) | None |
| **Support load** | Higher (time-limited) | Lower |
| **Viral potential** | Lower | Higher |
| **Data collection** | Limited time | Ongoing |

---

## Revenue Optimization

### Expansion Revenue

**Net Revenue Retention (NRR)**
```
NRR = (Starting MRR + Expansion - Contraction - Churn) / Starting MRR

Best-in-class: >120%
Good: 100-120%
Needs work: <100%
```

**Expansion Levers**
1. **Seat expansion**: More users
2. **Usage expansion**: More volume/storage
3. **Upsell**: Higher tier
4. **Cross-sell**: Additional products
5. **Price increases**: Existing customers

### Reducing Churn

**Churn Analysis Framework**

```
Why did they churn?

┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│  PREVENTABLE                    │  NATURAL                      │
│  ─────────────                  │  ───────                      │
│                                 │                               │
│  Didn't get value               │  Company went out of business │
│  → Improve onboarding           │                               │
│                                 │  Bought by company using      │
│  Found better alternative       │  competitor                   │
│  → Competitive analysis         │                               │
│                                 │  Project ended                │
│  Too expensive                  │                               │
│  → Pricing/packaging review     │  Seasonal business            │
│                                 │                               │
│  Missing features               │                               │
│  → Roadmap consideration        │                               │
│                                 │                               │
│  Poor support                   │                               │
│  → Support improvement          │                               │
│                                 │                               │
└─────────────────────────────────────────────────────────────────┘
```

**Churn Prevention Tactics**
1. Proactive health scoring
2. At-risk intervention
3. Offboarding interviews
4. Win-back campaigns
5. Pause/downgrade options
6. Annual contracts

### LTV/CAC Analysis

**Calculating LTV**
```
LTV = ARPU × Gross Margin × Customer Lifetime

Customer Lifetime = 1 / Monthly Churn Rate

Example:
ARPU: $100/month
Gross Margin: 80%
Monthly Churn: 2%
Lifetime: 1 / 0.02 = 50 months

LTV = $100 × 0.80 × 50 = $4,000
```

**LTV/CAC Ratio Interpretation**

| Ratio | Interpretation | Action |
|-------|---------------|--------|
| <1:1 | Losing money | Fix urgently |
| 1-2:1 | Barely viable | Optimize |
| 3:1 | Healthy | Balanced growth |
| >5:1 | Very efficient | Invest more in growth |

**CAC Payback Period**
```
Payback = CAC / (ARPU × Gross Margin)

Target: <12 months (B2B SaaS)
Target: <6 months (high-volume B2C)
```

---

## Pricing Psychology

### Psychological Principles

**Anchoring**
- Show highest price first
- Display "was $X, now $Y"
- Enterprise tier anchors perception

**Charm Pricing**
- $99 vs $100 (left digit effect)
- Works better for emotional purchases
- Less effective for B2B

**Decoy Effect**
```
Small: $5 (poor value)
Medium: $10 (best value) ← Target
Large: $12 (decoy - makes medium look good)
```

**Loss Aversion**
- Emphasize what they'll lose, not gain
- Free trial ending: "Don't lose your data"
- Upgrade prompt: "You're missing out on..."

### Pricing Page Best Practices

**Layout**
1. Three tiers (max four)
2. Highlight recommended tier
3. Clear feature comparison
4. Annual/monthly toggle (annual default)
5. Enterprise CTA
6. FAQ section
7. Social proof

**Copy**
- Tier names that convey value
- Benefits over features
- Clear upgrade reasons
- Urgency where appropriate

**Testing**
- A/B test tier names
- Test price points
- Test feature bundling
- Test annual discount levels
- Track conversion by tier
