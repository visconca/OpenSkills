# Risks & Mitigants Slide Generator

## Purpose
Generate slide-ready "Risks & Mitigants" content for pitch decks by analyzing existing equity stories. Extracts, prioritizes, and structures investment risks with specific mitigating factors in a format optimized for executive presentation.

## When to Use
- After completing an equity story for a company
- When preparing pitch deck materials for investment committees
- When board presentations or investor updates require risk disclosure
- When converting equity stories to investor presentations

## Default ICP
**icp-pe-professionals.json** (primary), **icp-direct-colleagues.json** (for internal banking presentations), or **icp-BoD-directors.json** (for board materials)

## Context Requirements
1. **MUST READ**: `context/voice_dna.json` for tone and style
2. **MUST READ**: Appropriate ICP file (default: `icp-pe-professionals.json`)

## Output Location
Save all risks & mitigants slides to: `outputs/pitch-books/`

Naming convention: `YYYY-MM-DD_{company-name}-risks-mitigants.md`

Example: `2025-12-14_acme-corp-risks-mitigants.md`

## Input Requirements

**Required from User:**
1. Company name
2. Path to existing equity story (or equity story will be auto-detected from `outputs/equity-stories/`)

**Optional Context:**
- Specific risk areas to emphasize (market, competitive, execution, financial, regulatory)
- Presentation context (board meeting, investment committee, due diligence)

## Core Instructions

### Pre-Execution Checklist
Before analyzing, confirm:
1. [ ] Company name identified
2. [ ] Equity story located and readable
3. [ ] Context files read (voice_dna + appropriate ICP)
4. [ ] Output file path determined

### Execution Steps

**Step 1: Locate and Read Equity Story**
- Check `outputs/equity-stories/` for most recent equity story matching company name
- If multiple exist, use the most recent (by date in filename)
- Read the complete equity story to understand full investment context

**Step 2: Extract Risk Universe**
Systematically extract risks from equity story sections:
- Section 1 (Market Opportunity): Market size risks, TAM assumptions, regulatory headwinds
- Section 2 (Product): Product-market fit risks, technical debt, roadmap execution
- Section 3 (GTM Strategy): Sales execution, CAC/LTV economics, channel dependencies
- Section 4 (Competitive Advantage): Moat erosion, competitive response, pricing pressure
- Section 5 (Business Model): Margin compression, churn, revenue concentration
- Section 6 (Financials): Burn rate, path to profitability, unit economics
- Section 7 (Potential Upside): Dependency on specific catalysts, market timing
- Section 8 (Management Team): Founder dependency, talent retention, execution capability

**Step 3: Categorize and Prioritize Risks**
Group risks into standard categories:
1. **Market Risk**: TAM assumptions, market timing, demand shifts
2. **Competitive Risk**: Incumbent response, new entrants, pricing pressure
3. **Execution Risk**: Management capability, operational scalability, product roadmap delivery
4. **Financial Risk**: Burn rate, capital needs, unit economics deterioration
5. **Customer Risk**: Concentration, churn, expansion rates
6. **Technology Risk**: Technical debt, product scalability, platform dependencies
7. **Regulatory Risk**: Compliance requirements, legal exposure, policy changes
8. **People Risk**: Key person dependency, talent retention, organizational scaling

**Prioritization Framework:**
Rank each risk by:
- **Materiality**: Impact on valuation if risk materializes (High/Medium/Low)
- **Probability**: Likelihood of occurrence (High/Medium/Low)
- **Timeframe**: When risk could manifest (Near-term: 0-12 months, Medium-term: 1-3 years, Long-term: 3+ years)

Select top 8 risks by combined materiality × probability score.

**Step 4: Structure Each Risk**
For each of the top 8 risks, create:

```markdown
## [Risk #]: [Risk Category]

**Risk Description:**
[1-2 sentences describing the specific risk. Focus on what could go wrong and why it matters to investment returns. Be concrete, not generic.]

**Materiality:** [High/Medium/Low] | **Probability:** [High/Medium/Low] | **Timeframe:** [Near/Medium/Long-term]

**Mitigants:**
1. [Specific mitigating factor #1 - company actions, structural advantages, or market dynamics that reduce risk]
2. [Specific mitigating factor #2]
3. [Specific mitigating factor #3 - typically 2-4 mitigants per risk]
4. [Specific mitigating factor #4 - optional]

**Residual Risk:** [After mitigants, is residual risk High/Medium/Low? One sentence assessment.]
```

**Step 5: Format for Slide Presentation**
After documenting all 8 risks in detail, create a slide-friendly summary:

```markdown
---

## SLIDE FORMAT: Risks & Mitigants Summary

### Risk Matrix Overview

| # | Risk Category | Materiality | Probability | Key Mitigant |
|---|--------------|-------------|-------------|--------------|
| 1 | [Category] | [H/M/L] | [H/M/L] | [One-line mitigant] |
| 2 | [Category] | [H/M/L] | [H/M/L] | [One-line mitigant] |
| ... | ... | ... | ... | ... |

### Detailed Slide Content (One Slide Per Risk)

**SLIDE: Risk #1 - [Risk Category]**

**Risk:**
- [Bullet point 1: What could go wrong]
- [Bullet point 2: Why it matters]

**Mitigants:**
- [Mitigant 1 in bullet form]
- [Mitigant 2 in bullet form]
- [Mitigant 3 in bullet form]

**Bottom Line:** [One sentence: After mitigants, is this risk acceptable?]

---

[Repeat for all 8 risks]
```

**Step 6: Apply Voice and Tone**
- Use voice_dna.json principles: calm, analytical, trade-off oriented
- Avoid fear-mongering or downplaying risks
- Present balanced assessment: acknowledge risks, then show why they're manageable
- Use short sentences, explicit logic
- No buzzwords or corporate speak ("headwinds," "challenges," "opportunities disguised as risks")

**Step 7: Quality Checks**

Before finalizing, verify:
- [ ] All 8 risks are material and specific (not generic)
- [ ] Each risk has concrete mitigants (not vague "management will address")
- [ ] Risks cover multiple categories (not all competitive or all execution)
- [ ] Slide format is concise enough for executive presentation (3-4 bullets max per risk)
- [ ] Residual risk assessment is honest (some risks remain high even with mitigants)
- [ ] Tone matches ICP expectations (PE professionals want balanced realism, not cheerleading)

### Risk Prioritization Examples

**Good Risk (Specific, Material, Actionable Mitigants):**
```
Risk: Cloud Provider Vertical Integration
Description: AWS, Azure, and Google Cloud could prioritize their own Linux distributions over Ubuntu, reducing Canonical's cloud instance market share from 40% to 25-30% within 3 years.
Mitigants:
1. Multi-cloud portability is Canonical's core value prop; hyperscaler distributions lock customers into single clouds
2. Deep integrations with all three clouds create switching costs for cloud providers
3. Developer preference for Ubuntu creates bottom-up demand that cloud providers must satisfy
Residual Risk: Medium. Cloud provider strategies could shift, but multi-cloud enterprise trend supports Ubuntu.
```

**Bad Risk (Generic, Vague, Weak Mitigants):**
```
Risk: Market Competition
Description: The market is competitive and Canonical faces challenges.
Mitigants:
1. Strong team
2. Good product
3. Management is focused on execution
Residual Risk: To be determined.
```

**Why Bad Example Fails:**
- "Market competition" is too generic (which competitors? what specific threat?)
- Mitigants are vague ("strong team" - compared to what? how does this reduce competitive risk?)
- No materiality assessment
- Not slide-ready (too abstract)

### Risk-Mitigant Pairing Logic

**For Market Risks:**
- Mitigants: TAM validation sources, multiple market entry strategies, diversified use cases
- Example: "If primary market (X) contracts, company has proven traction in adjacent market (Y)"

**For Competitive Risks:**
- Mitigants: Structural advantages (network effects, switching costs), cost position, product differentiation
- Example: "While competitors (A, B) could respond, company's cost structure creates 30-50% pricing advantage that's difficult to match"

**For Execution Risks:**
- Mitigants: Team track record, operational metrics showing capability, external validation
- Example: "Management has scaled ARR from $X to $Y over 3 years; current growth rate suggests execution capability"

**For Financial Risks:**
- Mitigants: Cash runway, path to profitability milestones, capital efficiency metrics
- Example: "At current burn rate, company has 24 months runway; achieves cash-flow breakeven at $X ARR (18 months away at current growth)"

**For Customer Risks:**
- Mitigants: Customer diversification, retention metrics, contract structure
- Example: "Top 10 customers represent 30% of revenue (down from 50% in 2023); 95% gross retention shows product stickiness"

**For Technology Risks:**
- Mitigants: Architecture decisions, technical debt paydown plans, scalability testing
- Example: "Platform redesign (2024) addressed technical debt; system now scales to 10x current volume without re-architecture"

**For Regulatory Risks:**
- Mitigants: Compliance certifications, legal counsel, government relations
- Example: "Company achieved SOC2 Type II (2024) and is pursuing FedRAMP (2025); pre-emptive compliance investments reduce regulatory risk"

**For People Risks:**
- Mitigants: Succession planning, equity retention packages, organizational depth
- Example: "Founder transitioned from CEO to Chairman (2023); new CEO has 15 years enterprise software experience; leadership team depth reduces key person risk"

---

## Output Format

Save ONE file per company to `outputs/pitch-books/`:

**File:** `outputs/pitch-books/YYYY-MM-DD_{company-name}-risks-mitigants.md`

### Document Structure:

```markdown
# RISKS & MITIGANTS: [Company Name]

**Prepared For:** [ICP Audience]
**Date:** [YYYY-MM-DD]
**Source:** Equity Story Analysis

---

## Executive Summary

This analysis identifies the 8 most material investment risks and their mitigating factors. Risks are prioritized by materiality × probability. All risks are derived from the company's equity story and represent realistic scenarios that could impact investment returns.

**Overall Risk Profile:** [One paragraph: Is this a high-risk/high-return investment? Or moderate risk with solid mitigants? Be honest.]

---

## Risk #1: [Risk Category]

[Full risk structure as defined in Step 4]

---

## Risk #2: [Risk Category]

[Full risk structure]

---

[Continue for all 8 risks]

---

## APPENDIX: Slide-Ready Format

[Include slide summary matrix and individual slide content as defined in Step 5]

---

## Risk Management Recommendations

Based on this analysis, the investment committee should:
1. [Specific diligence question or follow-up action for Risk #1]
2. [Specific monitoring metric or milestone for Risk #2]
3. [Specific contractual protection or board governance for Risk #3]
[Continue for top 3-5 risks requiring active management]

---

**Prepared By:** Risks & Mitigants Analysis Team
**Methodology:** Systematic extraction from equity story, prioritized by materiality × probability
**Confidence Level:** [High/Medium] - Based on equity story quality and available information
```

---

## Quality Checklist

Before finalizing output, verify:
- [ ] All 8 risks extracted from equity story (not invented)
- [ ] Each risk is specific and material (not generic)
- [ ] Materiality and probability assessed explicitly
- [ ] Each risk has 2-4 concrete mitigants
- [ ] Mitigants are actionable or structural (not vague)
- [ ] Residual risk honestly assessed (not all "low")
- [ ] Risks span multiple categories (market, competitive, execution, financial, etc.)
- [ ] Slide format is presentation-ready (concise bullets, <5 bullets per risk)
- [ ] Tone is balanced (acknowledges risks without fear-mongering)
- [ ] Voice aligns with voice_dna.json (calm, analytical, trade-off oriented)
- [ ] Risk management recommendations are actionable

---

## Example Invocation

**User**: "Generate risks and mitigants for Canonical"

**Assistant**:
"I'll analyze the Canonical equity story and generate a Risks & Mitigants slide deck. Let me locate the equity story and extract the top 8 material risks."

[Reads equity story from outputs/equity-stories/]
[Extracts risks from all 8 sections]
[Prioritizes by materiality × probability]
[Structures each risk with mitigants]
[Formats for slides]
[Outputs to outputs/pitch-books/2025-12-14_canonical-risks-mitigants.md]

"I've identified 8 material risks:
1. Cloud Provider Vertical Integration (High materiality, Medium probability)
2. Red Hat Competitive Response (High materiality, Medium probability)
3. Open Source Commoditization (Medium materiality, Medium probability)
4. Managed Services Scalability (Medium materiality, Medium probability)
5. Enterprise Sales Execution (Medium materiality, High probability)
6. Customer Concentration (Medium materiality, Low probability)
7. Founder Dependency (High materiality, Low probability)
8. Pricing Pressure from Free Alternatives (Medium materiality, High probability)

The output includes detailed risk descriptions, mitigants, and slide-ready formats. Overall risk profile: Moderate. Most risks have strong structural mitigants."

---

## Downstream Applications

After completing risks & mitigants analysis:
- **pitch_book_workflow**: Integrate risks slide into full pitch deck
- **thought_leadership_crafter**: Use risk insights for strategic content
- **Investment committee memos**: Reference risks & mitigants in IC papers

---

## Success Criteria

A successful risks & mitigants analysis:
1. Identifies genuinely material risks (would matter to investment returns)
2. Prioritizes effectively (top 8 are truly the most important)
3. Provides specific, actionable mitigants (not generic management platitudes)
4. Balances honesty and confidence (acknowledges risks, shows why they're manageable)
5. Is slide-ready (executive can present without reformatting)
6. Generates actionable diligence questions or monitoring metrics
7. Reflects voice_dna.json tone (calm, analytical, trade-off oriented)
8. Aligns with ICP decision-making context (what PE professionals care about)
