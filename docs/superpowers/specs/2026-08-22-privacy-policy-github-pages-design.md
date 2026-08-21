# Privacy Policy on GitHub Pages — Design

**Date:** 2026-08-22  
**Status:** Approved for implementation planning  
**Owner:** Kunal Tandon (`kunaltandon.kt@gmail.com`)

## Goal

Publish a Play Store–ready privacy policy for Kunal Tandon’s Google Play developer account (covering multiple apps) at a stable public URL on GitHub Pages.

## Decisions

| Topic | Choice |
| --- | --- |
| Policy scope | Developer account / all apps under one policy |
| Data practices | Mix — varies by app; policy lists common categories |
| Legal / operator name | Kunal Tandon |
| Contact email | kunaltandon.kt@gmail.com |
| Hosting approach | Static HTML on GitHub Pages |
| Repository | `KunalTandonAppStore` under `devkunaltandon` |
| Public URL | `https://devkunaltandon.github.io/KunalTandonAppStore/` |

## Architecture

- Public GitHub repository `KunalTandonAppStore` on account `devkunaltandon`.
- Default branch `main`.
- GitHub Pages served from the repository root on `main` (or `/docs` only if root deploy is unavailable; prefer root).
- No build toolchain, no framework, no Jekyll theme dependency.
- Play Console privacy policy field points at the Pages URL above.

## Components

1. **`index.html`** — Full privacy policy page (primary deliverable for Play Console).
2. **Inline or small `styles.css`** — Readable legal-document styling only (typography, spacing, max width). No marketing layout.
3. **`README.md`** — Short description of the repo and the live policy URL.
4. **GitHub Pages config** — Enabled via GitHub CLI / API so the site is public.

## Policy content outline

The page must include:

1. Who we are and what the policy covers (apps published by Kunal Tandon on Google Play).
2. Information that may be collected (device info, diagnostics, analytics, advertising IDs, account/contact data if an app uses them, permission-related data), with a clear note that details vary by app.
3. How data may be used.
4. Third parties that may be involved (e.g. Google Play services, Firebase, AdMob) as possible processors — not claimed for every app.
5. Sharing, retention, and security (high-level, accurate defaults).
6. Children’s privacy.
7. User choices, contact, and deletion/privacy requests via `kunaltandon.kt@gmail.com`.
8. Changes to the policy and an effective date.

Tone: clear English suitable for Play Console. Not a substitute for legal advice; sufficient as a published developer privacy policy.

## Visual presentation

- Single-column readable page.
- Title: “Privacy Policy”.
- Clean typography, comfortable line length, light background.
- Contact email as a `mailto:` link.
- No nav chrome, cards, or promotional content.

## Publish flow

1. Add policy and supporting files in this workspace.
2. Create public GitHub repo `KunalTandonAppStore` under `devkunaltandon` if it does not exist.
3. Push `main`.
4. Enable GitHub Pages for the repo.
5. Verify the live URL renders the full policy.

## Success criteria

- `https://devkunaltandon.github.io/KunalTandonAppStore/` loads the complete privacy policy.
- Operator name and contact email match the decisions table.
- URL is suitable to paste into Google Play Console for apps under this developer account.

## Out of scope

- Per-app privacy policy pages.
- Custom domain.
- Backend, analytics on the policy site, or consent SDK integration in apps.
- Formal legal review or jurisdiction-specific addenda beyond a standard developer policy.

## Risks / notes

- GitHub Pages may take a few minutes after enablement before the URL is live.
- If any app later collects sensitive data not covered by the common categories, the policy HTML should be updated and the effective date refreshed.
