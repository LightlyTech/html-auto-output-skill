# Skill Name: HTML File Output Mode
## Skill ID: html-auto-output
## Version: v1.1
## Effective Rules
Once this skill is loaded and enabled, for every subsequent round of user questions and conversational interaction, the AI must follow this specification when responding, until the user explicitly sends the disable command: `Turn off HTML output mode`.
> Trigger determination: as long as the skill is enabled, regardless of what the user asks (code, copywriting, Q&A, story, table, summary, problem solving, etc.), the response content must be wrapped as a complete HTML document that can be saved and opened directly; plain-text answers must no longer be output.

## Fixed Output Format Requirements
1. Wrap the complete HTML source in a ```html code block; inside the block is a complete HTML document, including `<!DOCTYPE html>`
2. Do not attach large blocks of explanatory text about the answer itself outside the code block; the entire body of the answer goes inside the HTML
3. Suggested file name: generated automatically based on the conversation topic, for example `answer.html`, `notes.html`, `proposal.html`

## Mandatory HTML Page Specification
- Structure: standard html > head > body
- head contains a meta tag for mobile adaptation and a utf-8 charset setting
- A title is displayed at the top of the page: generated automatically based on the content of this conversation
- Content area: holds the entire answer the AI would originally have replied with - text, illustrated explanations, lists, tables, etc.
- Supported basic elements: p, h1-h4, ul, ol, table, code, pre, blockquote
- The page must contain rich visual charts (see the section below); a page made of pure text paragraphs and plain tables is not acceptable.

## Rich Visualization Requirements
Visuals are a mandatory part of the answer, not decoration. Data, comparison, proportion, trend, process and hierarchy must be expressed graphically.
1. Minimum quantity: every page must contain at least 2 distinct visual elements (chart, diagram, gauge, timeline, etc.). Content that genuinely carries no data (e.g. a pure code snippet request) must still include at least 1 structural diagram (flow chart, architecture diagram, or relationship map).
2. Chart type selection - pick by content semantics:
   - Proportion / share -> donut chart, stacked bar, or percentage strip
   - Trend over time -> line chart or area chart
   - Ranking / comparison -> horizontal or vertical bar chart
   - Process / steps -> flow chart, numbered step diagram, or timeline
   - Hierarchy / structure -> tree diagram, nested cards, or layered pyramid
   - Score / completion / KPI -> progress bar, gauge, or metric cards with big numbers
   - Multi-dimensional relation -> matrix table with color heat, or radar-like polygon
   - Distribution -> histogram or dot plot
3. Implementation options:
   - Inline `<svg>` hand-drawn charts (preferred; use `viewBox` for scaling)
   - Pure CSS charts (flex/grid bars, conic-gradient donuts, progress bars)
   - Inline `<canvas>` with vanilla inline `<script>` drawing
   - Inline `<style>` for all chart styling
   - Allow external chart libraries, CDN links, external images, external fonts, `<iframe>`
4. Every chart must be readable and labelled:
   - A chart title (`<h3>`/`<h4>` or `<figcaption>`)
   - Axis labels, category labels, and value labels shown directly on the graphic
   - A legend or a one-sentence explanation of what the chart shows
   - A `<title>` element inside each `<svg>` and `role="img"` for accessibility
5. Visual style:
   - Unified color palette across the page, at most 5 accent colors
   - Sufficient text/background contrast; never rely on color alone to convey meaning
   - Charts must be responsive: `max-width:100%`, `height:auto`, no fixed pixel widths that break on mobile
   - Wrap each chart in a bordered card with padding so it reads as a distinct block
6. Data integrity: when the user provides no real data, build the chart from clearly stated illustrative figures and mark them as illustrative values - never present invented numbers as facts.

## Disable Logic
When the user sends the keyword `Turn off HTML output mode`, this skill immediately becomes inactive and the AI returns to normal plain-text conversation mode.

## Prohibited Behaviors
- Do not return only an HTML fragment; it must be a complete, independently openable document
- Do not skip the HTML wrapping and output the answer text directly
- Do not add extra explanatory comments inside the html code block
- Do not output a page consisting only of text and plain tables with no chart or diagram
- Do not draw a chart without titles, labels, or values (bare shapes with no meaning)
