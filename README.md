# mp-skills-kit

**Built by Selr AI, selrai.com.au**

Installs the mainline [Matt Pocock skills](https://github.com/mattpocock/skills) for Claude Code and Codex, in one paste. The skills are Matt Pocock's own work, MIT licensed; this kit only installs them.

It does not invent an installer. The kit is one prompt that drives the official [`skills` CLI](https://skills.sh/) end to end, installs the set as links into one shared copy, verifies it and reports.

## Install

Open [`SETUP-PROMPT.md`](SETUP-PROMPT.md) in this folder and have your AI agent (Claude Code or Codex) follow it from start to finish. It is the only install path, on Mac and Windows, and it holds every step: this README does not repeat them.

## Update

Run `SETUP-PROMPT.md` again. It is safe to re-run. The `skills` CLI and Matt's skills are both pinned to the versions this kit was tested with, so a re-run refreshes the install to those versions, and a newer release of this kit brings newer ones.

## What gets installed

The 27 skills of Matt's mainline set ("Mattpocock Skills", the engineering and productivity skills in his plugin manifest) at the pinned commit, among them **grill me**, **teach** and **handoff**. His in-progress and miscellaneous extras are left out.

The skills land once in `~/.agents/skills/`, which Codex reads, and each is linked into `~/.claude/skills/` for Claude Code. One copy serves both apps.

## Ground rules the prompt enforces

- **Links into one shared copy, never loose copies.** A loose copy of one of these skills in `~/.claude/skills/` is moved aside and replaced by the link.
- **Nothing of yours is deleted, and nothing is written through a link.** Anything else already using one of the 27 names is moved to `~/.loup/installed/mp-skills-kit.previous-<date and time>/`.
- **Another setup's install is left alone.** If grill me, teach and handoff are already installed by another setup (the LOUP workshop assistant kit installs this same set), nothing is changed.
- **Project-level skill installs are never touched.** Only the global skill folders are managed.

## Requirements

- Claude Code or Codex, on Mac or Windows
- Node.js 22.20 or newer (the setup installs it if missing)
- Internet access to npm and github.com. Both are public: no account, sign-in or token.

## Credits

The skills: [Matt Pocock](https://github.com/mattpocock/skills), MIT licence. The installer: the [`skills` CLI](https://github.com/vercel-labs/skills) by Vercel Labs, MIT licence.
