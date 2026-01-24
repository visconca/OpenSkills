# Coverage Campaign Generator

## Purpose
Generate multi-quarter coverage campaign plans for investment bankers to maintain consistent "share of mind" with key client constituencies when no immediate transaction is on the table. Helps bankers avoid "blanking out" on what to discuss during non-deal periods by providing a structured calendar of touchpoints, strategic themes, and specific actions.

## Context
Investment bankers excel in transaction mode but struggle with systematic coverage. Without disciplined touchpoints during non-deal periods, they lose share of mind and arrive late when transactions emerge. This skill transforms strategic content themes and service capabilities into actionable coverage calendars.

## Input Requirements

Ask the user for:
1. **Company name and industry**
2. **Company stage/situation** (e.g., growth-stage SaaS, mature enterprise, pre-IPO, post-acquisition, cost optimization phase)
3. **Key constituencies** (CFO, CEO, Board, Finance team, Operations, etc.)
4. **Current business context/challenges** (e.g., expanding internationally, optimizing costs, preparing for fundraise, managing debt)
5. **Relationship stage**: Nurturing, Farming, or Hunting
6. **Coverage period**: 3 months (quarterly) or 6 months (bi-annual)

## Data Sources

This skill MUST read two foundational Excel files:
- `knowledge/TOC/Content for IBD.xlsx` - Strategic themes taxonomy with nested sub-themes across 6 sheets: Growth, Optimization Initiatives, CapTable Considerations, Risk Management, Liability Management, Other Content
- `knowledge/TOC/CVB-services-list.xlsx` - CVB services mapped to marketing stages (Nurturing/Farming/Hunting)

## Constituency-Theme Affinity Matrix

**CRITICAL:** Not all themes scale to all constituencies. Use this matrix to ensure appropriate content routing:

### CEO
- **Primary Themes:** Growth (all sub-themes), M&A Strategy, Market Expansion, Product Innovation, Platform Development, Strategic Partnerships, Revenue Monetization
- **Secondary Themes:** Risk Management (strategic risks only), Equity Story, Competitive Positioning
- **Exclude:** Tactical financial mechanics (debt covenants, working capital details, treasury operations)

### CFO
- **Primary Themes:** ALL financial themes (Liability Management, Capital Raising, Debt Structuring, Cash Flow Management, FX Risk, Cost Optimization, Treasury, Interest Rate Management, Asset Management)
- **Secondary Themes:** Growth (with financial ROI lens), Risk Management (financial risks), Infrastructure Economics, Operational Efficiency (margin impact)
- **Scalable:** Any theme if tied to financial impact

### Board of Directors
- **Primary Themes:** Governance, Risk Management (all types), ESG, Strategic Risks, Equity Story Comparison, CapTable Considerations, Shareholder Value
- **Secondary Themes:** High-level Growth themes, M&A strategy (board approval lens), Long-term value creation
- **Exclude:** Operational/tactical execution details, day-to-day financial operations

### COO / Operations Leaders
- **Primary Themes:** Operational Efficiency, Cost Reduction, Infrastructure Optimization, Workforce Productivity, DevOps, Scaling Operations, Supply Chain
- **Secondary Themes:** Growth (operational scaling lens), Risk Management (operational risks)
- **Exclude:** Financial structuring, investor relations, governance

### CTO / Product Leaders
- **Primary Themes:** Product Innovation, AI/ML Integration, Technical Architecture, Infrastructure Economics, Technical Debt, Platform Development, Developer Ecosystem
- **Secondary Themes:** Growth (product-led growth), API Economy, Cloud Economics
- **Exclude:** Financial structuring, governance, capital raising

### General Counsel / Compliance
- **Primary Themes:** Regulatory Risk, ESG, Governance, Cross-Border Compliance, Antitrust, Data Privacy
- **Secondary Themes:** M&A (regulatory approval lens), Strategic Risks (legal exposure)
- **Exclude:** Growth strategy, operational efficiency, product development

### Shareholders / Investors (non-Board)
- **Primary Themes:** Equity Story, CapTable Management, Exit Planning, Value Enhancement, Financial Positioning, Liquidity Events
- **Secondary Themes:** Growth themes (valuation impact), Risk Management (investment risks)
- **Exclude:** Operational details, tactical execution, day-to-day management

### Finance Team / VP Finance
- **Primary Themes:** Working Capital, Cash Flow Forecasting, Treasury Operations, Financial Planning, Budgeting, Cost Management
- **Secondary Themes:** Growth (budget implications), Infrastructure Economics (FinOps)
- **Exclude:** Strategic M&A, board-level governance, shareholder relations

---

## Processing Logic

### Step 1: Load Foundational Data
Read both Excel files using Python with openpyxl:
```python
from openpyxl import load_workbook

# Load strategic themes
content_wb = load_workbook('knowledge/TOC/Content for IBD.xlsx')
themes = {}
for sheet_name in content_wb.sheetnames:
    sheet = content_wb[sheet_name]
    # Parse themes and sub-themes from each sheet

# Load CVB services
services_wb = load_workbook('knowledge/TOC/CVB-services-list.xlsx')
services_data = services_wb['dataset']
# Filter by relationship stage
```

### Step 2: Map Client Situation to Strategic Themes
Analyze the company's stage and challenges to identify the 3-5 most relevant strategic themes from the content taxonomy:

- **Growth-stage companies** → Market Penetration, Geographic Expansion, Revenue Stream Exploitation, Product Innovation
- **Optimization phase** → Cost Reduction, Operational Efficiency, Customer Retention, Infrastructure Economics
- **Pre-transaction** → CapTable Considerations, Equity Story Comparison, Financial Risk Management
- **Post-acquisition** → M&A Integration, Synergy Identification, Post-Merger Integration
- **Debt concerns** → Liability Management, Debt Restructuring, Cash Flow Management

### Step 3: Map Themes to Constituencies
For each identified strategic theme, determine constituency relevance using the affinity matrix:
- **Primary match** = Theme is core to this constituency's responsibilities (must include)
- **Secondary match** = Theme is relevant with appropriate framing (include if capacity allows)
- **Exclude** = Theme is not relevant to this constituency (never include)

Create constituency-specific theme lists based on the company's key constituencies provided by user.

### Step 4: Select Relevant CVB Services
From the services list, filter services matching:
- The relationship stage (Nurturing/Farming/Hunting)
- The strategic themes identified
- The constituencies involved

### Step 5: Generate Coverage Calendar
Create 8-12 touchpoints per quarter with:
- **Distribution**: 60% emails/research shares, 20% meetings, 20% case studies
- **Frequency**: 1 touchpoint every 1-2 weeks
- **Variety**: No two consecutive touchpoints on same theme
- **Progression**: Early touchpoints = value-giving insights, later touchpoints = service positioning
- **Constituency coverage**: Ensure balanced distribution across all constituencies (no constituency should be ignored for >3 weeks)

### Step 6: Structure Each Touchpoint
Every touchpoint must include:
1. **Week range** (e.g., "Week 3-4")
2. **Constituency relevance tags** (Primary/Secondary/All)
3. **Strategic theme** (from Content for IBD.xlsx)
4. **Touchpoint type** (Email, Meeting, Research Share, Case Study)
5. **Content angle** (specific topic/insight)
6. **CVB services to position** (from services-list.xlsx)
7. **3-5 talking points** (what to say)
8. **Deliverable** (what banker sends/presents)

## Output Format

Generate a markdown file with this structure:

```markdown
# Coverage Campaign: [Company Name]

**Period:** [Start Date] to [End Date]
**Relationship Stage:** [Nurturing/Farming/Hunting]
**Key Constituencies:** [List all]
**Strategic Focus Areas:** [Top 3-5 themes identified]

---

## Coverage Matrix

| Constituency | Total Touchpoints | Primary | Secondary | Shared |
|--------------|-------------------|---------|-----------|---------|
| CEO          | X               | Y       | Z         | N       |
| CFO          | X               | Y       | Z         | N       |
| Board        | X               | Y       | Z         | N       |
| [Others...]  | X               | Y       | Z         | N       |

*Primary = touchpoint designed specifically for this constituency*
*Secondary = touchpoint relevant but not core*
*Shared = all-hands strategic content*

---

## Campaign Architecture

[2-3 paragraphs explaining:
- Why these themes matter to this client right now
- How the campaign sequences value delivery with service positioning
- How constituency coverage is balanced and sequenced
- Expected outcomes and engagement metrics]

---

## Quarter [X] Coverage Calendar

### Week 1-2: [Theme Name]

**👥 Constituency Relevance:**
- **Primary:** [CEO/CFO/etc.] - [Brief rationale why]
- **Secondary:** [Others] - [Brief rationale]
- **Exclude:** [Who doesn't receive this and why]

**Touchpoint Type:** [Email/Meeting/Research Share/Case Study]
**Strategic Theme:** [From Content for IBD taxonomy]
**Content Angle:** [Specific topic/insight to deliver]

**CVB Services to Position:**
- [Service 1 from services list]
- [Service 2 from services list]

**Talking Points:**
- [Key point 1 - specific, actionable insight]
- [Key point 2 - tied to their business context]
- [Key point 3 - bridges to CVB capability]

**Deliverable:** [What banker sends/presents - be specific]

**Preparation Time:** [Est. 15-30 minutes]

---

[Repeat for each touchpoint across 12 weeks]

---

## Success Metrics & Follow-Up Actions

**Engagement Tracking:**
- Response rate to emails (target: >40%)
- Meeting conversion rate (target: >60% acceptance)
- Inbound inquiries generated

**Next Campaign Iteration:**
- Themes to emphasize in Q[X+1]
- Services to introduce next
- Relationship stage evolution

**CRM Notes:**
[Template for logging coverage activities]
```

## Voice & Tone

- **Banker-to-banker pragmatic**: This is an internal tool, not client-facing content
- **Action-oriented**: Every touchpoint = specific, executable action
- **Strategic but practical**: No fluff, high utility, realistic workload
- **Time-conscious**: Each touchpoint designed for <30min prep time

## Constraints & Guidelines

1. **Realistic workload**: Maximum 12 touchpoints per quarter (1 every 7-10 days)
2. **Variety**: Mix touchpoint types - no more than 3 consecutive emails
3. **Value first**: Early touchpoints focus on giving insights, later ones on service positioning
4. **Constituency-appropriate depth**:
   - CFO → Financial rigor, metrics, ROI
   - CEO → Strategic vision, competitive positioning
   - Board → Governance, risk, long-term value
   - Finance team → Operational tactics, implementation
5. **Theme sequencing**: Logical flow (e.g., Growth themes → Optimization → Risk Management)
6. **Service relevance**: Only position services genuinely relevant to the touchpoint theme

## Output Location

Save to: `outputs/coverage-campaigns/YYYY-MM-DD_[company-name]-[period]-coverage-plan.md`

Example: `outputs/coverage-campaigns/2026-01-03_acme-corp-q1-coverage-plan.md`

## ICP Selection

Use `context/icp-direct-colleagues.json` (this skill produces internal banker tools, not client-facing content)

## Example Touchpoint (for reference)

### Week 3-4: Geographic Expansion Readiness

**👥 Constituency Relevance:**
- **Primary:** CFO, VP Finance - Core financial/operational execution responsibility for international expansion; need pricing, compliance, and working capital strategies
- **Secondary:** CEO - Strategic oversight of expansion timing and market selection
- **Exclude:** Board (too operational for board-level), CTO (not technical architecture focus)

**Touchpoint Type:** Email with attached research
**Strategic Theme:** Market Penetration and Expansion → Geographic Expansion
**Content Angle:** EMEA market entry playbook for SaaS companies - compliance & pricing elasticity

**CVB Services to Position:**
- Market Entry & Expansion Strategies
- Corporate Strategy & Business Model Optimisation
- FX risk management, interest rate hedging

**Talking Points:**
- Regional pricing elasticity varies 30-50% across EMEA markets - single EUR pricing leaves money on table
- Data residency and GDPR compliance frameworks typically add 4-6 months to GTM timeline - proactive planning accelerates
- Multi-currency cash management and FX hedging strategies reduce working capital needs by 15-20% in expansion phase
- CVB recently advised [Similar Company] on EMEA expansion - reduced time-to-revenue by 40% with structured market entry playbook

**Deliverable:** 2-page brief - "EMEA Expansion Checklist for SaaS: Compliance, Pricing, and Working Capital Optimization" (use case study from recent CVB engagement if available)

**Preparation Time:** 25 minutes

---

## Execution Notes

When generating the campaign:
1. Start by reading and parsing both Excel files completely
2. Map client situation to themes systematically (don't guess)
3. **Use the Constituency-Theme Affinity Matrix rigorously** - never send irrelevant content to constituencies
4. For each touchpoint, explicitly state Primary/Secondary/Exclude with brief rationale
5. Ensure balanced coverage: no constituency should go >3 weeks without a touchpoint
6. Vary content types and constituencies to maintain engagement
7. Sequence logically: insights early, services positioning later
8. Create "shared" touchpoints (all constituencies) for 2-3 strategic moments per quarter
9. Be specific in deliverables (not "send an email" but "send 2-page brief on [topic]")
10. Include realistic time estimates so bankers can plan workflow
11. Generate the Coverage Matrix table to show distribution at a glance

This skill should produce a complete, executable coverage plan that bankers can follow week-by-week without further strategic thinking required.
