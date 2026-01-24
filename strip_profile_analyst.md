# Strip Profile Analyst

## Purpose
Generate concise, standardized "strip profiles" for one or multiple companies. Each profile fits on **½ page or less**, designed for market maps, coverage initiation notes, pitch decks, investment committee overviews, and screening workflows.

## When to Use
- Rapid company profiling across a sector or market
- Creating comparable snapshots for many companies at once
- Supplementing deeper memos or diligence with high-level overviews
- Building internal company databases or coverage lists
- Pre-work for pitch_book_workflow or company_memo_analyst
- Competitive landscape mapping

## Default ICP
**icp-pe-professionals.json** (primary) or **icp-direct-colleagues.json** (for internal banking use)

Use icp-c-suite.json if profiles are for executive strategic review.

## Context Requirements
1. **MUST READ**: `context/voice_dna.json` for tone and style
2. **MUST READ**: Appropriate ICP file (default: `icp-pe-professionals.json`)

## Output Location
Save all strip profiles to: `outputs/company-strip-profiles/`

**Naming convention**:
- Single company: `YYYY-MM-DD_{company-name}-strip-profile.md`
- Multiple companies: `YYYY-MM-DD_{sector-or-theme}-strip-profiles.md`

Examples:
- `2025-12-14_stripe-strip-profile.md`
- `2025-12-14_payments-infrastructure-strip-profiles.md`

## Input Sources
This skill relies on **authoritative public sources only**.

**Allowed Sources**:
- Company official website / About page
- Investor relations pages
- Regulatory filings (10-K, 10-Q for public companies)
- Crunchbase / PitchBook (factual data only, not estimates)
- Bloomberg / Financial Times / Reuters company profiles
- Recent funding announcements from reputable sources
- Wikipedia (foundational facts only)

**Exclusions**:
- Blog posts or SEO content
- Unverified estimates or projections
- Rumor-based valuations
- Social media claims
- Marketing hyperbole

**Evidence Standard**: If information is not publicly disclosed, explicitly state:
> "Not publicly disclosed."

## Research Integration
Strip profiles can be enhanced by prior research outputs:

**Optional Pre-Research**:
- 10k_research_assistant → Financial fundamentals
- company_news_signals_research → Recent developments
- financial_positioning_research → Comp set context

If research exists in `knowledge/company-strip-profiles/`, read and synthesize it. Otherwise, conduct focused web research during execution.

## Core Instructions

### Pre-Execution: Gather Input
Before starting, ask the user:

> "Please list the company or companies you want to profile (comma-separated).
> Optionally include tickers if public, or specify a sector/theme if profiling multiple companies."

**Example inputs**:
- Single: "Stripe"
- Multiple: "Stripe, Adyen, Checkout.com"
- Sector-based: "European payments infrastructure companies"

### Execution Steps

1. **Identify Companies**
   - Parse user input to extract company names
   - Determine if single or batch profiling
   - Note any public tickers provided

2. **Research Each Company**
   For each company, systematically gather:
   - Official website and About page
   - Latest funding or financial disclosures
   - Ownership structure (if public or disclosed)
   - Headquarters and founding date
   - Core product/service description
   - Target market and customer profile

3. **Generate Strip Profile(s)**
   Use the **exact structure below** for each company:

   ```markdown
   ## {Company Name}

   **Business Description**
   1–2 sentences describing:
   - What the company does
   - Who it serves
   - The core product or service

   ---

   **Channel, Market & ICP**
   - **Primary channel(s):** (e.g. direct sales, self-serve, channel partners, marketplace)
   - **Market:** (e.g. SMB, mid-market, enterprise, consumer, prosumer)
   - **ICP:** (role, company size, industry vertical)

   ---

   **Founded / Headquarters**
   - **Founded:** YYYY
   - **Headquarters:** City, Country

   ---

   **Key Financials**
   - **Revenue:** {latest reported figure with year, or "Not publicly disclosed"}
   - **Equity Value / Market Cap:** {if public; else "N/A"}
   - **Funding:** {total funding raised + latest round if private, or "N/A" if public}

   ---

   **Major Shareholders / Owners**
   - **Public company:**
     - Top institutional holders (if available from public filings)
   - **Private company:**
     - Lead investors / notable shareholders
     - Founder ownership percentage (if disclosed)

   If ownership structure is unclear or undisclosed:
   > "Detailed ownership not publicly disclosed."

   ---
   ```

4. **Apply Voice and Tone**
   - **Factual and concise**: No marketing language or superlatives
   - **Analytical**: Focus on structural facts (channel, market, ICP)
   - **Honest about gaps**: Flag missing data explicitly rather than guessing
   - Use voice_dna.json principles: calm, grounded, low adjective density
   - Write for decision-makers who need comparable snapshots

5. **Maintain Comparability**
   - Use consistent structure for all profiles
   - Apply same evidence standards across companies
   - Format bullets uniformly
   - Keep each profile to ½ page maximum

### Quality Checks Before Output
- [ ] Business description is 1-2 sentences, not a paragraph
- [ ] Channel, Market & ICP are specific (not generic)
- [ ] Financials distinguish "not disclosed" from "not applicable"
- [ ] No speculation or inference presented as fact
- [ ] Ownership section clearly separates public vs private treatment
- [ ] Consistent formatting across all profiles
- [ ] Each profile fits on ½ page or less
- [ ] Tone aligns with voice_dna.json (factual, grounded, analytical)

## Multi-Company Output Format

When profiling **multiple companies**, structure output as:

```markdown
# Strip Profiles: {Sector or Theme}
**Date:** {YYYY-MM-DD}
**Companies:** {Company A, Company B, Company C, ...}

---

[Strip Profile for Company A]

---

[Strip Profile for Company B]

---

[Strip Profile for Company C]

---

## Sources & Methodology
This analysis is based on publicly available information from:
- Company websites and investor relations pages
- Regulatory filings (where applicable)
- Verified funding announcements
- Reputable financial news sources

Information marked "Not publicly disclosed" indicates unavailability of verified data.

---

## Disclosures
This document is for informational purposes only.
It is based on publicly available information and does not constitute investment advice.
```

## Example Invocation

**User**: "Create strip profiles for Stripe, Adyen, and Checkout.com"

**Assistant**:
"I'll create standardized strip profiles for Stripe, Adyen, and Checkout.com. Each profile will cover:
- Business description
- Channel, market, and ICP
- Founding and headquarters
- Key financials (revenue, market cap/funding)
- Major shareholders

I'll use only publicly available, verified sources. Where information isn't disclosed, I'll state that explicitly. Let me research and generate the profiles now."

## Pipeline Integration

Strip profiles fit into your research workflow:

**Pre-Strip Profile** (optional but recommended for depth):
- 10k_research_assistant → Latest financials
- company_news_signals_research → Recent developments
- financial_positioning_research → Comp set context

**Post-Strip Profile** (downstream applications):
- **pitch_book_workflow**: Use profiles as competitive landscape slides
- **company_memo_analyst**: Expand specific profiles into full memos
- **market_analysis_deep_dive**: Use profiles as player mapping input

## Batch Processing Workflow

For **sector-wide profiling**, suggest this workflow:

1. User requests: "Profile 10 vertical SaaS companies"
2. Ask user for specific company list
3. Generate all profiles in single file
4. Suggest next steps:
   - "Would you like me to expand any of these into full company memos?"
   - "Should I create a competitive positioning framework from these profiles?"
   - "Would you like pitch deck slides based on this landscape?"

## Success Criteria
A successful strip profile:
1. Fits on ½ page or less
2. Contains only verified, factual information
3. Explicitly flags undisclosed data
4. Uses consistent structure across companies
5. Enables rapid comparison and decision-making
6. Reflects voice_dna.json tone (factual, grounded, analytical)
7. Could be dropped directly into a pitch deck or IC memo
8. Maintains investment-grade evidence standards
