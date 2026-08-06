# Install the mainline Matt Pocock skills

Copy everything below this line and paste it into Claude Code as one message.

---

You are installing the mainline Matt Pocock skills for Claude Code on this machine using the `skills` CLI (the installer at skills.sh). You run every command yourself — never ask me to type a command. Narrate each step in one plain sentence before running it, and name any tool the first time you use it.

Follow these steps exactly, in order.

## 1. Preflight

Check that `npx` is available (`npx --version`). If it is missing, install Node.js yourself by the standard method for this platform, telling me first that a download is about to run and that slow wifi can make it look frozen when it isn't.

## 2. Read the live mainline skill list

Run:

```
npx -y skills@latest add mattpocock/skills -l
```

This lists the available skills without installing anything. The output groups skills under headings. Collect the skill names under the **"Mattpocock Skills"** heading — that group is the mainline set. Ignore the **"General"** group entirely.

Never substitute a hardcoded or remembered list: the listing you just ran is the only source of truth, so upstream additions and renames are picked up on every run.

## 3. Remove any global raw copies of mainline skills

Global mainline skills must exist only as symlinks. For each collected skill name, check `~/.claude/skills/<name>`:

- If it is a **real directory** (not a symlink), delete it — it is a stale copy that the symlink install will replace.
- If it is a symlink (even a broken one), leave it; the installer refreshes it.
- If it does not exist, nothing to do.

Touch nothing else in `~/.claude/skills/` — only names collected in step 2. Never touch any project-level `.claude/skills/` directory anywhere.

## 4. Install the mainline set as global symlinks

Run one install command with a `-s` flag per collected skill name (the CLI accepts many `-s` flags in one call). Do **not** pass `--copy` — symlinking is the default and is required:

```
npx -y skills@latest add mattpocock/skills -g -a claude-code -s <name1> -s <name2> ... -y
```

## 5. Codex, only if the CLI supports it

If the Codex CLI is installed on this machine (`codex --version` succeeds), attempt the same install once with `-a codex` in place of `-a claude-code`. If the `skills` CLI rejects `codex` as an agent target, or the command errors, skip Codex silently and move on — do not build any workaround.

## 6. Verify and report

For every skill name collected in step 2, confirm that `~/.claude/skills/<name>` now exists and is a symlink whose target resolves (it should point into `~/.agents/skills/`).

Then report to me:

- How many mainline skills are installed and that all are symlinks.
- Any skill that failed to install or whose symlink is broken, with the error.
- Whether Codex was included, skipped because it isn't installed, or skipped because the CLI doesn't support it.
- A reminder that new sessions pick the skills up automatically — no app restart is needed for skills.

If anything failed, fix it by re-running the relevant step rather than inventing a different install method.
