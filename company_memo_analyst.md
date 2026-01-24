# Company Memo Analyst

## Purpose
Generate investment-grade company analysis memos for private equity, investment banking, and strategic analysis. Produces structured, analytical memos that synthesize company positioning, market dynamics, competitive landscape, and investment considerations with PE/IB-grade rigor.

## When to Use
- Due diligence preparation for investment committees
- Pre-pitch research for banker colleagues
- Portfolio company deep-dives for PE professionals
- Strategic assessment for board directors or C-suite
- Systematic company research before pitch_book_workflow

## Default ICP
**icp-pe-professionals.json** (primary) or **icp-direct-colleagues.json** (for internal banking use)

Use icp-BoD-directors.json if the memo is for board-level strategic review.

## Context Requirements
1. **MUST READ**: `context/voice_dna.json` for tone and style
2. **MUST READ**: Appropriate ICP file (default: `icp-pe-professionals.json`)

## Output Location
Save all memos to: `outputs/company-memos/`

Naming convention: `YYYY-MM-DD_{company-name}-memo.md`

Example: `2025-12-14_acme-corp-memo.md`

## Input Sources
This skill can work with or without pre-uploaded research:

**With Research (Recommended)**:
- Read from `knowledge/company-memos/` folder
- Ideal inputs:
  - 10-K or annual reports (from 10k_research_assistant)
  - News and signals research (from company_news_signals_research)
  - Product positioning research (from product_positioning_pricing_research)
  - Financial positioning research (from financial_positioning_research)
  - Market analysis (from market_analysis_deep_dive)
  - Company websites, investor decks, press releases

**Without Research**:
- Gather information through web search and synthesis during execution
- Ask user for company name, sector, and any known context
- Build memo from publicly available information

## Research-First Workflow
When user requests a company memo, proactively suggest:

> "I can create a comprehensive company memo for [Company]. To ensure PE/IB-grade rigor, would you like me to first run a full research cycle? I can:
> 1. Retrieve their latest 10-K and investor documents (10k_research_assistant)
> 2. Gather 12 months of news and market signals (company_news_signals_research)
> 3. Analyze product positioning and pricing (product_positioning_pricing_research)
> 4. Build financial comp set analysis (financial_positioning_research)
>
> This creates a strong data foundation. Should I run research first, or do you already have materials ready?"

## BATCH EXECUTION MODE (For DeepSeek or Token-Limited Models)

**CRITICAL**: This skill generates comprehensive company memos (~4,000-6,000 words, 6,000-9,000 tokens). DeepSeek-chat has a ~4,000-4,500 token output limit.

**Detection:** If using DeepSeek or another model with <5,000 token output limit, execute in TWO batches automatically.

**Batch 1: Foundation + Analysis**
Generate and save to output file:
- Memo Header (company, sector, date)
- Thesis (core insight, structural shift, differentiation)
- Founding Story (origin, founder background, inflection moments)
- Product & Value Proposition (what they sell, buyer, pain points, differentiation)
- Market & Opportunity (TAM/SAM, growth drivers, positioning)

**Batch 2: Competitive + Investment View**
APPEND to the same output file:
- Competitive Landscape (direct competitors, positioning, market dynamics)
- Business Model & Unit Economics (revenue streams, pricing, margins, scalability)
- Traction & Metrics (customers, growth rates, retention, milestones)
- Management & Organization (team strength, culture, execution capability)
- Investment Considerations (strengths, risks, catalysts, valuation context)
- Sources & Methodology (research trail, data quality assessment)

**File Management:**
- Batch 1: Create file with "--- BATCH 2 TO FOLLOW ---" marker at end
- Batch 2: Remove marker and complete the memo

**Note:** For complete output with DeepSeek:
1. Manually execute 2 separate prompts, each appending to the file
2. Use Claude (no limit) for single-pass execution
3. Use deepseek-reasoner (higher limit, may complete in single batch)
4. Accept partial output and request continuation: "Continue with section X"

---

## Core Instructions

### Pre-Execution Checklist
Before writing, confirm:
1. [ ] Company name and sector identified
2. [ ] Context files read (voice_dna + appropriate ICP)
3. [ ] Input sources identified (knowledge folder or web research)
4. [ ] Output file path determined

### Execution Steps

1. **Gather Information**
   - If knowledge/company-memos/ has files, read and synthesize them
   - If not, conduct systematic web research:
     - Company website and About page
     - Recent funding announcements or press releases
     - Industry reports mentioning the company
     - Competitor landscape research
     - Customer testimonials or case studies

2. **Structure Analysis**
   Follow this exact memo structure:

   ```markdown
   # MEMO
   **Company:** {company}
   **Sector:** {sector}
   **Date:** {YYYY-MM-DD}

   ---

   ## Thesis
   Frame the **core insight** behind the company:
   - What structural or technological shift makes this company possible *now*
   - Why the problem it addresses is large, persistent, and poorly solved
   - How incumbents or legacy workflows fail
   - Why {company}'s approach is meaningfully different (not just better)

   This section should read as a **top-down argument**, not a product description.

   ---

   ## Founding Story
   Describe:
   - Founder(s) background and prior experience
   - The specific moment or exposure that revealed the problem
   - How founder insight translates into product philosophy
   - Early decisions that shaped positioning (ICP, GTM, product scope)

   Anchor the story in **cause → effect**, not biography.

   ---

   ## Product
   Explain the product through **workflows**, not features.

   Cover:
   - Core modules or functional pillars
   - End-to-end workflow the product enables
   - What tools or processes it replaces or consolidates
   - Degree of configurability vs opinionation
   - Integrations and system-of-record dependencies

   If relevant, break into subsections (e.g. Module A, Module B).

   ---

   ## Market

   ### Customer
   Define precisely:
   - Primary buyer (role, function)
   - End users
   - Typical customer size (employees, revenue)
   - Where complexity increases (scale, geography, compliance, etc.)

   Explain *why* this customer segment feels the pain acutely.

   ---

   ### Market Size
   Present **multiple lenses**, explicitly:
   - Top-down (industry or category size)
   - Bottom-up (ACV × number of target customers)
   - Adjacent or expansion markets

   If estimates are directional or inferred, state so clearly.

   ---

   ## Competition
   Structure competition by **problem orientation**, not just category labels.

   Cover:
   - Direct competitors (same job, same buyer)
   - Adjacent competitors (partial overlap, budget competitors)
   - Incumbents / status quo solutions

   Explain:
   - Where differentiation is real vs cosmetic
   - Where the market is fragmented vs consolidating
   - Switching costs and buyer inertia

   If relevant, include a **competitive positioning framework** (quadrant or spectrum).

   ---

   ## Business Model
   Describe how the company makes money and why it matters:
   - Primary revenue streams
   - Pricing logic (subscription, usage, transaction, hybrid)
   - Contract structure and typical ACV
   - Gross margin profile (reported or inferred)
   - How incentives differ vs competitors

   Explicitly note if pricing is opaque or sales-led.

   ---

   ## Traction
   Focus on **validated signals only**:
   - Revenue or usage growth (if disclosed)
   - Volume flowing through the platform (if applicable)
   - Customer adoption and logos
   - Retention or expansion signals
   - Third-party validation (awards, rankings, partnerships)

   Distinguish clearly between **company-stated** and **externally validated** traction.

   ---

   ## Valuation
   If available:
   - Funding history and round sizes
   - Latest known valuation
   - Context vs comparable companies
   - Market multiple environment (expansion or compression)

   If unavailable, state explicitly:
   > Valuation data is not publicly disclosed.

   ---

   ## Key Opportunities
   Identify **structural upside**, such as:
   - Market tailwinds
   - Product expansion rooted in existing workflows
   - Monetization leverage
   - Strategic partnerships or distribution advantages

   Tie each opportunity to something the company **already does well**.

   ---

   ## Key Risks
   Be specific and concrete. Typical categories:
   - Competitive intensity
   - Go-to-market execution
   - Product scope creep
   - Customer graduation or churn
   - Incumbent lock-in
   - Market timing

   Avoid generic startup risks.

   ---

   ## Summary
   Synthesize the memo:
   - What the company does exceptionally well
   - Where it is structurally advantaged
   - Where it is most exposed
   - What must go right over the next phase

   End with a **balanced, analytical conclusion**, not a recommendation.

   ---

   ## Disclosures
   This memo is for informational and educational purposes only.
   It is based on publicly available information and does not constitute investment advice.
   ```

3. **Apply Voice and Tone**
   - Use voice_dna.json principles: reflective, calm, analytical
   - Write with quiet authority and long-term perspective
   - Privilege trade-offs over absolutes
   - Focus on structural advantages and constraints
   - Use short-to-medium sentences with one clear point per paragraph
   - Avoid superlatives and excessive adjectives

4. **Analytical Rigor Standards**
   - **Distinguish stated vs validated**: Separate company claims from verified data
   - **Quantify when possible**: Cite specific numbers, ranges, or estimates
   - **Show your work**: If inferring market size or margins, explain the logic
   - **Acknowledge gaps**: If data is unavailable, state it explicitly
   - **Balanced assessment**: Present both opportunities and risks with equal rigor

5. **Source Transparency**
   - If using research from knowledge folder, reference source materials
   - If using web research, cite authoritative sources
   - Maintain audit trail mentality

### Quality Checks Before Output
- [ ] Thesis section reads as structural argument, not product description
- [ ] Product section explains workflows, not just features
- [ ] Competition section is problem-oriented, not just category listing
- [ ] Traction section distinguishes company-stated vs externally validated
- [ ] Opportunities and Risks are specific, not generic
- [ ] Summary provides balanced synthesis, not recommendation
- [ ] Voice aligns with voice_dna.json (calm, analytical, trade-off oriented)
- [ ] Tone matches ICP audience expectations

## Example Invocation

**User**: "Create a company memo for Stripe"

**Assistant**:
"I'll create an investment-grade company memo for Stripe. To ensure comprehensive analysis, should I first run research skills to gather:
- Latest financial positioning and metrics
- Recent news and market signals
- Product positioning analysis

Or would you like me to proceed with publicly available information and web research?"

## Downstream Applications
After completing a company memo, suggest:
- **pitch_book_workflow**: Convert memo insights into presentation format
- **thought_leadership_crafter**: Use market insights for strategic content
- **generate_weekly_issue**: Include company analysis in industry brief
- **ma_case_study_generator**: Use company research as foundation for M&A case studies
- **strategic_signal_forecaster**: Use company analysis as foundational research for market predictions

## Success Criteria
A successful company memo:
1. Reads as investment committee-ready analysis
2. Provides structural insight, not just description
3. Balances opportunities and risks with equal rigor
4. Distinguishes validated data from inference
5. Reflects voice_dna.json tone throughout
6. Aligns with target ICP's decision-making context
7. Could be used as foundational research for pitch books or investment memos
