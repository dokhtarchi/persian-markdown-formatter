<div align="center">

# 🇮🇷 Persian Markdown Formatter

### An Agent-Agnostic Skill for Any AI Assistant or Coding Harness

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Format: SKILL.md](https://img.shields.io/badge/Format-SKILL.md-purple.svg)](./SKILL.md)
[![Agent Agnostic](https://img.shields.io/badge/Agent-Agnostic-green.svg)](#-compatibility)

**Format Persian and mixed Persian-English Markdown documents for maximum readability — without changing the content.**

[⚡ Quick Start](#-quick-start) • [🧩 Compatibility](#-compatibility) • [🎯 Examples](#-examples) • [🇮🇷 فارسی](#-توضیحات-فارسی)

</div>

## 🎯 What is this?

A structured, harness-agnostic **Skill file** (`SKILL.md`) that teaches any AI agent or coding assistant how to properly format Persian and RTL/LTR mixed Markdown documents — **without altering the content**.

Perfect for:
- 📘 Documentation and guides
- 📓 Technical notes
- 📄 README files
- 📚 Long-form tutorials
- 📋 Project specifications

## ⚡ Quick Start

1. **Download:**
   ```bash
   git clone https://github.com/dokhtarchi/persian-markdown-formatter.git
   ```
2. **Add to your project:** copy `SKILL.md` to your project root.
3. **Ask your agent** (Cline, Claude Code, Cursor, or any assistant):
   ```
   این فایل را با persian-markdown-formatter بازآرایی کن.
   ```
   ```
   این فایل را با persian-markdown-formatter قالب‌بندی و استانداردسازی کن.
   ```
   ```
   Apply persian-markdown-formatter to this document.
   ```

Works on **any** Markdown file — just open or attach the file you want, then use one of the commands above.
   ```

## 🧩 Compatibility

This skill is **harness-agnostic**: it is a plain `SKILL.md` instruction file, so any AI agent or coding assistant that can read project files can use it.

| Agent / Harness | How to use |
|---|---|
| Cline (VS Code) | Copy `SKILL.md` to the project root |
| Claude Code | Place in project root or `.claude/skills/` |
| Claude.ai (Projects) | Upload `SKILL.md` to the project's knowledge |
| Cursor | Reference `SKILL.md` in your rules |
| Windsurf / Copilot / Aider / OpenCode | Include `SKILL.md` in the agent's context |

Developed and tested with Cline; expected to work with any SKILL.md-aware agent.

## ✨ Features

- ✅ **Pure Markdown output** — no HTML, no CSS, no wrappers
- ✅ **RTL/LTR aware** — handles mixed Persian/English gracefully
- ✅ **Content-preserving** — formats without rewriting or summarizing
- ✅ **Navigation-first** — TOC, headings, and structure prioritized
- ✅ **Emoji-smart** — emoji only for navigation, never decoration
- ✅ **Structure-safe** — preserves code blocks, tables, trees, and links

## 🎯 Examples

Full before/after sample: [`examples/before.md`](./examples/before.md) → [`examples/after.md`](./examples/after.md)

## 📖 Documentation

The full specification lives in [`SKILL.md`](./SKILL.md): purpose & principles, RTL/LTR handling, heading structure, TOC, emoji usage, lists/tables/structural elements, emphasis & callouts, spacing, and a final validation checklist.

## 🤝 Contributing

Contributions are welcome: bug reports, edge cases, improvements, more examples, and translations.

## 📄 License

MIT — free to use, modify, and share. See [LICENSE](./LICENSE).

## ⭐ Support

If this skill helps your workflow, star the repo and share it with your network.

---

## 🇮🇷 توضیحات فارسی

### این چیست؟

یک فایل **Skill** ساختاریافته و مستقل از هر ابزار (agent-agnostic) که به دستیارهای هوش مصنوعی یاد می‌دهد چگونه مستندات مارک‌داون فارسی و ترکیبی را **بدون تغییر محتوا** حرفه‌ای قالب‌بندی کنند.

### شروع سریع

1. فایل `SKILL.md` را در ریشهٔ پروژهٔ خود کپی کنید.
2. به دستیار هوش مصنوعی (Cline، Claude Code، Cursor و...) بگویید:
   ```
   این فایل را با persian-markdown-formatter بازآرایی کن.
   ```

### حمایت

اگر این Skill به کارتان می‌آید، با ⭐ دادن به ریپو از آن حمایت کنید.