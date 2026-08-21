# Privacy Policy GitHub Pages Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish a Play Store–ready privacy policy for Kunal Tandon’s developer account at `https://devkunaltandon.github.io/KunalTandonAppStore/`.

**Architecture:** Static `index.html` + optional `styles.css` at repo root; public GitHub repo; GitHub Pages from `main` / root. No build step.

**Tech Stack:** HTML5, CSS, Git, GitHub CLI (`gh`), GitHub Pages

## Global Constraints

- Operator name: Kunal Tandon
- Contact: kunaltandon.kt@gmail.com
- Scope: all apps under this Play developer account; data practices may vary by app
- URL: `https://devkunaltandon.github.io/KunalTandonAppStore/`
- Repo: public `KunalTandonAppStore` under `devkunaltandon`
- No framework, no Jekyll dependency, no custom domain

## File Structure

| File | Responsibility |
| --- | --- |
| `index.html` | Full privacy policy page (Play Console target) |
| `styles.css` | Readable legal-document styling |
| `README.md` | Repo purpose + live URL |

---

### Task 1: Create privacy policy page

**Files:**
- Create: `index.html`
- Create: `styles.css`
- Create: `README.md`

**Interfaces:**
- Consumes: Design decisions (operator, email, multi-app scope)
- Produces: Static site root files ready for Pages

- [ ] **Step 1: Create `styles.css`**

```css
:root {
  --bg: #f7f5f1;
  --text: #1a1a1a;
  --muted: #555;
  --accent: #0b3d2e;
  --rule: #d9d4cb;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: "Source Serif 4", "Iowan Old Style", "Palatino Linotype", Palatino, Georgia, serif;
  background: linear-gradient(180deg, #efebe3 0%, var(--bg) 28%, var(--bg) 100%);
  color: var(--text);
  line-height: 1.65;
}

main {
  max-width: 42rem;
  margin: 0 auto;
  padding: 3rem 1.25rem 4rem;
}

h1 {
  font-size: clamp(2rem, 4vw, 2.75rem);
  line-height: 1.15;
  letter-spacing: -0.02em;
  color: var(--accent);
  margin: 0 0 0.5rem;
}

.meta {
  color: var(--muted);
  font-size: 0.95rem;
  margin: 0 0 2rem;
  padding-bottom: 1.25rem;
  border-bottom: 1px solid var(--rule);
}

h2 {
  font-size: 1.2rem;
  margin: 2rem 0 0.75rem;
  color: var(--accent);
}

p,
li {
  font-size: 1.05rem;
}

ul {
  padding-left: 1.25rem;
}

a {
  color: var(--accent);
}

footer {
  margin-top: 2.5rem;
  padding-top: 1.25rem;
  border-top: 1px solid var(--rule);
  color: var(--muted);
  font-size: 0.95rem;
}
```

- [ ] **Step 2: Create `index.html` with full policy**

Use this structure (fill body with the approved outline sections; effective date `2026-08-22`):

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Privacy Policy — Kunal Tandon</title>
  <meta name="description" content="Privacy Policy for apps published by Kunal Tandon on Google Play.">
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <main>
    <h1>Privacy Policy</h1>
    <p class="meta">Effective date: August 22, 2026<br>
      Operator: Kunal Tandon<br>
      Contact: <a href="mailto:kunaltandon.kt@gmail.com">kunaltandon.kt@gmail.com</a>
    </p>
    <!-- Sections 1–8 from design spec -->
  </main>
</body>
</html>
```

Policy body requirements (all must appear as real prose, not placeholders):

1. Covers apps published by Kunal Tandon on Google Play; practices may vary by app.
2. May collect: device info, diagnostics/crash data, analytics, advertising IDs, account/contact data if an app offers accounts or forms, data related to permissions the user grants.
3. Uses: operate and improve apps, fix bugs, analytics, ads (if used), respond to requests, comply with law.
4. Third parties may include Google Play, Google analytics/Firebase, AdMob/ad networks, OS vendors — only when a given app integrates them.
5. Sharing only as needed for those services, legal compliance, or with consent; retention as long as needed for the purposes above; reasonable security measures.
6. Not directed at children under 13; contact for deletion if collected inadvertently.
7. Contact email for access/deletion/privacy questions; device settings for ads/permissions.
8. Policy may change; continued use after update means acceptance of revised policy; check this page for the current version.

- [ ] **Step 3: Create `README.md`**

```markdown
# Kunal Tandon App Store — Privacy Policy

Public privacy policy for apps published by **Kunal Tandon** on Google Play.

**Live URL:** https://devkunaltandon.github.io/KunalTandonAppStore/

Contact: kunaltandon.kt@gmail.com
```

- [ ] **Step 4: Verify files locally**

Run: `ls -la index.html styles.css README.md && grep -n "kunaltandon.kt@gmail.com\|Kunal Tandon\|Effective date" index.html`

Expected: three files exist; email, name, and effective date present in `index.html`.

- [ ] **Step 5: Commit**

```bash
git add index.html styles.css README.md
git commit -m "$(cat <<'EOF'
Add Play Store privacy policy static site.

EOF
)"
```

---

### Task 2: Create GitHub repo and enable Pages

**Files:**
- Modify: remote git configuration only (no local content changes expected)

**Interfaces:**
- Consumes: committed site from Task 1
- Produces: public repo + live Pages URL

- [ ] **Step 1: Create public GitHub repository**

```bash
gh repo create KunalTandonAppStore --public --source=. --remote=origin --description "Privacy policy for Kunal Tandon Google Play apps"
```

Expected: repo created at `https://github.com/devkunaltandon/KunalTandonAppStore`

If the repo already exists, set `origin` to that URL instead and continue.

- [ ] **Step 2: Push `main`**

```bash
git push -u origin main
```

Expected: push succeeds.

- [ ] **Step 3: Enable GitHub Pages from `main` / root**

```bash
gh api repos/devkunaltandon/KunalTandonAppStore/pages -X POST -f build_type=legacy -f source[branch]=main -f source[path]=/
```

If Pages already exists, update instead:

```bash
gh api repos/devkunaltandon/KunalTandonAppStore/pages -X PUT -f build_type=legacy -f source[branch]=main -f source[path]=/
```

Expected: HTTP success; Pages source is `main` `/`.

- [ ] **Step 4: Verify live URL**

Wait briefly if needed, then:

```bash
curl -sI "https://devkunaltandon.github.io/KunalTandonAppStore/" | head -20
curl -sL "https://devkunaltandon.github.io/KunalTandonAppStore/" | grep -o "Privacy Policy" | head -3
```

Expected: HTTP 200 (or 200 after short propagation); page contains “Privacy Policy”.

- [ ] **Step 5: Commit plan completion note only if needed**

No further commit required unless Pages config files were added locally. Prefer documenting the live URL in the final report to the user.

---

## Spec coverage check

| Spec requirement | Task |
| --- | --- |
| Static HTML policy | Task 1 |
| Operator + email + multi-app wording | Task 1 |
| Readable styling | Task 1 (`styles.css`) |
| README with live URL | Task 1 |
| Public repo + Pages at specified URL | Task 2 |
| Play Console–ready URL | Task 2 verification |
