# Markdown to HTML Publisher

## Role
You are a document publishing specialist that transforms markdown outputs from this project into professional, brand-compliant HTML documents suitable for web viewing and sharing.

## Task
Convert any markdown file (`.md`) from the `outputs/` folder into a fully-styled HTML document following CVB brand guidelines, with proper handling of tables, code blocks, and document structure.

## Input Requirements
1. **Source File Path**: Path to the markdown file to convert (e.g., `outputs/company-memos/2026-01-03_personetics_memo.md`)
2. **Output Destination**: (Optional) Custom output path, defaults to `outputs/html/[same-name].html`

## Brand Guidelines (CVB)
Apply the following brand specifications to all HTML outputs:

### Visual Identity
- **Primary Colors**:
  - White: `#FFFFFF` (background)
  - Black: `#000000` (primary text)
  - Accent Red: `#E00000` (headings, highlights, strategic elements)
- **Accent Tones**: Warm grey tones (`#a19e9a`, `#edebe7cb`) for value/opportunity elements
- **Typography**: Aptos font family throughout
- **Aesthetic**: Premium, high-contrast, clean design
- **Accessibility**: WCAG AAA contrast standards (minimum 7:1 for normal text, 4.5:1 for large text)

### Layout Requirements
- **Logo Placement**: Reserve space in bottom-right margin for CVB logo
- **Impulse Line**: Include strategic red accent line (2-3px) as visual anchor
- **Whitespace**: Generous margins and padding for premium feel
- **Responsive**: Must render correctly on desktop and tablet

## Implementation Specification

### Python Dependencies
```bash
pip install markdown beautifulsoup4 pygments
```

### Conversion Process
1. **Parse Markdown**: Use Python's `markdown` library with extensions:
   - `tables` - GitHub Flavored Markdown tables
   - `fenced_code` - Code blocks with syntax highlighting
   - `codehilite` - Syntax highlighting via Pygments
   - `toc` - Table of contents generation
   - `nl2br` - Convert newlines to `<br>` where appropriate

2. **Apply Brand Styling**: Inject CSS template (see below)

3. **Post-Process HTML**: Use BeautifulSoup4 to:
   - Add ARIA labels for accessibility
   - Ensure all tables have proper semantic structure
   - Add responsive image handling
   - Insert logo placeholder and impulse line

4. **Output**: Save to `outputs/html/` with same base filename

## CSS Template

```css
/* CVB Brand CSS Template */
:root {
    --CVB-white: #FFFFFF;
    --CVB-black: #000000;
    --CVB-red: #E00000;
    --CVB-grey: #a19e9a;
    --CVB-grey-light: #edebe7cb;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Aptos', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background-color: var(--CVB-white);
    color: var(--CVB-black);
    line-height: 1.6;
    max-width: 1200px;
    margin: 0 auto;
    padding: 60px 80px 120px 80px;
    position: relative;
}

/* Strategic impulse line */
body::before {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 3px;
    background: linear-gradient(90deg, var(--CVB-red) 0%, var(--CVB-red) 60%, var(--CVB-grey) 100%);
    z-index: 1000;
}

/* Logo placement area */
body::after {
    content: '';
    position: fixed;
    bottom: 20px;
    right: 40px;
    width: 120px;
    height: 60px;
    background-color: transparent;
    z-index: 999;
}

/* Typography */
h1, h2, h3, h4, h5, h6 {
    font-family: 'Aptos', sans-serif;
    font-weight: 600;
    margin-top: 2em;
    margin-bottom: 0.75em;
    color: var(--CVB-red);
}

h1 {
    font-size: 2.5em;
    border-bottom: 3px solid var(--CVB-red);
    padding-bottom: 0.3em;
    margin-bottom: 1em;
}

h2 {
    font-size: 2em;
    border-bottom: 2px solid var(--CVB-grey-light);
    padding-bottom: 0.25em;
}

h3 {
    font-size: 1.5em;
    color: var(--CVB-black);
}

h4 {
    font-size: 1.25em;
    color: var(--CVB-black);
}

p {
    margin-bottom: 1.2em;
    font-size: 1.05em;
}

/* Links */
a {
    color: var(--CVB-red);
    text-decoration: none;
    border-bottom: 1px solid transparent;
    transition: border-bottom-color 0.2s ease;
}

a:hover {
    border-bottom-color: var(--CVB-red);
}

/* Lists */
ul, ol {
    margin-left: 1.5em;
    margin-bottom: 1.2em;
}

li {
    margin-bottom: 0.5em;
    line-height: 1.7;
}

/* Tables */
table {
    width: 100%;
    border-collapse: collapse;
    margin: 2em 0;
    background-color: var(--CVB-white);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
}

thead {
    background-color: var(--CVB-red);
    color: var(--CVB-white);
}

th {
    padding: 16px;
    text-align: left;
    font-weight: 600;
    font-size: 1em;
    border-bottom: 3px solid var(--CVB-grey);
}

td {
    padding: 14px 16px;
    border-bottom: 1px solid #E0E0E0;
}

tbody tr:hover {
    background-color: var(--CVB-grey-light);
    transition: background-color 0.2s ease;
}

tbody tr:last-child td {
    border-bottom: 2px solid var(--CVB-black);
}

/* Code blocks */
pre {
    background-color: #F5F5F5;
    border-left: 4px solid var(--CVB-red);
    padding: 1.5em;
    overflow-x: auto;
    margin: 1.5em 0;
    border-radius: 4px;
}

code {
    font-family: 'Courier New', Courier, monospace;
    font-size: 0.9em;
    background-color: #F5F5F5;
    padding: 2px 6px;
    border-radius: 3px;
}

pre code {
    background-color: transparent;
    padding: 0;
}

/* Blockquotes */
blockquote {
    border-left: 4px solid var(--CVB-grey);
    padding-left: 1.5em;
    margin: 1.5em 0;
    color: #4A4A4A;
    font-style: italic;
    background-color: var(--CVB-grey-light);
    padding: 1em 1.5em;
}

/* Horizontal rules */
hr {
    border: none;
    border-top: 2px solid var(--CVB-grey-light);
    margin: 3em 0;
}

/* Opportunity/value highlights */
.highlight-value {
    background: linear-gradient(120deg, var(--CVB-grey-light) 0%, transparent 100%);
    padding: 0.2em 0.4em;
    border-radius: 3px;
}

/* Responsive design */
@media (max-width: 768px) {
    body {
        padding: 40px 30px 100px 30px;
    }

    h1 {
        font-size: 2em;
    }

    h2 {
        font-size: 1.5em;
    }

    table {
        font-size: 0.9em;
    }

    th, td {
        padding: 10px;
    }
}

/* Print styles */
@media print {
    body {
        padding: 20px;
        max-width: 100%;
    }

    body::before,
    body::after {
        display: none;
    }

    a {
        color: var(--CVB-black);
        text-decoration: underline;
    }
}
```

## HTML Template Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{DOCUMENT_TITLE}</title>
    <style>
        {CSS_TEMPLATE_HERE}
    </style>
</head>
<body>
    <main role="main" aria-label="Document content">
        {CONVERTED_MARKDOWN_CONTENT}
    </main>

    <!-- Logo placeholder - replace with actual CVB logo -->
    <div class="logo-container" style="position: fixed; bottom: 20px; right: 40px; z-index: 1000;">
        <!-- <img src="CVB-logo.svg" alt="CVB Logo" width="120" height="60"> -->
    </div>
</body>
</html>
```

## Python Script Template

Create `scripts/markdown_to_html.py`:

```python
#!/usr/bin/env python3
"""
Markdown to HTML Publisher
Converts project markdown outputs to brand-compliant HTML documents.
"""

import sys
import os
from pathlib import Path
import markdown
from bs4 import BeautifulSoup

# CSS template embedded here
CSS_TEMPLATE = """
/* Paste CSS from above */
"""

def convert_markdown_to_html(input_path: str, output_path: str = None) -> str:
    """
    Convert markdown file to branded HTML.

    Args:
        input_path: Path to source markdown file
        output_path: Optional custom output path

    Returns:
        Path to generated HTML file
    """
    # Read source markdown
    input_file = Path(input_path)
    if not input_file.exists():
        raise FileNotFoundError(f"Source file not found: {input_path}")

    with open(input_file, 'r', encoding='utf-8') as f:
        md_content = f.read()

    # Configure markdown extensions
    md = markdown.Markdown(extensions=[
        'tables',
        'fenced_code',
        'codehilite',
        'toc',
        'nl2br',
        'attr_list',
        'def_list'
    ])

    # Convert to HTML
    html_body = md.convert(md_content)

    # Post-process with BeautifulSoup
    soup = BeautifulSoup(html_body, 'html.parser')

    # Add ARIA labels to tables
    for table in soup.find_all('table'):
        table['role'] = 'table'
        table['aria-label'] = 'Data table'

        thead = table.find('thead')
        if thead:
            thead['role'] = 'rowgroup'

        tbody = table.find('tbody')
        if tbody:
            tbody['role'] = 'rowgroup'

    # Extract title from first h1 or use filename
    title_tag = soup.find('h1')
    document_title = title_tag.get_text() if title_tag else input_file.stem.replace('_', ' ').title()

    # Build complete HTML document
    html_template = f"""<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="generator" content="AI Co-Writer Markdown Publisher">
    <title>{document_title}</title>
    <style>
{CSS_TEMPLATE}
    </style>
</head>
<body>
    <main role="main" aria-label="Document content">
{soup.prettify()}
    </main>

    <!-- Logo placeholder -->
    <div class="logo-container" style="position: fixed; bottom: 20px; right: 40px; z-index: 1000;">
        <!-- Replace with actual CVB logo: -->
        <!-- <img src="CVB-logo.svg" alt="CVB Logo" width="120" height="60"> -->
    </div>
</body>
</html>"""

    # Determine output path
    if output_path is None:
        output_dir = Path('outputs/html')
        output_dir.mkdir(parents=True, exist_ok=True)
        output_path = output_dir / f"{input_file.stem}.html"
    else:
        output_path = Path(output_path)
        output_path.parent.mkdir(parents=True, exist_ok=True)

    # Write HTML file
    with open(output_path, 'w', encoding='utf-8') as f:
        f.write(html_template)

    return str(output_path)

def main():
    """CLI entry point."""
    if len(sys.argv) < 2:
        print("Usage: python markdown_to_html.py <input.md> [output.html]")
        sys.exit(1)

    input_path = sys.argv[1]
    output_path = sys.argv[2] if len(sys.argv) > 2 else None

    try:
        result_path = convert_markdown_to_html(input_path, output_path)
        print(f"✓ HTML generated: {result_path}")
    except Exception as e:
        print(f"✗ Error: {e}", file=sys.stderr)
        sys.exit(1)

if __name__ == '__main__':
    main()
```

## Usage Instructions

### Installation
```bash
# Navigate to project root
cd C:\Users\visco\OneDrive\Projects\AI_CoWriter_v002

# Install dependencies
pip install markdown beautifulsoup4 pygments
```

### Command Line Usage
```bash
# Convert single file
python scripts/markdown_to_html.py outputs/company-memos/2026-01-03_company_memo.md

# Convert with custom output path
python scripts/markdown_to_html.py outputs/equity-stories/2026-01-03_equity_story.md outputs/html/custom_name.html
```

### Claude Execution
When user requests HTML conversion, execute:

1. **Validate Input**:
   ```python
   input_file = Path("<user-provided-path>")
   if not input_file.exists():
       raise FileNotFoundError(f"Source not found: {input_file}")
   ```

2. **Run Conversion**:
   ```bash
   python scripts/markdown_to_html.py "<input_path>" "<output_path>"
   ```

3. **Verify Output**:
   ```python
   output_path = Path("outputs/html/<filename>.html")
   if output_path.exists():
       print(f"✓ HTML published: {output_path}")
       print(f"  File size: {output_path.stat().st_size / 1024:.1f} KB")
   ```

## Output Structure

```
outputs/
  html/
    2026-01-03_company_memo.html
    2026-01-03_equity_story.html
    2026-01-03_market_analysis.html
    ...
```

## Quality Checklist

Before delivering HTML output, verify:

1. **Brand Compliance**:
   - [ ] Aptos font loaded and applied
   - [ ] CVB color palette (#FFFFFF, #000000, #E00000, grey tones)
   - [ ] Strategic impulse line visible at top
   - [ ] Logo placeholder in bottom-right
   - [ ] Premium, high-contrast aesthetic

2. **Content Integrity**:
   - [ ] All markdown sections converted
   - [ ] Tables render correctly with brand styling
   - [ ] Code blocks have proper syntax highlighting
   - [ ] Links are functional and styled
   - [ ] Document structure preserved

3. **Accessibility**:
   - [ ] WCAG AAA contrast ratios met (7:1 for normal text)
   - [ ] ARIA labels on tables and semantic elements
   - [ ] Proper heading hierarchy (h1 → h2 → h3)
   - [ ] Alt text on images (if any)

4. **Responsiveness**:
   - [ ] Renders correctly on desktop (1200px+)
   - [ ] Readable on tablet (768px - 1199px)
   - [ ] Print-friendly styles applied

## Error Handling

**Common Issues**:

1. **Missing Dependencies**:
   ```
   Error: No module named 'markdown'
   Solution: pip install markdown beautifulsoup4 pygments
   ```

2. **File Not Found**:
   ```
   Error: Source file not found
   Solution: Verify path is relative to project root
   ```

3. **Encoding Issues**:
   ```
   Error: UnicodeDecodeError
   Solution: Ensure source markdown is UTF-8 encoded
   ```

4. **Font Loading**:
   - If Aptos not available, fallback to system sans-serif
   - Add web font loading if needed: `@import url('...')`

## Future Enhancements

- PDF export via wkhtmltopdf or weasyprint
- Batch conversion for entire output folders
- Interactive table of contents generation
- Chart/graph rendering from data tables
- Custom logo injection (replace placeholder)
- Multi-page document splitting for long content

## Success Criteria

A successful HTML output:
- Opens immediately in any modern browser without errors
- Displays all content with CVB brand identity
- Maintains document structure and readability
- Passes WCAG AAA accessibility standards
- Prints cleanly without layout breaks
- Requires no post-processing or manual fixes
