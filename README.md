# antarasurvey

Static, GitHub Pages–hosted build of Antara's anonymous teen spending
survey. Live at:

**https://survey.antara.money**

(GitHub's default `https://parthchhabraa.github.io/antarasurvey/` URL no
longer resolves to this content — the `CNAME` file below points Pages at
the custom domain instead, so the build here is root-relative, not
`/antarasurvey/`-prefixed.)

## What's in here

This repo holds only the *built* static output (`index.html`, `_next/`
assets, `CNAME`) — it isn't the survey's source code. The survey itself is
a Next.js route (`/survey`) that lives in
[`parthchhabraa/antara`](https://github.com/parthchhabraa/antara)'s
`frontend/src/app/survey`, sharing that app's theme, components, and
Firebase project.

## Regenerating this site

From a checkout of `antara`, with `frontend/` dependencies installed:

```bash
CUSTOM_DOMAIN=survey.antara.money ./scripts/export-survey-static.sh /path/to/antarasurvey
```

That pulls out just the HTML/JS/CSS the `/survey` page references (not the
rest of the app), builds it root-relative (no `BASE_PATH`, since a custom
domain serves from `/`), and writes a `CNAME` file alongside it — all ready
to commit here as-is.

If you ever move off the custom domain back to the default
`github.io/antarasurvey/` URL, use `BASE_PATH=/antarasurvey
./scripts/export-survey-static.sh` instead (no `CUSTOM_DOMAIN`, and delete
the `CNAME` file from this repo).

## GitHub Pages + DNS

Two separate things both have to be true for the custom domain to work —
Pages serving the branch, and DNS actually pointing at Pages:

1. **Settings → Pages → Build and deployment → Source: Deploy from a
   branch.** Branch: `claude/antara-spending-survey-6o4o2w` (or `main`,
   once merged) — Folder: `/ (root)`. This has been toggled off before;
   if the domain stops resolving, check here first.
2. **Settings → Pages → Custom domain** should show `survey.antara.money`
   (GitHub reads this from the committed `CNAME` file, but it's worth
   confirming it actually took and that "Enforce HTTPS" is checked once
   the certificate provisions).
3. **DNS**, at whoever manages the `antara.money` zone: a `CNAME` record
   for the `survey` subdomain pointing at `parthchhabraa.github.io`. This
   is the part a git push can never do — GitHub Pages settings only
   control the *serving* side, not the DNS record that routes
   `survey.antara.money` traffic there in the first place.

## Data

Submissions write directly from the visitor's browser to the
`survey_responses` collection in the `antara-moneycontrol` Firestore
project — see `firestore.rules` in the `antara` repo for the write-only,
validated access rule.
