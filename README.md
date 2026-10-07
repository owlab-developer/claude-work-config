# Shared Claude config (work)

One `CLAUDE.md`, skills and settings for the whole team. Accounts, tokens, history and memory are never committed
(see `.gitignore`: everything is ignored except the shared files).

## Install

Clone into your Claude config folder: `~/.claude` (plain Claude) or a separate one (e.g. `~/.claude-work`, used with
`CLAUDE_CONFIG_DIR`). If the folder already exists, move it aside first and copy your local files back.

```bash
git clone https://github.com/owlab-developer/claude-work-config.git ~/.claude
git clone https://github.com/vlitvinenko97/prototype-kit.git ~/.claude/skills/prototype-kit
```

## Updates

Automatic: the `SessionStart` hook in `settings.json` runs `git pull --ff-only` on the config folder Claude is using
(`$CLAUDE_CONFIG_DIR`, else `~/.claude`) and on `skills/prototype-kit`, only if that folder is a clone of this repo.

Your changes: commit and push from the config folder. Personal rules go to `CLAUDE.personal.md` (not shared).
