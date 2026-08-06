# mp-skills-kit

**Built by Selr AI — selrai.com.au**

Installs the mainline [Matt Pocock skills](https://github.com/mattpocock/skills) into Claude Code, globally, as symlinks — in one paste.

It does not invent an installer. The whole kit is one prompt that drives the existing [`skills` CLI](https://skills.sh/) end to end: list the live skill set, install it in symlink mode, clean up any stale copies, verify, report.

## Install

1. Open Claude Code (terminal, desktop app, or VS Code).
2. Paste the entire contents of [`docs/start/setup.md`](docs/start/setup.md) as your message.
3. Let Claude run it. You don't need to type any commands yourself.

## Update

Re-run the same prompt. It's idempotent: it re-reads the live skill list from the installer, so new and renamed upstream skills are picked up automatically, and existing installs are refreshed in place.

## What gets installed

The **"Mattpocock Skills"** group as the `skills` CLI lists it — the mainline engineering and productivity skills (code-review, tdd, grilling, wayfinder, and friends). The "General" group of extras is deliberately excluded. The list is read live at install time, never hardcoded here.

Skills land as symlinks: the CLI materialises them into `~/.agents/skills/` and links them into `~/.claude/skills/`. That means one source of truth and clean updates.

## Ground rules the prompt enforces

- **Global installs are symlinks, never raw copies.** If a mainline skill already exists globally as a copied directory, it is replaced by the symlink install.
- **Project-level skill installs are never touched.** Only the global `~/.claude/skills/` directory is managed.
- **Claude Code is the target.** Codex is included only if the `skills` CLI itself accepts it as an agent target; nothing custom is bolted on.

## Requirements

- Claude Code
- Node.js / `npx` (the prompt checks for this and tells Claude to install Node if missing)
