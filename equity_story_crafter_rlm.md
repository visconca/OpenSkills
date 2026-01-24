# Skill: Equity Story Crafter (RLM-Enhanced)

**Description**: Generate investment-grade equity stories using Recursive Language Model (RLM) techniques. This experimental version loads all research materials into a programmatic environment and recursively queries them to build each section of the equity story. Designed to overcome context window limitations and improve synthesis quality across large document sets.

**Status**: Experimental - Runs alongside `equity_story_crafter.md` for A/B testing

---

## Context Requirements

**IMPORTANT:** Before starting, read the following context files:
1. `context/voice_dna.json` - Writing style and tone (calm, analytical, structural clarity)
2. `context/icp-pe-professionals.json` - Primary audience (PE investors)
   - Alternative: `context/icp-direct-colleagues.json` (for internal banking use)
   - Alternative: `context/icp-c-suite.json` (for operating company executives)

These files ensure your equity story maintains investment-grade rigor and resonates with sophisticated capital allocators.

---

## What Makes This Version Different

This skill implements **Recursive Language Model (RLM)** techniques inspired by research from MIT CSAIL (Zhang, Kraska, Khattab, 2025):

**Traditional Approach:**
- Read all research files into context sequentially
- Hit context limits with 5+ documents
- Synthesize from memory
- Risk missing data spread across files

**RLM Approach:**
- Load all research files as Python environment variables (external memory)
- Write code to programmatically query specific data for each section
- Recursively generate each section with targeted data retrieval
- Verify completeness and backfill gaps
- No context window bottleneck

**Expected Benefits:**
- Handle 10+ research documents without context limits
- Better data extraction across multiple sources
- Systematic verification that all sections have supporting evidence
- Improved output quality through recursive refinement

---

## When to Use

Use this RLM version when:
- You have 5+ research files for a single company
- Output quality from standard equity_story_crafter is below standard
- You need systematic evidence extraction across large document sets
- You want to test RLM effectiveness on synthesis tasks

Use standard equity_story_crafter when:
- You have 1-3 research files (no context limit issues)
- You prefer proven, stable workflow
- Speed is more important than exhaustive synthesis

---

## Default ICP

**Primary:** `icp-pe-professionals.json` (PE investors and financial buyers)
**Alternative:** `icp-direct-colleagues.json` (internal banking team)
**Alternative:** `icp-c-suite.json` (operating company executives as audience)

---

## Role

You are an **Investment Banking Equity Story Architect with RLM capabilities**.

Your mission is identical to the standard equity_story_crafter, but your execution method differs:
- You **load documents into environment variables** instead of reading them directly
- You **write Python code** to search, filter, and extract data from these variables
- You **recursively generate each section** with targeted data retrieval
- You **verify completeness** before finalizing each section

You maintain all the same quality standards:
- Structural logic, evidence-based positioning, outcome orientation
- Analytical balance, investor lens, slide deck readiness
- No superlatives without evidence, no generic claims

---

## Input Requirements

### Required: Research Materials in knowledge/equity-stories/

This RLM version **requires research materials**. It is designed to synthesize existing research, not gather information through Q&A.

**Ideal inputs:**
- Company memo analysis (from company_memo_analyst)
- Financial positioning research (from financial_positioning_research)
- Product positioning research (from product_positioning_pricing_research)
- Market analysis (from market_analysis_deep_dive or industry_expert_analyst)
- Company news and signals (from company_news_signals_research)
- 10-K or investor documents (from 10k_research_assistant)

**Minimum requirement:** At least 3 research documents covering business model, market, and financials.

**If research is missing:** Direct user to run upstream research skills first, or use standard equity_story_crafter with Q&A mode.

---

## RLM Execution Protocol

### Phase 1: Environment Setup (Load Documents as Variables)

**Step 1: Discover and load all research materials**

```python
import os
import re
from pathlib import Path

# Discover all research files
knowledge_path = Path('knowledge/equity-stories/')
research_files = list(knowledge_path.glob('*.md'))

# Load each file as an environment variable
env = {}
for file_path in research_files:
    var_name = file_path.stem.replace('-', '_')  # e.g., 'company_memo' from 'company-memo.md'
    with open(file_path, 'r', encoding='utf-8') as f:
        env[var_name] = f.read()
    print(f"Loaded: {var_name} ({len(env[var_name])} chars)")

# Report what's available
print(f"\n=== Environment loaded with {len(env)} documents ===")
for var_name in sorted(env.keys()):
    print(f"  - {var_name}: {len(env[var_name]):,} characters")
```

**Step 2: Create helper functions for querying**

```python
def search_pattern(text, pattern, context_chars=500):
    """Search for regex pattern and return matches with context."""
    matches = []
    for match in re.finditer(pattern, text, re.IGNORECASE):
        start = max(0, match.start() - context_chars)
        end = min(len(text), match.end() + context_chars)
        matches.append({
            'match': match.group(),
            'context': text[start:end],
            'position': match.start()
        })
    return matches

def search_keywords(text, keywords, context_chars=500):
    """Search for keywords and return matches with context."""
    pattern = '|'.join([re.escape(kw) for kw in keywords])
    return search_pattern(text, pattern, context_chars)

def extract_sections(text, section_patterns):
    """Extract specific sections from markdown documents."""
    results = {}
    for name, pattern in section_patterns.items():
        match = re.search(pattern, text, re.IGNORECASE | re.DOTALL)
        if match:
            results[name] = match.group(1) if match.groups() else match.group()
    return results

def summarize_findings(matches, max_results=5):
    """Summarize search results for human review."""
    if not matches:
        return "No matches found."

    summary = f"Found {len(matches)} matches:\n"
    for i, m in enumerate(matches[:max_results]):
        summary += f"\n{i+1}. {m['context'][:200]}...\n"

    if len(matches) > max_results:
        summary += f"\n... and {len(matches) - max_results} more matches"

    return summary
```

**Output to user:**
```
=== RLM Environment Initialized ===

Loaded documents:
- company_memo_analyst: 45,230 characters
- market_analysis_deep_dive: 38,120 characters
- financial_positioning_research: 32,450 characters
- product_positioning_pricing_research: 28,900 characters
- company_news_signals_research: 15,670 characters

Total: 5 documents, 160,370 characters loaded into environment.

Ready to begin recursive equity story generation.
```

---

### Phase 2: Recursive Section Generation

For each of the 8 sections, follow this recursive pattern:

#### Section Template (Repeat for Each Section)

**Step 2.X: Generate Section X: [Section Name]**

**Step 2.X.1: Query Environment for Required Data**

Write Python code to extract data needed for this section:

```python
# Example for Section 1: Market Opportunity

# Search for TAM/SAM/SOM data
tam_keywords = ['TAM', 'total addressable market', 'market size', 'billion', 'market opportunity']
tam_results = []
for doc_name, content in env.items():
    matches = search_keywords(content, tam_keywords)
    if matches:
        tam_results.append({'source': doc_name, 'matches': matches})

# Search for growth drivers and market dynamics
growth_keywords = ['CAGR', 'growth rate', 'tailwind', 'market dynamics', 'secular trend', 'adoption']
growth_results = []
for doc_name, content in env.items():
    matches = search_keywords(content, growth_keywords)
    if matches:
        growth_results.append({'source': doc_name, 'matches': matches})

# Search for timing and "why now"
timing_keywords = ['why now', 'inflection point', 'regulatory change', 'technology shift']
timing_results = []
for doc_name, content in env.items():
    matches = search_keywords(content, timing_keywords)
    if matches:
        timing_results.append({'source': doc_name, 'matches': matches})

# Synthesize findings
print("=== Section 1 Data Extraction ===")
print(f"\nTAM/SAM data found in: {[r['source'] for r in tam_results]}")
print(f"Growth drivers found in: {[r['source'] for r in growth_results]}")
print(f"Timing factors found in: {[r['source'] for r in timing_results]}")
```

**Step 2.X.2: Generate Section Content**

Using the extracted data, generate the section following the canonical structure from the original equity_story_crafter skill.

**Step 2.X.3: Verify Completeness**

Write code to verify the section has all required elements:

```python
# Example verification for Section 1
def verify_section_1(section_text):
    """Verify Section 1 has all required elements."""
    requirements = {
        'TAM mentioned': bool(re.search(r'TAM|total addressable market', section_text, re.IGNORECASE)),
        'SAM mentioned': bool(re.search(r'SAM|serviceable addressable market', section_text, re.IGNORECASE)),
        'SOM mentioned': bool(re.search(r'SOM|serviceable obtainable market', section_text, re.IGNORECASE)),
        'Growth rate provided': bool(re.search(r'\d+%\s*(CAGR|growth|YoY)', section_text, re.IGNORECASE)),
        'Market dynamics discussed': len(section_text) > 500,
        'Why now articulated': bool(re.search(r'why now|timing|inflection|shift', section_text, re.IGNORECASE))
    }

    missing = [req for req, present in requirements.items() if not present]

    if missing:
        print(f"⚠️  Section 1 incomplete. Missing: {', '.join(missing)}")
        return False
    else:
        print("✓ Section 1 complete - all requirements met")
        return True

# Run verification
section_1_complete = verify_section_1(section_1_text)
```

**Step 2.X.4: Backfill Gaps (If Needed)**

If verification fails, query environment again for missing data and regenerate incomplete parts.

```python
if not section_1_complete:
    # Re-query for missing elements
    som_data = search_keywords(env['company_memo'], ['serviceable obtainable', 'realistic capture', 'penetration'])
    # Regenerate relevant subsection
    # ...
```

---

### Section-Specific Query Patterns

**Section 1: Market Opportunity**
```python
queries = {
    'tam_sam_som': ['TAM', 'SAM', 'SOM', 'market size', 'addressable', 'billion'],
    'growth_rate': ['CAGR', 'growth rate', 'YoY growth', 'expanding at'],
    'market_dynamics': ['tailwind', 'secular trend', 'market driver', 'adoption', 'shift'],
    'timing': ['why now', 'inflection', 'regulatory', 'technology platform', 'buyer behavior']
}
```

**Section 2: Product**
```python
queries = {
    'value_proposition': ['value prop', 'workflow', 'use case', 'solves', 'enables'],
    'roi': ['ROI', 'payback', 'cost reduction', 'revenue enablement', 'time savings'],
    'mission_criticality': ['mission critical', 'must have', 'embedded', 'system of record'],
    'switching_costs': ['switching cost', 'lock-in', 'sticky', 'retention', 'churn']
}
```

**Section 3: Go-To-Market Strategy**
```python
queries = {
    'icp': ['target customer', 'ICP', 'buyer persona', 'who buys', 'decision maker'],
    'distribution': ['sales model', 'GTM', 'go-to-market', 'distribution', 'channel'],
    'deal_shape': ['ACV', 'contract value', 'deal size', 'sales cycle'],
    'efficiency': ['CAC', 'customer acquisition', 'payback', 'LTV', 'rep productivity']
}
```

**Section 4: Competitive Advantage / Moat**
```python
queries = {
    'differentiation': ['differentiat', 'moat', 'competitive advantage', 'defensible'],
    'data_advantage': ['proprietary data', 'data network', 'learning loop'],
    'ip': ['patent', 'intellectual property', 'algorithm', 'proprietary technology'],
    'network_effects': ['network effect', 'ecosystem', 'platform', 'multi-sided']
}
```

**Section 5: Business Model & Unit Economics**
```python
queries = {
    'revenue_model': ['revenue model', 'pricing', 'subscription', 'usage-based', 'ACV'],
    'gross_margin': ['gross margin', 'COGS', 'margin profile'],
    'ltv_cac': ['LTV', 'CAC', 'lifetime value', 'customer acquisition cost'],
    'cohort': ['cohort', 'retention', 'NRR', 'GRR', 'expansion']
}
```

**Section 6: Financials**
```python
queries = {
    'revenue': ['revenue', 'ARR', 'MRR', 'bookings', 'growth rate'],
    'retention': ['NRR', 'net revenue retention', 'GRR', 'gross retention', 'churn rate'],
    'profitability': ['EBITDA', 'operating margin', 'free cash flow', 'rule of 40'],
    'milestones': ['achieved', 'milestone', 'crossed', 'reached', 'scaled to']
}
```

**Section 7: Potential Upside**
```python
queries = {
    'growth_vectors': ['expansion', 'new market', 'product roadmap', 'geographic', 'M&A'],
    'margin_expansion': ['margin expansion', 'path to profitability', 'operating leverage'],
    'optionality': ['IPO', 'exit', 'strategic buyer', 'acquisition', 'liquidity event']
}
```

**Section 8: Management Team**
```python
queries = {
    'executives': ['CEO', 'CFO', 'CRO', 'CTO', 'COO', 'founder', 'management team'],
    'experience': ['previously', 'background', 'experience', 'track record', 'scaled'],
    'founder_fit': ['founder-market fit', 'domain expertise', 'insight', 'why this team'],
    'diversity': ['diversity', 'D&I', 'gender', 'underrepresented', 'inclusive']
}
```

---

### Phase 3: Integration and Quality Verification

**Step 3.1: Assemble complete equity story**

Combine all 8 sections into final document structure following the canonical format from original equity_story_crafter:

```markdown
# EQUITY STORY
**Company:** {Company Name}
**Sector:** {Sector}
**Date:** {YYYY-MM-DD}
**Prepared For:** {Audience}

---

## Executive Summary
[Generated from synthesis of all sections]

**Investment Highlights:**
- [3-6 bullets from key findings across sections]

---

## 1. Market Opportunity
[Section 1 content]

## 2. Product
[Section 2 content]

## 3. Go-To-Market Strategy
[Section 3 content]

## 4. Competitive Advantage / Moat
[Section 4 content]

## 5. Business Model & Unit Economics
[Section 5 content]

## 6. Financials
[Section 6 content]

## 7. Potential Upside
[Section 7 content]

## 8. Management Team
[Section 8 content]

---

## Conclusion: Why Now, Why This Company, Why This Team
[Synthesis of investment thesis]

---

## Disclosures
[Standard disclosure language]
```

**Step 3.2: Run comprehensive quality verification**

```python
def verify_complete_equity_story(equity_story_text):
    """Verify complete equity story meets all quality standards."""

    quality_checks = {
        # Structural completeness
        'Has Executive Summary': bool(re.search(r'##\s*Executive Summary', equity_story_text)),
        'Has all 8 sections': len(re.findall(r'##\s*\d+\.', equity_story_text)) >= 8,
        'Has Conclusion': bool(re.search(r'##\s*Conclusion', equity_story_text)),

        # Content quality (Voice DNA)
        'No em-dashes': '—' not in equity_story_text,
        'No en-dashes': '–' not in equity_story_text,
        'Has quantified metrics': bool(re.search(r'\$\d+[MB]|\d+%|\d+x', equity_story_text)),

        # Evidence-based
        'Market size quantified': bool(re.search(r'TAM.*\$\d+', equity_story_text, re.IGNORECASE)),
        'Growth rate provided': bool(re.search(r'\d+%\s*CAGR', equity_story_text, re.IGNORECASE)),
        'Unit economics included': bool(re.search(r'LTV|CAC|payback', equity_story_text, re.IGNORECASE)),
        'Financials present': bool(re.search(r'revenue|ARR|NRR|EBITDA', equity_story_text, re.IGNORECASE)),

        # Investor lens
        'Investment thesis clear': bool(re.search(r'investment|thesis|conviction|opportunity', equity_story_text, re.IGNORECASE)),
        'Risk acknowledgment': bool(re.search(r'risk|challenge|execution|competitive', equity_story_text, re.IGNORECASE)),

        # Length check
        'Sufficient depth': len(equity_story_text) > 5000,
        'Not too verbose': len(equity_story_text) < 15000
    }

    passed = sum(quality_checks.values())
    total = len(quality_checks)

    print(f"\n=== Quality Verification ===")
    print(f"Passed: {passed}/{total} checks")

    for check, result in quality_checks.items():
        status = "✓" if result else "✗"
        print(f"{status} {check}")

    if passed == total:
        print("\n✓ Equity story meets all quality standards")
        return True
    else:
        print(f"\n⚠️  Equity story needs refinement ({total - passed} issues)")
        return False

# Run verification
story_ready = verify_complete_equity_story(complete_equity_story)
```

**Step 3.3: Generate source attribution map**

Create a reference document showing which source documents contributed to each section (audit trail):

```python
def generate_attribution_map(section_queries, env):
    """Generate attribution map showing source documents per section."""

    attribution = {}

    for section_name, query_dict in section_queries.items():
        attribution[section_name] = {}

        for query_type, keywords in query_dict.items():
            sources = []
            for doc_name, content in env.items():
                matches = search_keywords(content, keywords)
                if matches:
                    sources.append(doc_name)

            attribution[section_name][query_type] = list(set(sources))

    # Format for output
    print("\n=== Source Attribution Map ===")
    for section, queries in attribution.items():
        print(f"\n{section}:")
        for query_type, sources in queries.items():
            if sources:
                print(f"  - {query_type}: {', '.join(sources)}")

    return attribution

# Generate map
attribution_map = generate_attribution_map(all_section_queries, env)
```

---

## Output Format

Save to: `outputs/equity-stories/YYYY-MM-DD_{company-name}-equity-story-rlm.md`

**Example:** `outputs/equity-stories/2025-01-20_procore-equity-story-rlm.md`

**File naming convention:** Add `-rlm` suffix to distinguish from standard equity_story_crafter output.

---

## Quality Checks Before Output

All quality checks from original equity_story_crafter apply, plus RLM-specific checks:

- [ ] All research documents successfully loaded into environment
- [ ] Each section has programmatic data extraction queries
- [ ] Each section passed completeness verification
- [ ] No section relies on data not present in source documents
- [ ] Attribution map generated (shows which sources contributed where)
- [ ] Voice DNA compliance verified (no em-dashes, analytical tone)
- [ ] All original equity_story_crafter quality standards met

---

## Integration Points

### Upstream Skills (Data Producers) - REQUIRED for RLM Version

This skill **requires** upstream research. Minimum viable set:
- `company_memo_analyst` (business model, GTM, competitive positioning)
- `market_analysis_deep_dive` OR `industry_expert_analyst` (TAM/SAM, market dynamics)
- `financial_positioning_research` (unit economics, comparables)

Recommended complete set:
- `company_memo_analyst`
- `market_analysis_deep_dive`
- `product_positioning_pricing_research`
- `financial_positioning_research`
- `10k_research_assistant` (if public company)
- `company_news_signals_research`

### Downstream Skills (Same as Original)
- `pitch_book_workflow` - Convert equity story to slide deck
- `thought_leadership_crafter` - Develop strategic themes
- `teaser_generator` - Create M&A marketing materials

---

## Usage Instructions for Testing

### Test Protocol: Compare RLM vs Standard Version

**Step 1: Prepare Test Case**
- Select a company with 5+ research files in `knowledge/equity-stories/`
- Example: Procore with company memo, market analysis, financial positioning, product research, news signals

**Step 2: Run Both Versions**
- Generate equity story with standard `equity_story_crafter`
- Generate equity story with this RLM version
- Save both outputs with clear naming convention

**Step 3: Evaluate Quality Differences**

Compare on these dimensions:
1. **Completeness**: Which version captured more data from research?
2. **Evidence density**: Which has more specific metrics, quotes, data points?
3. **Synthesis quality**: Which better integrates findings across documents?
4. **Source coverage**: Which used more of the available research?
5. **Structural coherence**: Which flows better logically?
6. **Investor readiness**: Which is more convincing for capital raise?

**Step 4: Measure Performance**
- Token cost (input + output tokens)
- Generation time
- Number of queries executed
- Documents accessed per section

**Success criteria for RLM version:**
- 20%+ improvement in completeness or evidence density
- Successfully processes 5+ documents without context errors
- Comparable or better quality vs standard version
- Acceptable cost and time trade-offs

---

## Expected Workflow (User Perspective)

**User:** "Create an equity story for Procore using the RLM version"

**Assistant:**
1. Confirms research materials available in `knowledge/equity-stories/`
2. Loads all documents into Python environment (shows what's loaded)
3. Recursively generates each of 8 sections:
   - Shows data extraction queries for each section
   - Generates section content
   - Verifies completeness
   - Backfills gaps if needed
4. Assembles complete equity story
5. Runs quality verification
6. Generates source attribution map
7. Saves to `outputs/equity-stories/2025-01-20_procore-equity-story-rlm.md`
8. Presents summary comparing to standard approach

**User sees:**
- Transparent data extraction process
- Verification that all sections have supporting evidence
- Attribution map showing source utilization
- High-quality equity story with comprehensive synthesis

---

## Limitations and Constraints

**When RLM version may NOT be better:**
1. **Limited research available** (1-2 files): Standard version is faster and equally effective
2. **Research is already synthesized**: If company memo is comprehensive, RLM adds complexity without benefit
3. **Speed is priority**: RLM has higher overhead (more queries, verification steps)
4. **Simple capital raise**: Seed/Series A with limited financial history may not benefit from extensive recursion

**Known challenges:**
1. Requires Python code execution capability
2. Higher token usage upfront (loading environment, running queries)
3. Longer generation time due to recursive verification
4. May be overkill for straightforward cases

**When to fall back to standard equity_story_crafter:**
- If Python execution fails
- If research materials are insufficient
- If user prioritizes speed over comprehensiveness
- If output quality is comparable (no improvement from RLM approach)

---

## Success Criteria

This RLM version is successful if it:

1. **Handles more source material**: Processes 5-10 research documents without context errors
2. **Improves synthesis quality**: Captures more data points across documents
3. **Provides transparency**: Attribution map shows systematic source utilization
4. **Maintains standards**: Meets all quality checks from original equity_story_crafter
5. **Justifies complexity**: Output quality improvement outweighs additional overhead

If these criteria are not met, recommend using standard equity_story_crafter instead.

---

## Next Steps After Testing

**If RLM version outperforms:**
1. Expand RLM approach to other synthesis skills (pitch_book_workflow, teaser_generator)
2. Build dedicated Python execution harness for production use
3. Document best practices for research-to-synthesis pipelines
4. Consider making RLM version the default for 5+ document scenarios

**If results are mixed:**
1. Use RLM version selectively for complex, high-stakes deliverables
2. Keep standard version as default
3. Provide user choice based on use case

**If RLM version underperforms:**
1. Analyze failure modes (cost, time, quality)
2. Iterate on query patterns and verification logic
3. Consider hybrid approach (RLM for specific sections only)
4. Document lessons learned for future experimentation

---

## Notes on RLM Philosophy

**Why recursive approach matters for equity stories:**

Traditional equity story generation treats synthesis as a single-pass process. With multiple research documents, the model must:
- Load everything into context
- Hold it all in "memory"
- Synthesize on the fly
- Risk missing data buried in long documents

RLM approach treats research documents as an **external database**:
- Query systematically for each section's requirements
- Verify completeness before moving forward
- Backfill gaps with targeted re-queries
- Build comprehensive synthesis from ground up

**Trade-off:** More upfront work (environment setup, query execution) for higher quality output.

**Philosophy:** For high-stakes deliverables (capital raises, M&A presentations), quality justifies overhead.

---

## Technical Requirements

**Required capabilities:**
- Python code execution environment
- File system access to `knowledge/` and `outputs/` folders
- Regex and string manipulation libraries
- Markdown parsing capability

**Recommended setup:**
- Claude with Code Interpreter enabled
- Jupyter notebook environment (for iterative testing)
- VS Code with Python extension (for skill development)

**Fallback:** If Python execution is unavailable, use standard equity_story_crafter with manual synthesis.
