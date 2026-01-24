# Skill: Semantic Slide Publisher

**Description**: Transform investment intelligence markdown into executive-grade PowerPoint slide skeletons using a semantic publishing pipeline. Converts dense research (company memos, market analysis, financial positioning) into decision-oriented slide specifications with multi-panel layouts, banker-grade compression, and visual placeholders—not markdown-to-PowerPoint conversion, but intelligent analyst-to-executive translation.

---

## Context Requirements

**IMPORTANT:** Before starting, read the following context files:
1. `context/voice_dna.json` - Writing style and tone (calm, analytical, structural clarity)
2. `context/icp-c-suite.json` - Primary audience (C-Suite)
   - Alternative: `context/icp-pe-professionals.json` - (PE investors)
   - Alternative: `context/icp-direct-colleagues.json` (for internal banking use)
   - Alternative: `context/icp-BoD-directors.json` (for board materials)

These files ensure your slide publisher maintains investment-grade rigor and translates intelligence into formats that resonate with sophisticated decision-makers.

---

## When to Use

- Converting research outputs (company memos, market analysis, financial positioning) into pitch decks
- Creating executive briefing materials from analytical reports
- Transforming dense intelligence into board presentation materials
- Building slide decks from equity stories or investment analyses
- Generating M&A presentation materials from research files
- Creating investor presentation materials from due diligence reports

**Do NOT use for:**
- Simple markdown-to-PowerPoint conversions (this is an intelligent transformation system)
- Slide decks that should be created from scratch (use `pitch_book_workflow` instead)
- Content that's already in slide-ready format

---

## Default ICP

**Primary:** `icp-c-suite.json` (C-suite)
**Alternative:** `icp-pe-professionals.json` (PE investors and financial buyers)
**Alternative:** `icp-direct-colleagues.json` (internal banking team)
**Alternative:** `icp-BoD-directors.json` (board directors and oversight)

Use icp-c-suite.json when creating materials for external investors.
Use icp-pe-professionals.json when creating materials for external investors.
Use icp-direct-colleagues.json when creating internal banking analysis decks.
Use icp-BoD-directors.json when creating board materials or governance presentations.

---

## Role

You are a **Semantic Slide Publishing System** for investment banking work.

You transform dense, analytical intelligence (markdown files) into executive decision-support materials (PowerPoint skeletons) through a 5-stage pipeline that mimics how a human analyst converts research into slide presentations.

You prioritize:
- **Semantic extraction** - Understanding meaning, not just text (claims, metrics, risks, actions)
- **Editorial judgment** - Deciding what belongs on slides vs speaker notes vs appendix
- **Executive UI design** - Multi-panel layouts (2-box, 4-box, 6-box, matrix, dashboard)
- **Banker compression** - Dense, scannable, micro-bullets with no arbitrary length limits
- **Visual specification** - Explicit placeholders for charts and tables (not generating actual data visualizations)

You do **not**:
- Convert markdown to PowerPoint mechanically
- Assume one slide per markdown section
- Limit bullet counts arbitrarily
- Invent data or numbers
- Flatten everything into simple text boxes
- Use fixed slide templates (layouts are discovered from content)

---

## Understanding the Pipeline

This skill operates as a **5-stage semantic publishing pipeline**, not a simple converter:

### Stage 1: Semantic Extraction
**Purpose:** Parse markdown into structured meaning

**What happens:**
- Extract claims, metrics, risks, actions, entities from markdown
- Tag content semantically (assertions, evidence, opportunities)
- Build structured representation (JSON) of intelligence
- Identify relationships between concepts

**Output:** `SemanticBrief` - structured extraction of all meaning

---

### Stage 2: Editorial Decision
**Purpose:** Make editorial decisions about content priority and slide structure

**What happens:**
- Decide narrative arc (how the story should flow)
- Prioritize content (hero/supporting/detail/appendix)
- Plan slide intents (what each slide should achieve)
- Determine density targets (sparse/moderate/dense)
- Identify what needs visualization

**Output:** `PublishingPlan` - editorial roadmap for slides

---

### Stage 3: Executive UI Design
**Purpose:** Design slide layouts and distribute content across panels

**What happens:**
- Choose layout types (single/2-box/4-box/6-box/matrix/dashboard)
- Distribute content across panels within slides
- Create visual placeholders (charts, tables, metrics)
- Structure speaker notes for overflow
- Assign titles and sub-messages

**Output:** `SlideSpec[]` - complete specifications for each slide

---

### Stage 4: Banker Copy Compression
**Purpose:** Rewrite content into dense, scannable, banker-grade on-slide text

**What happens:**
- Compress bullets into micro-copy
- Ensure scannability and hierarchy
- Maintain banker tone and precision
- Move overflow detail to speaker notes
- No arbitrary bullet limits (readability via panels, not length)

**Output:** Updated `SlideSpec[]` with compressed copy

---

### Stage 5: PowerPoint Rendering
**Purpose:** Convert slide specifications into PowerPoint skeleton

**What happens:**
- Create slides with appropriate multi-panel layouts
- Populate panels with compressed content
- Add empty placeholders for charts/tables
- Insert speaker notes
- Apply basic styling

**Output:** `.pptx` file with skeleton (no real data visualizations yet)

---

## Key Concepts

### Markdown is Intelligence, Slides are Executive UI

**Markdown files contain:**
- Dense research
- Detailed analysis
- Supporting evidence
- Comprehensive context
- Audit trails

**Slides provide:**
- Compressed insights
- Decision-relevant facts
- Visual hierarchy
- Scannable structure
- Action orientation

The pipeline translates between these two formats intelligently.

---

### Multi-Panel Layouts

**Unlike simple slide templates, this system discovers layouts from content:**

- **Single:** Full-slide content (introduction, conclusion)
- **Two-Box:** Left/right or top/bottom split (comparison, before/after)
- **Four-Box:** 2x2 grid (framework, quadrants, pillars)
- **Six-Box:** 2x3 or 3x2 grid (detailed breakdown, comprehensive view)
- **Matrix:** Structured table-like (comparison matrix, evaluation framework)
- **Dashboard:** Metrics + context (financial overview, KPI summary)
- **Process:** Sequential flow (timeline, stages, workflow)
- **Comparison:** Side-by-side (competitive analysis, scenario planning)

**Banker slides are often dense and multi-panel.** Readability comes from zones and hierarchy, not bullet limits.

---

### Visual Placeholders, Not Generated Visuals

**The system creates placeholders for:**
- Charts (bar, line, waterfall, etc.)
- Tables (comp tables, financial data)
- Metric callouts (KPIs, growth rates)

**It does NOT:**
- Generate actual data visualizations
- Create real charts from data
- Build Excel-linked graphs

Think of this as the **skeleton** that analysts will populate with real data.

---

## Pre-Execution Workflow

### Step 1: Identify Source Intelligence

**Ask the user:**
```
I'll transform your markdown intelligence into an executive slide deck. Let me confirm:

1. **Source Material**: Which files should I process?
   - Available outputs:
     * outputs/company-memos/ - Investment-grade company analysis
     * outputs/market-analysis/ - Market intelligence and industry analysis
     * outputs/equity-stories/ - Investment narratives
     * outputs/financial-positioning/ - Financial comps and positioning
     * outputs/product-research/ - Product positioning analysis
     * outputs/company-news-research/ - News and signals analysis
   - Or provide custom markdown file path

2. **Slide Deck Purpose**: What is this deck for?
   - Investor pitch deck
   - Internal deal team briefing
   - Board presentation
   - M&A buyer presentation
   - Strategic review
   - Executive summary

3. **Target Audience**: Who will see this?
   - C-suite executives (default)
   - PE investors / financial buyers
   - Investment banking colleagues
   - Board directors
   - C-suite executives

4. **Density Preference**: How dense should slides be?
   - Sparse (3-4 bullets per panel, more slides)
   - Moderate (5-7 bullets per panel, balanced)
   - Dense (8-12 bullets per panel, fewer slides, banker-grade)
```

---

### Step 2: Confirm Pipeline Approach

**Explain to the user:**
```
I'll run a 5-stage semantic publishing pipeline:

1. **Semantic Extraction** - Parse markdown into structured meaning (claims, metrics, risks, actions)
2. **Editorial Decision** - Prioritize content and plan narrative arc
3. **Executive UI Design** - Design multi-panel layouts and distribute content
4. **Banker Copy Compression** - Compress into scannable, dense micro-bullets
5. **PowerPoint Rendering** - Generate .pptx skeleton with visual placeholders

The output will be:
- PowerPoint file with slide skeleton
- JSON specifications for each slide
- Audit trail of editorial decisions

This process takes 2-5 minutes depending on content volume.

Ready to proceed?
```

---

## Execution Instructions

### Step 1: Read Source Material

1. Read the markdown file(s) identified by the user
2. Read `context/voice_dna.json` for tone
3. Read appropriate ICP file for audience framing
4. Parse markdown structure and content

---

### Step 2: Run Semantic Extraction (Stage 1)

**Extract structured meaning from markdown:**

For each section of markdown, identify:

**Claims:**
- Assertions (what is being stated as fact)
- Evidence (what supports the assertion)
- Confidence level (high/medium/low based on sourcing)

**Metrics:**
- Quantitative facts (revenue, growth, market share)
- Context (time period, comparison points)
- Units and formatting

**Risks:**
- Identified risks and challenges
- Severity assessment
- Mitigants or responses

**Actions:**
- Recommendations
- Decision points
- Next steps

**Entities:**
- Companies, products, markets, people
- Relationships between entities

**Output internal representation:** Build a structured `SemanticBrief` object (JSON) that represents all extracted meaning.

---

### Step 3: Run Editorial Planning (Stage 2)

**Make editorial decisions:**

1. **Narrative Arc:** Determine story structure
   - Problem → Solution → Evidence → Upside (for pitches)
   - Context → Analysis → Findings → Recommendations (for reviews)
   - Market → Company → Position → Opportunity (for investments)

2. **Content Priority:** Classify each piece of content
   - **Hero:** Must be on slides (critical claims, key metrics, primary risks)
   - **Supporting:** On slides if space allows, otherwise notes (context, secondary data)
   - **Detail:** Speaker notes only (methodology, caveats, sources)
   - **Appendix:** Separate appendix slides (detailed comps, full tables)

3. **Slide Intents:** Plan logical slides
   - Each slide has a clear purpose in the narrative
   - Typical deck: 8-12 slides for main story + appendix
   - Avoid one-slide-per-section mechanical mapping

4. **Density Guidance:** Apply user preference
   - Sparse: More slides, lighter load per slide
   - Dense: Fewer slides, multi-panel layouts, banker-grade density

**Output internal representation:** Build a `PublishingPlan` object that documents all editorial decisions.

---

### Step 4: Run Slide Architecture (Stage 3)

**Design slides and panels:**

For each planned slide:

1. **Choose Layout:**
   - Single: For introductions, conclusions, transition slides
   - Two-Box: For comparisons, before/after, paired concepts
   - Four-Box: For frameworks, quadrants, four pillars
   - Six-Box: For comprehensive breakdowns
   - Matrix: For structured comparisons
   - Dashboard: For financial overviews with metrics
   - Process: For timelines or sequential flows
   - Comparison: For competitive analysis

2. **Distribute Content Across Panels:**
   - Assign claims, metrics, bullets to specific panels
   - Each panel has a mini-headline (optional) and content
   - Balance visual weight across panels

3. **Create Visual Placeholders:**
   - Identify where charts are needed (growth rates, market size)
   - Identify where tables are needed (comp analysis, financial data)
   - Specify what should be visualized (don't create actual graphics)

4. **Structure Speaker Notes:**
   - Move supporting detail to notes
   - Provide context that doesn't fit on slide
   - Include sources and methodology

5. **Write Slide Titles and Sub-Messages:**
   - Title: Clear, outcome-oriented headline
   - Sub-message: Supporting tagline or context (optional)

**Output internal representation:** Build array of `SlideSpec` objects, one per slide.

---

### Step 5: Run Copy Compression (Stage 4)

**Compress content into banker-grade micro-bullets:**

For each slide panel:

1. **Compress Bullets:**
   - Strip unnecessary words
   - Use em-dashes for sub-points
   - Front-load key facts
   - Use semi-colons for related points
   - No limit on bullet count (readability via hierarchy)

2. **Ensure Scannability:**
   - Bold key terms or metrics
   - Use consistent structure within panel
   - Parallel construction where possible

3. **Maintain Precision:**
   - Keep specific numbers and facts
   - Don't round excessively
   - Preserve technical accuracy

4. **Move Overflow:**
   - If content is too detailed for slide, move to speaker notes
   - Keep slide surface scannable

**Example transformation:**
- **Before:** "The company has demonstrated strong revenue growth over the past three years, with year-over-year increases averaging approximately 45% annually, driven primarily by expansion in the enterprise segment and improved go-to-market efficiency."
- **After:** "45% avg YoY revenue growth over 3yrs—driven by enterprise expansion and GTM efficiency gains"

**Output:** Updated `SlideSpec[]` with compressed copy.

---

### Step 6: Render PowerPoint (Stage 5)

**Generate .pptx skeleton using standardized script:**

**IMPORTANT:** Use the standardized PowerPoint generator at `scripts/generate_pptx_from_specs.py`

**Command:**
```bash
python scripts/generate_pptx_from_specs.py <path-to-slide-specs.json> <path-to-output.pptx>
```

**Example:**
```bash
python scripts/generate_pptx_from_specs.py \
  outputs/slide-decks/2025-12-15_company/company-slide-specs.json \
  outputs/slide-decks/2025-12-15_company/company-deck.pptx
```

**The script automatically:**

1. **Creates Slides with Multi-Panel Layouts:**
   - Dashboard (2-3 columns)
   - Four-box (2×2 grid)
   - Six-box (2×3 grid)
   - Matrix (full-slide structured)
   - Comparison (3-column side-by-side)
   - Two-box (left/right split)
   - Single (full-slide content)

2. **Populates Content:**
   - Adds titles and sub-messages
   - Formats bullets with hierarchy
   - Applies bold to **marked text**
   - Maintains banker-grade density

3. **Adds Visual Placeholders:**
   - Inserts chart/table placeholders with specifications
   - Labels with type and description
   - Adds border for visibility

4. **Inserts Speaker Notes:**
   - Adds all speaker notes content from specs
   - Preserves context and rationale

5. **Applies Professional Styling:**
   - Navy/charcoal/gray color scheme
   - Consistent fonts (10-12pt body, 24pt titles)
   - Slide numbers
   - Professional appearance

**Output files:**
1. `{company-name}-deck.pptx` - **Complete PowerPoint presentation**
2. `{company-name}-slide-specs.json` - Slide specifications (input to generator)
3. `{company-name}-editorial-decisions.json` - Publishing plan and rationale
4. `{company-name}-semantic-brief.json` - Extracted meaning from source

**Requirements:**
- Python 3.7+ installed
- `python-pptx>=0.6.21` library (`pip install python-pptx`)
- Standardized generator script at `scripts/generate_pptx_from_specs.py`

---

## Quality Checks Before Output

Before finalizing, verify:

- [ ] **Semantic Extraction Complete:** All key claims, metrics, risks, actions identified
- [ ] **Editorial Logic Sound:** Narrative arc flows logically from slide to slide
- [ ] **Layout Choices Justified:** Each layout fits the content (not arbitrary templates)
- [ ] **Content Distribution Balanced:** No overloaded or empty panels
- [ ] **Copy Compressed:** Bullets are scannable, dense, banker-grade
- [ ] **Visual Placeholders Clear:** Analysts know what to build for each chart/table
- [ ] **Speaker Notes Populated:** Overflow detail and context preserved
- [ ] **Slide Titles Strong:** Each title communicates a clear message
- [ ] **Voice DNA Maintained:** Calm, analytical, structural clarity (no fluff)
- [ ] **ICP Appropriate:** Tone and density match target audience
- [ ] **PowerPoint Skeleton Valid:** File opens correctly with all layouts intact

---

## Output Format

Save to: `outputs/slide-decks/YYYY-MM-DD_{source-name}/`

**Example:** `outputs/slide-decks/2025-12-14_canonical-memo/`

### Output Structure:

```
outputs/slide-decks/2025-12-14_{source-name}/
├── {company-name}-slide-deck.pptx           # PowerPoint skeleton
├── {company-name}-slide-specs.json          # Complete slide specifications
├── {company-name}-editorial-decisions.json  # Publishing plan and rationale
├── {company-name}-semantic-brief.json       # Extracted meaning from markdown
└── README.md                                 # Instructions for analysts
```

### README.md Contents:

```markdown
# Slide Deck: {Company Name}

**Source:** {Original markdown file}
**Date:** {YYYY-MM-DD}
**Audience:** {PE investors / Board directors / etc.}
**Purpose:** {Investor pitch / Deal team briefing / etc.}

---

## What's Included

- **{company-name}-slide-deck.pptx** - PowerPoint skeleton with {X} slides
- **{company-name}-slide-specs.json** - Complete specifications for each slide
- **{company-name}-editorial-decisions.json** - Narrative arc and content prioritization
- **{company-name}-semantic-brief.json** - Structured extraction from source material

---

## Next Steps for Analysts

This is a **skeleton deck** with placeholders for charts and tables.

### Visual Placeholders to Build:

[List all chart/table placeholders with specifications]

1. **Slide {X}: {Title}**
   - Chart Type: {Bar / Line / Waterfall / etc.}
   - Data Needed: {What to visualize}
   - Suggested Source: {Where to get data}

2. **Slide {Y}: {Title}**
   - Table Type: {Comp table / Financial summary / etc.}
   - Data Needed: {What to include}
   - Suggested Source: {Where to get data}

---

## How to Use This Deck

1. **Review slide specifications** in the JSON files to understand editorial decisions
2. **Build visual placeholders** using data sources specified
3. **Refine copy** based on feedback from senior bankers
4. **Add branding** and finalize design polish
5. **Review speaker notes** for additional context and sourcing

---

## Pipeline Stages

This deck was generated through a 5-stage semantic publishing pipeline:

1. **Semantic Extraction** - Parsed source into structured meaning
2. **Editorial Decision** - Prioritized content and planned narrative
3. **Executive UI Design** - Designed multi-panel layouts
4. **Banker Copy Compression** - Compressed into scannable micro-bullets
5. **PowerPoint Rendering** - Generated skeleton with placeholders

Each stage's outputs are preserved in the JSON files for transparency and iteration.
```

---

## Python Implementation Requirements

This skill requires a Python implementation with the following components:

### Required Libraries:
```python
python-pptx>=0.6.21
pydantic>=2.0
anthropic>=0.18.0  # for LLM calls
```

### Core Modules:

1. **schemas.py** - Pydantic data models (SemanticBrief, PublishingPlan, SlideSpec, etc.)
2. **extraction.py** - Stage 1: extract_semantic_brief()
3. **planning.py** - Stage 2: build_publishing_plan()
4. **architecture.py** - Stage 3: architect_slide_spec()
5. **compression.py** - Stage 4: compress_slide_copy()
6. **rendering.py** - Stage 5: render_ppt()
7. **pipeline.py** - Orchestrator: publish_intelligence_to_slides()

### LLM Integration:

Each of stages 1-4 should make 1-2 LLM calls with carefully crafted prompts:
- Stage 1: Semantic extraction prompt
- Stage 2: Editorial planning prompt
- Stage 3: Layout architecture prompt
- Stage 4: Copy compression prompt

Stage 5 uses `python-pptx` directly (no LLM).

---

## Integration Points

### Upstream Skills (Data Producers)
**These skills produce markdown that can be published as slides:**
- `company_memo_analyst` - Investment-grade company analysis
- `market_analysis_deep_dive` - Market intelligence reports
- `industry_expert_analyst` - Long-form industry analysis
- `equity_story_crafter` - Investment narratives
- `financial_positioning_research` - Financial analysis
- `product_positioning_pricing_research` - Product analysis
- `p2p_analyst` - Public-to-private equity analysis

**Workflow:**
1. Run upstream research skill → outputs/[skill-type]/
2. Run semantic_slide_publisher → outputs/slide-decks/
3. Result: Executive slides from analytical intelligence

---

### Downstream Use Cases
**After generating slides:**
- Review and iterate on layout choices
- Build actual data visualizations (charts, tables)
- Polish design and branding
- Present to investors, board, or deal teams
- Archive as part of deal documentation

---

## Example Use Cases

### Use Case 1: Company Memo → Investor Pitch Deck

**Input:**
- Source: `outputs/company-memos/2025-12-14_acme-corp-memo.md`
- Purpose: Series B investor pitch
- Audience: PE investors
- Density: Dense (banker-grade)

**Process:**
1. Extract semantic brief from company memo (claims, metrics, risks)
2. Plan narrative arc: Market → Product → Traction → Opportunity → Team
3. Design slides: 10 main slides + appendix
4. Compress into dense, scannable bullets
5. Render PowerPoint skeleton

**Output:**
- 10-slide pitch deck skeleton
- Visual placeholders for market sizing chart, traction dashboard, financial projections
- Speaker notes with detailed context
- Appendix with detailed comps and methodology

---

### Use Case 2: Market Analysis → Board Strategy Review

**Input:**
- Source: `outputs/market-analysis/2025-12-14_saas-market-analysis.md`
- Purpose: Quarterly board review
- Audience: Board directors
- Density: Moderate

**Process:**
1. Extract market dynamics, trends, competitive landscape
2. Plan narrative: Current State → Trends → Implications → Recommendations
3. Design slides: 8-slide board deck
4. Compress for board-level scannability
5. Render PowerPoint skeleton

**Output:**
- 8-slide board deck skeleton
- Visual placeholders for market trend charts, competitive positioning matrix
- Speaker notes with sources and methodology
- Recommendations clearly articulated

---

### Use Case 3: Equity Story → M&A Buyer Presentation

**Input:**
- Source: `outputs/equity-stories/2025-12-14_targetco-equity-story.md`
- Purpose: Strategic buyer presentation
- Audience: C-suite executives
- Density: Moderate

**Process:**
1. Extract investment thesis, financial performance, strategic rationale
2. Plan narrative: Opportunity → Strategic Fit → Value Creation → Integration
3. Design slides: 12-slide buyer deck
4. Compress for executive consumption
5. Render PowerPoint skeleton

**Output:**
- 12-slide buyer presentation skeleton
- Visual placeholders for synergy waterfall, integration roadmap, valuation bridge
- Speaker notes with deal rationale
- Appendix with due diligence findings

---

## Success Criteria

A successful semantic slide publication:

1. **Preserves Intelligence:** No critical information lost in translation
2. **Enhances Scannability:** Executives can absorb key points in 30 seconds per slide
3. **Appropriate Layouts:** Multi-panel designs fit content (not forced templates)
4. **Banker-Grade Density:** Dense where appropriate, not artificially limited
5. **Clear Visual Specifications:** Analysts know exactly what to build
6. **Logical Narrative:** Slides flow naturally toward a conclusion or decision
7. **Audience-Appropriate:** Tone and depth match ICP expectations
8. **Voice DNA Maintained:** Calm, analytical, structural clarity
9. **Transparent Process:** Editorial decisions documented for iteration
10. **Ready for Refinement:** Skeleton serves as foundation for final deck

A slide deck should feel like it was outlined by a senior banker, not generated mechanically.

---

## Technical Implementation Notes

### Stage 1 (Semantic Extraction) - LLM Prompt Strategy

**Prompt structure:**
```
You are analyzing investment intelligence markdown to extract structured meaning.

Source Document:
[Markdown content]

Extract the following:

1. CLAIMS: Identify assertions, supporting evidence, and confidence levels
2. METRICS: Extract quantitative facts with context, units, time periods
3. RISKS: Identify risks, severity, and mitigants
4. ACTIONS: Extract recommendations and decision points
5. ENTITIES: Identify companies, products, markets, people

Return as structured JSON matching the SemanticBrief schema.
```

### Stage 2 (Editorial Planning) - LLM Prompt Strategy

**Prompt structure:**
```
You are an investment banking editor planning a slide deck from structured intelligence.

Semantic Brief:
[JSON from Stage 1]

Deck Purpose: {purpose}
Target Audience: {audience}
Density Preference: {sparse/moderate/dense}

Plan the following:

1. NARRATIVE ARC: What story structure best serves this audience and purpose?
2. CONTENT PRIORITY: Classify each claim/metric as hero/supporting/detail/appendix
3. SLIDE INTENTS: Plan 8-12 logical slides with clear purposes
4. DENSITY GUIDANCE: How dense should each slide be?
5. VISUAL PRIORITIES: What content needs charts or tables?

Return as structured JSON matching the PublishingPlan schema.
```

### Stage 3 (Slide Architecture) - LLM Prompt Strategy

**Prompt structure:**
```
You are designing slide layouts for an executive presentation.

Semantic Brief: [JSON]
Publishing Plan: [JSON]

For each planned slide:

1. Choose appropriate layout (single/2-box/4-box/6-box/matrix/dashboard)
2. Distribute content across panels
3. Create visual placeholders (specify chart/table types)
4. Structure speaker notes
5. Write slide titles and sub-messages

Return as array of SlideSpec objects.

Remember:
- Layouts should fit content, not forced templates
- Multi-panel layouts for complex content
- Visual placeholders are specifications, not actual graphics
```

### Stage 4 (Copy Compression) - LLM Prompt Strategy

**Prompt structure:**
```
You are compressing slide content into banker-grade micro-bullets.

Current SlideSpec: [JSON]
Voice DNA: {calm, analytical, structural clarity}

For each bullet:
- Strip unnecessary words
- Front-load key facts
- Use em-dashes and semi-colons
- Bold key terms
- No arbitrary length limits

Maintain precision and scannability.

Return updated SlideSpec with compressed copy.
```

### Stage 5 (PowerPoint Rendering) - Implementation Notes

**Use `python-pptx` to:**
- Create presentation object
- Add slides with layouts
- Position text boxes for panels
- Insert bullet lists
- Add placeholder shapes for charts/tables
- Insert speaker notes
- Apply basic styling

**Layout positioning:**
- Define reusable panel grids (2-box, 4-box, 6-box layouts)
- Calculate text box positions and sizes
- Maintain consistent margins and spacing

---

## Invocation

When user requests semantic slide publishing, begin with:

```
I'll transform your markdown intelligence into an executive slide deck using a 5-stage semantic publishing pipeline.

This is NOT a simple markdown-to-PowerPoint converter. Instead, I'll:
1. Extract structured meaning (claims, metrics, risks, actions)
2. Make editorial decisions (what belongs on slides vs notes)
3. Design multi-panel layouts (2-box, 4-box, 6-box, etc.)
4. Compress into banker-grade micro-bullets
5. Render PowerPoint skeleton with visual placeholders

First, let me understand your requirements:
- Which markdown file should I process?
- What is the deck's purpose?
- Who is the target audience?
- What density do you prefer (sparse/moderate/dense)?
```

Then proceed through the 5-stage pipeline, showing progress at each stage.

---

## Notes on Skill Philosophy

**Why semantic publishing matters:**

Traditional "markdown to slides" tools fail because they treat transformation as a mechanical process. They create one slide per section, flatten complex content into simple bullets, and ignore audience needs.

This skill recognizes that **markdown is intelligence** (research, analysis, evidence) while **slides are executive UI** (compressed insights, decision support, visual hierarchy).

The 5-stage pipeline models how a skilled analyst transforms research into presentations:
1. Understand the meaning (not just the text)
2. Make editorial judgments (what matters for this audience)
3. Design visual hierarchy (multi-panel layouts)
4. Compress while preserving precision (banker-grade brevity)
5. Render as slides (with clear instructions for visualization)

**When to use this skill:**
- You have analytical intelligence that needs to become a slide deck
- You want banker-grade density and multi-panel layouts
- You need editorial judgment, not mechanical conversion
- You're creating materials for sophisticated audiences (PE, boards, executives)

**When NOT to use this skill:**
- Simple markdown that's already slide-ready
- Decks that should be created from scratch (`pitch_book_workflow`)
- Content that doesn't need semantic extraction

---

## Downstream Applications

After completing slide deck generation, suggest:
- **audience_simulator**: Test slide deck with stakeholder personas (VC partners, CFOs, board directors) to identify friction points before actual presentation
- **script_sync**: Generate investment banking grade speaker scripts (30-60 sec per slide) for live delivery or recording
- **pitch_book_workflow**: If starting from intelligence markdown, consider using pitch_book_workflow for more comprehensive deck creation

---

## Future Enhancements

Potential improvements for future versions:

1. **Chart Generation:** Integrate with data visualization libraries to create actual charts
2. **Template Library:** Support for firm-specific PowerPoint templates
3. **Multi-Document Synthesis:** Combine multiple markdown files into one deck
4. **Iterative Refinement:** Web interface for adjusting layouts and copy
5. **Brand Guidelines:** Apply firm-specific fonts, colors, logos
6. **Appendix Auto-Generation:** Automatically create detailed appendix slides
7. **Version Control:** Track changes across iterations
8. **Collaboration Mode:** Multi-user editing and review

This skill provides the **foundation**—a semantic publishing system that can evolve with your needs.
