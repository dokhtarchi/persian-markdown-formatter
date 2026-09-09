---
name: persian-markdown-formatter
description: Format Persian and mixed Persian-English Markdown documents for maximum readability, navigation, and visual consistency. Use when cleaning, restructuring, standardizing, or polishing Markdown presentation without changing the content, meaning, logical order, scope, or technical accuracy. Suitable for documentation, guides, notes, manuals, README files, project documentation, tutorials, specifications, and long-form Markdown files.
metadata:
  version: "1.6.0"
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

This skill is a Markdown formatter, not a semantic content editor.

Its responsibility is to improve:

- presentation
- readability
- navigation
- visual hierarchy
- structural consistency
- RTL/LTR stability

while preserving:

- content
- meaning
- logical order
- scope
- technical accuracy
- exact technical identifiers

## Execution Rules

Apply this skill by reading the Markdown source and rewriting it yourself.

- Default delivery: write the complete formatted Markdown back to the same file, then give a 3–5 bullet summary of changes.
- If the user asks for the result in chat, return the full document in one fenced Markdown block.
- Never create helper, probe, or temporary files (`.mjs`, `.py`, `.txt`, ...).
- Never run shell commands or scripts to inspect, escape, or transform the document.
- Reading the target file as plain UTF-8 text is sufficient for accessing its visible content.
- Target workflow: read the target file, rewrite the target file, summarize. Normal read/write tool calls for the target file are allowed.
- Scope: operate only on the file the user names. Do not read, search, or borrow content from other project files. Do not create, edit, or delete any file other than the target file.
- Realistic audit: this skill performs a careful textual audit, not a linter. Where invisible characters or renderer-specific anchor behavior cannot be verified by plain reading, choose the safer construction: Persian wrapper, ASCII anchor, or moving the Latin identifier after a Persian word.

## Core Principles

### Preserve the Document

Preserve meaning, intent, and factual accuracy.

Minor wording, spelling, punctuation, and readability improvements are allowed if they do not alter meaning.

Do not introduce new factual claims, remove meaningful claims, or change the author's intent.

By default preserve:

- all content
- all sections
- all technical details
- all examples
- all code
- all tables
- all links
- all lists
- all reference names
- all URLs
- all error messages
- all directory trees

Do not:

- semantically rewrite content unless explicitly requested
- summarize
- expand
- reinterpret
- translate technical identifiers
- optimize the content itself
- add new factual information
- remove meaningful information
- change the logical structure of the document

Stripping accidental invisible direction characters is not considered the removal of meaningful information. Adding minimal Persian wrapper words for direction is not considered the addition of factual information.

### Allowed Presentation-Level Changes

The following changes are presentation fixes, not semantic content changes:

- Adding a minimal Persian wrapper word before an unchanged technical identifier to satisfy the Line-Start Direction Rule.
- Moving a Latin technical identifier into parentheses after a Persian word.
- Removing accidental `RLM` / `LRM` direction characters from narrative lines.
- Fixing duplicate or missing mechanical numbering in headings or ordered lists when it is clearly a numbering bug.
- Adding ASCII anchor targets for TOC navigation.
- Normalizing spacing, list markers, heading hierarchy, and emphasis.

These actions are exceptions to the general no-rewrite/no-add rule only when they do not change facts, meaning, or technical accuracy.

### Forbidden Content Changes

Do not:

- translate `Git` to «گیت»
- translate `GitHub` to «گیت‌هاب»
- translate `Conventional Commits` to Persian
- translate book titles, standard names, documentation names, tool names, or repository names
- change exact CLI commands
- change exact settings, paths, flags, variables, tickers, or UI labels
- rewrite error messages
- alter the meaning of a sentence by adding a wrong category word
- add fictional examples
- add new sections that did not exist
- reorder sections for stylistic preference

### Conflict Resolution Hierarchy

When two rules conflict, resolve them in this order:

1. Preserve the exact technical identifier, command, path, UI label, URL, error message, standard name, or reference title.
2. Do not translate, transliterate, or Persianize that technical identifier.
3. Make the narrative line Persian-first by adding a minimal Persian wrapper or by moving the identifier after a Persian word.
4. If the exact category is unclear, use a neutral Persian frame such as «در»، «با»، «از»، «مورد»، or parentheses.
5. Never use invisible direction characters as a shortcut.

Examples:

```text
Bad:
**Git** یک سیستم کنترل نسخه است.

Good:
**نرم‌افزار Git** یک سیستم کنترل نسخه است.

Bad:
- push کامل می‌شود.

Good:
- عملیات push کامل می‌شود.

Bad:
3. **Update release**

Good:
3. دکمهٔ **Update release**
```

## Navigation Is More Important Than Decoration

If there is a conflict between:

- visual decoration
- fast navigation
- readability
- RTL stability

always prioritize:

1. navigation
2. readability
3. RTL stability
4. decoration

The goal is professional documentation, not visual effects.

## Markdown Only

Output must remain pure Markdown.

Never use:

- HTML layout tags
- CSS
- JavaScript
- embedded styling
- `<div dir="rtl">`
- `<span>`
- `<style>`

Do not solve RTL issues with HTML wrappers.

Use Markdown-native formatting only.

Single controlled exception: empty anchor tags `<a id="..."></a>` are allowed exclusively as TOC navigation targets. No other HTML is permitted.

## Persian-First Boundary

The Persian-first rule applies to narrative text only.

It does not require every list item, table row, code line, directory entry, URL, or technical identifier to be Persian-first.

When formatting mixed Persian-English documents, strictly respect the boundary between narrative text and technical identifiers.

Do not over-Persianize technical elements, and do not leave narrative elements in English.

### Narrative Text Must Be Persian-First

The following must start with a Persian or Arabic letter after ignoring emoji, digits, punctuation, list markers, heading markers, and invisible direction characters:

- headings and subheadings
- Table of Contents entries
- narrative paragraphs
- narrative list items
- blockquote notes that contain Persian narrative
- Persian explanatory table cells

### Technical Identifiers Must Remain English

The following must remain untouched in English:

- fenced code blocks and CLI commands
- inline code representing exact settings, paths, CLI flags, variables, tickers, or identifiers
- URLs
- email addresses
- social media handles
- exact error messages
- standard technical tables
- glossary term columns
- UI identifier columns
- book titles
- documentation names
- standard names
- tool names
- repository names
- reference titles

References and resource names must never be translated, transliterated, or Persianized. Only surrounding descriptive labels may be Persian-first.

Examples:

```text
Good:
کتاب Pro Git را بخوانید.

Good:
مستندات GitHub Docs را ببینید.
```

The examples keep `Pro Git` and `GitHub Docs` unchanged.

### Operational Exemptions

The Line-Start Direction Rule does not apply to:

- fenced code blocks, including comments inside fenced code blocks
- directory trees
- URLs
- email addresses
- lines that are purely English
- pure technical lists whose items contain only commands, paths, identifiers, versions, error messages, or settings
- technical tables whose cells are primarily identifiers, values, commands, settings, standards, or exact UI labels
- glossary tables where the term column must remain English
- reference/resource lists where titles must remain in the original language

The Line-Start Direction Rule does apply to:

- headings
- TOC entries
- narrative paragraphs
- mixed narrative list items
- blockquote notes with Persian narrative
- table cells containing Persian explanatory text

If a list item is only a command or identifier, it may remain technical. If it contains Persian explanation, it becomes narrative and needs a Persian-first start.

Examples:

```text
Technical list, exempt:
- `git push`
- `git pull`
- `git fetch`

Narrative list, must be fixed:
Bad:
- `git push` برای ارسال تغییرات استفاده می‌شود.

Good:
- دستور `git push` برای ارسال تغییرات استفاده می‌شود.
```

## Persian Wrapper Dictionary

When a narrative line must start with Persian but must preserve a Latin technical identifier, use a consistent wrapper. Choose the wrapper from context. If the exact category is unclear, use a neutral frame such as «در»، «با»، «از», or parentheses.

| نوع موجودیت | لفاف فارسی پیشنهادی | مثال |
| --- | --- | --- |
| ابزار / نرم‌افزار / سرویس | «ابزار»، «نرم‌افزار»، «سرویس» | ابزار `Git` |
| دستور / کامند | «دستور» | دستور `git push` |
| کلید / تنظیم / پیکربندی | «کلید»، «تنظیم» | کلید `push.default` |
| مسیر / فایل | «مسیر»، «فایل» | مسیر `.git/config` |
| گزینه / منو / چک‌باکس | «گزینهٔ» | گزینهٔ `Set as the latest release` |
| دکمه | «دکمهٔ» | دکمهٔ `Update release` |
| تب / پنل | «تب»، «در تب» | تب `Changes` |
| فیلد ورودی | «فیلد»، «در فیلد» | فیلد `Title` |
| پیام خطا | «پیام خطای» | پیام خطای `error: ...` |
| نسخه / تگ / ریلیز | «نسخهٔ»، «تگ»، «عنوان نسخه» | نسخهٔ `v1.0.0` |
| شاخه | «شاخهٔ» | شاخهٔ `main` |
| متغیر / نماد / برچسب داده | «متغیر»، «نماد»، «برچسب» | متغیر `AUDUSD` |
| روش / اصل / الگو | «روش»، «اصل»، «الگوی» | روش `fast-forward` |
| عملیات / رویداد | «عملیات»، «رویداد» | عملیات `push` |
| منبع / کتاب / مستند / استاندارد | «کتاب»، «مستند»، «استاندارد» | کتاب `Pro Git` |
| حالت عمومی | «در»، «با»، «از»، «مورد» | در `user.name` |

Rules for wrapper usage:

- The wrapper is a presentation fix, not a new fact.
- The technical identifier remains exactly unchanged.
- Do not invent a wrong category. If unsure, use a neutral frame.
- Do not translate the identifier just to make the line Persian-first.
- Prefer inline code for short technical identifiers.

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

## Line-Start Direction Rule

Renderers choose each line's base direction from its first strong directional letter.

Digits, emoji, punctuation, spaces, and invisible direction marks are not strong directional letters. Formatting markers such as `#`, `>`, `-`, `*`, `+`, `1.`, `[ ]`, `[x]`, backticks, underscores, and asterisks are not strong directional letters.

Latin letters inside bold, italic, or inline code are strong LTR characters. Persian and Arabic letters are strong RTL characters.

Therefore, in a Persian or mixed document, the first real letter of every narrative line must be a Persian or Arabic letter.

This rule applies only to narrative lines:

- headings and subheadings
- Table of Contents entries
- narrative list items
- checklist items that contain Persian narrative or need a Persian frame
- blockquote notes with Persian narrative
- standalone narrative paragraph lines
- Persian explanatory table cells

This rule does not apply to:

- fenced code blocks
- directory trees
- URLs
- purely English lines
- exempt technical tables
- pure technical lists containing only commands or identifiers
- reference titles that must remain English

### Emoji Does Not Set Direction

Emoji at the beginning of a line does not make the line Persian-first. The first word after emoji must begin with a Persian letter.

```text
Bad:
🚩 Tag و Release

Good:
🚩 تگ و نسخه (Tag و Release)
```

### Invisible Direction Characters Are Not a Fix

Do not use RLM `U+200F` or LRM `U+200E` as a shortcut.

Pre-existing RLM or LRM at the start of a heading, TOC entry, narrative list item, or narrative paragraph is a bug marker, not a fix.

When auditing an existing document:

1. Strip any visible or suspected RLM/LRM from the start of narrative lines.
2. Judge direction from the first real visible letter.
3. If the first real letter is Latin, rewrite the line with a Persian wrapper.
4. Do not re-add RLM/LRM.

ZWNJ `U+200C` is allowed inside Persian words, such as half-space usage. It must not be used to fake line direction.

## Common Missed Line Types

These five patterns are common violations.

### 1. Paragraph Starting with a Tool Name

```text
Bad:
**Git** یک سیستم کنترل نسخه است.

Good:
**نرم‌افزار Git** یک سیستم کنترل نسخه است.
```

### 2. List Item Starting with an English Verb or Operation

```text
Bad:
- push کامل می‌شود.

Good:
- عملیات push کامل می‌شود.

Bad:
4. commit کنید

Good:
4. تغییرات را commit کنید
```

### 3. UI Checkbox or Action Item

```text
Bad:
- ☑️ **Set as the latest release** (اگر آخرین نسخه است)

Good:
- ☑️ گزینهٔ **Set as the latest release** (اگر آخرین نسخه است)
```

If the exact UI control type is known, prefer the correct wrapper:

```text
دکمهٔ **Update release**
گزینهٔ **Set as the latest release**
در تب **Changes**
در فیلد **Title**
```

### 4. Line Starting with Emoji plus English

```text
Bad:
✅ **Build** مرحلهٔ ساخت است.

Good:
✅ مرحلهٔ **Build** مرحلهٔ ساخت است.
```

Emoji does not count as the first strong character. The word after emoji must be Persian.

### 5. Blockquote Starting with Inline Code

```text
Bad:
> `user.name` را تنظیم کنید.

Good:
> کلید `user.name` را تنظیم کنید.
```

A warning blockquote is fine if the first real word after the warning emoji is Persian:

```text
Good:
> ⚠️ نکته: این دستور تاریخچه را بازنویسی می‌کند.
```

## Hidden Latin-Start Patterns

Check these patterns explicitly:

```text
Bad:
**Remote** آدرس نسخهٔ راه دور است.

Good:
**ریموت (Remote)** آدرس نسخهٔ راه دور است.

Bad:
- `v1.0.0`: اولین نسخهٔ پایدار

Good:
- نسخهٔ `v1.0.0`: اولین نسخهٔ پایدار

Bad:
- Checkout: دانلود کد

Good:
- مرحلهٔ Checkout: دانلود کد

Bad:
- `on.push.tags`: انتشار فقط با تگ

Good:
- کلید `on.push.tags`: انتشار فقط با تگ

Bad:
4. commit کنید

Good:
4. تغییرات را commit کنید

Bad:
Command Palette → `Git: Merge...`

Good:
از Command Palette مسیر `Git: Merge...` را انتخاب کنید.
```

## Direction Audit Algorithm

Use this deterministic mental procedure after all edits. Do not use shell commands or helper files.

### Step 1: Identify Excluded Zones

Skip:

- fenced code blocks
- directory trees
- URLs
- email addresses
- purely English lines
- pure technical lists containing only commands, paths, identifiers, versions, or settings
- exempt technical tables
- reference/resource titles that must remain English

### Step 2: Inspect Each Remaining Narrative Line

For every non-exempt narrative line:

1. Remove leading indentation.
2. Remove heading markers: `#`, `##`, `###`.
3. Remove blockquote markers: `>`.
4. Remove list markers: `-`, `*`, `+`, `1.`, `۱.`.
5. Remove checklist markers: `[ ]`, `[x]`.
6. Remove emoji, digits, punctuation, spaces, and invisible direction marks.
7. Remove neutral formatting markers: `*`, `_`, backticks, brackets.
8. Find the first strong directional letter.

A Latin letter is a strong LTR character. A Persian or Arabic letter is a strong RTL character.

### Step 3: Decide Violation

A line violates the rule if:

- a Latin letter exists, and
- no Persian letter exists, or
- the first strong letter is Latin.

If the line is exempt, do not treat it as a violation.

### Step 4: Fix Violations

Fix each violation by:

- adding a Persian wrapper from the wrapper dictionary
- moving the Latin identifier after a Persian word
- placing the Latin identifier in parentheses after a Persian word
- using a neutral Persian frame such as «در»، «با»، «از»

Never fix a violation by adding RLM/LRM.

### Step 5: Re-Audit

Re-run the audit after every batch of fixes.

Exit criterion:

```text
REMAINING VIOLATIONS: 0
```

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

## Numbering Major Sections and Mechanical Numbering

For long documents, number major sections using Persian digits.

Example:

```markdown
## ۱. معرفی
## ۲. تنظیمات
## ۳. قوانین
```

Use Persian digits (۱, ۲, ۳, ...) for mechanical section numbering.

Use numbering when:

- the document is long
- the document has many major sections
- navigation benefits from numbering

Do not force numbering on short documents.

Fixing duplicate, missing, or obviously broken mechanical numbering is allowed as a presentation fix. It is not considered a content change if:

- the section order is unchanged
- no section is added or removed
- the factual meaning is unchanged
- the numbering bug is mechanical

Do not change numbering if it is a semantic identifier, such as legal clause numbers, specification clause numbers, or contract item numbers, unless it is clearly a typo.

## Table of Contents

For large documents, generating a linked Table of Contents is the default.

Rules:

- every TOC entry must be a working link
- a plain unlinked TOC is not acceptable for long documents
- place the TOC near the beginning
- preserve section order
- mirror heading emoji in TOC entries when emoji are used
- keep TOC entries Persian-first after emoji
- do not fragment a linked phrase into multiple broken links

Default safe method: use ASCII invisible anchors.

Example:

```markdown
## 📋 فهرست مطالب

1. [معرفی](#sec-1)
2. [تنظیمات](#sec-2)
3. [قوانین](#sec-3)

<a id="sec-1"></a>

## 📖 معرفی

<a id="sec-2"></a>

## 🧩 تنظیمات

<a id="sec-3"></a>

## 🧠 قوانین
```

Rules for ASCII anchors:

- id must be ASCII: `sec-1`, `sec-2`, ...
- use one empty line before and after the anchor tag
- use anchors only for TOC/navigation targets
- never place anchors inside ordinary content
- use sequential numbering based on document order
- if headings are duplicated, still use unique `sec-n` anchors

Slug-based anchors may be used only when the document already has stable slugs and no emoji, punctuation, invisible character, or renderer difference can break them. For maximum reliability, prefer ASCII anchors.

## Emoji Usage

Emoji are allowed only when they improve navigation.

Use emoji to the necessary and sufficient degree — neither absent nor excessive.

Rules:

- Add exactly one contextually meaningful emoji per major heading.
- Mirror the same emoji in the matching TOC entry.
- Use functional emoji only on real warnings and tips.
- Do not decorate ordinary paragraphs with emoji.
- Do not place emoji at the beginning of every paragraph.

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

## Variation-Selector Rule

Never use emoji that contain U+FE0F variation selector in headings.

Forbidden heading emoji examples:

```text
✍️ ❤️ ☑️ 🛡️ ⚙️ ✔️ ⚠️ 🛠️
```

Use single-codepoint emoji instead:

```text
📖 🧩 📊 🔔 🧠 🎯 💡 🏁 🎨 🧭 ✅ ❓ 📋 💾
```

Reason: slug generators may keep invisible variation selector characters inside heading slugs, which can break anchor links.

This rule applies to headings. Callouts and blockquotes may still use functional emoji because they do not generate anchors.

## Lists

Choose the most appropriate list type.

### Numbered Lists

Use when:

- order matters
- steps exist
- rules are enumerated
- priorities exist

### Bullet Lists

Use when:

- order does not matter
- features are listed
- options are listed
- characteristics are listed

### Checklists

Use when:

- prerequisites exist
- validation exists
- setup requirements exist
- review tasks exist

Example:

```markdown
- [ ] نصب Python
- [ ] نصب Git
- [ ] تنظیم API Key
```

Every narrative list item in a Persian document must obey the Line-Start Direction Rule.

A list item that is only a command, path, identifier, or exact technical value may remain exempt. A list item that contains Persian explanation must be Persian-first.

## Tables

Use tables only when they improve readability.

Good candidates:

- settings
- comparisons
- labels and meanings
- structured data
- glossaries
- UI identifiers

Example:

```markdown
| تنظیم | مقدار |
| --- | --- |
| روزها | ۵ |
| هفته‌ها | ۲ |
```

Do not convert ordinary text into tables unnecessarily.

### Technical Table Exemption

A table is exempt from Persian-first rewriting when it is primarily technical.

A table is technical if:

- its cells are commands, paths, settings, values, versions, error messages, identifiers, or standards
- its first column is an exact technical identifier
- it is a glossary table whose term column must remain English
- it is a UI identifier table whose first column is an exact UI label
- it is a reference/resource table whose titles must remain in the original language

In exempt technical tables:

- keep the technical column English
- keep exact identifiers unchanged
- keep Persian description columns readable
- do not translate technical terms

In narrative tables:

- prefer Persian column headers
- if a Persian explanatory cell starts with a Latin identifier, add a Persian wrapper or move the identifier after a Persian word
- do not create awkward or wrong category claims

## Structural Elements

Preserve existing structural elements.

Never destroy or flatten:

- tables
- code blocks
- checklists
- blockquotes
- directory trees
- reference lists
- resource lists

## Directory Trees

Preserve directory trees exactly.

Example:

```text
project/
├── docs/
├── src/
└── tests/
```

Never convert directory trees into plain text lists.

## Code Blocks

Preserve fenced code blocks.

Example:

```python
print("hello")
```

Do not convert code blocks into prose.

Comments inside fenced code blocks are part of the code block and are exempt from Persian-first rewriting.

## Emphasis

Use emphasis sparingly.

### Bold

Use for:

- important concepts
- important conclusions
- key settings
- important distinctions

Do not bold entire paragraphs.

### Inline Code

Use for:

- settings
- identifiers
- commands
- labels
- paths
- technical names
- exact UI labels when short

Example:

```markdown
مقدار `Cooldown` را تنظیم کنید.
```

## Callouts and Quotes

Use blockquotes only when they improve scanning.

Examples:

```markdown
> 💡 نکته مهم

> 🔔 اولویت هشدار:
> ماه > هفته > روز

> ⚠️ این ابزار معامله انجام نمی‌دهد.
```

Do not turn ordinary text into blockquotes.

A blockquote containing Persian narrative must have a Persian-first first real word after blockquote marker, emoji, digits, and punctuation.

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

Only use a horizontal rule when a major visual break is needed.

## Internal Links

When a Table of Contents exists:

- create internal Markdown links
- keep anchors synchronized with headings
- preserve heading order
- prefer ASCII anchors for reliability
- do not fragment linked phrases

Internal links are preferred for long documents.

## Anchor Reliability

Slug algorithm behavior in common viewers:

- removes emoji
- removes punctuation such as `—`, `«`, `»`, `(`, `)`, `.`
- removes ZWNJ
- keeps Persian/Arabic letters and Persian digits
- replaces each whitespace with `-`
- may keep an invisible variation selector if present

Never compute anchors by guessing.

For guaranteed navigation, use invisible ASCII anchors as TOC targets.

Example:

```markdown
<a id="sec-1"></a>

## 👀 بخش ۱ — در یک نگاه

- [بخش ۱](#sec-1)
```

Manual verification:

1. Count TOC entries.
2. Count ASCII anchors.
3. Ensure each TOC link has exactly one matching `id`.
4. Ensure no TOC link is split into multiple links.
5. Ensure anchor ids are unique.
6. Ensure anchor ids are ASCII.
7. If the counts differ, add the missing anchors rather than removing TOC entries.

## Formatting Workflow

When formatting a document:

1. Read the Markdown source as plain UTF-8 text.
2. Preserve content, order, code, tables, links, and references.
3. Detect headings.
4. Build heading hierarchy.
5. Classify lines as narrative, technical, exempt, or table content.
6. Improve navigation.
7. Generate TOC with ASCII anchors if useful.
8. Improve lists.
9. Improve tables.
10. Improve emphasis.
11. Fix RTL/LTR line-start direction using the wrapper dictionary.
12. Remove known accidental RLM/LRM direction marks from narrative lines.
13. Fix mechanical numbering bugs.
14. Normalize spacing.
15. Run the Direction Audit Algorithm until zero violations remain.
16. Run the Final Validation Checklist.
17. Deliver per Execution Rules.

## Things This Skill Must Never Do

Never:

- semantically rewrite content
- summarize content
- translate technical identifiers
- translate reference titles
- reorder sections
- add new factual information
- remove meaningful information
- simplify technical details
- add fictional examples
- add new sections that did not exist
- convert Markdown to HTML
- inject CSS
- create or run scripts or programs
- create helper, probe, or temporary files
- run shell commands
- add RLM/LRM as a direction shortcut
- leave known line-start RLM/LRM in narrative text
- fragment TOC links
- use emoji with variation selector in headings

This skill formats presentation.

It does not semantically author, edit, or rewrite content. The allowed presentation-level changes defined above are permitted.

## Final Validation Checklist

Before returning the final document verify the following.

### Critical Blockers

- [ ] Only the target file was changed.
- [ ] No other files were created, edited, or deleted.
- [ ] Output is pure Markdown.
- [ ] The only HTML is empty `<a id="..."></a>` anchor tags.
- [ ] No CSS, JavaScript, or HTML styling wrappers exist.
- [ ] Semantic content, facts, examples, code, links, tables, and lists are preserved.
- [ ] No semantic rewrite occurred except allowed presentation-level changes.
- [ ] Logical order is preserved.
- [ ] Technical identifiers, commands, paths, URLs, error messages, and reference names remain unchanged.
- [ ] No RLM/LRM was added.
- [ ] Known line-start RLM/LRM in narrative text was removed.
- [ ] Zero known line-start violations remain outside exempt zones.
- [ ] For long documents, every TOC entry is a single unfragmented link.
- [ ] Every TOC link points to an existing ASCII anchor or verified slug.
- [ ] Heading emoji contain no U+FE0F variation selector.
- [ ] No helper/probe/temporary files were created.
- [ ] No shell commands were executed.

### Structural Integrity

- [ ] Heading hierarchy has no skipped levels.
- [ ] Major section numbering, if present, has no duplicate mechanical numbers and uses Persian digits.
- [ ] Missing mechanical numbering was fixed only when clearly a numbering bug.
- [ ] Tables are preserved.
- [ ] Code blocks are preserved.
- [ ] Directory trees are preserved.
- [ ] Checklists are preserved.
- [ ] Blockquotes are preserved, and any narrative line-start inside them is fixed with a Persian wrapper.
- [ ] TOC order matches document order.
- [ ] ASCII anchors, if used, are unique and sequential.
- [ ] Reference/resource titles remain in their original language.

### Presentation Quality Objective Checks

- [ ] Long documents have a linked TOC.
- [ ] TOC entries mirror major heading emoji when headings use emoji.
- [ ] Major headings have at most one emoji.
- [ ] Emoji are not added to ordinary paragraphs.
- [ ] No entire paragraph is bolded.
- [ ] Inline code is used for exact settings, commands, paths, identifiers, and labels.
- [ ] No triple blank lines exist outside code fences.
- [ ] Headings and fenced code blocks are separated from surrounding blocks by exactly one blank line, except at the very beginning or end of the document.
- [ ] Horizontal rules are used only for major boundaries.
- [ ] The document is ready for standard Markdown previews such as GitHub and VS Code.

### Advisory Quality Guidance

These are quality goals, not subjective blockers:

- Navigation should be clearer than before, especially through TOC and heading hierarchy.
- Emphasis should be sparing and functional.
- Spacing should be compact and consistent.
- Emoji should aid recognition, not decorate the text.