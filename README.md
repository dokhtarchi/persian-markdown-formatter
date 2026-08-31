<div align="center">

# 🇮🇷 Persian Markdown Formatter

### یک Skill مستقل از هر ابزار، برای هر دستیار هوش مصنوعی یا هارنس کدنویسی

### An Agent-Agnostic Skill for Any AI Assistant or Coding Harness

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Format: SKILL.md](https://img.shields.io/badge/Format-SKILL.md-purple.svg)](./SKILL.md)
[![Agent Agnostic](https://img.shields.io/badge/Agent-Agnostic-green.svg)](#-compatibility)

**قالب‌بندی مستندات مارک‌داون فارسی و ترکیبی فارسی/انگلیسی برای خوانایی حداکثری — بدون تغییر محتوا.**

**Format Persian and mixed Persian-English Markdown documents for maximum readability — without changing the content.**

[🇮🇷 فارسی](#-این-چیست) • [🌐 English](#-english)

</div>

## 🎯 این چیست؟

یک فایل **Skill** ساختاریافته و مستقل از هر ابزار (agent-agnostic) که به هر دستیار هوش مصنوعی یا دستیار کدنویسی یاد می‌دهد چگونه مستندات مارک‌داون فارسی و ترکیبی RTL/LTR را به‌درستی قالب‌بندی کند — **بدون تغییر محتوا**.

مناسب برای:
- 📘 مستندات و راهنماها
- 📓 یادداشت‌های فنی
- 📄 فایل‌های README
- 📚 آموزش‌های بلند
- 📋 مشخصات پروژه

## ⚡ شروع سریع

1. **دانلود:**
   ```bash
   git clone https://github.com/dokhtarchi/persian-markdown-formatter.git
   ```
2. **افزودن به پروژه:** فایل `SKILL.md` را در ریشهٔ پروژهٔ خود کپی کنید.
3. **از دستیار هوش مصنوعی بخواهید** (Cline، Claude Code، Cursor یا هر دستیار دیگر):
   ```
   این فایل را با persian-markdown-formatter بازآرایی کن.
   ```
   ```
   این فایل را با persian-markdown-formatter قالب‌بندی و استانداردسازی کن.
   ```
   ```
   Apply persian-markdown-formatter to this document.
   ```

روی **هر** فایل مارک‌داونی کار می‌کند — کافی است فایل مورد نظر را باز یا پیوست کنید و یکی از دستورات بالا را بزنید.

## 🧩 سازگاری

این skill **مستقل از هارنس** است: یک فایل دستورالعمل `SKILL.md` ساده است، بنابراین هر دستیار هوش مصنوعی که بتواند فایل‌های پروژه را بخواند، از آن استفاده می‌کند.

| دستیار / هارنس | نحوهٔ استفاده |
|---|---|
| Cline (VS Code) | کپی `SKILL.md` در ریشهٔ پروژه |
| Claude Code | ریشهٔ پروژه یا `.claude/skills/` |
| Claude.ai (Projects) | آپلود `SKILL.md` در دانش پروژه |
| Cursor | ارجاع به `SKILL.md` در قوانین |
| Windsurf / Copilot / Aider / OpenCode | گنجاندن `SKILL.md` در زمینهٔ ایجنت |

توسعه‌یافته و تست‌شده با Cline؛ سازگار با هر ایجنتِ پشتیبانِ SKILL.md.

## ✨ ویژگی‌ها

- ✅ **خروجی مارک‌داون خالص** — بدون HTML، بدون CSS، بدون wrapper
- ✅ **آگاه به RTL/LTR** — مدیریت هوشمند متن ترکیبی فارسی/انگلیسی
- ✅ **حفظ کامل محتوا** — قالب‌بندی بدون بازنویسی یا خلاصه‌سازی
- ✅ **اولویت با ناوبری** — فهرست مطالب، سرتیترها و ساختار
- ✅ **ایموجی هدفمند** — فقط برای ناوبری، نه تزئین
- ✅ **حفظ ساختار** — بلوک‌های کد، جدول‌ها، درخت‌ها و پیوندها دست‌نخورده
- ✅ **مستقل از فایل** — روی هر فایل مارک‌داونی، نه فقط README

## 🎯 نمونه‌ها

نمونهٔ کامل قبل/بعد: [`examples/before.md`](./examples/before.md) → [`examples/after.md`](./examples/after.md)

## 📖 مستندات

مشخصات کامل در [`SKILL.md`](./SKILL.md): هدف و اصول، مدیریت RTL/LTR، ساختار سرتیترها، فهرست مطالب، استفاده از ایموجی، فهرست‌ها/جدول‌ها/عناصر ساختاری، تأکید و نقل‌قول، فاصله‌گذاری و چک‌لیست اعتبارسنجی نهایی.

## 🤝 مشارکت

مشارکت خوش‌آمد است: گزارش باگ، موارد لبه، بهبودها، نمونه‌های بیشتر و ترجمه‌ها.

## 📄 مجوز

MIT — استفاده، تغییر و اشتراک آزاد. See [LICENSE](./LICENSE).

## ⭐ حمایت

اگر این skill به کارتان می‌آید، به ریپو ستاره بدهید و آن را با شبکهٔ خود به اشتراک بگذارید.

---

## 🌐 English

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

