# 🦞 Auto-Diary

> OpenClaw 自动日记技能 — 中文给 Jialin 看，英文给 HexaLoop 系统看。

**语言 / Languages**: [English](README.md) | [中文](README-zh.md)

---

## 功能概述

- **每日日记**：每天 08:20 自动生成（总结前一天）
- **周度回顾**：每周六 09:00（聚合7天）
- **月度回顾**：每月1日 09:00（聚合30天）
- 双语输出：中文摘要 + 英文系统备注
- 提取 1-3 条价值洞察 → 写入 `auto-learn.md`（供冥想层）
- 推送飞书 Interactive 卡片到 `oc_15949806c791613dbf45b872e8bc111a`

## 快速开始

### 安装

```bash
# 复制到 skills 目录
cp -r auto-diary ~/.openclaw/skills/
```

### Cron 配置

```bash
# 每日日记（08:20）
openclaw cron add --name "每日日记" --cron "20 8 * * *" --tz "Asia/Shanghai" \
  --message "diary write" --session isolated --agent main

# 周度回顾（周六 09:00）
openclaw cron add --name "周度日记回顾" --cron "0 9 * * 6" --tz "Asia/Shanghai" \
  --message "diary weekly" --session isolated --agent main

# 月度回顾（每月1日 09:00）
openclaw cron add --name "月度日记回顾" --cron "0 9 1 * *" --tz "Asia/Shanghai" \
  --message "diary monthly" --session isolated --agent main
```

### 手动触发

向皮皮虾发送消息：
- `diary write` — 立即生成昨日日记
- `diary weekly` — 立即生成周度回顾
- `diary monthly` — 立即生成月度回顾

## 文件结构

```
auto-diary/
├── SKILL.md                      # 技能定义
├── scripts/
│   ├── write_diary.py           # 核心：读上下文 → AI 写日记 → 保存
│   ├── send_diary.py            # 构建并推送飞书 Interactive 卡片
│   ├── weekly_review.py         # 周度聚合
│   └── monthly_review.py        # 月度聚合
└── templates/
    └── diary_template.md         # 日记 Markdown 模板
```

## HexaLoop 集成

日记洞察汇入 HexaLoop 系统：

```
diary insights → auto-learn.md → 冥想 (02:30) → 反思 → 农场种子 → 收获 → OPD Scorer → SOUL.md/SKILL.md
```

详见 [HexaLoop 系统架构](https://github.com/0xcjl/hexaloop-core)。

## 标签

`auto-diary` `daily-diary` `weekly-review` `monthly-review` `hexaloop` `feishu` `openclaw-skill` `bilingual` `self-improvement` `meditation`

---

*隶属于 [HexaLoop](https://github.com/0xcjl/hexaloop-core) 生态系统。*
