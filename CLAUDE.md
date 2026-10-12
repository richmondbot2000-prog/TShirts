# CLAUDE.md — musicalmagic.uk

_Auto-loaded every session. Read `CLAUDE_CONTEXT.md` for the t-shirt shop's full history._

## What this repo is

One public GitHub repo, served by GitHub Pages at **musicalmagic.uk**, holding two
unrelated things:

1. **Musical Magic** — a small t-shirt shop. `index.html`, `product.html`,
   `admin.html`, `tshirts.json`, `style.css`. Built May 2026. See `CLAUDE_CONTEXT.md`.
2. **Latin game** — a Latin learning game the owner is building for his daughter.
   New, October 2026. Lives on its own page(s); must not disturb the shop.

Keep the two apart. Shared `style.css` is the shop's — give the game its own
stylesheet rather than editing that one.

## Non-negotiables

- **This repo is PUBLIC.** Every file is readable by anyone. Never put a token, a
  password, a key, or anything personal in it. That includes the daughter's name,
  school, age or any photo of her — the game must work without them.
- **The site is served over plain HTTP.** The Let's Encrypt certificate has never
  issued (stuck since May 2026; `gh api repos/richmondbot2000-prog/TShirts/pages`
  returns `certificate does not exist yet`). Until that is fixed, nothing here may
  ask for a login, a payment, or any personal data. A game that keeps progress in
  `localStorage` is fine; anything that leaves the browser is not.
- **No accounts, no tracking, no third-party analytics** on the game. It is for one
  child and whoever else stumbles on it.

## How it deploys

Push to `main`. GitHub Pages serves it at `musicalmagic.uk/<file>.html` within a
minute. There is no build step — plain HTML, CSS and JS, no bundler, no framework.

## Working style

The owner is non-technical and works from a phone via claude.ai/code. Don't give him
terminal commands to run. Don't ask him to install anything. Ship the change, tell him
the URL to look at.

Phone-first: he will almost always be looking at this on a phone, so check the layout
at 390px wide before saying something is done.
