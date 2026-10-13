# Set up the Matt Pocock skills (mp-skills-kit)

This file is written to you, the attendee's AI agent (Claude Code or Codex). It is the whole setup for this kit. Follow it from start to finish as if the attendee had pasted it into the chat.

## What this kit installs

**Matt Pocock's mainline skill set**: 27 skills, his own work, free and MIT licensed, from his public project at https://github.com/mattpocock/skills. Three of them are the ones the attendee was told about:

- **grill me** (`/grill-me`): Claude stops agreeing and interviews them, one hard question at a time, until the weak spots in a plan surface and it understands what they want.
- **teach** (`/teach`): Claude teaches them something they are not familiar with and checks they understood, instead of just answering.
- **handoff** (`/handoff`): packs everything that matters in a long chat into a document, so a fresh session picks up exactly where this one left off.

The other 24 are Matt's engineering and writing skills: planning, specs and tickets, test-first building, code review, bug diagnosis and more.

The kit does not invent an installer. It drives the official `skills` installer (the one behind skills.sh, by Vercel Labs, MIT licensed) end to end. Two public things are fetched from the internet, each pinned to the one version this kit was tested with:

- the `skills` installer from npm, version `1.7.2`, run with `npx`;
- Matt's skills, as GitHub's archive of commit `49dd158d1076134a641b33efb035946536778336`: `https://github.com/mattpocock/skills/archive/49dd158d1076134a641b33efb035946536778336.tar.gz`.

Nothing from Selr is downloaded or cloned. Git is not needed, and the attendee never needs a GitHub account, sign-in, password or token.

What this setup changes on the computer:

- copies this kit to its home, `~/.loup/installed/mp-skills-kit`, or moves an earlier copy of the kit there (step 1);
- installs Node.js if it is missing or older than 22.20 (step 2);
- puts the 27 skills in `~/.agents/skills`, where Codex reads them, and links each one into `~/.claude/skills` for Claude Code: one copy serves both apps (step 3);
- moves anything else already using one of those 27 names into `~/.loup/installed/mp-skills-kit.previous-<date and time>/`, so nothing of the attendee's is lost (step 3).

**Already have them?** The LOUP workshop assistant kit installs Matt's skills the same way, pinned to its own version. When step 3 finds grill me, teach and handoff already installed by another setup like that, it changes nothing at all and tells the attendee they already have the skills. It never replaces or re-points a skill another setup installed.

## How to work

Do all of this yourself. Run every command without asking for a go-ahead, and never hand the attendee a command to type. Tell them in plain English, with no jargon, as each step finishes, and name a tool the first time you use it. The only places you pause are named in the steps: the Node.js installer on a Mac without Homebrew (the attendee clicks through it and types their Mac password into the Mac's own box, never into the chat), and a restart at the end if the skills are not showing yet. If a step fails, show the real error, fix it yourself and try again. Only come back to the attendee if you genuinely cannot go on, and then explain it in plain English. Never report a failed step as done. Never ask the attendee to paste a password, token or code into the chat: nothing here needs one.

**Safe to run again.** Every step looks at what is already there. Running this file again refreshes the kit's home and the skills this kit installed to the versions pinned above, and changes nothing else. A newer release of this kit brings newer pinned versions; running its `SETUP-PROMPT.md` is how the attendee updates.

## 0. Work out where you are (do not ask)

- **Mac or Windows.** On a Mac (or Linux), run the bash blocks; they also work as they are in zsh, the Mac's default shell. On Windows, always run the Windows PowerShell blocks, in Windows PowerShell (`powershell.exe`; version 5.1 is fine), never the bash ones. If your shell tool on Windows is Git Bash, save each PowerShell block to a temporary `.ps1` file and run `powershell -NoProfile -ExecutionPolicy Bypass -File <that file>`. Never use WSL: it has a different home folder.
- **Claude Code or Codex.** Work it out from this session: your own tools and the app you can see you are running in. Do not ask. Step 3 installs for both apps either way, in one go: the skills go in `~/.agents/skills` (Codex's skill folder) and are linked into `~/.claude/skills` (Claude Code's; the `skills` folder inside `CLAUDE_CONFIG_DIR` when that is set), on Windows `$HOME\.agents\skills` and `$HOME\.claude\skills`. Which app you are only changes step 4: whose skill list you check, and which app restarts.
- **The kit folder** means the folder that holds this `SETUP-PROMPT.md`, wherever it is. If you were sent here from `docs/start/setup.md`, the kit folder is the one that holds `README.md` and this file, not `docs/start`. It may be Loup's verified copy under `~/.loup/kits/`: never write, change, delete or run anything there, because Loup re-checks every byte of it. You only copy out of it.

## 1. Give the kit its home: `~/.loup/installed/mp-skills-kit`

The kit's home is `~/.loup/installed/mp-skills-kit` (Windows: `$HOME\.loup\installed\mp-skills-kit`), beside Loup's verified copies in `~/.loup/kits`, never inside them. It holds the kit's own files and `installed-skills.txt`, the list of skills this setup installed, which a later run reads to tell its own installs from anyone else's. A later refresh never copies over that list. Apart from this folder, and the `mp-skills-kit.previous-<date and time>` folder beside it that step 3 makes only if something is in the way, write nothing under `~/.loup`: the rest belongs to Loup.

- A folder is a copy of this kit if the first line of its `README.md` is exactly `# mp-skills-kit` and it has a file `docs/start/setup.md`.
- **Never write through a link.** The block stops before writing anything if the home, a folder above it inside the home folder, or anything inside it is a link (a symbolic link or a Windows junction). It also stops if the kit folder is reached through a link or holds one: the kit is never copied from or through a link.
- If the home exists, is not empty and is not a copy of this kit, the block stops: tell the attendee what you found there, and never overlay, move or delete it. (A home that holds only files identical to the kit folder's is a copy that was interrupted part way, and is refreshed.)
- **Earlier copies of this kit.** Before this file existed, the kit's School page had the agent clone it into whatever folder the session happened to be in. The block looks for an earlier copy in `~/mp-skills-kit`, `~/skool-kits/mp-skills-kit`, `~/Documents/mp-skills-kit`, `~/Desktop/mp-skills-kit` and `~/Projects/mp-skills-kit` (Windows: the same folders under `$HOME\`). An earlier copy is never deleted:
  - it is moved to the home, whole, so anything the attendee added inside it comes too (its `.git` history included), only when all of these hold: the home does not exist yet; the earlier copy is a real folder, not a link, with no link above it inside the home folder and none inside it; it is a copy of this kit; and setup is not running from it (or from another earlier copy);
  - if setup is running from an earlier copy, it stays where it is and the kit is copied from it into the home, exactly like a copy from a Loup download. If the home already exists in that case, the block stops before writing anything (see below);
  - in every other case (the home already exists, the earlier copy is or holds a link, or it is not this kit) it is left exactly as it is.
  Nothing else on the computer names an earlier copy (the earlier setup installed the skills from Matt's project, not from the copy), so there is nothing else to re-point.
- Then the kit folder is copied over the home, creating it if it is missing. When the home is already there, this refreshes it: the kit's own files are brought up to date and anything else in the home is kept. `.git`, `.loup-receipt.json`, `.loup-archive.tar.gz` and `installed-skills.txt` are left out of the copy, a `.git` folder already in the home is never touched, and the copied files are made writable so a later run can refresh them. If the kit folder already is the home, there is nothing to copy.

Put the kit folder's full path in place of `<kit folder>` in the block.

Mac or Linux:

```bash
KIT="<kit folder>"
NEW="$HOME/.loup/installed/mp-skills-kit"
# linked PATH: PATH, a folder above it inside the home folder, or anything inside it is a link
linked() {
  p="$1"
  while [ "$p" != "$HOME" ] && [ "$p" != "/" ] && [ -n "$p" ]; do
    [ -L "$p" ] && return 0
    p="$(dirname "$p")"
  done
  [ -d "$1" ] && [ -n "$(find "$1" -type l 2>/dev/null | head -n 1)" ]
}
# a copy of this kit: README.md starts with "# mp-skills-kit" and docs/start/setup.md exists
is_this_kit() {
  [ -f "$1/docs/start/setup.md" ] && [ "$(head -n 1 "$1/README.md" 2>/dev/null | tr -d '\r')" = "# mp-skills-kit" ]
}
# same DIR: every file and folder in DIR is also in the kit folder, and every file is identical
same() {
  ( set -o pipefail
    ( cd "$1" && find . -mindepth 1 -print0 ) | while IFS= read -r -d '' p; do
      if [ -d "$1/$p" ]; then [ -d "$KIT/$p" ] || exit 1
      else [ -f "$1/$p" ] && [ -f "$KIT/$p" ] && cmp -s "$1/$p" "$KIT/$p" || exit 1; fi
    done )
}
[ -d "$KIT" ] || { echo "STOP: the kit folder is not there: $KIT" >&2; exit 1; }
if linked "$KIT"; then echo "STOP: the kit folder $KIT is reached through a link, or holds one. Run setup from the kit folder Loup delivered." >&2; exit 1; fi
if linked "$NEW"; then echo "STOP: $NEW, or a folder above it or inside it, is a link. Not writing through it." >&2; exit 1; fi
if [ -e "$NEW" ]; then
  [ -d "$NEW" ] || { echo "STOP: $NEW is not a folder; leaving it alone" >&2; exit 1; }
  if ! is_this_kit "$NEW" && [ -n "$(find "$NEW" -mindepth 1 -maxdepth 1 2>/dev/null | head -n 1)" ] && ! same "$NEW"; then
    echo "STOP: $NEW is not this kit; leaving it alone" >&2; exit 1
  fi
fi
FROM=""
for OLD in "$HOME/mp-skills-kit" "$HOME/skool-kits/mp-skills-kit" "$HOME/Documents/mp-skills-kit" "$HOME/Desktop/mp-skills-kit" "$HOME/Projects/mp-skills-kit"; do
  if [ "$KIT" -ef "$OLD" ]; then FROM="$OLD"; fi
done
if [ -n "$FROM" ] && { [ -e "$NEW" ] || [ -L "$NEW" ]; }; then echo "STOP: setup is running from $FROM, but the kit now lives at $NEW. Run setup from the kit folder Loup delivered." >&2; exit 1; fi
for OLD in "$HOME/mp-skills-kit" "$HOME/skool-kits/mp-skills-kit" "$HOME/Documents/mp-skills-kit" "$HOME/Desktop/mp-skills-kit" "$HOME/Projects/mp-skills-kit"; do
  if [ -e "$OLD" ] || [ -L "$OLD" ]; then
    if [ "$KIT" -ef "$OLD" ]; then
      echo "KEPT: setup is running from $OLD, so it stays where it is and the kit is copied from it."
    elif [ -e "$NEW" ]; then
      echo "KEPT: $OLD is still there beside the new home $NEW. Nothing in it was changed."
    elif [ -n "$FROM" ]; then
      echo "KEPT: $OLD is still there. Setup is running from $FROM, so nothing else was moved."
    elif linked "$OLD"; then
      echo "KEPT: $OLD is, or holds, a link to another folder, so it was not moved."
    elif ! is_this_kit "$OLD"; then
      echo "KEPT: $OLD is not this kit, so it was left alone."
    else
      mkdir -p "$HOME/.loup/installed" || exit 1
      mv "$OLD" "$NEW" || { echo "STOP: could not move $OLD to $NEW" >&2; exit 1; }
      echo "MOVED: $OLD to $NEW"
    fi
  fi
done
if [ "$KIT" -ef "$NEW" ]; then
  echo "HOME: the kit folder is the home already, so there is nothing to copy."
else
  if linked "$NEW"; then echo "STOP: $NEW, or a folder above it or inside it, is a link. Not writing through it." >&2; exit 1; fi
  ARCHIVE="$(mktemp "${TMPDIR:-/tmp}/mp-skills-kit.XXXXXX")" || { echo "STOP: the copy failed: no temporary file" >&2; exit 1; }
  { mkdir -p "$NEW" &&
    tar -C "$KIT" --exclude=.git --exclude=.loup-receipt.json --exclude=.loup-archive.tar.gz --exclude=installed-skills.txt -cf "$ARCHIVE" . &&
    tar -C "$NEW" -xf "$ARCHIVE" &&
    tar -tf "$ARCHIVE" | while IFS= read -r p; do [ -L "$NEW/$p" ] || chmod u+w "$NEW/$p" || exit 1; done &&
    rm -f "$ARCHIVE"; } ||
    { echo "STOP: the copy failed" >&2; rm -f "$ARCHIVE"; exit 1; }
  echo "HOME: the kit is copied to $NEW"
fi
```

Windows PowerShell (no backslash at the end of the kit folder path; robocopy reports success with exit codes 0 to 3, and 4 to 7 as long as no file and folder clash; `/IS /IT /IM` make it refresh every kit file even when its date and size look unchanged, and `/A-:R` leaves the copies writable):

```powershell
$Kit = "<kit folder>"
$New = "$HOME\.loup\installed\mp-skills-kit"
$Olds = @("$HOME\mp-skills-kit", "$HOME\skool-kits\mp-skills-kit", "$HOME\Documents\mp-skills-kit", "$HOME\Desktop\mp-skills-kit", "$HOME\Projects\mp-skills-kit")
function Test-Linked($Path) {
  $p = $Path
  while ($p -and ($p.TrimEnd('\') -ne $HOME.TrimEnd('\'))) {
    $item = Get-Item -LiteralPath $p -Force -ErrorAction SilentlyContinue
    if ($item -and $item.LinkType) { return $true }
    $p = Split-Path -Parent $p
  }
  if (Test-Path -LiteralPath $Path -PathType Container) {
    if (@(Get-ChildItem -LiteralPath $Path -Recurse -Force -Attributes ReparsePoint -ErrorAction SilentlyContinue).Count -gt 0) { return $true }
  }
  return $false
}
function Test-LinkedPath($Path) {
  $p = $Path
  while ($p -and ($p.TrimEnd('\') -ne $HOME.TrimEnd('\'))) {
    $item = Get-Item -LiteralPath $p -Force -ErrorAction SilentlyContinue
    if ($item -and $item.LinkType) { return $true }
    $p = Split-Path -Parent $p
  }
  return $false
}
function Test-SameFolder($A, $B) {
  if (-not (Test-Path -LiteralPath $A) -or -not (Test-Path -LiteralPath $B)) { return $false }
  return ((Resolve-Path -LiteralPath $A).ProviderPath.TrimEnd('\') -eq (Resolve-Path -LiteralPath $B).ProviderPath.TrimEnd('\'))
}
# a copy of this kit: README.md starts with "# mp-skills-kit" and docs\start\setup.md exists
function Test-ThisKit($Path) {
  if (-not (Test-Path -LiteralPath "$Path\docs\start\setup.md" -PathType Leaf)) { return $false }
  if (-not (Test-Path -LiteralPath "$Path\README.md" -PathType Leaf)) { return $false }
  return (@(Get-Content -LiteralPath "$Path\README.md" -TotalCount 1)[0] -eq '# mp-skills-kit')
}
# every file in $Dir is also in the kit folder with the same content (a copy interrupted part way)
function Test-Same($Dir) {
  $Base = (Resolve-Path -LiteralPath $Dir -ErrorAction Stop).ProviderPath.TrimEnd('\')
  foreach ($Item in @(Get-ChildItem -LiteralPath $Dir -Recurse -Force -File -ErrorAction Stop)) {
    $Src = Join-Path $Kit $Item.FullName.Substring($Base.Length + 1)
    if (-not (Test-Path -LiteralPath $Src -PathType Leaf)) { return $false }
    if ((Get-FileHash -LiteralPath $Item.FullName).Hash -ne (Get-FileHash -LiteralPath $Src).Hash) { return $false }
  }
  return $true
}
if (-not (Test-Path -LiteralPath $Kit -PathType Container)) { Write-Host "STOP: the kit folder is not there: $Kit"; exit 1 }
if (Test-LinkedPath $Kit) { Write-Host "STOP: the kit folder $Kit is reached through a link. Run setup from the kit folder Loup delivered."; exit 1 }
if (Test-Linked $Kit) { Write-Host "STOP: the kit folder $Kit holds a link. Run setup from the kit folder Loup delivered."; exit 1 }
if (Test-Linked $New) { Write-Host "STOP: $New, or a folder above it or inside it, is a link. Not writing through it."; exit 1 }
if (Test-Path -LiteralPath $New) {
  if (-not (Test-Path -LiteralPath $New -PathType Container)) { Write-Host "STOP: $New is not a folder; leaving it alone"; exit 1 }
  if (-not (Test-ThisKit $New) -and (@(Get-ChildItem -LiteralPath $New -Force).Count -gt 0)) {
    $Partial = $false
    try { $Partial = Test-Same $New } catch { $Partial = $false }
    if (-not $Partial) { Write-Host "STOP: $New is not this kit; leaving it alone"; exit 1 }
  }
}
$From = $null
foreach ($Old in $Olds) { if (Test-SameFolder $Kit $Old) { $From = $Old } }
if ($From -and (Test-Path -LiteralPath $New)) { Write-Host "STOP: setup is running from $From, but the kit now lives at $New. Run setup from the kit folder Loup delivered."; exit 1 }
foreach ($Old in $Olds) {
  if (Test-Path -LiteralPath $Old) {
    if (Test-SameFolder $Kit $Old) {
      Write-Host "KEPT: setup is running from $Old, so it stays where it is and the kit is copied from it."
    } elseif (Test-Path -LiteralPath $New) {
      Write-Host "KEPT: $Old is still there beside the new home $New. Nothing in it was changed."
    } elseif ($From) {
      Write-Host "KEPT: $Old is still there. Setup is running from $From, so nothing else was moved."
    } elseif (Test-Linked $Old) {
      Write-Host "KEPT: $Old is, or holds, a link to another folder, so it was not moved."
    } elseif (-not (Test-ThisKit $Old)) {
      Write-Host "KEPT: $Old is not this kit, so it was left alone."
    } else {
      New-Item -ItemType Directory -Force "$HOME\.loup\installed" | Out-Null
      try { Move-Item -LiteralPath $Old -Destination $New -ErrorAction Stop }
      catch { Write-Host "STOP: could not move $Old to ${New}: $($_.Exception.Message)"; exit 1 }
      Write-Host "MOVED: $Old to $New"
    }
  }
}
if (Test-SameFolder $Kit $New) {
  Write-Host "HOME: the kit folder is the home already, so there is nothing to copy."
} else {
  if (Test-Linked $New) { Write-Host "STOP: $New, or a folder above it or inside it, is a link. Not writing through it."; exit 1 }
  if (-not (Get-Command robocopy -ErrorAction SilentlyContinue)) { Write-Host "STOP: the copy failed: robocopy is not available"; exit 1 }
  New-Item -ItemType Directory -Force "$HOME\.loup\installed" | Out-Null
  robocopy $Kit $New /E /IS /IT /IM /A-:R /R:2 /W:2 /XD .git /XF .git .loup-receipt.json .loup-archive.tar.gz installed-skills.txt /NFL /NDL /NJH /NJS /NP
  if ($LASTEXITCODE -ge 8 -or ($LASTEXITCODE -band 4)) { Write-Host "STOP: the copy failed: robocopy exit code $LASTEXITCODE (8 or more is an error, 4 means a file and a folder clash)"; exit 1 }
  $global:LASTEXITCODE = 0
  Write-Host "HOME: the kit is copied to $New"
}
```

Then read what the block printed:

- A `STOP:` line means the block stopped there. Show the attendee what it says in plain English and fix the cause before going on; never skip it. For a folder that is not this kit, or a link, change nothing and ask the attendee what that folder is. A failed move or copy matters too: fix it, because a half-made home would otherwise look like an earlier copy next time.
- `STOP: setup is running from ... but the kit now lives at ...` means this kit is already in its home and you were started from an older copy of it. Nothing was written. Tell the attendee in one plain line, then carry on with the copy in its home: open `~/.loup/installed/mp-skills-kit/SETUP-PROMPT.md` and follow it from step 1, with `~/.loup/installed/mp-skills-kit` as the kit folder. The older copy is left exactly as it is.
- `MOVED:` means an earlier copy of the kit moved into the Loup folder, with anything the attendee had added to it. Tell them in one line.
- `KEPT:` about an earlier copy of the kit means it is still where it was. Tell the attendee in one plain line where it is, that the kit now lives in `~/.loup/installed/mp-skills-kit` and nothing uses the older folder any more, and that they can delete it once they have checked nothing of theirs is in it. A `KEPT:` line about a folder that is not this kit, or is a link, needs no mention unless the attendee asks.

Confirm `~/.loup/installed/mp-skills-kit/SETUP-PROMPT.md` exists before moving on.

## 2. Node.js 22.20 or newer

The `skills` installer needs Node.js 22.20 or newer. Run `node --version`. If it prints `v22.20` or higher (`v24`, `v26` and so on are fine), carry on. If `node` is missing or older, install the current Node.js LTS. Tell the attendee first that a download is about to run and that on slow wifi it can look frozen while it is still working, and give the command a generous timeout so a dead download fails loudly.

- **Mac:** if `brew --version` works, run `brew install node` (or `brew upgrade node` when Homebrew already has an older one). If `command -v node` points into `~/.nvm`, run `nvm install --lts` instead. If this Mac has neither, download the current LTS installer (`node-v<version>.pkg`) from https://nodejs.org/dist/ (the newest entry in https://nodejs.org/dist/index.json whose `lts` is not `false`) and open it: the attendee clicks through it and types their Mac password into the Mac's own box. That is a pause: wait until they say it has finished.
- **Linux:** install the current LTS from nodejs.org or the distribution's package manager.
- **Windows:**

  ```powershell
  winget install --id OpenJS.NodeJS.LTS -e --accept-package-agreements --accept-source-agreements
  $env:Path = [Environment]::GetEnvironmentVariable("Path", "Machine") + ";" + [Environment]::GetEnvironmentVariable("Path", "User")
  node --version
  ```

  The second line reloads the command path so this window finds the new install. If there is no `winget`, download the LTS `.msi` installer from nodejs.org and have the attendee open it and click through.

Then run `node --version` again to confirm the new version is the one found. If the old one still answers, a fresh shell picks up the new install: on a Mac open a new one, and if that is not enough, the attendee restarts the app you are running in.

## 3. Install the 27 skills

One block per computer does the whole install and prints what it did:

1. **Never writes through a link.** It stops before changing anything if `~/.agents/skills`, `~/.claude/skills`, `~/.loup/installed` or a folder above any of them inside the home folder is a link. (The skill folders themselves are full of links by design: that is how Claude Code shares each skill with Codex.)
2. **Leaves other setups' skills alone.** A skill another setup installed (it is a real skill folder in `~/.agents/skills` that this kit did not install, with `~/.claude/skills/<name>` linked to it, or one the `skills` installer pinned to a version of Matt's project, as the LOUP workshop assistant kit does) is never replaced, moved or re-pointed, and is left out of the install. If grill me, teach and handoff are all installed like that, the block changes nothing at all and says so: the attendee already has the skills.
3. **Clears the way for the rest.** The `skills` installer replaces whatever sits at a skill's name, so anything else at one of those names (a copy of a skill, the attendee's own skill that happens to share the name, a link to some other folder, or a `<name>.bak` folder an earlier version of this kit left behind) is moved, never deleted, into `~/.loup/installed/mp-skills-kit.previous-<date and time>/`, outside every skill folder so no skill is loaded twice. Moving a link moves only the link, never what it points to. A skill this kit installed before (it is in `installed-skills.txt`), or that an earlier version of this kit installed from Matt's project, is refreshed in place. Nothing else in either skill folder is touched, and no project's own `.claude/skills` folder is ever touched.
4. **Installs.** It runs the pinned `skills` installer once for both apps: `-g` installs for this user rather than for one project, and `-a claude-code -a codex` is what makes the installer keep one shared copy of each skill in `~/.agents/skills` and link it into `~/.claude/skills`. Never add `--copy`, and never install from anywhere but the pinned archive. The first run also downloads the installer itself, a few megabytes.
5. **Proves it.** Every skill it installed must have a `SKILL.md` with its own name in `~/.agents/skills/<name>`, and `~/.claude/skills/<name>` must be a link that opens that same folder. It then records them in `installed-skills.txt`.

Mac or Linux:

```bash
set -- ask-matt code-review codebase-design diagnosing-bugs domain-modeling grill-me grill-with-docs grilling handoff implement implement-spec improve-codebase-architecture pr prototype research retro setup-matt-pocock-skills tdd teach to-questionnaire to-spec to-tickets triage wait-what wayfinder wizard writing-for-agents
SOURCE="https://github.com/mattpocock/skills/archive/49dd158d1076134a641b33efb035946536778336.tar.gz"
NEW="$HOME/.loup/installed/mp-skills-kit"
STORE="$HOME/.agents/skills"
CLAUDE="${CLAUDE_CONFIG_DIR:-$HOME/.claude}/skills"
ASIDE="$HOME/.loup/installed/mp-skills-kit.previous-$(date +%Y%m%d-%H%M%S)"
# linked PATH: PATH, a folder above it inside the home folder, or anything inside it is a link
linked() {
  p="$1"
  while [ "$p" != "$HOME" ] && [ "$p" != "/" ] && [ -n "$p" ]; do
    [ -L "$p" ] && return 0
    p="$(dirname "$p")"
  done
  [ -d "$1" ] && [ -n "$(find "$1" -type l 2>/dev/null | head -n 1)" ]
}
# linked_path PATH: PATH or a folder above it inside the home folder is a link
linked_path() {
  p="$1"
  while [ "$p" != "$HOME" ] && [ "$p" != "/" ] && [ -n "$p" ]; do
    [ -L "$p" ] && return 0
    p="$(dirname "$p")"
  done
  return 1
}
[ -f "$NEW/SETUP-PROMPT.md" ] || { echo "STOP: $NEW is not set up yet: do step 1 first" >&2; exit 1; }
if linked "$NEW"; then echo "STOP: $NEW, or a folder above it or inside it, is a link. Not writing through it." >&2; exit 1; fi
for root in "$STORE" "$CLAUDE" "$ASIDE"; do
  if linked_path "$root"; then echo "STOP: $root, or a folder above it, is a link. Not writing through it." >&2; exit 1; fi
done
# skills the skills installer recorded as coming from Matt's project: "<name> <pinned version>", or "<name> -" when not pinned
LOCK="$(node -e 'try { const l = require(process.argv[1]); for (const [n, e] of Object.entries(l.skills || {})) if (e && e.source === "mattpocock/skills") console.log(n + " " + (e.ref || "-")) } catch (e) {}' "$HOME/.agents/.skill-lock.json" | tr -d '\r')"
MINE="$(cat "$NEW/installed-skills.txt" 2>/dev/null | tr -d '\r')"
named() { awk -v want="name: $2" '{sub(/\r$/,"")} NR==1{if($0!="---")exit 1;next} /^---$/{c=1;exit} $0==want{f=1} END{exit !(f&&c)}' "$1/SKILL.md" 2>/dev/null; }
mine() { printf '%s\n' "$MINE" | grep -qxF -- "$1" || printf '%s\n' "$LOCK" | grep -qxF -- "$1 -"; }
pinned() { printf '%s\n' "$LOCK" | grep -q "^$1 [0-9a-f]"; }
# held NAME: another setup installed this skill, so it is left exactly as it is
held() {
  [ -d "$STORE/$1" ] && [ ! -L "$STORE/$1" ] && named "$STORE/$1" "$1" || return 1
  pinned "$1" && return 0
  [ -L "$CLAUDE/$1" ] && [ "$CLAUDE/$1" -ef "$STORE/$1" ] && ! mine "$1"
}
aside() {
  { mkdir -p "$ASIDE/$2" && mv "$1" "$ASIDE/$2/"; } || { echo "STOP: could not move $1 aside" >&2; exit 1; }
  echo "MOVED ASIDE: $1 to $ASIDE/$2/"
}
if held grill-me && held teach && held handoff; then
  echo "ALREADY: Matt Pocock's skills, grill me, teach and handoff among them, are already installed by another setup (the LOUP workshop assistant kit installs them this way). Nothing was changed."
  for n in grill-me teach handoff; do [ -f "$CLAUDE/$n/SKILL.md" ] && echo "FOUND: $CLAUDE/$n/SKILL.md" || echo "FOUND: $STORE/$n/SKILL.md (Codex only)"; done
  exit 0
fi
for n in "$@"; do
  shift
  a="$STORE/$n"; c="$CLAUDE/$n"
  if held "$n"; then echo "LEFT AS IT IS: $n is installed by another setup"; continue; fi
  if [ -L "$a" ] || { [ -e "$a" ] && ! { [ -d "$a" ] && named "$a" "$n" && mine "$n"; }; }; then aside "$a" agents-skills; fi
  if [ -L "$c" ]; then
    if [ -e "$c" ] && ! [ "$c" -ef "$a" ]; then aside "$c" claude-skills; fi
  elif [ -e "$c" ]; then aside "$c" claude-skills; fi
  if [ -e "$c.bak" ] || [ -L "$c.bak" ]; then aside "$c.bak" claude-skills; fi
  set -- "$@" "$n"
done
[ "$#" -gt 0 ] || { echo "ALREADY: every one of these skills is installed by another setup. Nothing was changed."; exit 0; }
echo "CLEAR: $# names are free for the install"
npx -y skills@1.7.2 add "$SOURCE" -g -a claude-code -a codex -y -s "$@" || { echo "STOP: the skills installer failed; its error is above" >&2; exit 1; }
printf '%s\n' "$@" > "$NEW/installed-skills.txt" || { echo "STOP: could not write $NEW/installed-skills.txt" >&2; exit 1; }
bad=""
for n in "$@"; do
  if named "$STORE/$n" "$n" && [ -L "$CLAUDE/$n" ] && [ "$CLAUDE/$n" -ef "$STORE/$n" ]; then :; else bad="$bad $n"; fi
done
[ -z "$bad" ] || { echo "STOP: these skills did not install correctly:$bad" >&2; exit 1; }
echo "VERIFIED: $# skills are in $STORE (Codex) and linked into $CLAUDE (Claude Code)"
```

Windows PowerShell (it calls `npx.cmd`, not `npx`, so a locked-down script setting on the computer cannot block it):

```powershell
$Skills = @('ask-matt', 'code-review', 'codebase-design', 'diagnosing-bugs', 'domain-modeling', 'grill-me', 'grill-with-docs', 'grilling', 'handoff', 'implement', 'implement-spec', 'improve-codebase-architecture', 'pr', 'prototype', 'research', 'retro', 'setup-matt-pocock-skills', 'tdd', 'teach', 'to-questionnaire', 'to-spec', 'to-tickets', 'triage', 'wait-what', 'wayfinder', 'wizard', 'writing-for-agents')
$Source = 'https://github.com/mattpocock/skills/archive/49dd158d1076134a641b33efb035946536778336.tar.gz'
$New = "$HOME\.loup\installed\mp-skills-kit"
$Store = "$HOME\.agents\skills"
if ($env:CLAUDE_CONFIG_DIR) { $Claude = "$($env:CLAUDE_CONFIG_DIR.Trim().TrimEnd('\'))\skills" } else { $Claude = "$HOME\.claude\skills" }
$Aside = "$HOME\.loup\installed\mp-skills-kit.previous-" + (Get-Date -Format 'yyyyMMdd-HHmmss')
$env:Path = [Environment]::GetEnvironmentVariable("Path", "Machine") + ";" + [Environment]::GetEnvironmentVariable("Path", "User")
function Test-Linked($Path) {
  $p = $Path
  while ($p -and ($p.TrimEnd('\') -ne $HOME.TrimEnd('\'))) {
    $item = Get-Item -LiteralPath $p -Force -ErrorAction SilentlyContinue
    if ($item -and $item.LinkType) { return $true }
    $p = Split-Path -Parent $p
  }
  if (Test-Path -LiteralPath $Path -PathType Container) {
    if (@(Get-ChildItem -LiteralPath $Path -Recurse -Force -Attributes ReparsePoint -ErrorAction SilentlyContinue).Count -gt 0) { return $true }
  }
  return $false
}
function Test-LinkedPath($Path) {
  $p = $Path
  while ($p -and ($p.TrimEnd('\') -ne $HOME.TrimEnd('\'))) {
    $item = Get-Item -LiteralPath $p -Force -ErrorAction SilentlyContinue
    if ($item -and $item.LinkType) { return $true }
    $p = Split-Path -Parent $p
  }
  return $false
}
if (-not (Test-Path -LiteralPath "$New\SETUP-PROMPT.md" -PathType Leaf)) { Write-Host "STOP: $New is not set up yet: do step 1 first"; exit 1 }
if (Test-Linked $New) { Write-Host "STOP: $New, or a folder above it or inside it, is a link. Not writing through it."; exit 1 }
foreach ($Root in @($Store, $Claude, $Aside)) {
  if (Test-LinkedPath $Root) { Write-Host "STOP: $Root, or a folder above it, is a link. Not writing through it."; exit 1 }
}
# skills the skills installer recorded as coming from Matt's project, pinned to a version or not
$Pinned = @(); $Unpinned = @()
if (Test-Path -LiteralPath "$HOME\.agents\.skill-lock.json" -PathType Leaf) {
  try {
    $Lock = Get-Content -LiteralPath "$HOME\.agents\.skill-lock.json" -Raw | ConvertFrom-Json
    foreach ($p in @($Lock.skills.PSObject.Properties)) {
      if ($p.Value.source -eq 'mattpocock/skills') { if ($p.Value.ref) { $Pinned += $p.Name } else { $Unpinned += $p.Name } }
    }
  } catch { }
}
$Mine = @()
if (Test-Path -LiteralPath "$New\installed-skills.txt" -PathType Leaf) { $Mine = @(Get-Content -LiteralPath "$New\installed-skills.txt") }
function Get-Entry($Path) { return Get-Item -LiteralPath $Path -Force -ErrorAction SilentlyContinue }
function Get-Full($Path) { return [System.IO.Path]::GetFullPath($Path).TrimEnd('\') }
# the folder a link points at, as a full path, or $null
function Get-LinkTarget($Item) {
  $t = @($Item.Target)[0]
  if (-not $t) { return $null }
  if (-not [System.IO.Path]::IsPathRooted($t)) { $t = Join-Path (Split-Path -Parent $Item.FullName) $t }
  return (Get-Full $t)
}
function Test-Named($Dir, $Name) {
  if (-not (Test-Path -LiteralPath "$Dir\SKILL.md" -PathType Leaf)) { return $false }
  $Lines = @(Get-Content -LiteralPath "$Dir\SKILL.md")
  if ($Lines.Count -lt 2 -or $Lines[0] -ne '---') { return $false }
  $Found = $false
  for ($i = 1; $i -lt $Lines.Count; $i++) {
    if ($Lines[$i] -eq '---') { return $Found }
    if ($Lines[$i] -eq "name: $Name") { $Found = $true }
  }
  return $false
}
# another setup installed this skill, so it is left exactly as it is
# this setup installed it before, or an earlier version of this kit did (from Matt's project, not pinned)
function Test-Mine($n) { return (($Mine -contains $n) -or ($Unpinned -contains $n)) }
function Test-Held($n) {
  $ai = Get-Entry "$Store\$n"
  if (-not $ai -or $ai.LinkType -or -not $ai.PSIsContainer -or -not (Test-Named "$Store\$n" $n)) { return $false }
  if ($Pinned -contains $n) { return $true }
  $ci = Get-Entry "$Claude\$n"
  return [bool]($ci -and $ci.LinkType -and ((Get-LinkTarget $ci) -eq (Get-Full "$Store\$n")) -and -not (Test-Mine $n))
}
function Move-Aside($Path, $Group) {
  try {
    New-Item -ItemType Directory -Force "$Aside\$Group" -ErrorAction Stop | Out-Null
    Move-Item -LiteralPath $Path -Destination "$Aside\$Group\" -ErrorAction Stop
  } catch { Write-Host "STOP: could not move $Path aside: $($_.Exception.Message)"; exit 1 }
  Write-Host "MOVED ASIDE: $Path to $Aside\$Group\"
}
if ((Test-Held 'grill-me') -and (Test-Held 'teach') -and (Test-Held 'handoff')) {
  Write-Host "ALREADY: Matt Pocock's skills, grill me, teach and handoff among them, are already installed by another setup (the LOUP workshop assistant kit installs them this way). Nothing was changed."
  foreach ($n in @('grill-me', 'teach', 'handoff')) {
    if (Test-Path -LiteralPath "$Claude\$n\SKILL.md" -PathType Leaf) { Write-Host "FOUND: $Claude\$n\SKILL.md" } else { Write-Host "FOUND: $Store\$n\SKILL.md (Codex only)" }
  }
  exit 0
}
$Install = @()
foreach ($n in $Skills) {
  $a = "$Store\$n"; $c = "$Claude\$n"
  if (Test-Held $n) { Write-Host "LEFT AS IT IS: $n is installed by another setup"; continue }
  $ai = Get-Entry $a
  if ($ai -and ($ai.LinkType -or (-not $ai.PSIsContainer) -or -not (Test-Named $a $n) -or -not (Test-Mine $n))) { Move-Aside $a 'agents-skills' }
  $ci = Get-Entry $c
  if ($ci -and $ci.LinkType) {
    $t = Get-LinkTarget $ci
    if ($t -and (Test-Path -LiteralPath $t) -and ($t -ne (Get-Full $a))) { Move-Aside $c 'claude-skills' }
  } elseif ($ci) { Move-Aside $c 'claude-skills' }
  if (Get-Entry "$c.bak") { Move-Aside "$c.bak" 'claude-skills' }
  $Install += $n
}
if ($Install.Count -eq 0) { Write-Host "ALREADY: every one of these skills is installed by another setup. Nothing was changed."; exit 0 }
Write-Host "CLEAR: $($Install.Count) names are free for the install"
$CliArgs = @('-y', 'skills@1.7.2', 'add', $Source, '-g', '-a', 'claude-code', '-a', 'codex', '-y', '-s') + $Install
& npx.cmd @CliArgs
if ($LASTEXITCODE -ne 0) { Write-Host "STOP: the skills installer failed; its error is above"; exit 1 }
try { Set-Content -LiteralPath "$New\installed-skills.txt" -Value $Install -Encoding Ascii -ErrorAction Stop } catch { Write-Host "STOP: could not write $New\installed-skills.txt"; exit 1 }
$Bad = @()
foreach ($n in $Install) {
  $ci = Get-Entry "$Claude\$n"
  $Linked = $ci -and $ci.LinkType -and ((Get-LinkTarget $ci) -eq (Get-Full "$Store\$n")) -and (Test-Path -LiteralPath "$Claude\$n\SKILL.md" -PathType Leaf)
  if (-not ((Test-Named "$Store\$n" $n) -and $Linked)) { $Bad += $n }
}
if ($Bad.Count -gt 0) { Write-Host "STOP: these skills did not install correctly: $($Bad -join ', ')"; exit 1 }
Write-Host "VERIFIED: $($Install.Count) skills are in $Store (Codex) and linked into $Claude (Claude Code)"
```

Then read what the block printed:

- `VERIFIED: 27 skills ...` is the proof the install worked. A lower number with `LEFT AS IT IS:` lines is also a finished install: those names were already installed by another setup and were left alone.
- `ALREADY:` means the attendee already has Matt's skills from another setup, most likely the LOUP workshop assistant kit. Nothing was installed or changed, and that is a finished install too: the `FOUND:` lines are the proof. Do not install them again any other way.
- A `STOP:` line means it stopped there. Show the attendee the real error in plain English and fix it, then run the block again; it is safe to run again. A `STOP:` about a link means one of the attendee's folders points somewhere else: change nothing and ask them about it. If the installer could not reach npm or GitHub, or timed out, that is the wifi, not the kit: have the attendee check they are online and run it again. If it says the archive could not be found, the pinned version of Matt's skills is no longer available: tell the attendee the host needs to know, and stop. Never switch to another version, `skills@latest` or a different install method on your own.
- Each `MOVED ASIDE:` line is something of the attendee's that was in the way. Keep the paths for step 4.

## 4. Check the skills are showing, then tell the attendee

Check that `grilling` (the skill behind grill me), `diagnosing-bugs` and `tdd` are in your own list of available skills. grill me, teach and handoff are commands the attendee types, so they may not appear in that list even when they are installed; that is expected, and step 3's `VERIFIED` or `FOUND` lines already proved they are there. New sessions pick the skills up by themselves. If the ones you checked are not listed in this session, tell the attendee to start a new session (Claude Code: a new chat; Codex: a new thread), and if they still do not show, to restart the app once (Claude Code, or the Codex app). That is the only restart, and nothing else needs doing.

If `~/.claude/plugins/installed_plugins.json` mentions `mattpocock-skills`, this Claude Code also has Matt's own plugin, so each of his skills now shows twice. That does no harm. Tell the attendee in one line, and that they can turn the plugin off in Claude Code's plugin settings if they would rather see each skill once.

Then tell the attendee, in plain English and in a few short lines:

- Matt Pocock's mainline skills are installed for Claude Code and Codex, one shared copy, his own work, free and MIT licensed (https://github.com/mattpocock/skills). If step 3 said `ALREADY:`, say instead that they already had them from their workshop setup, so nothing needed installing.
- How to use the three everyday ones, with the exact words. In Claude Code type the slash command at the start of a message; in Codex type `$` and the name instead (`$grill-me`):
  - **`/grill-me`** and then the plan or idea: Claude interviews them, one hard question at a time, until the plan holds up. Use it before committing to anything.
  - **`/teach`** and then the topic: Claude teaches it properly and checks they understood. It keeps its lesson notes in the folder the session is in.
  - **`/handoff`** when a chat has run long: it writes everything that matters into a document, then they open a fresh session and point it at that document.
- The engineering skills (`/to-spec`, `/tdd`, `/code-review` and the rest) ask for a one-time `/setup-matt-pocock-skills` in each code project before their first use. grill me, teach and handoff need nothing.
- If step 1 or step 3 moved or kept anything, say where it is now in one line each: the kit's home `~/.loup/installed/mp-skills-kit`, any earlier copy that was kept, and anything moved aside in `~/.loup/installed/mp-skills-kit.previous-<date and time>/`, which they can look through and delete once they have checked nothing of theirs is needed.
- To update later: run the `SETUP-PROMPT.md` of a newer release of this kit. Running this one again is always safe.

## Rules

- This folder is the kit: never clone, pull or download it or any Selr repository. The only things fetched are the two pinned public projects named at the top.
- Never delete anything of the attendee's. Things in the way are moved aside; links are moved, never followed or written through.
- Never replace, move or re-point a skill another setup installed.
- Never ask the attendee to paste a password, token or code into the chat.
- An error is shown and fixed, never reported as success.
