# Install the mainline Matt Pocock skills

Copy everything below this line and paste it into Claude Code as one message.

---

You are installing the mainline Matt Pocock skills for Claude Code on this machine using the `skills` CLI (the installer at skills.sh). You run every command yourself — never ask me to type a command. Narrate each step in one plain sentence before running it, and name any tool the first time you use it.

Follow these steps exactly, in order.

## 1. Preflight

Check that `npx` is available (`npx --version`). If it is missing, install Node.js yourself — on macOS via Homebrew (`brew install node`) if Homebrew is present, otherwise with the official installer from nodejs.org for this platform, telling me first that a download is about to run and that slow wifi can make it look frozen when it isn't.

## 2. Read the live mainline skill list

Run:

```
npx -y skills@latest add mattpocock/skills -l
```

This lists the available skills without installing anything. The output groups skills under headings. Collect the skill names under the **"Mattpocock Skills"** heading — that group is the mainline set. Ignore the **"General"** group entirely.

Never substitute a hardcoded or remembered list: the listing you just ran is the only source of truth, so upstream additions and renames are picked up on every run. If no "Mattpocock Skills" heading appears in the output, stop and report exactly what the listing showed — do not guess the set or fall back to installing everything.

## 3. Move aside any global raw copies of mainline skills

Global mainline skills must exist only as symlinks. For each collected skill name, check `~/.claude/skills/<name>`:

- If it is a **real directory** (not a symlink), rename it to `<name>.bak` — it is a stale copy the symlink install will replace. Do not delete anything yet: the `.bak` folders are the rollback if the install fails, and are removed only after step 6 verifies.
- If it is a symlink (even a broken one), leave it; the installer refreshes it.
- If it does not exist, nothing to do.

Touch nothing else in `~/.claude/skills/` — only names collected in step 2. Never touch any project-level `.claude/skills/` directory anywhere.

## 4. Install the mainline set as global symlinks

Run one install command with a `-s` flag per collected skill name (the CLI accepts many `-s` flags in one call). Do **not** pass `--copy`, and target **both** agents — the two-agent form is load-bearing: it makes the CLI place skills in the shared `~/.agents/skills/` store and symlink them into `~/.claude/skills/`, whereas a single-agent install copies files instead. Codex reads the shared store directly, so Codex support comes free from the same call:

```
npx -y skills@latest add mattpocock/skills -g -a claude-code -a codex -s <name1> -s <name2> ... -y
```

If you script the `-s` flags in zsh, expand them as an array (zsh does not word-split unquoted variables) — or simply write every `-s <name>` out literally in the command.

## 5. If the CLI ever rejects the codex agent target

Only if the command in step 4 errors because `codex` is not a recognised agent target: re-run it with `-a claude-code` alone, accept that the CLI will install copies rather than symlinks, and say so plainly in the final report. Do not build any other workaround.

## 6. Verify and report

For every skill name collected in step 2, confirm that `~/.claude/skills/<name>` now exists and is a symlink whose target resolves (it should point into `~/.agents/skills/`). Once every skill verifies, delete the `.bak` folders from step 3. If any skill failed, restore its `.bak` folder to its original name instead, and say so in the report.

Then report to me:

- How many mainline skills are installed and that all are symlinks.
- Any skill that failed to install or whose symlink is broken, with the error.
- That Codex picks the same skills up from `~/.agents/skills/` (or, if step 5's fallback ran, that skills were installed as copies and why).
- A reminder that new sessions pick the skills up automatically — no app restart is needed for skills.

If anything failed, fix it by re-running the relevant step rather than inventing a different install method.
