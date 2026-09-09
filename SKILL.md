---
name: persian-markdown-formatter
description: Format Persian and mixed Persian-English Markdown documents for maximum readability, navigation, and visual consistency. Use when cleaning, restructuring, standardizing, or polishing Markdown presentation without changing the content, meaning, logical order, scope, or technical accuracy. Suitable for documentation, guides, notes, manuals, README files, project documentation, tutorials, specifications, and long-form Markdown files.
metadata:
  version: "1.5.0"
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
- By default:
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
- Never rewrite content unless the user explicitly requests rewriting.
- Never add new information.
- Never remove meaningful information.
- Never change the logical structure of the document.

### Navigation is more important than decoration
If there is a conflict between:
1. visual decoration
2. fast navigation
3. readability

always prioritize:
1. navigation
2. readability
3. decoration

The goal is professional documentation, not visual effects.

### Markdown only
- Output must remain pure Markdown.
- Never use:
  - HTML
  - CSS
  - JavaScript
  - embedded styling
- Examples of forbidden elements:
  - `<div dir="rtl">`
  - `<span>`
  - `<style>`
- Do not solve RTL issues with HTML wrappers.
- Use Markdown-native formatting only.
- Single controlled exception: empty anchor tags `<a id="..."></a>` are allowed exclusively as TOC navigation targets. No other HTML is permitted.

## The Persian-First Boundary (Crucial for Mixed Documents)
When formatting mixed Persian-English documents, you must strictly respect the boundary between "narrative text" and "technical identifiers". Do not over-Persianize technical elements, and do not leave narrative elements in English.

**MUST be Persian-First (Rewrite/Wrap if starting with Latin):**
- Headings and subheadings
- Table of Contents (TOC) entries
- Narrative paragraphs and sentences
- Mixed narrative list items (e.g., bullet points explaining a concept)

**MUST Remain English (Untouched / Exempt from Persian-First rule):**
- Fenced code blocks and CLI commands
- Inline code representing exact settings, paths, or CLI flags (e.g., `push.default`, `--rebase`)
- URLs, email addresses, and social media handles
- Standard technical tables where the first column is an exact standard (e.g., Semantic Versioning `MAJOR/MINOR/PATCH`, Conventional Commits `feat/fix/docs`)
- Exact error messages (kept in English for searchability)
- Glossary tables (the term column remains English, the definition column is Persian)
- UI identifier tables (the first column is an exact UI label or action name, e.g., `Stage` / `Commit` / `Push` in a VS Code operations table; keep the identifier column English, the description columns stay Persian)
- **References and Resources:** Book titles, documentation names, standard names, tool names, and repository names inside resource/reference lists must remain in their original language (e.g., "Pro Git", "GitHub Docs", "Conventional Commits", "Semantic Versioning"). Never translate, transliterate, or Persianize these names. Only the surrounding descriptive labels may be Persian-first. URLs and links are always exempt.

## RTL and Mixed-Language Handling
The document may contain:
- Persian text
- English text
- code, commands, settings, labels, file names, paths, variables, tickers, identifiers

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
Renderers choose each line's base direction from its first strong directional letter.
Digits (Persian or ASCII), emoji, and punctuation are NOT strong: they do not set the line direction. Backticks are neutral too, but the Latin letters inside an inline code span ARE strong — so a line starting with a Latin identifier in backticks still renders LTR.

Therefore: the first letter of every heading, subheading, narrative list item, TOC entry, and standalone narrative line in a Persian document **must be a Persian (or Arabic) letter**. Numbers and emoji may precede it, but the first word after them must begin with a Persian letter.

**Bad** (first letter is Latin → line renders LTR and scrambles):
- 🚩 . Tag و Release (راهنمای کامل)
- ۸.۱ Branch چیست؟
- Branch متحرک است
- Release title: v1.2.0
- ``.gitignore` جامع`

**Good** (first letter is Persian → line renders RTL in correct order):
- 🚩 ۹. تگ و Release (راهنمای کامل)
- ۸.۱ شاخه (Branch) چیست؟
- شاخه (Branch) متحرک است
- عنوان Release: v1.2.0
- فایل `.gitignore` جامع

**Rewrite techniques:**
1. Transliterate: Tag → تگ، Branch → شاخه
2. Wrap in a Persian frame: "Branch چیست؟" → "شاخه (Branch) چیست؟"
3. Move the term later or into parentheses:
   - ❌ `Remote و Remote Management` → ✅ `مدیریت ریموت (Remote)`
   - ❌ `Branching و Merging` → ✅ `شاخه‌سازی و ادغام (Branching و Merging)`
   - ❌ `GitHub Actions و انتشار خودکار` → ✅ `انتشار خودکار با GitHub Actions`
   - ❌ `Conventional Commits` → ✅ `پیام‌های commit قراردادی (Conventional Commits)`

**Strict Prohibition on RLM:**
Do NOT use the invisible RLM (U+200F) as a shortcut to bypass this rule for headings, TOC entries, or narrative lists. If a heading starts with a Latin word, you MUST rewrite it using the techniques above. RLM is strictly reserved *only* for lines that technically must start with a literal CLI command or file path (e.g., `` `git push` ...``).

**Pre-existing RLM is a bug marker, not a fix:** when auditing an existing document, first strip any RLM (U+200F) / LRM (U+200E) characters from the line, then judge the line's direction from its first real letter. A line that only "works" because of a leading RLM is a violation and must be rewritten.

This rule applies to:
- headings and subheadings
- list items (bulleted, numbered, checklist)
- Table of Contents entries
- standalone paragraph lines that mix Persian and English

It does not apply to:
- inline code spans within a Persian sentence
- code blocks
- URLs
- lines that are purely English
- exempt technical tables (as defined in the Boundary section)

### Hidden Latin-Start Patterns (Common Misses)
These patterns frequently slip through a visual scan. Check every one of them explicitly:

1. **Bold Latin term opening a paragraph or item:** ❌ `**Remote** آدرس نسخهٔ راه دور ...` → ✅ `**ریموت (Remote)** آدرس نسخهٔ راه دور ...`
2. **Inline code at line start** (Latin inside backticks is still a strong LTR letter): ❌ `- \`v1.0.0\`: اولین نسخهٔ پایدار` → ✅ `- نسخهٔ \`v1.0.0\`: اولین نسخهٔ پایدار`
3. **Nested items with an RLM shortcut:** ❌ `  - ‏Checkout: دانلود کد` → ✅ `  - مرحلهٔ Checkout: دانلود کد`
4. **Config/YAML key explanations:** ❌ `- ‏\`on.push.tags\`: ...` → ✅ `- کلید \`on.push.tags\`: ...`
5. **Menu / Command Palette paths:** ❌ `- ‏Command Palette → \`Git: Merge...\`` → ✅ `- از Command Palette: مسیر \`Git: Merge...\``
6. **Imperative steps starting with a verb in English:** ❌ `4. commit کنید` → ✅ `4. تغییرات را commit کنید`

### Direction Audit Algorithm (Definitive Check)
A visual scan is unreliable for long documents. Apply this deterministic procedure **mentally** after all edits (no shell commands, no helper files — just a careful re-read):

For every line **outside** fenced code blocks and **outside** exempt tables:
1. Strip list/heading/blockquote markers (`#`, `>`, `-`, `*`, `+`, `1.`), then strip emoji, digits, punctuation, and any pre-existing RLM/LRM characters.
2. Find the index of the first Latin letter and the index of the first Persian/Arabic letter.
3. If a Latin letter exists AND (there is no Persian letter, or the Latin one comes first) → the line violates the rule → rewrite it using the Rewrite Techniques or Hidden Latin-Start Patterns fixes.
4. Skip: fenced code blocks, URLs, lines that are purely English, and exempt tables (Persian-First Boundary).

**Exit criterion:** zero violating lines remain (`REMAINING VIOLATIONS: 0`). Re-run the mental audit after every batch of rewrites.

## Heading Structure
Create a clear heading hierarchy.
Preferred structure:

    # Main Title
    ## Major Section
    ### Subsection
    #### Detail

Do not skip heading levels.

**Bad:**

    # Title
    #### Section

**Good:**

    # Title
    ## Section
    ### Subsection

### Numbering Major Sections
For long documents, number major sections.
Example:

    ## ۱. معرفی
    ## ۲. تنظیمات
    ## ۳. قوانین

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

    ## 📋 فهرست مطالب
    1. [معرفی](#sec-1)
    2. [تنظیمات](#sec-2)
    3. [قوانین](#sec-3)

Do not generate a Table of Contents for short documents.
If section headings carry emoji, mirror the same emoji in their TOC entries so the TOC doubles as a visual map (see Emoji Usage).
TOC entries must also obey the Line-Start Direction Rule: start every entry with a Persian word (the emoji prefix does not set direction, so a Persian word must immediately follow it).

**TOC Link Integrity Rule:**
When a heading contains inline code (e.g., `فایل .gitignore جامع`), the TOC entry must wrap the entire phrase in a **single link**. Never fragment it into multiple broken links.

## Emoji Usage
Emoji are allowed only when they improve navigation.
Use emoji to the necessary and sufficient degree — neither absent nor excessive:
- Add exactly one contextually meaningful emoji per major heading, chosen so it reflects the section's content (for example: 📖 background, 🚨 problems, 🔍 root cause, 🧭 process/steps, 📊 current status, 🔧 how-to, 💎 lessons learned).
- Mirror the same emoji in the matching Table of Contents entry, so the TOC works as a visual map of the document.
- Use functional emoji (⚠️ 💡 🔔) only on real warnings and tips, never on ordinary text.

Emoji that add no meaning are decoration. If a heading is already clear without an emoji, the emoji must earn its place by aiding navigation or recognition.

Examples:

    ## 📖 معرفی
    ## 🧩 تنظیمات
    ## 📊 ساختار
    ## 🔔 هشدارها
    ## 🧠 قوانین
    ## 🎯 کاربردها
    ## 💡 نکات کاربردی
    ## 🚫 محدودیت‌ها
    ## 🏁 جمع‌بندی

### Variation-Selector Rule (Critical for Anchor Links)
Never use emoji that contain U+FE0F (VS16) in headings.

Forbidden heading emoji (contain VS16):
✍️ ❤️ ☑️ 🛡️ ⚙️ ✔️ ⚠️ 🛠️

Use single-codepoint emoji instead:
📖 🧩 📊 🔔 🧠 🎯 💡 🏁 🎨 🚧 🧭 ✅ ❓ 📋 💾

Reason: slug generators used by GitHub and VS Code may keep the invisible U+FE0F character inside the heading slug (a known slugger issue), which silently breaks every internal anchor link pointing to that heading.
Note: this rule applies to headings only. Callouts and blockquotes may still use any emoji (they do not generate anchors).

Avoid emoji overload.
- Do not place emoji at the beginning of every paragraph.
- Do not decorate normal text with random emoji.

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

| تنظیم|مقدار|
| ---|---|
| روزها|۵|
| هفته‌ها|۲|

Do not convert ordinary text into tables unnecessarily.
In RTL tables, prefer Persian column headers where possible so the whole table aligns consistently. Refer to the "Persian-First Boundary" for exceptions regarding standard technical tables.

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

    project/
    ├── docs/
    ├── src/
    └── tests/

Never convert directory trees into plain text lists.

### Code Blocks
Preserve fenced code blocks.
Example:

    print("hello")

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

**Bad:**

    ---
    ---
    ---

**Good:**

    ---

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

Never compute anchors by guessing: derive them from the algorithm above, or prefer ASCII anchors.

For guaranteed navigation in every viewer, use invisible ASCII anchors as TOC targets:

    <a id="sec-1"></a>
    ## 👀 بخش ۱ — در یک نگاه
    - [بخش ۱](#sec-1)

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
13. **Direction Sanity Check:** Visually scan the first strong letter of every heading, TOC entry, and narrative list item. If it is Latin, rewrite it. Do not rely solely on RLM. Then run the **Direction Audit Algorithm** (see Line-Start Direction Rule) mentally until the exit criterion (zero violations) is met — including the Hidden Latin-Start Patterns.
14. Run the Final Validation Checklist.
15. Deliver per Execution Rules (write back to the same file by default).

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
- [ ] TOC added for long documents and every entry is a working, unfragmented link
- [ ] Heading emoji contain no U+FE0F variation selector
- [ ] TOC anchors derived from the slug algorithm or use ASCII anchors
- [ ] **The Persian-First Boundary is respected:** Code, CLI commands, paths, URLs, and standard technical tables remain untouched in English.
- [ ] **Strict Line-Start Direction:** Headings, TOC entries, and narrative lists start with a Persian letter. RLM is NOT used as a shortcut to bypass rewriting Latin-starting headings.
- [ ] **Zero line-start violations:** the mental Direction Audit Algorithm reports 0 violating lines outside code blocks and exempt tables (pre-existing RLM stripped before judging; RLM does not count as a fix).
- [ ] **References and Resources preserved:** Book titles, documentation names, standard names, tool names, and URLs in resource/reference lists remain untouched in their original language; only surrounding descriptive labels are Persian-first.
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