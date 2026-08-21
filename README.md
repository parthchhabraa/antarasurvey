# antarasurvey

Static, GitHub Pages–hosted build of Antara's anonymous teen spending
survey. Live once Pages is enabled for this repo (see below) at:

**https://parthchhabraa.github.io/antarasurvey/**

## What's in here

This repo holds only the *built* static output (`index.html` + `_next/`
assets) — it isn't the survey's source code. The survey itself is a Next.js
route (`/survey`) that lives in
[`parthchhabraa/antara`](https://github.com/parthchhabraa/antara)'s
`frontend/src/app/survey`, sharing that app's theme, components, and
Firebase project.

## Regenerating this site

From a checkout of `antara`, with `frontend/` dependencies installed:

```bash
BASE_PATH=/antarasurvey ./scripts/export-survey-static.sh /path/to/antarasurvey
```

That pulls out just the HTML/JS/CSS the `/survey` page references (not the
rest of the app) and writes them ready to commit here.

## Enabling GitHub Pages (one-time, manual)

This repo's Pages site isn't turned on yet — that's a repo-settings change
only an owner/admin can make, not something that can be pushed via git:

1. Go to **Settings → Pages** on this repo.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Branch: `claude/antara-spending-survey-6o4o2w` (or `main`, once this
   branch is merged) — Folder: `/ (root)`.
4. Save. The site goes live at the URL above within a minute or two.

## Data

Submissions write directly from the visitor's browser to the
`survey_responses` collection in the `antara-moneycontrol` Firestore
project — see `firestore.rules` in the `antara` repo for the write-only,
validated access rule.
