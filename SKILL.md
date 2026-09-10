---
name: persian-markdown-formatter
description: Format Persian and mixed Persian-English Markdown documents for maximum readability, navigation, and visual consistency. Use when cleaning, restructuring, standardizing, or polishing Markdown presentation. Preserves meaning, logical order, scope, and technical accuracy; allows only the presentation-level edits listed in this skill. Suitable for documentation, guides, notes, manuals, README files, tutorials, specifications, and long-form Markdown.
metadata:
  version: "2.0.0"
  author: dokhtarchi
  repository: https://github.com/dokhtarchi/persian-markdown-formatter
---

# Persian Markdown Formatter

## Purpose

This skill is a Markdown formatter, not a semantic content editor.

It improves presentation, readability, navigation, visual hierarchy, structural
consistency, and RTL/LTR stability, while preserving content, meaning, logical
order, scope, technical accuracy, and exact technical identifiers.

Typical invocations:

- این فایل را با persian-markdown-formatter بازآرایی کن.
- این فایل را با persian-markdown-formatter قالب‌بندی و استانداردسازی کن.
- Apply persian-markdown-formatter to this document.

## Execution Rules

- Read the Markdown source and rewrite it yourself. Reading the file as plain
  UTF-8 text is sufficient.
- Default delivery: write the complete formatted Markdown back to the same file,
  then give a 3–5 bullet summary of changes.
- If the user asks for the result in chat, or pasted the content with no file,
  return the full document in one fenced Markdown block and change no file.
- Scope: operate only on the file the user names. Do not read, search, or borrow
  content from other project files. Do not create, edit, or delete any other file.
- Never create helper, probe, or temporary files. Never run shell commands or
  scripts to inspect, escape, or transform the document.
- Idempotence: running this skill again on its own output must produce an
  identical document. Never double-add wrappers, numbers, anchors, or a TOC.
- Realistic audit: this is a careful textual audit, not a linter. Where invisible
  characters or renderer-specific anchor behavior cannot be verified by plain
  reading, choose the safer construction: Persian wrapper, ASCII anchor, or
  moving the Latin identifier after a Persian word.

## Definitions

**Long document:** six or more level-2 headings, or roughly 150+ lines. Long
documents get a linked TOC and mechanical section numbering by default; short
documents get neither.

**Narrative line:** heading, TOC entry, paragraph, mixed-language list item,
checklist item with Persian text, blockquote note with Persian text, or a table
cell containing Persian explanatory text.

**Technical span:** fenced code, inline code, URL, email, handle, exact error
message, path, flag, variable, version, ticker, exact UI label, standard name,
tool name, repository name, or reference/book/documentation title.

## Preserve, Allow, Forbid

### Preserve

All content, sections, technical details, examples, code, tables, links, lists,
reference names, URLs, error messages, and directory trees. Minor spelling and
punctuation fixes are allowed only when meaning is untouched.

### Allowed Presentation-Level Changes

- Adding a minimal Persian wrapper word before an unchanged technical identifier.
- Moving a Latin identifier into parentheses after a Persian word.
- Removing accidental `RLM` (U+200F) / `LRM` (U+200E) from the start of narrative lines.
- Fixing duplicate, missing, or clearly broken mechanical numbering.
- Adding a Table of Contents section and ASCII anchor targets for navigation.
  This is the single permitted new section.
- Normalizing spacing, list markers, heading hierarchy, emphasis, and Persian
  typography per the normalization rules below.

### Forbidden

- Semantic rewriting, summarizing, expanding, reinterpreting, or reordering sections.
- Adding new factual information, fictional examples, or new sections other than the TOC.
- Removing meaningful information.
- Translating, transliterating, or Persianizing any technical span. `Git` stays
  `Git`, not «گیت». `GitHub`, `Conventional Commits`, `Pro Git`, and
  `GitHub Docs` stay unchanged.
- Changing exact commands, settings, paths, flags, variables, tickers, UI labels,
  or error messages.
- Converting Markdown to HTML, injecting CSS/JS, or using `<div dir="rtl">`,
  `<span>`, `<style>`.
- Adding `RLM`/`LRM` as a direction shortcut, or leaving them at narrative line starts.
- Using emoji containing U+FE0F in headings.
- Fragmenting a TOC link into multiple links.

Output must remain pure Markdown. The single exception is empty
`<a id="..."></a>` tags used exclusively as TOC navigation targets.

## Line-Start Direction Rule

Renderers pick each line's base direction from its first strong directional
letter. Digits, emoji, punctuation, spaces, invisible marks, and formatting
markers (`#`, `>`, `-`, `1.`, `[ ]`, backticks, `*`, `_`) are not strong letters.
Latin letters inside bold, italic, or inline code **are** strong LTR characters.

Therefore every narrative line must begin with a Persian or Arabic letter.

### Canonical Exemption List

This is the only exemption list in this skill. A line is exempt if it is:

1. Inside a fenced code block, including its comments.
2. A directory tree line.
3. A URL, email address, or social handle on its own.
4. A purely English line with no Persian text.
5. A list item containing only commands, paths, identifiers, versions, settings,
   or error messages.
6. A row in a technical table: cells are mostly identifiers, values, commands,
   settings, or exact UI labels; or the first column is an exact identifier,
   glossary term, or UI label.
7. A reference/resource list item that begins with the title or its link, e.g.
   `- [Pro Git](https://git-scm.com/book) — کتاب مرجع کار با Git`.
8. YAML frontmatter, footnote definitions, and math blocks.

Everything else is narrative and must be Persian-first.

### Audit Algorithm

Run this mentally after every batch of edits.

1. Skip all exempt lines from the list above.
2. On each remaining line, strip indentation, heading/blockquote/list/checklist
   markers, emoji, digits, punctuation, invisible marks, and neutral formatting
   markers.
3. Find the first strong directional letter. **If it is Latin, the line is a
   violation.** No other condition creates a violation.
4. Fix by adding a wrapper from the dictionary, moving the identifier after a
   Persian word, wrapping it in parentheses after a Persian word, or using a
   neutral frame («در»، «با»، «از»، «مورد»). Never fix with `RLM`/`LRM`.
5. Re-audit until zero violations remain outside exempt zones.

### Conflict Resolution Hierarchy

1. Preserve the exact technical span.
2. Do not translate or transliterate it.
3. Make the line Persian-first with a wrapper or reordering.
4. If the category is unclear, use a neutral Persian frame or parentheses.
5. Never use invisible direction characters.

### Persian Wrapper Dictionary

| نوع موجودیت | لفاف فارسی | مثال |
| --- | --- | --- |
| ابزار / نرم‌افزار / سرویس | «ابزار»، «نرم‌افزار»، «سرویس» | ابزار `Git` |
| دستور | «دستور» | دستور `git push` |
| کلید / تنظیم | «کلید»، «تنظیم» | کلید `push.default` |
| مسیر / فایل | «مسیر»، «فایل» | مسیر `.git/config` |
| گزینه / چک‌باکس | «گزینهٔ» | گزینهٔ **Set as the latest release** |
| دکمه | «دکمهٔ» | دکمهٔ **Update release** |
| تب / پنل / فیلد | «تب»، «در تب»، «فیلد» | در تب **Changes** |
| پیام خطا | «پیام خطای» | پیام خطای `error: ...` |
| نسخه / برچسب | «نسخهٔ»، «برچسب» | نسخهٔ `v1.0.0` |
| شاخه | «شاخهٔ» | شاخهٔ `main` |
| متغیر / نماد | «متغیر»، «نماد» | نماد `AUDUSD` |
| روش / الگو | «روش»، «الگوی» | روش `fast-forward` |
| عملیات / مرحله | «عملیات»، «مرحلهٔ»، «گام» | عملیات `push` |
| منبع / کتاب / استاندارد | «کتاب»، «مستند»، «استاندارد» | کتاب `Pro Git` |
| حالت عمومی | «در»، «با»، «از»، «مورد» | در `user.name` |

Rules: the wrapper is a presentation fix, never a new fact; the identifier stays
byte-identical; never invent a wrong category; prefer inline code for short
identifiers and bold for clickable UI labels.

### Fix Examples

```text
Bad:  **Git** یک سیستم کنترل نسخه است.
Good: **نرم‌افزار Git** یک سیستم کنترل نسخه است.

Bad:  - push کامل می‌شود.
Good: - عملیات push کامل می‌شود.

Bad:  4. commit کنید
Good: 4. تغییرات را commit کنید

Bad:  > `user.name` را تنظیم کنید.
Good: > کلید `user.name` را تنظیم کنید.

Bad:  ✅ **Build** مرحلهٔ ساخت است.
Good: ✅ گام **Build**: مرحلهٔ ساخت پروژه است.

Bad:  🚩 Tag و Release
Good: 🚩 برچسب‌گذاری و انتشار (Tag و Release)

Bad:  - `on.push.tags`: انتشار فقط با تگ
Good: - کلید `on.push.tags`: انتشار فقط با تگ

Bad:  **Remote** آدرس نسخهٔ راه دور است.
Good: **آدرس Remote** نشانی نسخهٔ راه دور است.

Bad:  Command Palette → `Git: Merge...`
Good: از **Command Palette** مسیر `Git: Merge...` را انتخاب کنید.
```

Note the last two: the Latin identifier is framed, never translated. Writing
«ریموت» or «گیت» is a forbidden transliteration.

Exempt by contrast — leave these alone:

```text
- `git push`
- `git pull`
```

## Persian Typography Normalization

Apply only outside technical spans:

- Arabic letters to Persian: `ي` to `ی`، `ك` to `ک`.
- Arabic-Indic digits to Persian: `٤٥٦` to `۴۵۶`.
- Persian punctuation where already the document's style: `،`، `؛`، `؟`.
- `ZWNJ` (U+200C) is allowed inside Persian words for half-space. It must never
  be used to fake line direction.
- Digits: never touch digits inside code, versions, paths, URLs, or identifiers.
  In narrative prose, convert to Persian digits only if the document already
  predominantly uses them; otherwise leave as-is.

## Headings and Numbering

Build a clear hierarchy and never skip levels: `#` then `##` then `###` then `####`.

For long documents, number level-2 sections with Persian digits. Canonical
heading format is emoji, then number, then title:

```markdown
## 📖 ۱. معرفی
## 🧩 ۲. تنظیمات
## 🧠 ۳. قوانین
```

The TOC section itself is never numbered. Fix duplicate or missing mechanical
numbering, but never renumber semantic identifiers such as legal, contract, or
specification clause numbers unless it is clearly a typo. Never use Persian
digits as list markers; `۱.` does not create an ordered list in CommonMark.

## Table of Contents and Anchors

For long documents a linked TOC is the default; a plain unlinked TOC is not
acceptable. Place it near the beginning, preserve section order, and make each
entry's link text exactly match its heading text, including emoji and number.
Use a bullet list so no second numbering appears.

```markdown
## 📋 فهرست مطالب

- [📖 ۱. معرفی](#sec-1)
- [🧩 ۲. تنظیمات](#sec-2)

<a id="sec-1"></a>

## 📖 ۱. معرفی

<a id="sec-2"></a>

## 🧩 ۲. تنظیمات
```

Anchor rules: ids are ASCII and sequential in document order (`sec-1`, `sec-2`),
unique even for duplicate headings, surrounded by one blank line, used only as
TOC targets, never inside ordinary content.

ASCII anchors are the most reliable option available, not a guarantee: renderers
that sanitize or disable inline HTML drop them. This is why TOC text must mirror
heading text — the TOC then still reads as a correct plain outline. Slug-based
anchors are acceptable only when the document already has stable, emoji-free,
punctuation-free slugs. Never compute a slug by guessing.

Verification: count TOC entries and anchors, confirm one matching unique ASCII
`id` per entry, confirm no entry is split into multiple links. If counts differ,
add the missing anchors rather than deleting TOC entries.

## Emoji

Use emoji only where they aid recognition — neither absent nor excessive.

- At most one emoji per level-2 heading, and only when the document uses emoji
  headings at all. Do not add emoji to a short document that has none.
- Mirror the heading emoji exactly in the matching TOC entry.
- No emoji on ordinary paragraphs. Functional emoji in callouts only.
- Headings must use single-codepoint emoji from this safelist:
  `📖 🧩 📊 🔔 🧠 🎯 💡 🏁 🎨 🧭 ✅ ❓ 📋 💾 🚫 🔗 📝 🚩 📦 🔍`
- Replace any existing heading emoji that has a variation selector — such as
  `✍️ ❤️ ☑️ 🛡️ ⚙️ ✔️ ⚠️ 🛠️` — with a safelist equivalent, because slug
  generators may retain the invisible U+FE0F and break anchors. Since plain
  reading cannot reliably detect U+FE0F, treat the safelist as authoritative:
  keep headings on it, and rewrite anything else.
- Callouts and blockquotes may keep functional emoji such as `⚠️`, since they
  generate no anchors.

## Lists, Tables, and Blocks

Use numbered lists for ordered steps, rules, and priorities; bullets for
unordered features and options; checklists for prerequisites and validation.
Canonical markers are `-` for bullets and sequential `1.` `2.` `3.` for ordered
lists.

```markdown
- [ ] نصب Python
- [ ] نصب Git
- [ ] تنظیم API Key
```

Use tables only where they improve readability, and never convert ordinary prose
into a table. In technical tables keep the identifier column English and exact;
in narrative tables prefer Persian headers and apply the direction rule to
Persian explanatory cells.

Preserve exactly, and never flatten into prose: fenced code blocks, tables,
checklists, blockquotes, directory trees, reference and resource lists, Mermaid
diagrams, footnote definitions and references (`[^1]`), math blocks (`$$`), and
admonition blocks (`:::note`). Treat their internals as technical spans.

Directory trees stay verbatim:

```text
project/
├── docs/
├── src/
└── tests/
```

Existing YAML frontmatter in the target document is preserved byte-for-byte.
Existing HTML in the target document is preserved as content — the pure-Markdown
rule governs what this skill *adds*, not what it deletes.

Blockquotes are for scanning aid only. A Persian blockquote must be Persian-first
after the marker and emoji:

```markdown
> ⚠️ نکته: این دستور تاریخچه را بازنویسی می‌کند.
```

## Emphasis and Spacing

Bold is for key concepts, conclusions, settings, and distinctions — never a whole
paragraph. Inline code is for settings, identifiers, commands, labels, paths,
tickers, and short exact UI labels: `Session Offset`, `Cooldown`, `AUDUSD`, `HH4`.
Do not wrap ordinary English prose in code formatting.

Keep one blank line between blocks, after headings, and before lists. No triple
blank lines outside code fences, no decorative gaps. Use a horizontal rule only
at major document boundaries, never consecutively.

## Priority Order

When rules conflict on presentation: navigation first, then readability, then RTL
stability, then decoration. The goal is professional documentation, not visual
effects.

## Workflow

Read the source; classify every line as narrative, technical, or exempt; fix
heading hierarchy and mechanical numbering; add TOC and ASCII anchors if the
document is long; normalize lists, tables, emphasis, emoji, typography, and
spacing; run the audit algorithm to zero violations; run the checklist; deliver
per the Execution Rules.

## Final Validation Checklist

- [ ] Only the target file changed; no helper files created; no shell commands run.
- [ ] Content, facts, order, code, tables, links, and reference titles are unchanged.
- [ ] Every technical span is byte-identical, untranslated, and untransliterated.
- [ ] Output is pure Markdown; the only added HTML is empty `<a id="..."></a>` tags.
- [ ] No `RLM`/`LRM` added; pre-existing narrative line-start ones removed.
- [ ] Zero line-start direction violations outside the canonical exemption list.
- [ ] Heading hierarchy skips no level; mechanical numbering is unique and
      sequential in Persian digits.
- [ ] For long documents: a linked TOC exists, entry text matches heading text,
      each entry is one unfragmented link to a unique ASCII anchor.
- [ ] Every heading emoji is on the safelist, at most one per heading.
- [ ] Spacing is normalized, and re-running this skill would change nothing.
````