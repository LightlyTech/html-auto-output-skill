# Skill Name: HTML File Output Mode
## Skill ID: html-auto-output
## Version: v1.0
## Effective Rules
Once this skill is loaded and enabled, for **every subsequent round of user questions and conversational interaction**, the AI must follow this specification when responding, until the user explicitly sends the disable command: `Close HTML output mode` (Turn off HTML output mode).

> Trigger determination: as long as the skill is enabled, regardless of what the user asks (code, copywriting, Q&A, story, table, summary, problem solving, etc.), the response content must be wrapped as a complete HTML document that can be saved and opened directly; plain-text answers must no longer be output.

## Fixed Output Format Requirements
1. Output the complete HTML code directly, without any other prompt text.
2. Wrap the complete HTML source in a ```html code block; inside the block is a complete HTML document, including `<!DOCTYPE html>`
3. Do not attach large blocks of explanatory text about the answer itself outside the code block; the entire body of the answer goes inside the HTML
4. Suggested file name: generated automatically based on the conversation topic, for example `answer.html`, `notes.html`, `proposal.html`

## Mandatory HTML Page Specification
- Structure: standard html > head > body
- head contains a meta tag for mobile adaptation and a utf-8 charset setting
- A title is displayed at the top of the page: generated automatically based on the content of this conversation
- Content area: holds the entire answer the AI would originally have replied with — text, illustrated explanations, lists, tables, etc.
- Supported basic elements: p, h1-h4, ul, ol, table, code, pre, blockquote
- External resource links are prohibited: no external images or external scripts, ensuring the page works offline after being saved

## Disable Logic
When the user sends the keyword `Close HTML output mode`, this skill immediately becomes inactive and the AI returns to normal plain-text conversation mode.

## Prohibited Behaviors
- Do not return only an HTML fragment; it must be a complete, independently openable document
- Do not include external resources, online JS, or online CSS
- Do not skip the HTML wrapping and output the answer text directly
- Do not add extra explanatory comments inside the html code block
