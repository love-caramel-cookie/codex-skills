---
name: notion-page-beautification
description: Beautify and restructure Notion page content without losing any original information. Use when the user provides a Notion page link, asks Codex to read the existing page style, waits to paste raw text, and then wants the text formatted, appended, inserted, or replaced in that Notion page for research notes, study notes, experiment logs, fabrication records, engineering records, or long-term review.
---

# Notion Page Beautification

Use this skill to transform raw user-provided text into clean, structured, Notion-native research notes while preserving every detail.

Core principle: format the content; do not rewrite the content.

## Workflow

### 1. Read the Notion page first

When the user provides a Notion page URL or page title:

1. Read the content of the page.
2. Inspect the existing style before making any changes.
3. Determine whether the top of the page already contains beautified content.
4. Report briefly that the page was read and that you are waiting for the raw text.
5. Do not update the page yet.

Observe these style signals:

- Heading levels and section depth.
- Emoji habits and repeated icons.
- Callout usage and tone.
- Bold text habits.
- Highlight and text color habits.
- Bullet, numbered list, and checklist formats.
- Table style and parameter formatting.
- Code block, inline code, and equation usage.
- Divider frequency.
- Overall density, spacing, and visual rhythm.

If the page is blank or has no usable style, use the default style below.

### 2. Wait for the user's raw text

After reading the page, wait for one of these user intents:

- Paste new raw text to beautify.
- Ask to beautify the whole page.
- Ask to replace a specific section.
- Ask to insert at a specified location.
- Ask to only return formatted content without writing to Notion.

Do not assume permission to replace existing content unless the user explicitly says so.

### 3. Beautify without changing meaning

Format the raw text into Notion-flavored Markdown. Before writing content, use the Notion Markdown specification available in the current connector context when needed; do not invent unsupported Notion syntax.

Preserve all original information exactly in meaning and detail.

Highest-priority preservation rules:

- Do not delete any sentence.
- Do not delete any number.
- Do not delete experiment parameters.
- Do not delete dimensions.
- Do not delete notes, partial notes, or uncertain fragments.
- Do not delete formulas.
- Do not delete links.
- Do not delete references.
- Do not delete technical terms.
- Do not summarize away details.
- Do not merge content in a way that loses any detail.

Allowed transformations:

- Reorder into clearer sections only when the original meaning and traceability remain intact.
- Add headings.
- Add light emoji markers.
- Add callouts for warnings, experience notes, key conclusions, and risks.
- Convert parallel items into bullet or numbered lists.
- Convert parameters, dimensions, experimental conditions, and result comparisons into tables.
- Put code, commands, KLayout parameters, Silvaco decks, terminal commands, and similar technical blocks in code fences.
- Put formulas in equation blocks when supported.
- Use toggles for long background explanation, derivations, or supplementary context, but do not hide key conclusions too deeply.
- Use a small number of dividers between major modules only.
- If some simple chemical formulas are designed, such as O2 and SiO2, then automatically use the inline formulas to change these numbers into superscripts or subscripts, which conforms to the standard usage norms of chemical formulas.

Forbidden transformations:

- Do not summarize unless the user explicitly asks for a summary.
- Do not compress a long text into a short version.
- Do not alter numerical values, units, material names, process conditions, measurement results, conclusions, code, or professional terms.
- Do not silently fix suspected mistakes.
- Do not make the page decorative, marketing-like, rainbow-colored, or overly emoji-heavy.

If a possible error is found, preserve the original text and add:

```text
⚠️ Possible typo / 需要确认：
<original text>
```

## Style Rules

Match the existing page style first. New content should look like it belongs to the same page and author.

When existing style is available:

- Reuse the same or similar emoji vocabulary.
- Reuse the same heading hierarchy.
- Reuse similar callout types.
- Reuse similar colors.
- Reuse similar table formatting.
- Reuse similar code and formula formatting.
- Keep the same level of visual simplicity.

When no style is available, use this default:

```text
Notion x Apple Notes x Research Lab Notebook
```

Default style keywords:

- Light.
- Fresh.
- Clean.
- Spacious.
- Structured.
- Academic.
- Engineering-oriented.
- Native to Notion.

Default color discipline:

- Blue: explanations or background.
- Green: valid conclusions or feasible solutions.
- Yellow: warnings or attention points.
- Gray: supplementary notes.
- Brown: experiment records or experience notes.

Use color sparingly. Simplicity and clarity are more important than decoration.

## Minimal Formatting Principle

This is a strict rule.

Most body text should remain normal plain text.

The page should look like a clean research note, not a decorated poster.

Target ratio:

- 90% of body text should remain plain text.
- Only less than 10% of content should receive visual emphasis.
- Tables should mostly use plain text in cells.
- Parameters should usually remain plain text unless they are the main conclusion or a critical warning.
- The user will manually mark additional highlights later if needed.
- Do not color multiple words in the same sentence.
- Do not apply multiple styles to the same text unless absolutely necessary.

Do not proactively add many:

- Highlights.
- Inline code.
- Bold text.
- Underlines.
- Colored text.

Use these only when they clearly improve structure or prevent misunderstanding.

If unsure whether to emphasize something, do not emphasize it.

## Inline Code Usage Rule

Inline code is easy to overuse. Use it very carefully.

Inline code should only be used for content that is truly code-like, machine-like, or needs exact software recognition.

Do not fill tables with inline code, highlights, and colored fragments.

## Notion Update Rules

Default behavior:

- If the user gives raw text and no insertion location, append the beautified content to the end of the page.
- If the user gives a location, insert there.
- If the user asks to replace a specific section, replace only that section.
- If the user asks to replace the whole page or "modify the entire page", replace the full body content.
- If the user asks "only return the formatted content" or similar, do not call a Notion update tool.

Before replacing content:

1. Fetch the page first.
2. Use exact existing snippets for targeted search-and-replace updates.
3. Preserve child pages and databases if present in fetched page content.
4. If a Notion update warns that child content would be deleted, stop and ask the user for confirmation; do not set destructive deletion flags automatically.

When appending:

- Do not modify earlier beautified content.
- Do not delete existing content.
- Keep the new section stylistically consistent with the page.

## Completion Response

After finishing, state briefly:

- The page was read and existing style was referenced.
- The new content was beautified.
- Whether the Notion page was updated.
- The write location: page end, specified location, section replacement, or full-page replacement.
- That the original content was fully preserved.

If the user asked only for formatted content, output the formatted content directly with minimal extra explanation.
