# MVRK Studios website — project notes for Claude Code

## Who I am
Shah Sultan Akib, Senior BD Manager at Skill Ventures. I am not a coder: explain every step in plain, simple words, and ask before anything that changes the live site.

## What this is
The redesigned website for **MVRK Studios** (always "MVRK Studios" — never "MVRK VFX" or "Maverick"). VFX studio, part of Skill Ventures.
- GitHub repo: `akib897/mvrk-site`, branch `main`
- Live test copy: https://akib897.github.io/mvrk-site/ (GitHub Pages, deploys automatically on push to `main`)
- Final home: Hostinger (mvrk.tv) — not connected yet, see "Hostinger" below.

## How the site is built (do not restructure without asking)
- `index.html` — the whole site in one file (all pages: home, work, project, reels, services, contact, privacy). Template uses `{{ }}` bindings, `<sc-if>`, `<sc-for>`; logic is in `<script type="text/x-dc">` (`class Component extends DCLogic`, `renderVals()`).
- `support.js` — runtime that renders the template; it loads React 18.3.1 from unpkg. `index.html` does NOT work opened directly from disk — test with a local web server (e.g. `npx serve .` or `python -m http.server`) and open http://localhost.
- `assets/` — logos, posters, stills, videos. Keep files light (images already compressed to JPEG; videos re-encoded, faststart).
- One responsive page for desktop and mobile (desktop sidebar ≥ 900px wide; mobile layout below that).
- Page links use hashes: `#/work`, `#/project/<id>`, `#/contact`, `#/privacy` etc. (back button supported).

## Facts that must stay as they are
- Studios: Dhaka (House 112, Road 6, Mohakhali DOHS, Dhaka-1212), MVRK Sharjah (Business Center, Sharjah Publishing City Free Zone), MVRK New York (2248 Broadway, #1619, NY 10024), MVRK Singapore (151 Chin Swee Road, #02-24 Manhattan House, 169876).
- Contacts: Global Sales alan.gomes@mvrk.tv, phil@mvrk.tv, ian@mvrk.tv · VFX post-production hasnayeen@mvrk.tv · WhatsApp +880 1671-685989.
- LinkedIn https://www.linkedin.com/company/mvrk-vfx/ · Book a call https://calendly.com/skill-ventures
- Privacy page: effective date November 13, 2026; data controller MVRK Studios; contact hasnayeen@mvrk.tv.
- Project data on the site is real — do not replace it with placeholders.

## Open items
- Chat widget on the site is a design only. The real bot is Featurebase (workspace mvrk.featurebase.app) — it needs the embed code, and the AI agent needs a paid Featurebase plan (workspace is on Free since Nov 14, 2026).
- "Start a project" form still opens an email (mailto) to hasnayeen@mvrk.tv.
- Partner logos (Amazon, Disney, Netflix…) were cut from a screenshot; replace with official SVGs when available.

## Git rules
- Always show me what changed (in plain words) before committing, and ask before `git push`.
- Commit messages in plain English.
- Never put passwords, tokens or API keys in any file in this folder.

## Hostinger
Not set up yet. Preferred route: in Hostinger hPanel → Websites → (mvrk.tv) → Advanced → GIT, connect repo `akib897/mvrk-site`, branch `main`, and turn on auto-deploy — then every push to GitHub also updates Hostinger. I log in to Hostinger myself; walk me through the clicks. Before switching mvrk.tv, back up the current live site from Hostinger's File Manager.
