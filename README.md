# rule-toolkit

[English](#english) | [中文](#中文)

---

## English

A skill for AI coding agents that scans your constraint files (CLAUDE.md, agents.md, soul.md, tools.md, .cursorrules, etc.), identifies rules that can be enforced by tools, and auto-generates linters, hooks, validators, and wrapper functions.

### Why

Rules written in prompt files are forgotten when context gets long, inconsistently applied across sub-agents, and never checked automatically.

Rules compiled into tools are 100% enforced, cost zero tokens, and self-verify on every save/commit.

### Install

**Claude Code**

```bash
npx skills add dachung/rule-toolkit
```

**OpenClaw**

```bash
openclaw skills install dachung/rule-toolkit
```

**Cursor / Copilot / Other**

```bash
git clone https://github.com/dachung/rule-toolkit.git ~/.claude/skills/rule-toolkit
```

### What It Does

1. **Detects platform** — Claude Code, OpenClaw, Cursor, Copilot
2. **Scans constraint files** — reads all your rules
3. **Classifies rules** — auto-toolable vs. prompt-only
4. **Generates tools** — ESLint, Prettier, Husky, commitlint, wrapper functions, custom validators
5. **Reports** — shows what was converted and what remains in prompt
6. **Cleans up** — removes toolified rules from constraint files, saving tokens

### Supported Constraint Files

| Platform | Files |
|----------|-------|
| Claude Code | `CLAUDE.md`, `.claude/commands/*.md` |
| OpenClaw | `agents.md`, `soul.md`, `identity.md`, `user.md`, `tools.md`, `bootstrap.md`, `memory.md` |
| Cursor | `.cursorrules` |
| Copilot | `.github/copilot-instructions.md` |
| Generic | `AGENT.md`, `SOUL.md` |

### Example

Given a `CLAUDE.md` with:

```markdown
## Code Style
- Use 2 spaces, no semicolons, single quotes
- Files must be kebab-case

## API
- All responses must use { code, data, msg }

## Git
- Conventional commits required
```

The skill generates:

- `.prettierrc` — indentation, semicolons, quotes
- ESLint rule — file naming convention
- `src/utils/response.ts` — API response wrapper
- `commitlint.config.js` + `.husky/commit-msg` — conventional commits

Report:

```
Converted: 4 rules -> tools
Remaining: 0 rules -> prompt
Token savings: ~500 tokens/conversation
```

### Project Structure

```
rule-toolkit/
├── SKILL.md                    # Main skill instructions
├── LICENSE                     # MIT
├── README.md                   # This file
├── references/
│   ├── tool-patterns.md        # Detailed generation patterns
│   └── openclaw-hooks.md       # OpenClaw-specific hooks reference
└── scripts/
    └── detect-rules.sh         # Dry-run rule detection script
```

### License

MIT

---

## 中文

一个 AI 编码 Agent 技能，扫描你的约束文件（CLAUDE.md、agents.md、soul.md、tools.md、.cursorrules 等），识别可以被工具强制执行的规则，自动生成 linter、hook、校验器和包装函数。

### 为什么需要

写在 prompt 文件里的规则：
- 上下文变长后会被遗忘
- 在多个子 Agent 间执行不一致
- 永远不会被自动检查

编译成工具的规则：
- 100% 强制执行（linter、hook、类型检查）
- 零 token 消耗（不占用上下文）
- 自动验证（每次保存/提交都检查）

### 安装

**Claude Code**

```bash
npx skills add dachung/rule-toolkit
```

**OpenClaw**

```bash
openclaw skills install dachung/rule-toolkit
```

**Cursor / Copilot / 其他**

```bash
git clone https://github.com/dachung/rule-toolkit.git ~/.claude/skills/rule-toolkit
```

### 功能

1. **检测平台** — Claude Code、OpenClaw、Cursor、Copilot
2. **扫描约束文件** — 读取所有规则
3. **分类规则** — 可工具化 vs. 仅 prompt
4. **生成工具** — ESLint、Prettier、Husky、commitlint、包装函数、自定义校验器
5. **生成报告** — 展示哪些规则已转换，哪些仍留在 prompt 中
6. **清理约束文件** — 移除已工具化的规则，节省 token

### 支持的约束文件

| 平台 | 文件 |
|------|------|
| Claude Code | `CLAUDE.md`、`.claude/commands/*.md` |
| OpenClaw | `agents.md`、`soul.md`、`identity.md`、`user.md`、`tools.md`、`bootstrap.md`、`memory.md` |
| Cursor | `.cursorrules` |
| Copilot | `.github/copilot-instructions.md` |
| 通用 | `AGENT.md`、`SOUL.md` |

### 示例

假设 `CLAUDE.md` 中有：

```markdown
## 代码风格
- 使用 2 空格缩进，不用分号，单引号
- 文件名必须 kebab-case

## API
- 所有响应必须用 { code, data, msg } 包装

## Git
- 提交信息必须遵循 Conventional Commits
```

技能会自动生成：

- `.prettierrc` — 缩进、分号、引号规则
- ESLint 规则 — 文件命名约定
- `src/utils/response.ts` — API 响应包装函数
- `commitlint.config.js` + `.husky/commit-msg` — Conventional Commits 校验

报告：

```
已转换: 4 条规则 -> 工具
保留: 0 条规则 -> prompt
Token 节省: ~500 tokens/对话
```

### 项目结构

```
rule-toolkit/
├── SKILL.md                    # 主指令文件
├── LICENSE                     # MIT 协议
├── README.md                   # 本文件
├── references/
│   ├── tool-patterns.md        # 详细生成模式参考
│   └── openclaw-hooks.md       # OpenClaw hooks 专属参考
└── scripts/
    └── detect-rules.sh         # 干运行检测脚本
```

### 许可证

MIT
