# Claude Context — TShirts (Musical Magic)

_If a future Claude is reading this, they've forgotten everything. This file is the fastest path back to being useful._

---

## 0. To resume next session — say this to Claude

> *"Read `~/Desktop/TShirts/CLAUDE_CONTEXT.md` and pick up where we left off."*

---

## 1. Right this minute (state at end of session)

- **Project name:** Musical Magic — a t-shirt shop
- **Logo:** `logo.jpg` in the project root. Crystalline garnet butterfly with a cream "M" centred on it, "MUSICAL" / "MAGIC" wordmark above & below, soft lavender background.
- **Live URLs:**
  - Custom domain (canonical): <https://musicalmagic.uk> — registered via Cloudflare 2026-05-08, DNS managed in Cloudflare (4 A records at apex pointing at GitHub Pages IPs, CNAME on `www`, all set to **DNS only / gray cloud** so GitHub can issue Let's Encrypt cert).
  - Origin URL (still works): <https://richmondbot2000-prog.github.io/TShirts/> — auto-redirects to the custom domain.
- **HTTPS cert:** as of last session, GitHub Let's Encrypt cert was still provisioning. A background watcher was polling `gh api repos/.../pages PUT https_enforced=true` until the API stopped returning "certificate does not exist yet" (404). If the green padlock isn't showing on `https://musicalmagic.uk`, manually re-run that PUT once.
- **Repo:** <https://github.com/richmondbot2000-prog/TShirts> — public.
- **Visibility:** `noindex, nofollow` removed from `index.html` + `product.html` (so Google indexes the shop). Kept on `admin.html` (back-office stays out of search).
- **Last commit (as of context-write):** `4b0f6db` — admin link moved to footer.

### What was built (2026-05-08, in order)

1. **Initial scaffold** — 4 files: homepage grid (`index.html`), product detail (`product.html?id=...`), local-first admin (`admin.html`), JSON datastore (`tshirts.json`), shared `style.css`. Lavender + cream + garnet palette pulled from the logo. GitHub Pages enabled via `gh api`.
2. **Image upload via GitHub Contents API** — admin's "Upload image" button puts the file into `images/<slug>-<timestamp>.<ext>` in the repo using the same PAT as Publish. URL field still works as a fallback for hosted images.
3. **Client-side resize-on-upload** — phone-camera 8MB JPEGs get max-edge=1200px / JPEG-q=0.85 via `<canvas>` before upload (typical: 8MB → 300-500KB). Skipped for already-small images. Status line surfaces before/after sizes.
4. **Tidy-up of unused images** — admin button GETs the repo's `images/` tree, diffs against (every saved tee's images) ∪ (in-progress form's images), and DELETEs orphans via the Contents API.
5. **Custom domain `musicalmagic.uk`** — `CNAME` file in repo, Cloudflare DNS records (4 apex A + `www` CNAME, all DNS-only), GitHub Pages picked it up.
6. **Currency switched £ from $** — three render sites + the admin form's price-field label.
7. **Removed `noindex`** from public pages now that the custom domain is live.
8. **Multi-image (up to 5 per tee)** — schema: `image: string` → `images: string[]`. First image is the cover; second cross-fades on hover via CSS (`card-image-hover { opacity: 0 } → :hover { 1 }`). Product page has a hero image + clickable thumbnail strip below.
9. **Per-size availability (S/M/L/XL/XXL)** — schema: `available: bool` → `sizes: { S, M, L, XL, XXL: bool }`. Product page has a size-picker (unavailable sizes disabled + struck through). Order CTA starts disabled ("Pick a size to order"), enables once a size is selected with a `mailto:` body that names the chosen size. Admin form has 5 size checkboxes (replacing the old single Available/Out-of-stock select).
10. **Backwards compat at read time** — every renderer (index, product, admin list) calls a `normalize(t)` helper that folds either schema (old `image: x, available: true` OR new `images: [...], sizes: {...}`) into a unified shape. New writes from admin only emit the new schema, so old records get cleaned up the next time the user saves them.
11. **Admin link demoted** — removed from the topbar nav on `index.html` + `product.html`, moved to a small footer at the very bottom of those pages, coloured `rgba(43, 26, 58, 0.25)` (dark ink at 25% opacity). Just visible enough that the admin user finds it; near-invisible to casual visitors.

---

## 2. The user

- **Email:** `richmondbot2000@gmail.com`
- **GitHub username:** `richmondbot2000-prog`
- **OS:** macOS (Darwin 25.4.0), arm64 (Apple Silicon)
- **Working directory:** `/Users/richmondrobot`
- **Self-described:** non-technical. Cannot write code, SQL, or shell. Can navigate the browser, take screenshots, follow numbered steps.

The shop's admin (referred to as "she" — likely a relative the user is building this for) is the day-to-day user of the admin page. The whole admin UX is designed assuming non-technical operators on both ends.

### Working style — observed across many sessions

- **Few questions.** Stated explicitly: *"ask as few questions as possible."* Default to executing.
- **Terse, push-immediately.** They want changes live, not staged.
- **Direct corrections.** Will tell you when something is wrong, sometimes bluntly. Don't get defensive — fix it.
- **Picky about meaning.** Every visible element must justify its existence.
- **Iterates on structure.** Don't get attached to layout.

---

## 3. The platform

- **Hosting:** GitHub Pages (static). Pages enabled with `source.branch=main`, `source.path=/`. There is no server.
- **Storage:** `tshirts.json` in the repo serves as the database. Public, so don't put anything secret in it.
- **Auth for the admin "Publish":** GitHub Personal Access Token (fine-grained, scoped to just this repo, with `Contents: Read and write`). Stored only in the admin's browser localStorage. Never sent anywhere except `api.github.com`.
- **Order flow:** for v1, a `mailto:` link on the product page. No checkout, no Stripe, no inventory tracking. The user can ask for a real checkout (Stripe Payment Links work fine for static sites) when they want it.
- **Image handling:** for v1, the admin pastes a URL. Either an external image URL or a path to a file already in the repo. No upload UI yet — would need an image-host integration (Cloudinary, GitHub-LFS-via-API, etc.) to add later.

---

## 4. File locations

- **Local clone:** `~/Desktop/TShirts/`
- **GitHub remote:** `https://github.com/richmondbot2000-prog/TShirts` (public)
- **Live URL:** <https://richmondbot2000-prog.github.io/TShirts/>
- **This file:** `~/Desktop/TShirts/CLAUDE_CONTEXT.md` (also ignored from indexing — but in a public repo, so don't put anything sensitive here either)

### Files in the repo

| Path | Purpose |
|---|---|
| `index.html` | Homepage with product grid (reads `tshirts.json`) |
| `product.html` | Single-tee detail page (reads `tshirts.json`, finds by `?id=`) |
| `admin.html` | CRUD admin with localStorage drafts + GitHub-API publish |
| `tshirts.json` | The data store |
| `style.css` | Shared styles (lavender + cream + garnet + Fredoka) |
| `logo.jpg` | The crystal-butterfly Musical Magic logo |

---

## 5. How deployment works

```
~/Desktop/TShirts/    ← edit here
       ↓ git commit + git push
github.com/richmondbot2000-prog/TShirts   (main branch)
       ↓ ~30s GitHub Pages build
https://richmondbot2000-prog.github.io/TShirts/   ← live
```

**Two routes to deploy `tshirts.json` updates:**

1. **From the admin page (intended for the admin user):** localStorage draft → click **Publish** → `PUT /repos/.../contents/tshirts.json` via Contents API → Pages rebuild.
2. **From the terminal (intended for the developer / the richmond user):** edit any file → `git add -A && git commit -m "…" && git push`. Same end state.

Code-and-style changes (HTML, CSS, JS) always go through route 2 because the admin page only edits `tshirts.json`.

---

## 6. Site structure (current)

**Topbar (every page):** logo + brand wordmark · nav links (Shop, Admin)

**Homepage (`index.html`):**
- Hero: large logo + brand name (gradient text) + "Handmade tees, with a touch of sparkle." tagline
- Product grid: cards in a `repeat(auto-fill, minmax(260px, 1fr))` grid. Each card = image + name + price + "Out of stock" badge if `available: false`.

**Product page (`product.html?id=<id>`):**
- Back link
- Two-column: square image left / details right (stacks on mobile)
- Title + price + description + CTA (`mailto:` order link, or disabled "Out of stock" button)

**Admin page (`admin.html`):**
- Status bar: shows "Not connected to GitHub", "Unpublished changes", or "Published — live site is up to date" (with discard/publish buttons)
- Add/edit form: name, price, status (Available / Out of stock), image URL, description
- Existing tees list: thumbnail · name · price · ID · Edit / Delete buttons
- Settings modal: walk-through to create a fine-grained PAT scoped just to this repo, with copy-pasteable repo slug and the exact permissions to enable

---

## 7. Visual design

**Palette (CSS custom properties on `:root` in `style.css`):**
- `--lav-bg: #d8bce8` — page background (matches logo bg)
- `--lav-soft: #e6d3f0` / `--lav-deep: #b893cf` — image-placeholder gradients
- `--cream: #fbf6e8` / `--cream-soft: #f5edd6` — card backgrounds
- `--garnet: #9c3a37` / `--garnet-deep: #6e2624` — primary accent (matches butterfly gem tones)
- `--rose: #d68a7a` — secondary accent
- `--ink: #2b1a3a` / `--ink-soft: #5a4870` / `--muted: #897ba0` — text

**Typography:**
- `Fredoka` 500–700 — display headlines, brand name, prices, card titles. Rounded chunky — echoes the logo's wordmark.
- `Plus Jakarta Sans` 400–700 — body text.

**Signature elements:**
- Hero h1 has a garnet → rose gradient via `background-clip: text`
- Cards lift on hover (`translateY(-4px)` + bigger shadow)
- Image placeholders: lavender gradient with a big cream-coloured first-letter as a fallback when no image URL is set

---

## 8. Pending / open work

| Item | Status | Notes |
|---|---|---|
| Real checkout (Stripe Payment Links?) | Not yet | Currently `mailto:` only. User confirmed they're aware; we can add Stripe later — works fine for static sites, no backend needed. |
| Image upload (vs URL) | Not yet | Admin pastes an image URL. Adding upload requires a host (Cloudinary, GitHub LFS via API, R2, etc.) |
| Sizes / variants | Not yet | The data model is one row per tee; no size selector. Add a `sizes` array if needed. |
| Discovery / SEO | Off by default | `noindex, nofollow` on every page. Remove the meta tag if you want Google to find the shop. |
| Analytics | None | No tracking installed. |
| Custom domain | None | Live at `*.github.io/TShirts/`. Custom domain via `CNAME` file + DNS if wanted. |

---

## 9. Things to do — and not do

- **Don't put secrets in `tshirts.json`.** It's public on GitHub Pages.
- **Don't put secrets in this file.** Same reason.
- **The admin's PAT lives ONLY in the admin's browser localStorage.** Don't ever bake it into a file. Don't commit it. Don't store it server-side (there's no server). If she switches devices, she repeats the Settings → Save token flow on the new browser.
- **Recommend the fine-grained token** with `Contents: Read and write` scoped to just the `TShirts` repo. Classic tokens with `repo` scope work but are over-broad.
- **The admin saves drafts to localStorage on every change.** A reload doesn't lose work. Discarding requires the explicit Discard button.
- **`Publish` always re-fetches the file's `sha` first** before PUT, so the user can't trample over a concurrent commit (e.g. one made from the terminal).
- **GitHub API rate limits:** 5,000 req/hour per token. Way more than this admin will ever hit.
- **Don't trust the homepage cache.** GitHub Pages serves with sensible caching, but after a publish always tell the user to hard-refresh (Cmd+Shift+R) if they don't see changes within ~30s.

---

## 10. Useful commands cheat sheet

```bash
# See the repo
ls ~/Desktop/TShirts
git -C ~/Desktop/TShirts log --oneline -10
git -C ~/Desktop/TShirts status

# Edit code/styles, push to deploy
cd ~/Desktop/TShirts
git add -A && git commit -m "summary" && git push

# Verify the live site
curl -sI https://richmondbot2000-prog.github.io/TShirts/ | head
curl -s https://richmondbot2000-prog.github.io/TShirts/ | grep '<title>'
curl -s https://richmondbot2000-prog.github.io/TShirts/tshirts.json | python3 -m json.tool | head -20

# Pages config (read)
gh api repos/richmondbot2000-prog/TShirts/pages
```

---

## 11. Personal-memory note (for me)

A `project_tshirts.md` entry in `~/.claude/projects/-Users-richmondrobot/memory/` auto-loads each session and pinpoints this file as the canonical source. The MEMORY.md index also links it.

---

_End of context. Last updated: 2026-05-08 (custom domain `musicalmagic.uk` via Cloudflare; multi-image up to 5 per tee with hover-swap on cards + thumbnail gallery on product page; per-size availability S/M/L/XL/XXL replacing item-level available; £ pricing; image upload + client-side resize + tidy-up of orphans; admin link demoted to discreet footer; noindex removed from public pages)._
