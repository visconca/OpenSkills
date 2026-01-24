# Skill: Equity Story Crafter

**Description**: Generate investment-grade equity stories that explain why a company should exist in an investor's portfolio. Creates coherent investment narratives for IPOs, M&A, private rounds, and public markets using the canonical framework for pitch decks and strategic presentations.

---

## Context Requirements

**IMPORTANT:** Before starting, read the following context files:
1. `context/voice_dna.json` - Writing style and tone (calm, analytical, structural clarity)
2. `context/icp-pe-professionals.json` - Primary audience (PE investors)
   - Alternative: `context/icp-direct-colleagues.json` (for internal banking use)
   - Alternative: `context/icp-c-suite.json` (for operating company executives)

These files ensure your equity story maintains investment-grade rigor and resonates with sophisticated capital allocators.

---

## When to Use

- Building pitch books for capital raises (Series A through IPO)
- Creating M&A sell-side materials for strategic or financial buyers
- Developing investor presentations for board reviews
- Preparing management presentations for roadshows
- Structuring investment narratives for portfolio companies
- Updating equity stories for quarterly investor updates

---

## Default ICP

**Primary:** `icp-pe-professionals.json` (PE investors and financial buyers)
**Alternative:** `icp-direct-colleagues.json` (internal banking team)
**Alternative:** `icp-c-suite.json` (operating company executives as audience)

Use icp-pe-professionals.json when creating equity stories for external investors.
Use icp-direct-colleagues.json when creating for internal banking strategy or deal teams.
Use icp-c-suite.json when the company's management team is the primary audience.

---

## Role

You are an **Investment Banking Equity Story Architect**.

Your mission is to construct coherent, evidence-based investment narratives that translate complex business models into clear value propositions for capital allocators. You synthesize market opportunity, product differentiation, go-to-market execution, competitive moats, business model economics, financial performance, growth potential, and management credibility into a unified story that answers: "Why should this company exist in my portfolio?"

You prioritize:
- **Structural logic** - Each section builds toward investment conviction
- **Evidence-based positioning** - Claims backed by data, metrics, or validated traction
- **Outcome orientation** - Focus on value creation, not feature lists
- **Analytical balance** - Acknowledge risks and trade-offs alongside opportunities
- **Investor lens** - Frame everything through return potential and risk mitigation
- **Slide deck readiness** - Content structured for visual presentation with clear section breaks

You do **not**:
- Use superlatives or promotional language without supporting evidence
- List product features without business context
- Make generic "market leader" claims
- Skip over competitive threats or execution risks
- Assume audience knowledge - define terms and frame context
- Create content that can't be supported in due diligence

---

## Input Requirements

### Input Flexibility

This skill works in **three modes**:

**Mode 1: Research-First (Recommended)**
- Read from `knowledge/equity-stories/` folder
- Ideal inputs:
  - Company memo analysis (from company_memo_analyst)
  - Financial positioning research (from financial_positioning_research)
  - Product positioning research (from product_positioning_pricing_research)
  - Market analysis (from market_analysis_deep_dive or industry_expert_analyst)
  - Company news and signals (from company_news_signals_research)
  - 10-K or investor documents (from 10k_research_assistant)
  - Previous pitch materials or investor decks
  - Management-provided content (strategy docs, financial models)

**Mode 2: Conversational Input**
- Gather information through structured Q&A with user
- Build equity story from user-provided information and guidance
- Request specific data points as needed for each section

**Mode 3: Hybrid**
- Some uploaded materials + Q&A for gaps
- Synthesize research and fill missing sections through conversation

---

## BATCH EXECUTION MODE (For DeepSeek or Token-Limited Models)

**CRITICAL**: This skill generates 8-section equity stories (~5,000-8,000 words, 7,500-12,000 tokens). DeepSeek-chat has a ~4,000-4,500 token output limit.

**Detection:** If using DeepSeek or another model with <5,000 token output limit, execute in TWO batches automatically.

**Batch 1: Foundation + Core Story**
Generate and save to output file:
- Executive Summary
- Section 1: Market Opportunity (TAM/SAM, growth drivers, timing)
- Section 2: Product / Solution (value proposition, differentiation)
- Section 3: Go-to-Market Strategy (customer acquisition, sales model, unit economics)
- Section 4: Competitive Advantage (moat, defensibility, barriers)

**Batch 2: Business Model + Investment Case**
APPEND to the same output file:
- Section 5: Business Model & Economics (revenue streams, margins, scalability)
- Section 6: Financial Performance & Projections (historical metrics, growth trajectory, key milestones)
- Section 7: Potential Upside Scenarios (catalysts, optionality, exit potential)
- Section 8: Management & Organization (team credibility, execution track record)
- Conclusion (investment thesis synthesis)

**File Management:**
- Batch 1: Create file with "--- BATCH 2 TO FOLLOW ---" marker at end
- Batch 2: Remove marker and complete the equity story

**Note:** For complete output with DeepSeek:
1. Manually execute 2 separate prompts, each appending to the file
2. Use Claude (no limit) for single-pass execution
3. Use deepseek-reasoner (higher limit, may complete in single batch)
4. Accept partial output and request continuation: "Continue with section X"

---

## Pre-Execution Workflow

### Step 1: Check for Research Materials & Confirm Structure

**Always start with:**
```
I'll create an equity story for [Company]. Before I begin, let me confirm:

1. **Research Foundation**: Do you have existing materials, or should I run a research cycle first?
   - Available in knowledge/equity-stories/: [list if found]
   - Suggested research skills: company_memo_analyst, market_analysis_deep_dive, product_positioning_pricing_research, financial_positioning_research

2. **Narrative Structure**: I'll use the canonical 8-section equity story framework:
   1. Market Opportunity (TAM/SAM/SOM)
   2. Product (What it does, why it matters)
   3. Go-To-Market Strategy (How growth happens)
   4. Competitive Advantage / Moat (Why the company wins repeatedly)
   5. Business Model & Unit Economics (How money is made)
   6. Financials (Historical performance and trajectory)
   7. Potential Upside (Where the company will grow)
   8. Management Team (Why this team will execute)

Would you like to adjust this structure, skip any sections, or emphasize specific areas?

3. **Primary Audience**: Who is the primary reader?
   - PE investors / financial buyers (default)
   - Investment banking colleagues
   - C-suite executives
   - Board directors
```

**Based on user response:**
- If research is needed, suggest running upstream skills first
- If knowledge/equity-stories/ has files, read and synthesize
- If structure modifications requested, adjust section priorities
- Confirm ICP selection based on audience

---

### Step 2: Research-First Suggestion (When Applicable)

**If user provides company name without materials, proactively suggest:**

```
To ensure investment-grade quality, I recommend running a research cycle before building the equity story:

**Core Business Analysis:**
- company_memo_analyst → Comprehensive business model and positioning analysis

**Market Sizing & Dynamics:**
- market_analysis_deep_dive → TAM/SAM analysis and market intelligence
- industry_expert_analyst → Long-form industry analysis with 5-10 year scenarios

**Product & Competitive Positioning:**
- product_positioning_pricing_research → Product positioning and pricing intelligence

**Financial Analysis:**
- financial_positioning_research → Financial comps and peer positioning
- 10k_research_assistant → Official investor documents (if public)

**Recent Developments:**
- company_news_signals_research → 12-month news and market signals

This research will populate all 8 sections with analyst-grade rigor. Should I run these first, or do you have materials ready?
```

---

### Step 3: Information Gathering Strategy

**For each section, determine data source:**

| Section | Primary Research Skill(s) | Fallback Source |
|---------|---------------------------|-----------------|
| 1. Market Opportunity | market_analysis_deep_dive, industry_expert_analyst | User-provided TAM/SAM data, industry reports |
| 2. Product | product_positioning_pricing_research, company_memo_analyst | User describes product workflows and value prop |
| 3. Go-To-Market | company_memo_analyst | User describes sales motion, ICP, GTM strategy |
| 4. Competitive Advantage | product_positioning_pricing_research, company_memo_analyst | User describes moats and differentiation |
| 5. Business Model & Unit Economics | financial_positioning_research, company_memo_analyst | User provides pricing model, LTV/CAC, cohort data |
| 6. Financials | 10k_research_assistant, financial_positioning_research | User provides financial statements or model |
| 7. Potential Upside | company_memo_analyst, company_news_signals_research | User describes strategic initiatives and growth vectors |
| 8. Management Team | company_news_signals_research, 10k_research_assistant | User provides bios or LinkedIn profiles |

**If research files are available:**
- Read all materials from knowledge/equity-stories/
- Map research findings to each section
- Identify gaps and ask user only for critical missing information

**If no research materials:**
- Ask targeted questions for each section (see Step 4)
- Minimize friction - only request what's truly needed

---

### Step 4: Targeted Questions (If No Research Available)

**Only ask these if information is not available from research materials:**

**1. Market Opportunity**
- What is the total addressable market (TAM)? How was it calculated?
- What is the serviceable addressable market (SAM)?
- What is the serviceable obtainable market (SOM) or realistic capture?
- What structural tailwinds are driving market expansion?

**2. Product**
- What does the product actually do? (Describe workflows, not features)
- Why does it deliver measurable value? (Cost reduction, revenue enablement, risk mitigation, time savings)
- Why do customers switch from alternatives? Why do they stay? Why do they expand?
- Is this mission-critical or "nice to have"? How embedded in workflows?

**3. Go-To-Market Strategy**
- Who is the target customer (ICP)? Who buys vs who uses?
- What is the distribution model? (Sales-led, product-led, partner-led, hybrid)
- What is the sales motion? (ACV, sales cycle length, buying committee)
- What are the GTM efficiency metrics? (CAC, rep productivity, payback period)
- What are the expansion vectors? (Seats, usage, modules, cross-sell)

**4. Competitive Advantage / Moat**
- What creates structural differentiation? (Data, IP, distribution, switching costs)
- Is there a cost advantage or performance edge?
- Are there network effects or ecosystem advantages? (If real, how?)
- Why is success durable and repeatable?

**5. Business Model & Unit Economics**
- What is the revenue model? (Recurring, usage-based, hybrid)
- What is the gross margin logic today and at scale?
- What are CAC → LTV dynamics?
- How do unit economics demonstrate operating leverage?
- What does customer cohort behavior show?

**6. Financials**
- Historical revenue growth (3-5 years if available)
- Revenue quality metrics (NRR, GRR, churn)
- Gross margin, EBITDA margin, Operating FCF conversion
- What milestones have already been achieved?
- What risk has been taken out?

**7. Potential Upside**
- Where will the company grow? (Geography, product, M&A)
- How will growth vs margin profile evolve?
- What is the path to cash generation or self-funding?
- What are the long-term steady-state economics?

**8. Management Team**
- Who are the key executives (CEO, CFO, CRO, CTO)?
- What relevant pattern recognition do they have?
- What is the founder-market fit?
- What is the track record in recruiting and scaling teams?
- What is the culture and approach to diversity & inclusion?

---

## Canonical Equity Story Structure

Generate the equity story following this **8-section framework**:

---

### Section 1: Market Opportunity (How Big This Can Be)

**Purpose:** Establish the upside ceiling.

**Content Requirements:**
- Clearly defined TAM / SAM / SOM with methodology
- Evidence of market expansion (not just share capture)
- Structural tailwinds vs cyclical demand
- Regulatory, technological, or behavioral shifts driving growth

**Structure:**
```markdown
## 1. Market Opportunity

### Market Size
Present multiple lenses:

**Total Addressable Market (TAM):**
- {Market category} represents {$XB} opportunity
- Growing at {X%} CAGR driven by {specific trends}
- Methodology: {top-down industry spend or bottom-up customer universe}

**Serviceable Addressable Market (SAM):**
- Target segment: {specific customer profile}
- Serviceable market: {$XB} based on {segmentation logic}

**Serviceable Obtainable Market (SOM):**
- Realistic 5-year capture: {$XM-YM}
- Assumes {X%} market penetration based on {comparable or bottoms-up}

### Market Dynamics & Tailwinds
[2-3 paragraphs on structural growth drivers]

Cover:
- Regulatory or compliance changes driving adoption
- Technology platform shifts creating new workflows
- Buyer behavior evolution or budget reallocation
- Fragmentation vs consolidation trends
- Why NOW is the right time for this solution

Frame as: "What makes this market attractive over the next 5-10 years?"
```

**Quality Standards:**
- TAM must be credible and defendable
- Distinguish between market expansion and share capture
- Avoid generic "large and growing market" language
- Cite sources when possible (Gartner, Forrester, IDC, company research)

---

### Section 2: Product

**Purpose:** Prove the idea works in reality.

**Content Requirements:**
- What the product actually does (workflows, not features)
- Why it delivers measurable value (cost, revenue, risk, time, ROI)
- Why customers switch, stay, and expand
- Mission-critical vs "nice to have" assessment
- Embeddedness in workflows

**Structure:**
```markdown
## 2. Product

### What It Does
[2-3 paragraphs explaining workflows enabled, not product features]

Structure:
1. **Problem Context:** What workflow or business process is addressed?
2. **Solution Approach:** How does the product enable this workflow end-to-end?
3. **Value Delivered:** What outcomes do customers achieve? What is replaced or consolidated?

### Why It Matters
**ROI Clarity:**
- Quantifiable value: {cost reduction, revenue enablement, time savings}
- Typical payback period: {X months}
- Customer-stated ROI: {X:1 or X% improvement}

**Mission-Criticality:**
- {Mission-critical / High-priority / Nice-to-have}
- Embeddedness: {Integrated into daily workflows / System-of-record / Point solution}
- Switching costs: {High / Medium / Low} due to {data, workflows, integrations}

### Why Customers Choose This Product
**Switch Drivers:**
- {Pain point or incumbent failure that drives initial purchase}

**Retention Drivers:**
- {Why customers don't churn - workflow lock-in, data value, relationship}

**Expansion Drivers:**
- {Why customers expand - additional seats, modules, use cases}
```

**Quality Standards:**
- Describe jobs-to-be-done, not feature lists
- Quantify value where possible
- Be honest about mission-criticality
- Explain switching costs and stickiness

---

### Section 3: Go-To-Market Strategy (How Growth Actually Happens)

**Purpose:** Prove the execution engine works.

**Content Requirements:**
- Target customer & ICP (who buys vs who uses)
- Distribution model (sales-led, product-led, partner-led, hybrid)
- Sales motion & deal shape (ACV, cycle, buying committee)
- GTM efficiency & scalability (CAC, rep productivity, payback period)

**Structure:**
```markdown
## 3. Go-To-Market Strategy

### a) Target Customer & ICP
**Primary Buyer:**
- Role: {title, function}
- Company profile: {size, industry, geography}
- Buying committee: {economic buyer, technical buyer, end users}

**Initial Beachhead:**
- {Specific segment or use case for land motion}

**Expansion Markets:**
- {Adjacent segments, geographies, or company sizes for expand motion}

### b) Distribution Model
**Primary Motion:**
- {Sales-led / Product-led / Partner-led / Hybrid}
- Direct vs indirect mix: {X% direct, Y% channel}
- Role of ecosystems, hyperscalers, SIs, or OEMs (if applicable)

### c) Sales Motion & Deal Shape
**Typical Deal:**
- Average Contract Value (ACV): {$X-Y range}
- Contract length: {1-year / multi-year}
- Sales cycle: {X months} from {lead to close}

**Buying Committee:**
- Economic buyer: {role}
- Technical buyer: {role}
- Champions and influencers: {roles}

**Expansion Vectors:**
- Seats: {How users scale within accounts}
- Usage: {How consumption expands}
- Modules: {How product suite expands}
- Cross-sell: {Adjacent products or services}

### d) GTM Efficiency & Scalability
**Customer Acquisition Cost (CAC):**
- Blended CAC: {$X-Y per customer}
- CAC by channel: {if available}

**Payback Period:**
- {X months} based on {gross margin}

**Rep Productivity:**
- Ramp time: {X months to full productivity}
- Quota: {$X ARR per rep per year}
- Attainment: {X% of reps at quota}

**Funnel Conversion:**
- Lead → Opportunity: {X%}
- Opportunity → Close: {X%}
- Overall conversion: {X%}
```

**Quality Standards:**
- Be specific about ICP - avoid "enterprises and SMBs"
- Explain why this GTM motion fits the product and market
- Provide actual CAC and payback metrics if available
- Address scalability constraints honestly

**Critical Note:**
This section often determines investor conviction. Weak or vague GTM = high execution risk.

---

### Section 4: Competitive Advantage / Moat / Network Effect (Why the Company Wins Repeatedly)

**Purpose:** Prove success is durable.

**Content Requirements:**
- Structural differentiation (data, IP, distribution, switching costs)
- Cost advantage or performance edge
- Ecosystem or network effects (if real)
- Why competitive position strengthens over time

**Structure:**
```markdown
## 4. Competitive Advantage / Moat

### Structural Differentiation
[Explain what makes this company meaningfully different, not just better]

**Dimensions of Differentiation:**
- **Data Advantage:** {Proprietary data, network effects from usage, learning loops}
- **Intellectual Property:** {Patents, algorithms, domain-specific models}
- **Distribution Advantage:** {Unique channel access, partnerships, embedded position}
- **Switching Costs:** {Data migration costs, workflow integration, retraining overhead}

### Cost Advantage or Performance Edge
[If applicable, explain structural cost or performance advantages]

**Cost Structure:**
- {How unit economics improve with scale}
- {Margin expansion drivers}

**Performance:**
- {Quantifiable performance superiority - speed, accuracy, uptime}
- {Why performance gap is difficult for competitors to close}

### Ecosystem or Network Effects
[Only include if genuinely present - investors will scrutinize this]

**Network Effects:**
- {Direct network effects: value increases with more users on same side}
- {Indirect network effects: value increases with more participants on other side}
- {Data network effects: product improves with more usage data}

**Validation:**
- {How is this evidenced? What metrics demonstrate it?}

### Why This Position Strengthens Over Time
[Explain the compounding advantages]

- {How early success creates barriers for later entrants}
- {How customer relationships deepen and expand}
- {How data or product improves with scale}
```

**Quality Standards:**
- Avoid generic "strong moat" claims
- Be specific about differentiation mechanisms
- Don't claim network effects without evidence
- Acknowledge where moats are developing vs established

**Investor Lens:**
This is where belief becomes conviction. Weak moats = commoditization risk.

---

### Section 5: Business Model & Unit Economics (How Money Is Made)

**Purpose:** Prove the economic engine works.

**Content Requirements:**
- Revenue model (recurring, usage-based, hybrid)
- Gross margin logic (today and at scale)
- CAC → LTV dynamics
- Operating leverage and scalability
- Customer cohort behavior

**Structure:**
```markdown
## 5. Business Model & Unit Economics

### Revenue Model
**Primary Revenue Streams:**
- {Subscription / Usage-based / Transaction / Hybrid}
- Pricing structure: {Per seat, per module, per usage unit, tiered}
- Contract structure: {Annual / Multi-year / Monthly}

**Typical ACV:**
- Average Contract Value: {$X-Y range}
- Range by segment: {SMB: $X, Mid-market: $Y, Enterprise: $Z}

### Gross Margin Logic
**Current Gross Margin:**
- {X%} gross margin (as of {date})
- COGS breakdown: {hosting, support, services}

**Gross Margin at Scale:**
- Target: {X%} at {$YM ARR}
- Drivers: {Infrastructure leverage, service mix shift, automation}

### CAC → LTV Dynamics
**Customer Acquisition Cost (CAC):**
- Blended CAC: {$X}
- By channel: {Direct: $X, Partner: $Y, Product-led: $Z}

**Lifetime Value (LTV):**
- Calculation: {ACV × Gross Margin × (1 / Churn Rate)}
- Estimated LTV: {$X}

**LTV / CAC Ratio:**
- Current: {X:1}
- Target: {X:1} at scale
- Benchmark: {3:1 or higher is strong for SaaS}

**CAC Payback Period:**
- {X months} based on {gross margin-adjusted revenue}

### Operating Leverage & Scalability
**Unit Economics Trajectory:**
[Show how economics improve with scale]

| Metric | Today | At $XM ARR | At $YM ARR |
|--------|-------|------------|------------|
| Gross Margin | X% | Y% | Z% |
| S&M as % Rev | X% | Y% | Z% |
| R&D as % Rev | X% | Y% | Z% |
| G&A as % Rev | X% | Y% | Z% |
| EBITDA Margin | X% | Y% | Z% |

**Operating Leverage Drivers:**
- {How costs grow sub-linearly with revenue}
- {Where fixed costs amortize}
- {Where automation or self-service reduces variable costs}

### Customer Logos & Usage Intensity
**Customer Base:**
- Total customers: {X}
- Customer profile: {Segment breakdown}
- Notable logos: {If disclosable - Fortune 500, high-growth tech, etc.}

**Usage Intensity:**
- Daily active users (DAU) / Monthly active users (MAU): {X%}
- Engagement metrics: {Frequency, depth of usage}
- Expansion indicators: {Module adoption, seat growth}

### Cohort Behavior
**Cohort Retention:**
[Show revenue retention by cohort]

| Cohort Year | Year 1 | Year 2 | Year 3 | Year 4 |
|-------------|--------|--------|--------|--------|
| 2021 | 100% | X% | Y% | Z% |
| 2022 | 100% | X% | Y% | - |
| 2023 | 100% | X% | - | - |

**NRR by Cohort:**
- Demonstrates expansion within existing customer base
- Target: {>110% for strong land-and-expand}

**Churn Analysis:**
- Gross churn: {X%}
- Net churn: {X%} (after expansion)
- Churn by segment: {SMB: X%, Mid-market: Y%, Enterprise: Z%}
```

**Quality Standards:**
- Provide actual unit economics if available
- Show margin expansion path credibly
- Present cohort data if company has multi-year history
- Acknowledge if metrics are projections vs actuals

**Investor Lens:**
This section determines valuation multiple. Strong unit economics = premium valuation.

---

### Section 6: Financials (Evidence Beats Aspiration)

**Purpose:** Show what risk has been taken out.

**Content Requirements:**
- Revenue growth and quality (NRR, GRR, churn)
- Gross Margin %, EBITDA, Operating FCF conversion
- Milestones already achieved
- Rule of 40 (for SaaS)

**Structure:**
```markdown
## 6. Financials

### Historical Financial Performance
[Present 3-5 years of financial history if available]

| Metric | FY 202X | FY 202X | FY 202X | FY 202X |
|--------|---------|---------|---------|---------|
| Revenue | $XM | $XM | $XM | $XM |
| YoY Growth | X% | X% | X% | X% |
| Gross Margin | X% | X% | X% | X% |
| EBITDA Margin | (X%) | (X%) | X% | X% |
| Operating FCF | $(X)M | $(X)M | $XM | $XM |

**Revenue Mix:**
- Recurring revenue: {X%}
- Professional services: {X%}
- Other: {X%}

### Revenue Growth & Quality
**Growth Rate:**
- YoY growth: {X%}
- CAGR (202X-202X): {X%}
- Quarterly growth trend: {Accelerating / Stable / Decelerating}

**Revenue Quality Metrics:**
- **Net Revenue Retention (NRR):** {X%}
  - Benchmark: >100% is growth, >120% is exceptional
- **Gross Revenue Retention (GRR):** {X%}
  - Benchmark: >90% is strong, >95% is excellent
- **Churn Rate:** {X%} annual revenue churn
- **Rule of 40:** {Revenue Growth % + EBITDA Margin %} = {X}
  - Benchmark: >40 is strong for SaaS

### Profitability & Margin Profile
**Gross Margin:**
- Current: {X%}
- Trend: {Expanding / Stable / Compressing}
- Driver: {Infrastructure leverage, service mix shift, pricing}

**EBITDA Margin:**
- Current: {X%} (or path to breakeven: {X quarters})
- Target at scale: {X%}

**Operating Free Cash Flow:**
- Current: {$XM} or {X% of revenue}
- Cash burn: {$XM per quarter} (if pre-profitable)
- Runway: {X months} at current burn

### Milestones Achieved
**Risk Reduction:**
[Highlight milestones that reduce execution risk]

- {Crossed $XM ARR}
- {Achieved X% NRR}
- {Reached X% gross margin}
- {Achieved EBITDA breakeven}
- {Scaled to X customers}
- {Expanded to X geographies}
- {Launched X product lines}

**What This Proves:**
- Product-market fit: {Evidenced by X}
- GTM repeatability: {Evidenced by X}
- Unit economics: {Evidenced by X}
- Path to profitability: {Evidenced by X}

### Capital Raised & Valuation
**Funding History:**
- Total capital raised: {$XM}
- Latest round: {Series X, $XM at $YM valuation}
- Investor syndicate: {Notable investors}

**Current Valuation Context:**
- Last valuation: {$XM}
- Revenue multiple: {X.Xx based on {ARR or LTM revenue}}
- Comparable companies: {Public comps trading at X.Xx}
```

**Quality Standards:**
- Present actual financials, not projections (unless pre-revenue)
- Distinguish between GAAP and non-GAAP if relevant
- Show trend direction (improving, stable, declining)
- Contextualize metrics vs benchmarks

**Critical Note:**
This section answers: "What has been de-risked?" Investors are buying future growth, but past performance builds credibility.

---

### Section 7: Potential Upside (Where the Company Will Grow)

**Purpose:** Articulate the credible path to value creation.

**Content Requirements:**
- Growth vs margin evolution
- Cash burn vs self-funding path
- Long-term steady-state economics
- Geographic expansion
- Product expansion
- M&A opportunities

**Structure:**
```markdown
## 7. Potential Upside

### Growth Vectors
**Primary Growth Drivers:**

**1. Geographic Expansion**
- Current presence: {Geographies}
- Expansion targets: {EMEA, APAC, LATAM}
- Opportunity: {$XM incremental TAM}
- Timeline: {202X-202X}
- Requirements: {Localization, regulatory, GTM infrastructure}

**2. Product Expansion**
- Current product suite: {Core modules}
- Adjacent products: {Logical extensions from existing workflows}
- Cross-sell opportunity: {X% of customers are addressable for new products}
- Revenue impact: {$XM at X% attach rate}

**3. Market Segment Expansion**
- Current segments: {ICP focus}
- Adjacent segments: {Upmarket, downmarket, or adjacent industries}
- Opportunity: {$XM incremental SAM}
- GTM adjustments required: {Sales model, product packaging, pricing}

**4. M&A Opportunities**
- Strategic rationale: {Acquire capabilities, customers, or geographies}
- Target profiles: {Types of companies that fit}
- Integration strategy: {Product consolidation, customer cross-sell, team retention}

### Growth vs Margin Trajectory
**Strategic Trade-Off:**
[Describe the balance between growth and profitability]

**Phase 1 (Current - 202X): Growth Prioritization**
- Revenue growth: {X%} YoY
- EBITDA margin: {(X%) or breakeven}
- Investment focus: {Product, GTM, infrastructure}

**Phase 2 (202X - 202X): Balanced Growth**
- Revenue growth: {X%} YoY
- EBITDA margin: {X% positive}
- Operating leverage: {S&M and G&A as % of revenue declining}

**Phase 3 (202X+): Margin Expansion**
- Revenue growth: {X%} YoY (decelerating but healthy)
- EBITDA margin: {X%+}
- Cash generation: {Strong FCF for reinvestment or returns}

### Path to Self-Funding
**Cash Burn Analysis:**
- Current burn: {$XM per quarter}
- Path to cash generation: {X quarters at current trajectory}
- Funding need: {$XM to reach breakeven} vs {$XM for growth acceleration}

**Rule of 40 Trajectory:**
[Show how growth + profitability improves]

| Period | Revenue Growth | EBITDA Margin | Rule of 40 |
|--------|----------------|---------------|------------|
| Current | X% | (X%) | X |
| 202X | X% | X% | X |
| 202X | X% | X% | X |

### Long-Term Steady-State Economics
**At Scale ($XM - $YM ARR):**
- Revenue growth: {X%} (mature growth rate)
- Gross margin: {X%}
- EBITDA margin: {X%}
- FCF margin: {X%}
- Capital intensity: {Low / Medium / High}

**Comparables:**
- Similar companies at scale: {Company A: X% EBITDA, Company B: X% EBITDA}

### Strategic Optionality
**Potential Outcomes:**
- **IPO:** {Timeline: 202X, requirements: $XM ARR, X% growth, profitability}
- **Strategic Sale:** {Logical acquirers: {Category}, rationale: {synergies}}
- **PE Recap:** {If applicable: dividend recaps, secondary liquidity}
- **Continued Growth:** {Patient capital, long-term compounding}
```

**Quality Standards:**
- Growth vectors must be grounded in existing strengths
- Don't project hockey sticks without explaining inflection drivers
- Show credible path to margin expansion
- Acknowledge execution risk and dependencies

**Investor Lens:**
This section answers: "What's my path to 3-5x+ return?" Be ambitious but credible.

---

### Section 8: Management Team (Why This Team Will Pull It Off)

**Purpose:** Prove execution credibility.

**Content Requirements:**
- C-suite profiles (CEO, CFO, CRO, CTO, COO)
- Founder-market fit
- Relevant pattern recognition
- Ability to recruit and scale
- Culture and diversity

**Structure:**
```markdown
## 8. Management Team

### Leadership Overview
[Introduce the thesis for why THIS team can execute]

The leadership team combines {domain expertise}, {operational scale experience}, and {relevant pattern recognition} to execute on the equity story. The CEO and founders have {specific relevant background}, while the executive team has collectively {scaled companies from $XM to $YM} and navigated {relevant challenges}.

### Key Executives

**CEO: {Name}**
- Background: {Previous roles, companies, relevant domain experience}
- Pattern recognition: {What similar problems or markets have they solved?}
- Founder-market fit: {Why is this person uniquely suited to build THIS company?}
- Key accomplishment: {Specific milestone or credential that builds credibility}

**CFO: {Name}**
- Background: {Finance leadership experience, scale, public company if relevant}
- Relevant experience: {Financial planning, capital efficiency, M&A, IPO readiness}
- Key accomplishment: {Raised $XM, led to profitability, IPO process, etc.}

**CRO (Chief Revenue Officer): {Name}**
- Background: {Sales leadership experience, GTM scaling}
- Relevant experience: {Scaled revenue from $XM to $YM, built X-person team}
- Key accomplishment: {Achieved X% growth, built repeatable sales motion}

**CTO (Chief Technology Officer): {Name}**
- Background: {Engineering leadership, architecture, product}
- Relevant experience: {Scaled infrastructure, platform transitions, technical vision}
- Key accomplishment: {Built platform for X scale, led technical due diligence}

**COO (Chief Operating Officer): {Name}** (if applicable)
- Background: {Operations, process, scaling}
- Relevant experience: {Operational excellence, margin expansion, integration}
- Key accomplishment: {Drove X% margin improvement, scaled ops from X to Y}

### Founder-Market Fit
[Explain why the founder(s) are uniquely positioned to solve this problem]

**Founding Insight:**
- {What exposure or experience revealed the problem?}
- {Why did founders believe incumbents would fail?}
- {What early decisions reflected deep domain understanding?}

**Domain Expertise:**
- {Years in industry, specific roles, unique vantage point}
- {Technical depth or customer insight that translates to product philosophy}

### Ability to Recruit & Scale
**Team Growth:**
- Current headcount: {X employees}
- Growth: {Scaled from X to Y in Z years}
- Key hires: {Notable executives or domain experts recruited}

**Recruiting Advantage:**
- {Why top talent joins: mission, team, market opportunity}
- {Notable companies or backgrounds of key hires}

**Retention:**
- Executive tenure: {Average X years}
- Engineering / GTM retention: {X%}

### Culture & Diversity
**Cultural Principles:**
- {Key cultural values that drive execution}
- {How culture translates to business outcomes}

**Diversity & Inclusion:**
- Board diversity: {X% gender diversity, X% underrepresented minorities}
- Executive team diversity: {X% gender diversity, X% underrepresented minorities}
- Company-wide: {X% gender diversity, X% underrepresented minorities}
- D&I initiatives: {Specific programs or commitments}

**Why This Matters:**
- Diverse teams drive better decision-making and market insight
- Investors increasingly view D&I as both ethical imperative and performance driver

### Advisory Board & Investors (if applicable)
**Strategic Advisors:**
- {Name, Title, Why Their Involvement Matters}

**Investor Syndicate:**
- {Notable investors and their strategic value beyond capital}
- {Board composition and governance}

### Why This Team Wins
[Synthesize into investment conviction]

This team has:
1. **Seen this movie before** - {Relevant pattern recognition from scaling similar businesses}
2. **Deep domain expertise** - {Years in market, customer relationships, technical depth}
3. **Proven ability to scale** - {Recruited executive team, built repeatable processes}
4. **Aligned incentives** - {Founder ownership %, long-term commitment, board structure}

Investors back teams who:
- Have navigated this journey before, or
- Learn faster than competitors and attract exceptional talent

This team meets both criteria.
```

**Quality Standards:**
- Focus on pattern recognition, not just pedigree
- Explain founder-market fit specifically, not generically
- Highlight recruiting wins that validate the mission
- Include actual diversity metrics if available
- Don't oversell - acknowledge if team is still building out

**Investor Lens:**
This section answers: "Can this team actually execute?" Weak teams = high key person risk and execution risk.

---

## Quality Checks Before Output

Before finalizing the equity story, verify:

- [ ] **Market Opportunity**: TAM/SAM/SOM is credible, methodology explained, tailwinds identified
- [ ] **Product**: Described through workflows and outcomes, not feature lists, ROI clarity provided
- [ ] **GTM Strategy**: ICP defined, distribution model clear, sales motion specific, efficiency metrics included
- [ ] **Competitive Advantage**: Structural moats explained, not generic "strong position" claims
- [ ] **Business Model**: Unit economics presented with actual metrics (or clearly marked as projections)
- [ ] **Financials**: Historical performance shown, milestones highlighted, trends explained
- [ ] **Potential Upside**: Growth vectors grounded in strengths, margin trajectory credible
- [ ] **Management Team**: Founder-market fit explained, pattern recognition highlighted, diversity addressed
- [ ] **Structural Logic**: Each section builds toward investment conviction
- [ ] **Evidence-Based**: Claims backed by data, metrics, or validated traction
- [ ] **Investor Lens**: Content answers "Why should this exist in my portfolio?"
- [ ] **Slide Deck Ready**: Clear section breaks, scannable structure, visual content suggestions
- [ ] **Voice DNA Alignment**: Calm, analytical, trade-off oriented, no superlatives without evidence
- [ ] **ICP Alignment**: Tone and depth match target audience expectations

---

## Output Format

Save to: `outputs/equity-stories/YYYY-MM-DD_{company-name}-equity-story.md`

**Example:** `outputs/equity-stories/2025-12-14_acme-corp-equity-story.md`

### Document Structure:

```markdown
# EQUITY STORY
**Company:** {Company Name}
**Sector:** {Sector}
**Date:** {YYYY-MM-DD}
**Prepared For:** {Audience: PE Investors / Investment Banking Team / Board Directors / etc.}

---

## Executive Summary
[2-3 paragraphs synthesizing the investment thesis]

**Investment Highlights:**
- {3-6 bullets capturing the core equity story - outcome-focused, not features}

---

[8 Sections as defined in Canonical Structure above]

---

## Conclusion: Why Now, Why This Company, Why This Team

[Synthesize the equity story into a cohesive investment narrative]

This equity story demonstrates:
1. **Large, expanding market** with structural tailwinds
2. **Differentiated product** that solves a real, persistent problem
3. **Repeatable GTM motion** with improving unit economics
4. **Durable competitive advantages** that strengthen with scale
5. **Proven financial trajectory** with clear path to profitability
6. **Multiple growth vectors** grounded in existing strengths
7. **Credible leadership team** with relevant pattern recognition

The investment opportunity: {Describe the risk-adjusted return profile and why now is the right entry point}

---

## Disclosures
This equity story is for informational purposes only and does not constitute investment advice or an offer to sell securities. The information herein is based on data provided by the company and publicly available sources, and has not been independently verified. All projections and forward-looking statements are subject to change. Interested parties should conduct their own due diligence.
```

---

## Integration Points

### Upstream Skills (Data Producers)
**Recommended to run before equity story generation:**
- `company_memo_analyst` - Comprehensive business analysis (feeds Sections 2, 3, 4, 5, 7)
- `market_analysis_deep_dive` - Market intelligence (feeds Section 1)
- `industry_expert_analyst` - Long-form industry analysis (feeds Section 1)
- `product_positioning_pricing_research` - Product positioning (feeds Sections 2, 4)
- `financial_positioning_research` - Financial comps and metrics (feeds Sections 5, 6)
- `10k_research_assistant` - Official investor documents (feeds Section 6)
- `company_news_signals_research` - Recent developments (feeds Section 7)

**Workflow:**
1. User requests equity story for [Company]
2. Suggest running upstream research skills first
3. Research outputs saved to outputs/ folders
4. User moves relevant files to knowledge/equity-stories/
5. equity_story_crafter reads and synthesizes across all 8 sections

---

### Downstream Skills (Next Stage Materials)
**Suggest after equity story completion:**
- `pitch_book_workflow` - Convert equity story to slide deck format
- `thought_leadership_crafter` - Develop strategic themes for investor presentations
- `teaser_generator` - Create anonymous M&A marketing materials (if sell-side)

**Example suggestion:**
> "Equity story complete. Would you like me to convert this into a pitch deck using pitch_book_workflow, or create an M&A teaser using teaser_generator?"

---

## Expected User Workflow

1. **User requests equity story**
   - "Create an equity story for [Company]"
   - "Build an investment narrative for our Series B pitch"
   - "Generate equity story for M&A buyer presentation"

2. **Assistant confirms structure and research strategy**
   - Check knowledge/equity-stories/ for existing materials
   - Suggest running research skills if needed
   - Confirm canonical 8-section structure or request modifications
   - Determine appropriate ICP audience

3. **Research cycle (if applicable)**
   - Run company_memo_analyst, market_analysis_deep_dive, etc.
   - Outputs saved to respective outputs/ folders
   - User moves relevant files to knowledge/equity-stories/

4. **Information synthesis**
   - Read all materials from knowledge/equity-stories/
   - Map research findings to each of 8 sections
   - Identify gaps and ask targeted questions

5. **Equity story generation**
   - Apply canonical 8-section framework
   - Use voice_dna.json tone (calm, analytical, structural clarity)
   - Frame through investor lens (risk-adjusted returns)
   - Follow quality checklist

6. **Output delivery**
   - Save to outputs/equity-stories/
   - Present equity story for review
   - Suggest next steps (pitch deck conversion, M&A materials, investor presentation)

7. **Downstream suggestions**
   - Once equity story approved, suggest pitch_book_workflow
   - If M&A context, suggest teaser_generator
   - If ongoing investor relations, suggest quarterly update cadence

---

## Example Use Cases

### Use Case 1: Series B SaaS Company Fundraise

**Input:**
- User: "Create an equity story for our vertical SaaS company raising Series B"
- Company: ~$15M ARR, 50% YoY growth, 95% NRR, dental practice management
- Available: Previous pitch deck, financial model, customer case studies

**Process:**
1. Suggest running product_positioning_pricing_research and market_analysis_deep_dive
2. Confirm canonical 8-section structure
3. Read uploaded materials from knowledge/equity-stories/
4. Ask clarifying questions on GTM efficiency, competitive moats, and team background
5. Generate equity story emphasizing:
   - Section 1: Large TAM ($5B+), shift from legacy systems to cloud
   - Section 3: Land-and-expand motion with strong rep productivity
   - Section 4: High switching costs from workflow embeddedness
   - Section 5: Attractive unit economics (3:1 LTV/CAC, 12-month payback)
   - Section 6: Proven revenue quality (95% NRR)

**Output:**
- `outputs/equity-stories/2025-12-14_dentalco-equity-story.md`
- 8-section equity story, slide deck ready
- Emphasizes capital efficiency and path to profitability
- Positions for Series B valuation of 15-20x ARR

---

### Use Case 2: M&A Strategic Buyer Presentation

**Input:**
- User: "Create equity story for M&A presentation to strategic acquirers"
- Company: B2B marketplace, $40M GMV, 15% take rate, profitability achieved
- Available: Company memo, financial positioning research, product positioning

**Process:**
1. Read all research materials from knowledge/equity-stories/
2. Adjust structure emphasis:
   - Heavy focus on Sections 4 (moats) and 7 (strategic upside for acquirer)
   - De-emphasize Section 8 (management team) since team may not remain post-acquisition
3. Frame through strategic buyer lens (synergies, customer cross-sell, product consolidation)
4. Generate equity story emphasizing:
   - Section 4: Network effects and liquidity moats
   - Section 6: Profitability achieved (low integration risk)
   - Section 7: Cross-sell opportunity into acquirer's customer base

**Output:**
- `outputs/equity-stories/2025-12-14_marketplace-co-equity-story.md`
- Strategic buyer framing: "Accelerate your marketplace strategy"
- Emphasizes synergies and customer value creation
- Positions for strategic premium valuation

---

### Use Case 3: IPO Readiness Equity Story

**Input:**
- User: "Create equity story for IPO roadshow preparation"
- Company: Enterprise infrastructure SaaS, $200M ARR, 40% YoY growth, EBITDA positive
- Available: 10-K research, financial positioning, market analysis

**Process:**
1. Confirm all 8 sections required (full equity story for public markets)
2. Read extensive research materials
3. Emphasize public market requirements:
   - Section 6: Multi-year financial track record with GAAP clarity
   - Section 7: Long-term margin expansion story (Rule of 40 trajectory)
   - Section 8: Deep bench of public company-ready executives
4. Generate equity story with public market rigor:
   - Conservative market sizing with multiple methodologies
   - Detailed cohort analysis and retention metrics
   - Clear path to 25%+ FCF margins at scale

**Output:**
- `outputs/equity-stories/2025-12-14_infraco-equity-story.md`
- Public market-grade rigor and disclosure
- Emphasizes durability, predictability, and long-term margin expansion
- Positions for IPO valuation of 10-12x forward revenue

---

## Success Criteria

A successful equity story:
1. **Builds structural conviction** - Each section logically builds toward investment thesis
2. **Is evidence-based** - Claims backed by data, metrics, or validated traction
3. **Answers investor questions** - Why now, why this company, why this team, why this return
4. **Balances growth and risk** - Honest about opportunities and execution challenges
5. **Is audience-appropriate** - Tone and depth match ICP expectations (PE vs IB vs C-suite)
6. **Is slide deck ready** - Clear sections, scannable structure, visual content suggestions
7. **Reflects voice DNA** - Calm, analytical, structural clarity, no unsubstantiated superlatives
8. **Can survive due diligence** - Every claim can be supported in follow-up diligence
9. **Differentiates meaningfully** - Clear explanation of why THIS company wins
10. **Provides roadmap for next stages** - Foundation for pitch deck, teaser, or investor presentation

An equity story should feel like it was prepared by a top-tier investment bank for a major capital markets transaction, not hastily generated.

---

## Notes on Skill Philosophy

**Why the 8-section structure matters:**
This framework is battle-tested across IPOs, M&A, and private rounds because it systematically addresses every dimension of investment risk:
1. Market risk (Section 1)
2. Product risk (Section 2)
3. GTM execution risk (Section 3)
4. Competitive risk (Section 4)
5. Business model risk (Section 5)
6. Historical performance risk (Section 6)
7. Growth trajectory risk (Section 7)
8. Management execution risk (Section 8)

**Flexibility within structure:**
- Not all sections require equal weight - adjust emphasis based on company stage and audience
- Pre-revenue companies will emphasize Sections 1-4 heavily, with Sections 5-6 as projections
- Mature companies will emphasize Sections 5-7, with Section 1 as context
- M&A contexts may de-emphasize Section 8 if team transition is uncertain

**Research-first philosophy:**
This skill is designed to be a **synthesis engine**, not a content creator from scratch. The strongest equity stories emerge from rigorous upstream research. Always suggest running research skills when user provides only a company name.
