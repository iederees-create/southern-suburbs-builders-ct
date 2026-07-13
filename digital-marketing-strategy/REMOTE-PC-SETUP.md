# Remote PC Setup — Second Computer

**Repository:** `https://github.com/iederees-create/southern-suburbs-builders-ct.git`  
**Branch:** `work/digital-marketing-strategy`

---

## Fresh clone (recommended on a new machine)

```bash
git clone https://github.com/iederees-create/southern-suburbs-builders-ct.git
cd southern-suburbs-builders-ct
git fetch origin --prune
git switch --track origin/work/digital-marketing-strategy
```

---

## If the repo already exists locally

```bash
cd southern-suburbs-builders-ct
git fetch origin --prune
git switch work/digital-marketing-strategy
git pull --ff-only origin work/digital-marketing-strategy
```

If the local branch does not exist yet:

```bash
git fetch origin --prune
git switch --track origin/work/digital-marketing-strategy
```

---

## Before editing (always)

```bash
git status --short
git branch --show-current
```

**Required branch name:**

```text
work/digital-marketing-strategy
```

If you are on `main` or any other branch, stop and switch before editing.

---

## First files to open

```text
digital-marketing-strategy/README.md
digital-marketing-strategy/STRATEGY-INDEX.md
digital-marketing-strategy/CURRENT-STATUS.md
digital-marketing-strategy/EDITING-RULES.md
digital-marketing-strategy/ANTIGRAVITY-PROMPT.md
```

---

## After editing

Stage only marketing docs you intentionally changed:

```bash
git add digital-marketing-strategy handoff/grok handoff/codex seller-pack/drafts
git status --short
git commit -m "Refine Southern Suburbs Builders digital strategy"
git push origin work/digital-marketing-strategy
```

If `seller-pack/marketing` is created later, you may include it; currently the folder is **`seller-pack/drafts`**.

---

## Commands you must not run (unless explicitly instructed)

```bash
git push --force
git merge main
git push origin main
```

Also avoid:

- Editing website source to “fix” marketing  
- Publishing Etsy or social posts from the agent  
- Inventing product URLs or screenshots  

---

## Optional: open in Antigravity / editor

After checkout:

```bash
cd southern-suburbs-builders-ct
# Open this folder in Antigravity / your editor, then paste:
# digital-marketing-strategy/ANTIGRAVITY-PROMPT.md
```

If Antigravity provides a CLI open command on your machine, use that on the repo root. Example pattern (only if installed):

```bash
# Example only — use whatever Antigravity documents on your PC:
# antigravity .
# or: open -a Antigravity .
```

---

## Confirm remote after push

```bash
git status -sb
git log -1 --oneline
git rev-parse HEAD
git ls-remote origin refs/heads/work/digital-marketing-strategy
```

The remote tip should match your local commit SHA after a successful push.
