# MVRK Studios website — project notes for Claude Code

## Who I am
Shah Sultan Akib, Senior BD Manager at Skill Ventures. I am not a coder: explain every step in plain, simple words, and ask before anything that changes the live site.

## What this is
The redesigned website for **MVRK Studios** (always "MVRK Studios" — never "MVRK VFX" or "Maverick"). VFX studio, part of Skill Ventures.
- GitHub repo: `akib897/mvrk-site`, branch `main`
- Live test copy: https://akib897.github.io/mvrk-site/ (GitHub Pages, deploys automatically on push to `main`)
- Final home: **mvrk.tv/vfx/** on **SiteGround** (not Hostinger) — see "mvrk.tv on SiteGround" below.

## How the site is built (do not restructure without asking)
- `index.html` — the whole site in one file (all pages: home, work, project, reels, services, contact, privacy). Template uses `{{ }}` bindings, `<sc-if>`, `<sc-for>`; logic is in `<script type="text/x-dc">` (`class Component extends DCLogic`, `renderVals()`).
- `support.js` — runtime that renders the template; it loads React 18.3.1 from unpkg. `index.html` does NOT work opened directly from disk — test with a local web server (e.g. `npx serve .` or `python -m http.server`) and open http://localhost.
- `assets/` — logos, posters, stills, videos. Keep files light (images already compressed to JPEG; videos re-encoded, faststart).
- One responsive page for desktop and mobile (desktop sidebar ≥ 900px wide; mobile layout below that).
- Page links use hashes: `#/work`, `#/project/<id>`, `#/contact`, `#/privacy` etc. (back button supported).

## Facts that must stay as they are
- Studios: Dhaka (House 112, Road 6, Mohakhali DOHS, Dhaka-1212), MVRK Sharjah (Business Center, Sharjah Publishing City Free Zone), MVRK New York (2248 Broadway, #1619, NY 10024), MVRK Singapore (151 Chin Swee Road, #02-24 Manhattan House, 169876).
- Contacts: Global Sales alan.gomes@mvrk.tv, phil@mvrk.tv, ian@mvrk.tv · VFX post-production hasnayeen@mvrk.tv · WhatsApp +880 1671-685989.
- LinkedIn https://www.linkedin.com/company/mvrk-vfx/ · Book a call https://calendly.com/hasnayeen-mvrk/discovery-call (Hasnayeen's own Calendly, named "MVRK Studios" with the MVRK logo; the Skill Ventures Calendly is for Skill Graphics only)
- Privacy page: effective date November 13, 2026; data controller MVRK Studios; contact hasnayeen@mvrk.tv.
- Project data on the site is real — do not replace it with placeholders.

## Open items
- Partner logos (Amazon, Disney, Netflix…) were cut from a screenshot; replace with official SVGs when available.

## Git rules
- Always show me what changed (in plain words) before committing, and ask before `git push`.
- Commit messages in plain English.
- Never put passwords, tokens or API keys in any file in this folder.

## Chatbot
- The chat panel talks to our own bot ("MVRK AI"): a Cloudflare Worker in `chatbot/` (https://mvrk-chat.wild-salad-7cd3.workers.dev) using Claude Haiku, paid from the Anthropic API credit that comes with Akib's Claude Max plan.
- What the bot knows is in `chatbot/src/knowledge.js`. After changing it: test on a preview (`npx wrangler versions upload --preview-alias training`), then go live with `npx wrangler deploy` from `chatbot/` — only after I say yes.
- The Anthropic key is a Cloudflare secret (`ANTHROPIC_API_KEY`), never in a file.

## "Start a project" form
- On mvrk.tv it sends straight to hasnayeen@mvrk.tv through WordPress Contact Form 7, form **5996** ("VFX website enquiry"). On the GitHub test copy, or if sending fails, it opens the visitor's mail app instead.
- mvrk.tv's SPF only lists Google, so these emails come from SiteGround and may land in spam.

## mvrk.tv on SiteGround
- mvrk.tv is hosted on **SiteGround** (email is Google Workspace). `/` is the VFX/ONE start page and `/one/` is a separate WordPress site — never touch either.
- The new site lives in the folder `public_html/vfx` (it overrides the old WordPress VFX page; renaming the folder brings the old page back). The old `/vfx/contact-vfx/` address forwards via `contact-vfx/index.html`.
- No SiteGround account access yet — only WordPress admin (mvrk.tv/wp-admin), which I log in to myself. Uploads were done with the "WP File Manager" plugin (install, drag files in, then delete the plugin again). It cannot create `.htaccess` files or unzip reliably — upload folders, not zips.
- `.github/workflows/deploy-mvrk.yml` is a "Deploy to mvrk.tv" button (manual only) that needs SiteGround SSH secrets in GitHub — not set up yet.
- After any change on the server, purge the cache ("Purge SG Cache" in the WordPress admin bar).
