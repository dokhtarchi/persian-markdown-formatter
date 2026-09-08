---
name: persian-markdown-formatter
description: Format Persian and mixed Persian-English Markdown documents for maximum readability, navigation, and visual consistency. Use when cleaning, restructuring, standardizing, or polishing Markdown presentation without changing the content, meaning, logical order, scope, or technical accuracy. Suitable for documentation, guides, notes, manuals, README files, project documentation, tutorials, specifications, and long-form Markdown files.
metadata:
  version: "1.3.0"
  author: dokhtarchi
  repository: https://github.com/dokhtarchi/persian-markdown-formatter
---

# Persian Markdown Formatter

## User Examples

Examples of how users may invoke this skill:

- این فایل را با persian-markdown-formatter بازآرایی کن.
- این فایل را با persian-markdown-formatter قالب‌بندی و استانداردسازی کن.
- Apply persian-markdown-formatter to this document.

## Purpose

This skill is a Markdown formatter, not a content editor.

Its responsibility is to improve:
- presentation
- readability
- navigation
- visual hierarchy
- structural consistency

while preserving:
- content
- meaning
- logical order
- scope
- technical accuracy

## Execution Rules (How to Apply This Skill)

- Apply this skill by reading the Markdown source and rewriting it yourself.
- Default delivery: write the complete formatted Markdown back to the same file, then give a 3–5 bullet summary of changes. If the user asks for the result in chat, return the full document in one fenced Markdown block.
- Never create helper, probe, or temporary files (`.mjs`, `.py`, `.txt`, ...).
- Never run shell commands or scripts to inspect, escape, or transform the document. Reading the file as plain UTF-8 text is always sufficient, including for Persian/RTL text.
- Target workflow: 1) read the file, 2) rewrite the file, 3) summarize. No other tool calls.
- Scope: operate only on the file the user names (the target file). Do not read, search, or borrow content from other project files. Do not create, edit, or delete any file other than the target file.

## Core Principles

### Preserve the document

- Preserve meaning, intent, and factual accuracy.
- Minor wording, spelling, punctuation, and readability improvements are allowed if they do not alter meaning.
- Do not introduce new claims, remove existing claims, or change the author's intent.

By default:
- Preserve all content.
- Preserve all sections.
- Preserve all technical details.
- Preserve all examples.
- Preserve all code.
- Preserve all tables.
- Preserve all links.
- Preserve all lists.
- Do not summarize.
- Do not expand.
- Do not reinterpret.
- Do not optimize the content itself.
- Only optimize how the content is presented.

Never rewrite content unless the user explicitly requests rewriting.
Never add new information.
Never remove meaningful information.
Never change the logical structure of the document.

### Navigation is more important than decoration

If there is a conflict between:
- visual decoration
- fast navigation
- readability

always prioritize:
1. navigation
2. readability
3. decoration

The goal is professional documentation, not visual effects.

### Markdown only

Output must remain pure Markdown.

Never use:
- HTML
- CSS
- JavaScript
- embedded styling

Examples of forbidden elements:
- `<div dir="rtl">`
- `<span>`
- `<style>`

Do not solve RTL issues with HTML wrappers.
Use Markdown-native formatting only.
Single controlled exception: empty anchor tags `<a id="..."></a>` are allowed
exclusively as TOC navigation targets. No other HTML is permitted.

## RTL and Mixed-Language Handling

The document may contain:
- Persian text
- English text
- code
- commands
- settings
- labels
- file names
- paths
- variables
- tickers
- identifiers

For short technical identifiers use inline code formatting:
`Session Offset`, `Cooldown`, `AUDUSD`, `Month`, `HH4`

This improves RTL/LTR rendering in Markdown viewers.

Use inline code for:
- software settings
- labels
- variable names
- tickers
- technical identifiers
- commands
- file names
- paths

Do not wrap ordinary English prose in code formatting.

### Line-Start Direction Rule (RTL Documents)

Renderers choose each line's base direction from its **first strong character**:

- A line starting with a Persian letter → rendered right-to-left, in correct order.
- A line starting with a Latin letter or a backtick-wrapped identifier → rendered left-to-right, which scrambles word order in RTL readers.
- Numbers and emoji are **not** strong directional characters and do not set the line direction.

In Persian documents, start every heading, list item, and standalone paragraph line with a Persian word so the line renders right-aligned and in correct reading order.

Rewrite patterns:

- ❌ `Remote و Remote Management` → ✅ `مدیریت ریموت (Remote)`
- ❌ `Branching و Merging` → ✅ `شاخه‌سازی و ادغام (Branching و Merging)`
- ❌ `GitHub Actions و انتشار خودکار` → ✅ `انتشار خودکار با GitHub Actions`
- ❌ `` `.gitignore` جامع`` → ✅ ``فایل `.gitignore` جامع``
- ❌ `Conventional Commits` → ✅ `پیام‌های commit قراردادی (Conventional Commits)`

Move English terms to the middle or the end of the line, or inside parentheses.

**When an English term must come first** (e.g. technical command names, file paths, exact identifiers), prepend an invisible **RLM** character (U+200F) to lock the line direction to RTL without changing the visible text.

This rule applies to:
- headings
- list items (bulleted, numbered, checklist)
- Table of Contents entries
- standalone paragraph lines that mix Persian and English

It does not apply to:
- inline code spans within a Persian sentence
- code blocks
- URLs
- lines that are purely English

## Heading Structure

Create a clear heading hierarchy.

Preferred structure:

```markdown
# Main Title
## Major Section
### Subsection
#### Detail
```

Do not skip heading levels.

Bad:

```markdown
# Title
#### Section
```

Good:

```markdown
# Title
## Section
### Subsection
```

## Numbering Major Sections

For long documents, number major sections.

Example:

```markdown
## ۱. معرفی
## ۲. تنظیمات
## ۳. قوانین
```

Use numbering when:
- the document is long
- the document has many major sections
- navigation benefits from numbering

Do not force numbering on short documents.

## Table of Contents

For large documents, generating a linked Table of Contents is the default:
- every TOC entry must be a working link — a plain (unlinked) TOC is not acceptable for long documents
- place it near the beginning
- preserve section order

Example:

```markdown
## 📋 فهرست مطالب
1. [معرفی](#۱-معرفی)
2. [تنظیمات](#۲-تنظیمات)
3. [قوانین](#۳-قوانین)
```

Do not generate a Table of Contents for short documents.

If section headings carry emoji, mirror the same emoji in their TOC entries
so the TOC doubles as a visual map (see Emoji Usage).

TOC entries must also obey the Line-Start Direction Rule: start every entry with a Persian word (the emoji prefix does not set direction, so a Persian word must immediately follow it).

## Emoji Usage

Emoji are allowed only when they improve navigation.

Use emoji to the necessary and sufficient degree — neither absent nor excessive:

- Add exactly one contextually meaningful emoji per major heading, chosen so it reflects the section's content (for example: 📖 background, 🚨 problems, 🔍 root cause, 🧭 process/steps, 📊 current status, 🔧 how-to, 💎 lessons learned).
- Mirror the same emoji in the matching Table of Contents entry, so the TOC works as a visual map of the document.
- Use functional emoji (⚠️ 💡 🔔) only on real warnings and tips, never on ordinary text.

Emoji that add no meaning are decoration. If a heading is already clear without an emoji, the emoji must earn its place by aiding navigation or recognition.

Examples:

```markdown
## 📖 معرفی
## 🧩 تنظیمات
## 📊 ساختار
## 🔔 هشدارها
## 🧠 قوانین
## 🎯 کاربردها
## 💡 نکات کاربردی
## 🚫 محدودیت‌ها
## 🏁 جمع‌بندی
```

### Variation-Selector Rule (Critical for Anchor Links)

Never use emoji that contain U+FE0F (VS16) **in headings**.

Forbidden heading emoji (contain VS16):
- ✍️ ❤️ ☑️ 🛡️ ⚙️ ✔️ ⚠️ 🛠️

Use single-codepoint emoji instead:
- 📖 🧩 📊 🔔 🧠 🎯 💡 🏁 🎨 🚧 🧭 ✅ ❓ 📋 💾

Reason: slug generators used by GitHub and VS Code may keep the invisible
U+FE0F character inside the heading slug (a known slugger issue), which
silently breaks every internal anchor link pointing to that heading.

Note: this rule applies to headings only. Callouts and blockquotes may
still use any emoji (they do not generate anchors).

Avoid emoji overload.
Do not place emoji at the beginning of every paragraph.
Do not decorate normal text with random emoji.

## Lists

Choose the most appropriate list type.

### Numbered Lists

Use when:
- order matters
- steps exist
- rules are enumerated
- priorities exist

Example:
1. مرحله اول
2. مرحله دوم
3. مرحله سوم

### Bullet Lists

Use when:
- order does not matter
- features are listed
- options are listed
- characteristics are listed

Example:
- ویژگی اول
- ویژگی دوم
- ویژگی سوم

### Checklists

Use when:
- prerequisites exist
- validation exists
- setup requirements exist
- review tasks exist

Example:
- [ ] نصب Python
- [ ] نصب Git
- [ ] تنظیم API Key

Every list item in a Persian document must obey the Line-Start Direction Rule.

## Tables

Use tables only when they improve readability.

Good candidates:
- settings
- comparisons
- labels and meanings
- structured data

Example:

| تنظیم | مقدار |
|---|---|
| روزها | ۵ |
| هفته‌ها | ۲ |

Do not convert ordinary text into tables unnecessarily.

In RTL tables, prefer Persian column headers where possible so the whole table aligns consistently.

## Structural Elements

Preserve existing structural elements.

Never destroy or flatten:
- tables
- code blocks
- checklists
- blockquotes
- directory trees

### Directory Trees

Preserve directory trees exactly.

Example:

```text
project/
├── docs/
├── src/
└── tests/
```

Never convert directory trees into:
- docs
- src
- tests

### Code Blocks

Preserve fenced code blocks.

Example:

```python
print("hello")
```

Do not convert code blocks into prose.

## Emphasis

Use emphasis sparingly.

### Bold

Use for:
- important concepts
- important conclusions
- key settings
- important distinctions

Example:
**این مهم‌ترین بخش سیستم است.**

Do not bold entire paragraphs.

### Inline Code

Use for:
- settings
- identifiers
- commands
- labels
- paths
- technical names

Example:
مقدار `Cooldown` را تنظیم کنید.

## Callouts and Quotes

Use blockquotes only when they improve scanning.

Examples:

> 💡 نکته مهم
> 🔔 اولویت هشدار:
>
> ماه > هفته > روز
> ⚠️ این ابزار معامله انجام نمی‌دهد.

Do not turn ordinary text into blockquotes.
Use them selectively.

## Spacing Rules

Keep spacing compact and consistent.

Use:
- one blank line between blocks
- one blank line after headings
- one blank line before lists

Avoid:
- excessive empty lines
- decorative spacing
- large visual gaps

## Horizontal Rules

Use horizontal rules only for major document boundaries.
Avoid unnecessary separators.

Bad:

```markdown
---
---
---
```

Good:

```markdown
---
```

Only when a major visual break is needed.

## Internal Links

When a Table of Contents exists:
- create internal Markdown links
- keep anchors synchronized with headings
- preserve heading order

Internal links are preferred for long documents.

### Anchor Reliability (VS Code Preview & GitHub)

Slug algorithm (VS Code githubSlugifier / github-slugger):
- removes emoji, punctuation (— « » ( ) .), and ZWNJ from the heading slug
- keeps Persian/Arabic letters and Persian digits
- replaces each whitespace with `-` (double space → `--`)
- may keep an invisible U+FE0F if present (see Variation-Selector Rule)

Never compute anchors by guessing: derive them from the algorithm above,
or prefer ASCII anchors.

For guaranteed navigation in every viewer, use invisible ASCII anchors as
TOC targets:

```markdown
<a id="sec-1"></a>

## 👀 بخش ۱ — در یک نگاه

- [بخش ۱](#sec-1)
```

Rules for these anchors:
- id must be ASCII (`sec-1`, `sec-2`, ...)
- one empty line before and after the anchor tag
- use them only for TOC/navigation targets, never inside content

## Formatting Workflow

When formatting a document:
1. Read the Markdown source as plain UTF-8 text.
2. Preserve content.
3. Preserve order.
4. Detect headings.
5. Build hierarchy.
6. Improve navigation.
7. Generate TOC if useful.
8. Improve lists.
9. Improve tables.
10. Improve emphasis.
11. Improve RTL/LTR rendering (including line-start direction).
12. Normalize spacing.
13. Run the Final Validation Checklist.
14. Deliver per Execution Rules (write back to the same file by default).

## Things This Skill Must Never Do

Never:
- rewrite content
- summarize content
- translate content
- reorder sections
- add new facts
- remove facts
- simplify technical details
- add fictional examples
- add new sections that did not exist
- convert Markdown to HTML
- inject CSS
- create or run scripts or programs
- create new or temporary files
- use the terminal / shell

This skill formats.
It does not author.
It does not edit.
It does not rewrite.

## Final Validation Checklist

Before returning the final document verify:
- [ ] Pure Markdown (only allowed exception: empty `<a id>` anchor tags)
- [ ] No HTML other than the allowed anchor tags
- [ ] No CSS
- [ ] Content preserved
- [ ] Logical order preserved
- [ ] Heading hierarchy improved
- [ ] Navigation improved
- [ ] TOC added for long documents and every entry is a working link
- [ ] Heading emoji contain no U+FE0F variation selector
- [ ] TOC anchors derived from the slug algorithm or use ASCII anchors
- [ ] Every heading, list item, and TOC entry in Persian documents starts with a Persian word (or RLM if an English term must lead)
- [ ] Lists normalized
- [ ] Tables preserved
- [ ] Code blocks preserved
- [ ] Directory trees preserved
- [ ] RTL/LTR readability improved
- [ ] Emoji usage necessary-and-sufficient: one meaningful emoji per major heading, mirrored in TOC; functional emoji only on warnings/tips
- [ ] Spacing normalized
- [ ] No helper/probe files created
- [ ] No shell commands executed
- [ ] Ready for standard Markdown previews (GitHub, VS Code)