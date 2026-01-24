# Pitch Preparation Intelligence Brief Generator

## Purpose
Generate comprehensive intelligence briefs for investment bankers competing for transaction mandates (M&A, IPO, capital raise, restructuring, etc.). Arms bankers with situation-specific insights, strategic theme analysis, CVB capability positioning, comparable transactions, and competitive differentiation to win mandates in pitches and RFPs.

## Context
Investment bankers compete for mandates by demonstrating: (1) deep understanding of the company's strategic situation, (2) relevant transaction expertise and capabilities, (3) credible execution plan, and (4) differentiation from competitors. This skill transforms company research and strategic analysis into actionable pitch intelligence that positions CVB as the natural choice for the transaction.

## Input Requirements

Ask the user for:
1. **Company name and industry**
2. **Transaction type**: M&A sell-side, M&A buy-side, IPO, Follow-on offering, Private capital raise (Series B/C/D), Debt financing, Financial restructuring, Dual-track (IPO/M&A), Spin-off/Carve-out, Secondary sale, SPAC transaction, Other
3. **Company stage/situation** (e.g., PE-backed preparing for exit, growth-stage pre-IPO, mature public company considering M&A, distressed requiring restructuring)
4. **Transaction context** (e.g., EUR 15B valuation, EUR 1.2B revenue, 22% growth, PE consortium ownership)
5. **Competitive landscape** (Who else is pitching? Goldman, Morgan Stanley, JPM? What are their strengths?)
6. **Pitch timing** (When is the pitch? How much time to prepare?)
7. **Optional**: Company memo or research materials in knowledge/ folder

## Data Sources

This skill MUST read two foundational Excel files:
- `knowledge/TOC/Content for IBD.xlsx` - Strategic themes taxonomy
- `knowledge/TOC/CVB-services-list.xlsx` - CVB services catalog

Optional additional sources:
- `outputs/company-memos/` - Company research from company_memo_analyst
- `knowledge/pitch-books/` - Any pre-existing company research materials

## Processing Logic

### Step 1: Load Foundational Data
Read both Excel files using Python with openpyxl (same as coverage_campaign_generator)

### Step 2: Analyze Company Situation and Map to Strategic Themes
Based on transaction type and company situation, identify 4-6 most relevant strategic themes:

**For M&A Sell-Side:**
- Primary: Equity Story Calibration, Growth themes (market positioning, product innovation), Financial Positioning, Risk Management
- Secondary: Optimization themes (margin expansion), Strategic Risks (competitive threats)

**For IPO:**
- Primary: Equity Story Calibration, Financial Positioning (margins, unit economics), Risk Management (ESG, regulatory), CapTable Considerations (ownership structure, governance)
- Secondary: Growth themes (TAM expansion, product roadmap), Investor Value Proposition

**For Private Capital Raise (Growth Equity):**
- Primary: Growth themes (market expansion, product innovation, GTM strategies), Financial Positioning (unit economics, LTV/CAC), Revenue Stream Exploitation
- Secondary: Risk Management, CapTable Considerations (dilution, investor alignment)

**For Debt Financing / Restructuring:**
- Primary: Liability Management (all themes), Cash Flow Management, Financial Risks, Asset Management
- Secondary: Cost Reduction, Working Capital Optimization, Investor Alignment

**For Dual-Track (IPO/M&A):**
- Primary: Equity Story Calibration, Exit Planning, Financial Positioning, Strategic M&A positioning
- Secondary: Growth themes, Risk Management, Investor Value Proposition

### Step 3: Select Relevant CVB Services
From CVB-services-list.xlsx, filter services matching:
- The transaction type (M&A, Capital Raising, Restructuring, etc.)
- The relationship stage (typically "Hunting" for pitch scenarios)
- The strategic themes identified

### Step 4: Identify Comparable Transactions
Based on transaction type and industry, reference relevant comparable transactions:
- Same transaction type (IPO, M&A, capital raise)
- Same or adjacent industry
- Similar company characteristics (size, growth, business model)

Note: This skill should suggest categories for comparables. Actual comparable transaction research should be done via `ma_case_study_generator` skill if needed.

### Step 5: Risk Analysis and CVB Mitigation
Identify transaction-specific risks using Risk Management themes from Excel:
- Financial risks (revenue concentration, margin pressure, debt levels)
- Strategic risks (competitive threats, market disruption, technology obsolescence)
- Regulatory/Compliance risks (ESG, data privacy, cross-border regulations)
- Execution risks (integration complexity, management retention, customer churn)

For each risk, articulate how CVB capabilities mitigate it.

### Step 6: Competitive Differentiation
Based on competitor intelligence (if provided), articulate:
- What CVB brings that competitors don't
- Where CVB has structural advantages (sector expertise, research coverage, investor relationships, execution track record)
- Deal team composition and relevant experience

## Output Format

Generate a markdown file with this structure:

```markdown
# Pitch Intelligence Brief: [Company Name] - [Transaction Type]

**Prepared for:** CVB [Team Name] Investment Banking
**Date:** [Date]
**Transaction:** [Transaction Type] ([Size/Valuation if known])
**Pitch Date:** [Date]
**Competing Banks:** [List if known]

---

## Executive Summary

[2-3 paragraph synthesis:
- Company's current situation and why this transaction now
- What makes this transaction compelling/complex
- Why CVB is uniquely positioned to win this mandate
- Key risks and how CVB mitigates them]

---

## Strategic Situation Analysis

### Company Profile
- **Business Model:** [Brief description]
- **Financial Profile:** [Revenue, growth, margins, valuation if known]
- **Ownership:** [PE-backed, founder-owned, public, consortium, etc.]
- **Stage:** [Growth, maturity, turnaround, etc.]

### Transaction Context
[Why is this transaction happening now? What's the strategic rationale?]

### Critical Strategic Themes for This Transaction

#### 1. [Theme 1 Name] - PRIORITY: HIGH
**Why This Matters:**
[Why this theme is critical for this transaction]

**Key Considerations:**
- [Specific aspect relevant to company situation]
- [Quantitative insight if available]
- [How this affects transaction positioning]

**CVB Capabilities:**
- [Relevant CVB service from services list]
- [Specific expertise or track record]

---

[Repeat for 4-6 strategic themes]

---

## CVB Capabilities Matrix

| Strategic Theme | Company Need | CVB Service | Track Record |
|-----------------|--------------|-------------|--------------|
| [Theme 1] | [Specific need] | [Service from list] | [Recent comparable deal or metric] |
| [Theme 2] | [Specific need] | [Service from list] | [Recent comparable deal or metric] |
| [Theme 3] | [Specific need] | [Service from list] | [Recent comparable deal or metric] |

---

## Comparable Transactions

**Relevant Transaction Categories:**
1. **[Category 1]**: [Transaction type] for [industry] companies with [characteristics]
   - Examples to research: [Company A], [Company B], [Company C]
   - Key metrics: [Valuation multiples, timing, process characteristics]

2. **[Category 2]**: [Transaction type] with [similar complexity]
   - Examples to research: [Company D], [Company E]
   - Key learnings: [What worked, what didn't]

**Note:** For detailed case study analysis, run `ma_case_study_generator` skill for specific transactions.

---

## Transaction Execution Roadmap

### Proposed Timeline ([X]-Month Process)

**Phase 1: Preparation & Positioning ([Timeframe])**
- [Key workstream 1]
- [Key workstream 2]
- [Key workstream 3]
- **CVB Services Engaged:** [Relevant services]

**Phase 2: [Process Phase] ([Timeframe])**
- [Key activities]
- [Milestones]
- **CVB Services Engaged:** [Relevant services]

**Phase 3: [Execution Phase] ([Timeframe])**
- [Key activities]
- [Closing considerations]
- **CVB Services Engaged:** [Relevant services]

**Phase 4: [Post-Transaction] ([Timeframe])**
- [Integration support / post-IPO support / other]
- **CVB Services Engaged:** [Relevant services]

---

## Risk Analysis & Mitigation

### Critical Risks

#### Risk 1: [Risk Name] - IMPACT: HIGH
**Description:** [What is the risk and why does it matter?]
**Probability:** [High/Medium/Low]
**Impact if Occurs:** [Specific consequences]
**CVB Mitigation Strategy:**
- [Specific CVB capability or approach]
- [Track record of handling similar risks]
- [Protective structuring or process design]

---

[Repeat for 5-8 key risks]

---

## Competitive Positioning

### Why CVB Wins This Mandate

**1. [Competitive Advantage 1]**
- [Specific differentiation]
- [Supporting evidence or track record]
- [How this helps client specifically]

**2. [Competitive Advantage 2]**
- [Specific differentiation]
- [Supporting evidence or track record]
- [How this helps client specifically]

**3. [Competitive Advantage 3]**
- [Specific differentiation]
- [Supporting evidence or track record]
- [How this helps client specifically]

### Competitor Analysis

**[Competitor 1]:**
- Strengths: [What they'll pitch]
- Weaknesses: [Where CVB is superior]
- Counter-positioning: [How to position against them]

**[Competitor 2]:**
- Strengths: [What they'll pitch]
- Weaknesses: [Where CVB is superior]
- Counter-positioning: [How to position against them]

---

## Deal Team & Credentials

**Proposed CVB Team:**
- **Lead Banker:** [Name, Title] - [Relevant experience]
- **Sector Coverage:** [Name, Title] - [Relevant experience]
- **Product Specialist:** [Name, Title] - [Relevant experience]
- **Execution:** [Names] - [Relevant experience]

**Team Credentials Summary:**
- [Number] similar transactions advised in past [X] years
- $[Amount] in aggregate transaction value
- [Sector-specific expertise or rankings]

---

## Key Messages for Pitch

### Opening Statement
"[Company] is at [strategic moment]. We believe [transaction type] is the right path because [core rationale]. CVB is uniquely positioned to advise this transaction because [3 key differentiators]. Our proposed [X]-month process will [key outcomes]."

### Core Messages (Rule of 3)
1. **[Message 1]**: [Supporting point]
2. **[Message 2]**: [Supporting point]
3. **[Message 3]**: [Supporting point]

### Anticipated Tough Questions & Responses

**Q: [Question client likely to ask]**
A: [Suggested response]

**Q: [Question about competitors]**
A: [Suggested response]

**Q: [Question about risk/concern]**
A: [Suggested response]

**Q: [Question about valuation/timing]**
A: [Suggested response]

---

## Appendix: Research References

**Sources Reviewed:**
- [Company memo, if available]
- [Financial statements, if available]
- [Market research, if available]
- [Competitor analysis, if available]

**Additional Research Recommended:**
- [ ] Run `ma_case_study_generator` for comparable transactions: [list]
- [ ] Run `company_news_signals_research` for recent developments
- [ ] Run `financial_positioning_research` for detailed comps analysis
- [ ] Prepare client-specific financial model with transaction scenarios
- [ ] Research competitor track record on similar mandates

---

## Next Steps Before Pitch

- [ ] Review and validate strategic themes with sector team
- [ ] Gather specific CVB transaction credentials for each comparable
- [ ] Prepare visual pitch deck based on this intelligence
- [ ] Rehearse pitch with internal team (focus on tough questions)
- [ ] Confirm deal team availability and engagement economics
- [ ] Schedule pre-pitch internal alignment call
```

## Voice & Tone

- **Banker-to-banker pragmatic**: This is an internal preparation tool
- **Competitive and confident**: Position CVB capabilities assertively
- **Evidence-based**: Support claims with specific track record, not generic statements
- **Client-centric**: Everything framed around client needs and outcomes
- **Concise but comprehensive**: Dense with insights, no fluff

## Constraints & Guidelines

1. **Situation-specific**: Every theme and capability must be directly relevant to THIS company and THIS transaction
2. **Evidence-based positioning**: Use specific deals, metrics, rankings—avoid generic "we're great at this"
3. **Risk transparency**: Acknowledge real risks honestly and show credible mitigation
4. **Competitive realism**: If competitor has an advantage in an area, acknowledge it and pivot to CVB strengths
5. **Actionable**: Banker should be able to walk into pitch with this brief and execute

## Output Location

Save to: `outputs/pitch-intelligence/YYYY-MM-DD_[company-name]-[transaction-type]-pitch-brief.md`

Example: `outputs/pitch-intelligence/2026-01-03_ifs-ipo-pitch-brief.md`

## ICP Selection

Use `context/icp-direct-colleagues.json` (this skill produces internal banker tools)

## Integration with Other Skills

**Before running this skill (recommended):**
- Run `company_memo_analyst` to gather company intelligence
- Run `financial_positioning_research` for competitive positioning
- Run `company_news_signals_research` for recent developments

**After running this skill (optional):**
- Run `ma_case_study_generator` for detailed comparable transaction analysis
- Run `pitch_book_workflow` to convert intelligence into client-facing pitch deck
- Run `audience_simulator` to stress-test pitch messaging with simulated client personas

## Execution Notes

When generating the pitch intelligence brief:
1. Start by reading and parsing both Excel files completely
2. Map company situation and transaction type to themes systematically
3. For each theme identified, pull specific sub-theme content from Excel files
4. Filter CVB services by transaction type category (M&A Advisory for M&A deals, Capital Raising for IPO/fundraise, etc.)
5. Be specific about HOW each CVB service addresses the company's specific situation—avoid generic capability statements
6. Identify 5-8 real risks (not theoretical)—use Risk Management sheet from Excel as source
7. For competitive positioning, be honest about competitor strengths but pivot to CVB differentiation
8. Provide 4-6 anticipated tough questions with credible responses
9. Ensure timeline is realistic and specific (not vague phases)
10. Cite any company research materials used (memos, research reports, etc.)

This skill should produce a complete, actionable brief that arms a banker for a competitive pitch meeting within 2-3 hours of preparation time.
