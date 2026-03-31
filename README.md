# 🦞 Auto-Diary

> Bilingual daily diary skill for OpenClaw.

**Languages / 语言**: [English](README.md) | [中文](README-zh.md)

---

## What It Does

- **Daily diary** at 08:20 (summarizes yesterday)
- **Weekly review** every Saturday at 09:00 (7-day aggregation)
- **Monthly review** on the 1st of each month at 09:00 (30-day aggregation)
- Bilingual output: Chinese summary for Jialin, English details for HexaLoop
- Extracts 1-3 actionable insights → `auto-learn.md` for the meditation layer
- Pushes Feishu Interactive cards to `oc_15949806c791613dbf45b872e8bc111a`

## Quick Start

### Install

```bash
# Place in your skills directory
cp -r auto-diary ~/.openclaw/skills/
```

### Cron Setup

```bash
# Daily diary (08:20)
openclaw cron add --name "每日日记" --cron "20 8 * * *" --tz "Asia/Shanghai" \
  --message "diary write" --session isolated --agent main

# Weekly review (Saturday 09:00)
openclaw cron add --name "周度日记回顾" --cron "0 9 * * 6" --tz "Asia/Shanghai" \
  --message "diary weekly" --session isolated --agent main

# Monthly review (1st of month 09:00)
openclaw cron add --name "月度日记回顾" --cron "0 9 1 * *" --tz "Asia/Shanghai" \
  --message "diary monthly" --session isolated --agent main
```

### Manual Trigger

Send a message to your OpenClaw bot:
- `diary write` — generate yesterday's diary now
- `diary weekly` — generate weekly review now
- `diary monthly` — generate monthly review now

## File Structure

```
auto-diary/
├── SKILL.md                      # Main skill definition
├── scripts/
│   ├── write_diary.py           # Core: read context → AI write → save
│   ├── send_diary.py            # Build & push Feishu Interactive cards
│   ├── weekly_review.py         # 7-day aggregation
│   └── monthly_review.py        # 30-day aggregation
└── templates/
    └── diary_template.md         # Diary Markdown template
```

## HexaLoop Integration

Diary insights flow into the HexaLoop system:

```
diary insights → auto-learn.md → Meditation (02:30) → reflection → farm seeds → harvest → OPD Scorer → SOUL.md/SKILL.md
```

See [HexaLoop System Architecture](https://github.com/0xcjl/hexaloop-core) for details.

## Tags

`auto-diary` `daily-diary` `weekly-review` `monthly-review` `hexaloop` `feishu` `openclaw-skill` `bilingual` `self-improvement` `meditation`

---

*Part of the [HexaLoop](https://github.com/0xcjl/hexaloop-core) ecosystem.*
