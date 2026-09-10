# Food Transparency Coalition — working notes for Claude

The public site for the Food Transparency Coalition.
Live at https://food-transparency-coalition.vercel.app — Vercel auto-deploys
whenever `main` changes, usually within about 30 seconds.

## What this project is

A plain static site. No build step, no dev server — the files in this repo are
exactly what the browser gets.

| File | What it is |
| --- | --- |
| `index.html` | The whole page: markup, CSS in one `<style>` block, JS in one `<script>` block at the bottom |
| `config.js` | The petition and FDA filing links |
| `assets/` | Background texture and the social share image |
| `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` | Tab and home-screen icons |

## Rules

**Static HTML, CSS, and JS only.** Don't add frameworks, build tools, bundlers,
npm packages, or a `package.json`. If something seems to need a library, write
it in plain JS instead, or ask first.

**Keep Tyler's design.** The fonts, colors, and spacing came from Tyler's Claude
Design file and should stay as they are unless I specifically ask for a design
change. The palette and type live in the `:root` block near the top of
`index.html` (`--ink`, `--paper`, `--cream`, `--green`, `--rust`, `--sans`,
and friends) — reuse those variables rather than introducing new one-off colors
or font stacks.

**Petition links belong in `config.js`.** `window.SITE_CONFIG.signUrl` and
`window.SITE_CONFIG.filingUrl` feed the "Sign the petition" and "Read the full
FDA filing" buttons. The script at the bottom of `index.html` fills in any
element with a `data-link="sign"` or `data-link="filing"` attribute, and shows a
friendly "opening soon" message when the URL is still blank. Never hard-code
either URL into `index.html`.

**Check phone width too.** Every change has to look right at roughly 390px wide
as well as on desktop. The layout is fluid (it leans on `clamp()` rather than
breakpoints), so it's easy to break narrow screens without noticing on a big
monitor. Watch for text that overflows, buttons that get cut off, and any
sideways scrolling.

## How I'd like changes handled

**Pull the latest `main` first.** Tyler and I both edit this site, sometimes
straight through GitHub's web editor, so `main` may have moved since you last
looked. Run `git pull origin main` before starting a change — don't build on a
stale copy.

**Push straight to `main`.** That's the default. Don't park changes on a branch
or open a pull request unless I've asked for a preview. Pushing to `main` puts
it live within about 30 seconds, so make sure it's right before you push.

When I ask for a change: make it, commit it with a plain-English message
(what changed, not jargon), push it, and then tell me in one or two sentences
what you changed. No long summaries unless I ask for them.
