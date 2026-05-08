# Claude Context — TShirts project

_If a future Claude is reading this, they've forgotten everything. This file is the fastest path back to being useful._

---

## 0. To resume next session — say this to Claude

> **On the Mac (terminal Claude Code):** *"Read `~/Desktop/TShirts/CLAUDE_CONTEXT.md` and pick up where we left off."*

---

## 1. Right this minute

- **Project status:** brand-new, scaffolded only. Folder exists at `~/Desktop/TShirts/`. No git repo, no GitHub remote, no live URL yet.
- **What we know about the project:** _<TBD — the user named the project "TShirts" and asked for a context file but hasn't yet described what it does. Fill this section in once they explain the goal.>_
- **Last commit:** none yet.

---

## 2. The user

- **Email:** `richmondbot2000@gmail.com`
- **GitHub username:** `richmondbot2000-prog`
- **Azure DevOps user:** `james.benamor@letme.com`
- **OS:** macOS (Darwin 25.4.0), arm64 (Apple Silicon)
- **Working directory at start of every session:** `/Users/richmondrobot`
- **Self-described:** non-technical. Cannot write code, SQL, or shell. Can navigate the browser, take screenshots, and follow numbered steps.

### How they like to work (from APIs For Kids project)

- **Few questions.** Default to executing.
- **Terse, push-immediately.** Iterate on the live site rather than staging.
- **Direct corrections.** They will tell you when something is wrong, sometimes bluntly. Don't get defensive — fix it.
- **Picky about meaning.** Every visible element should justify its existence. They reject decorative-only icons; they reject mismatched copy; they reject sections that don't communicate something useful.
- **Iterates on structure.** Will reorganise mid-conversation. Don't get attached to layout.
- **Likes pop-culture visual references.** Confirmed: Futurama-style retro-futurism for APIs For Kids. Lean toward playful / themed aesthetics over corporate-clean unless they ask for a specific look.

If a setup decision needs guidance the user gave for APIs For Kids, default to the same convention here unless they tell you otherwise (e.g. visibility = public, GitHub Pages deploy, hard rules below).

---

## 3. The platform / domain

_<TBD — what is "TShirts" about? Examples to discriminate when the user describes it:_
_- A site that designs / sells T-shirts? An online shop?_
_- A catalogue of internal team T-shirts at Richmond Group?_
_- A tool that generates T-shirt artwork from prompts?_
_- An inventory tracker?_
_- Something else entirely?_
_Pin this down before starting any structural work; it shapes every other decision._>

---

## 4. File locations

- **Project root (local):** `~/Desktop/TShirts/`
- **GitHub remote:** _<not created yet — will be `https://github.com/richmondbot2000-prog/TShirts` if following the APIs For Kids pattern>_
- **Live URL (if/when deployed via GitHub Pages):** _<not yet — would be `https://richmondbot2000-prog.github.io/TShirts/`>_
- **This file:** `~/Desktop/TShirts/CLAUDE_CONTEXT.md`

---

## 5. How deployment will work (if following APIs For Kids pattern)

```
~/Desktop/TShirts/    ← edit here
       ↓ git commit + git push
github.com/richmondbot2000-prog/TShirts   (main branch)
       ↓ ~30s GitHub Pages build
https://richmondbot2000-prog.github.io/TShirts/   ← live
```

**Auth state on this Mac (already set up from APIs For Kids):**
- `gh` CLI installed at `~/.local/bin/gh` (PATH set in `~/.zshrc`)
- `gh auth status` shows logged in as `richmondbot2000-prog` with scopes `gist, read:org, repo, workflow`
- Auth persisted in macOS keychain — survives across sessions
- Set the local repo's git config to:
  - `user.name=richmondbot2000-prog`
  - `user.email=richmondbot2000@gmail.com`
- `git push` works without prompting once the remote is created and `origin` is set.

**To bootstrap the GitHub repo when ready:**
```bash
cd ~/Desktop/TShirts
git init
git add -A
git commit -m "Initial commit"
gh repo create TShirts --public --source=. --push
# Then enable GitHub Pages in the repo settings (Settings → Pages → main → /)
```

---

## 6. Site structure (current)

_<TBD — define once the project's purpose is clear.>_

---

## 7. Visual design

_<TBD — pick a palette and typography once the project's purpose is clear. The APIs For Kids site uses a Futurama "New New York" palette (deep-space navy, neon cyan + magenta accents, Orbitron display font) — that's tied to that project's theme; pick a palette here that suits T-shirts.>_

---

## 8. Pending / open work

| Item | Status | Blocker / next step |
|---|---|---|
| **Define what the project does** | Not yet defined | User described the project name only — needs purpose, audience, and visible artefacts spelled out |
| **GitHub repo** | Not created | `gh repo create TShirts --public --source=. --push` once there's anything worth pushing |
| **GitHub Pages enable** | Not enabled | Settings → Pages → main → / (or `/docs`) once the repo exists |

---

## 9. Things to do — and not do

### Hard rules carried over from APIs For Kids

- **Don't add decorative-only elements.** Everything visible should communicate something.
- **Don't ask 5 questions when one will do.** Make the safe default and tell the user; let them correct it.
- **Don't promise a feature until it's tested live.** UI fixes especially — type-check ≠ feature-check. Open the browser before saying "done".
- **Don't bake an internal hostname or secret into a public repo.** If the project ever needs to talk to an internal Richmond Group system, it goes through a GitHub Actions workflow + repo secret, not a hard-coded URL.
- **Always create new commits, never amend** — the user has tooling and expectations around honest commit history.

### Project-specific lessons

_<Add lessons learned here as the project evolves — corrections from the user, gotchas discovered, patterns that worked.>_

---

## 10. Useful commands cheat sheet

```bash
# Auth status
gh auth status

# See what's in the repo
ls ~/Desktop/TShirts
git -C ~/Desktop/TShirts log --oneline -10
git -C ~/Desktop/TShirts status

# Once remote exists
cd ~/Desktop/TShirts
git add -A && git commit -m "summary" && git push
```

---

## 11. Personal-memory note (for me)

If I'm working from memory rather than this file, I have project memory under `~/.claude/projects/-Users-richmondrobot/memory/` — the per-project + per-user entries auto-load. Add a `project_tshirts.md` entry there once this project's purpose is known.

---

_End of context. Last updated: 2026-05-08 (skeleton only — project not yet defined; folder created, awaiting the user's description of the goal)._
