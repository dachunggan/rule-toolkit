# rule-toolkit

A skill for AI coding agents that scans your constraint files (CLAUDE.md, agents.md, soul.md, tools.md, .cursorrules, etc.), identifies rules that can be enforced by tools, and auto-generates linters, hooks, validators, and wrapper functions.

## Why

Rules written in prompt files are forgotten when context gets long, inconsistently applied across sub-agents, and never checked automatically.

Rules compiled into tools are 100% enforced, cost zero tokens, and self-verify on every save/commit.

## Install

### Claude Code

```bash
npx skills add dachung/rule-toolkit
```

### OpenClaw

```bash
openclaw skills install dachung/rule-toolkit
```

### Cursor / Copilot / Other

Clone this repo into your agent's skills directory:

```bash
git clone https://github.com/dachung/rule-toolkit.git ~/.claude/skills/rule-toolkit
```

## What It Does

1. **Detects platform** — Claude Code, OpenClaw, Cursor, Copilot
2. **Scans constraint files** — reads all your rules
3. **Classifies rules** — auto-toolable vs. prompt-only
4. **Generates tools** — ESLint, Prettier, Husky, commitlint, wrapper functions, custom validators
5. **Reports** — shows what was converted and what remains in prompt
6. **Cleans up** — removes toolified rules from constraint files, saving tokens

## Supported Constraint Files

| Platform | Files |
|----------|-------|
| Claude Code | `CLAUDE.md`, `.claude/commands/*.md` |
| OpenClaw | `agents.md`, `soul.md`, `identity.md`, `user.md`, `tools.md`, `bootstrap.md`, `memory.md` |
| Cursor | `.cursorrules` |
| Copilot | `.github/copilot-instructions.md` |
| Generic | `AGENT.md`, `SOUL.md` |

## Example

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

And reports:

```
Converted: 4 rules → tools
Remaining: 0 rules → prompt
Token savings: ~500 tokens/conversation
```

## Project Structure

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

## License

MIT
