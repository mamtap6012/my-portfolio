# Fleet Safety Case Study Portfolio Addition Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a project card for the fleet-safety AI correction pipeline to the portfolio homepage, and a full case study page (`samsara.html`) matching the existing Navya case study's visual system and structure.

**Architecture:** Two files: one small insertion into `index.html`'s existing `.projects-grid`, and one new static HTML file (`samsara.html`) cloned structurally from `navya.html` (same head/style/nav/theme-toggle boilerplate, new body copy). No JavaScript, no build step, no new CSS — this is a plain-HTML portfolio site per `my-portfolio/CLAUDE.md`.

**Tech Stack:** Plain HTML + CSS (existing `styles.css` design tokens: `--terracotta`, `--clay`, `--espresso`, `--sand`, `--muted`, `--white`, `--font-serif`), vanilla JS theme toggle (copied verbatim from `navya.html`, no changes).

**Testing approach:** No test runner or build step exists in this project (per `my-portfolio/CLAUDE.md`: "No npm, no build steps, no bundlers... must work by simply opening index.html in a browser"). Verification is visual: open both HTML files directly via a `file://` URL in a real browser (no dev server needed — plain static HTML with no fetch calls), check content renders, check dark mode, check links and nav.

---

### Task 1: Add the project card to `index.html`

**Files:**
- Modify: `C:\Users\karth\my-portfolio\index.html` (around line 148, right after the Navya project card's closing `</div>`)

- [ ] **Step 1: Locate the exact insertion point**

Open `C:\Users\karth\my-portfolio\index.html` and find this block (currently ending around line 148):

```html
          <a class="project-cta" href="navya.html">Read case study →</a>
        </div>

        <div class="project-card">
          <div class="project-card-header">
            <span class="project-tag">Community · Real Users</span>
          </div>
          <h3 class="project-name">PM Ecosystem Job Board</h3>
```

The insertion point is between the Navya card's closing `</div>` and the `PM Ecosystem Job Board` card's opening `<div class="project-card">`.

- [ ] **Step 2: Insert the new project card**

Insert this new block between those two lines (immediately after `<a class="project-cta" href="navya.html">Read case study →</a>\n        </div>` and immediately before the PM Ecosystem Job Board `<div class="project-card">`):

```html

        <div class="project-card">
          <div class="project-card-header">
            <span class="project-tag">Fleet Safety · AI/Ops</span>
            <a class="project-link-icon" href="https://samsara-safety-pipeline.vercel.app" target="_blank" rel="noopener noreferrer" aria-label="Open Fleet Safety Correction Pipeline">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
            </a>
          </div>
          <h3 class="project-name">Fleet Safety Correction Pipeline</h3>
          <p class="project-desc">A four-stage workflow that turns AI-flagged driver safety events into a retraining signal instead of dead weight — secondary AI re-check, driver dispute, manager adjudication, and a live pipeline dashboard showing which flag patterns are worth retraining against.</p>
          <a class="project-cta" href="samsara.html">Read case study →</a>
        </div>
```

- [ ] **Step 3: Verify the HTML is well-formed**

Run: view the file section from the Navya card through the Meditation App card and confirm there are exactly 5 `<div class="project-card">` opening tags and 5 matching closing `</div>` tags in the `.projects-grid` now (Navya, Fleet Safety Correction Pipeline, PM Ecosystem Job Board, Meditation App, Sadhana App). A quick way to check: count occurrences.

```bash
grep -c 'class="project-card"' "C:\Users\karth\my-portfolio\index.html"
```

Expected: `5` (was `4` before this change).

- [ ] **Step 4: Commit**

```bash
cd /c/Users/karth/my-portfolio
git add index.html
git commit -m "feat: add fleet safety pipeline project card to homepage"
```

---

### Task 2: Create the `samsara.html` case study page

**Files:**
- Create: `C:\Users\karth\my-portfolio\samsara.html`

- [ ] **Step 1: Create the file with the following complete content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Fleet Safety Correction Pipeline — Case Study · Mamta Pandey</title>
  <link rel="stylesheet" href="styles.css" />
  <script>
    (function () {
      if (localStorage.getItem('theme') === 'dark')
        document.documentElement.setAttribute('data-theme', 'dark');
    })();
  </script>
  <style>
    /* ── Case Study Page ── */
    .cs-page {
      max-width: 720px;
      margin: 0 auto;
      padding: 72px 48px 96px;
    }

    .cs-back {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-size: 0.8rem;
      font-weight: 600;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: var(--muted);
      text-decoration: none;
      margin-bottom: 56px;
      transition: color var(--transition);
    }
    .cs-back:hover { color: var(--terracotta); }
    .cs-back svg { transition: transform var(--transition); }
    .cs-back:hover svg { transform: translateX(-3px); }

    .cs-header { margin-bottom: 56px; }

    .cs-label {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-bottom: 20px;
      flex-wrap: wrap;
    }
    .cs-label-tag {
      font-size: 0.7rem;
      font-weight: 600;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--terracotta);
      background: var(--sand);
      border: 1px solid rgba(196,168,130,0.5);
      border-radius: 999px;
      padding: 3px 12px;
    }

    .cs-page-title {
      font-family: var(--font-serif);
      font-size: clamp(2rem, 5vw, 3rem);
      font-weight: 400;
      color: var(--espresso);
      line-height: 1.15;
      letter-spacing: -0.02em;
      margin-bottom: 16px;
    }

    .cs-page-subtitle {
      font-size: 1rem;
      font-weight: 300;
      color: var(--muted);
      line-height: 1.7;
    }

    .cs-divider {
      width: 48px;
      height: 2px;
      background: linear-gradient(90deg, var(--terracotta), var(--clay));
      border-radius: 2px;
      margin: 32px 0;
    }

    /* ── Body content ── */
    .cs-body { display: flex; flex-direction: column; gap: 48px; }

    .cs-section h2 {
      font-family: var(--font-serif);
      font-size: 1.5rem;
      font-weight: 400;
      color: var(--espresso);
      letter-spacing: -0.01em;
      margin-bottom: 18px;
    }
    .cs-section h2::after {
      content: '';
      display: block;
      width: 32px;
      height: 2px;
      background: linear-gradient(90deg, var(--terracotta), var(--clay));
      border-radius: 2px;
      margin-top: 10px;
    }

    .cs-section p {
      font-size: 1rem;
      font-weight: 300;
      line-height: 1.9;
      color: var(--muted);
      margin-bottom: 16px;
    }
    .cs-section p:last-child { margin-bottom: 0; }

    .cs-section strong {
      font-weight: 600;
      color: var(--espresso);
    }

    /* Insight callout */
    .cs-callout {
      background: var(--sand);
      border-left: 3px solid var(--terracotta);
      border-radius: 0 12px 12px 0;
      padding: 20px 24px;
      margin: 8px 0;
    }
    .cs-callout p {
      font-size: 0.97rem;
      font-style: italic;
      color: var(--espresso);
      margin: 0;
      line-height: 1.75;
    }

    /* Bullet lists */
    .cs-list {
      list-style: none;
      padding: 0;
      margin: 8px 0 16px;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    .cs-list li {
      font-size: 0.97rem;
      font-weight: 300;
      line-height: 1.75;
      color: var(--muted);
      padding-left: 20px;
      position: relative;
    }
    .cs-list li::before {
      content: '';
      position: absolute;
      left: 0;
      top: 10px;
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background: var(--terracotta);
      opacity: 0.7;
    }

    /* Footer CTA */
    .cs-footer {
      margin-top: 64px;
      padding-top: 40px;
      border-top: 1px solid var(--sand);
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 16px;
    }
    .cs-footer-meta {
      font-size: 0.82rem;
      font-weight: 300;
      color: var(--clay);
      line-height: 1.7;
    }
    .cs-footer-meta a {
      color: var(--terracotta);
      text-decoration: none;
      font-weight: 500;
      transition: color var(--transition);
    }
    .cs-footer-meta a:hover { color: var(--espresso); }

    @media (max-width: 768px) {
      .cs-page { padding: 48px 24px 72px; }
      .cs-footer { flex-direction: column; align-items: flex-start; }
    }
  </style>
</head>
<body>

  <nav class="site-nav" aria-label="Page sections">
    <ul class="nav-links">
      <li><a href="index.html#about">About</a></li>
      <li><a href="index.html#journey">Journey</a></li>
      <li><a href="index.html#projects">Projects</a></li>
      <li><a href="index.html#casestudies">Case Studies</a></li>
      <li><a href="mailto:mamta.p6012@gmail.com">Contact</a></li>
    </ul>
  </nav>

  <button class="theme-toggle" id="themeToggle" aria-label="Toggle dark mode">
    <span class="icon-sun">
      <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="5"/><line x1="12" y1="1" x2="12" y2="3"/><line x1="12" y1="21" x2="12" y2="23"/><line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/><line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/><line x1="1" y1="12" x2="3" y2="12"/><line x1="21" y1="12" x2="23" y2="12"/><line x1="4.22" y1="19.78" x2="5.64" y2="18.36"/><line x1="18.36" y1="5.64" x2="19.78" y2="4.22"/></svg>
    </span>
    <span class="icon-moon">
      <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/></svg>
    </span>
  </button>

  <article class="cs-page">

    <a class="cs-back" href="index.html#projects">
      <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="19" y1="12" x2="5" y2="12"/><polyline points="12 19 5 12 12 5"/></svg>
      Back to Projects
    </a>

    <header class="cs-header">
      <div class="cs-label">
        <span class="cs-label-tag">Case Study</span>
        <span class="cs-label-tag">Fleet Safety</span>
        <span class="cs-label-tag">AI/Ops</span>
      </div>
      <h1 class="cs-page-title">Fleet Safety Correction Pipeline</h1>
      <p class="cs-page-subtitle">Designing the workflow that turns an AI false positive into a training signal instead of a dead end.</p>
      <div class="cs-divider"></div>
    </header>

    <div class="cs-body">

      <div class="cs-section">
        <h2>The Problem</h2>
        <p>Camera-based driver monitoring systems flag behaviors like phone use or inattentive driving automatically — but a meaningful share of those flags are false positives. A driver reaching for a water bottle, checking a mirror, or driving into low light and sun glare can look identical to a genuine phone-use event to a model trained on visual patterns alone.</p>
        <p>Two things tend to go wrong in these systems. First, every flag costs a human review cycle regardless of how obviously wrong it is — nobody's time gets saved on the easy cases. Second, once a flag gets dismissed as a false positive, that judgment usually evaporates. Nothing captures which patterns the model keeps getting wrong, so the same false positives keep recurring indefinitely instead of shrinking over time.</p>
        <div class="cs-callout">
          <p>The fix isn't a better model on day one. It's a workflow that captures every human correction as a labeled data point — so "the model was wrong" becomes something the system can act on, not just something a driver has to shrug off.</p>
        </div>
      </div>

      <div class="cs-section">
        <h2>The Pipeline I Designed</h2>
        <p>I designed this as four stages, each with a specific job:</p>
        <ul class="cs-list">
          <li><strong>Secondary AI check</strong> — before any human sees the flag, a second pass re-analyzes the scene description for the cheapest, most obvious false positives (an object near the face, a mirror check, a briefly obstructed camera). High-confidence false positives get auto-cleared here and never reach a person at all.</li>
          <li><strong>Driver dispute</strong> — anything the secondary check isn't confident about goes to the driver, who was actually in the vehicle. They confirm the flag is accurate, or say what actually happened, from a fixed set of reason codes.</li>
          <li><strong>Manager adjudication</strong> — escalation only for the genuinely ambiguous cases, where the model's confidence and the driver's account disagree. This is the expensive path, reserved for judgment calls that actually need a human with authority.</li>
          <li><strong>Correction dashboard</strong> — every decision (dismissed or upheld) at every stage rolls up into a pattern-level view: which flag types have the highest false-positive rate, at what confidence the model's stated certainty stops matching its actual accuracy, and which patterns have enough volume to justify a retraining pass.</li>
        </ul>
      </div>

      <div class="cs-section">
        <h2>Key Product Decisions</h2>
        <p>Two decisions from actually building this were worth calling out:</p>
        <ul class="cs-list">
          <li><strong>A free, rule-based secondary check instead of a live model call.</strong> The deployed check is pure keyword-pattern scoring against the scene description — no external API, no per-request cost. That was a deliberate trade: this pipeline is meant to run against every flagged event, not a sampled subset, so a paid model call on every single flag doesn't scale the way a cheap, honestly-labeled rule-based pass does. A live-model version of the same check exists separately, for walkthroughs where showing a genuine model call matters more than production cost.</li>
          <li><strong>Gating the driver's dispute behind an explicit yes/no choice.</strong> Originally, "is this accurate?" was a single confirm button, with dispute reason chips sitting directly below it, already clickable. That layout let a driver select a dispute reason without the system ever recording that they'd actively said the flag was wrong — confirm and dispute were two paths with only one of them requiring a real decision. Replacing it with an explicit yes/no dropdown that gates the reason chips closed a small but real gap between "the driver did this" and "the driver clicked near this."</li>
        </ul>
      </div>

      <div class="cs-section">
        <h2>What's Real vs. Simulated</h2>
        <p>Transparency on what this demo actually is:</p>
        <ul class="cs-list">
          <li><strong>Real:</strong> the four-stage pipeline logic, the rule-based secondary check (genuinely runs server-side on every request, not canned per-event), and the persistence layer — every stage transition and correction is written to and read back from a real Postgres database, so progress survives a page refresh.</li>
          <li><strong>Simulated:</strong> the confidence scores, scene descriptions, and the backfilled correction history shown on the pipeline dashboard are synthetic — built to reflect realistic false-positive patterns, not pulled from real fleet telemetry.</li>
        </ul>
      </div>

      <div class="cs-section">
        <h2>What's Next</h2>
        <p>The biggest gap right now: the driver and manager stages currently render in the same single screen, swapping content based on an event's stage — fine for a demo where one person clicks through the whole pipeline, but a real deployment would need these as genuinely separate views with their own access control, since a driver and a fleet manager are different people with different permissions. Beyond that: real telemetry instead of synthetic backfill data, and a second look at edge cases in the rule-based check as real-world scene descriptions turn out messier than the patterns it was tuned against.</p>
      </div>

    </div>

    <footer class="cs-footer">
      <div class="cs-footer-meta">
        <div>Live app → <a href="https://samsara-safety-pipeline.vercel.app" target="_blank" rel="noopener noreferrer">samsara-safety-pipeline.vercel.app</a></div>
        <div>Status: Deployed prototype</div>
      </div>
      <a class="btn btn-resume" href="index.html#projects">← Back to Projects</a>
    </footer>

  </article>

  <script>
    const toggle = document.getElementById('themeToggle');
    toggle.addEventListener('click', () => {
      const isDark = document.documentElement.getAttribute('data-theme') === 'dark';
      const next = isDark ? 'light' : 'dark';
      document.documentElement.setAttribute('data-theme', next);
      localStorage.setItem('theme', next);
    });
  </script>

</body>
</html>
```

- [ ] **Step 2: Verify the file was created correctly**

```bash
grep -c "cs-section" "C:\Users\karth\my-portfolio\samsara.html"
```

Expected: `10` (5 opening `<div class="cs-section">` + 5 closing references across the 5 sections — if the count differs, re-check the file against Step 1's content for a missed/duplicated section).

- [ ] **Step 3: Commit**

```bash
cd /c/Users/karth/my-portfolio
git add samsara.html
git commit -m "feat: add fleet safety pipeline case study page"
```

---

### Task 3: Visual verification

**Files:** none (verification only)

- [ ] **Step 1: Open the homepage directly (no server needed — plain static HTML)**

Use the `mcp__Claude_Browser__navigate` tool (or equivalent Browser-pane tool) to open:

```
file:///C:/Users/karth/my-portfolio/index.html
```

- [ ] **Step 2: Confirm the new card renders in the Projects section**

Use `read_page` or `get_page_text` to confirm the page contains "Fleet Safety Correction Pipeline" and "Fleet Safety · AI/Ops", positioned between the Navya card and the "PM Ecosystem Job Board" card.

- [ ] **Step 3: Confirm the card's external link icon points to the right URL**

Use `read_page` (filter: interactive) to find the link with `aria-label="Open Fleet Safety Correction Pipeline"` and confirm its `href` is `https://samsara-safety-pipeline.vercel.app`.

- [ ] **Step 4: Click through to the case study**

Click the "Read case study →" link under the new card. Confirm navigation lands on `samsara.html` and the page renders: title "Fleet Safety Correction Pipeline", the three header tags (Case Study, Fleet Safety, AI/Ops), and all five section headings (The Problem, The Pipeline I Designed, Key Product Decisions, What's Real vs. Simulated, What's Next).

- [ ] **Step 5: Verify dark mode toggle works on the new page**

Click the theme toggle button. Confirm (via `javascript_tool` checking `document.documentElement.getAttribute('data-theme')`, or a screenshot) that it switches to `dark` and the page's colors update (this reuses the exact toggle script from `navya.html`, so if Navya's dark mode already works, this should too — just confirm it wasn't broken by a typo in the copied script).

- [ ] **Step 6: Verify the "Back to Projects" links work**

Click both the top `cs-back` link and the bottom footer "← Back to Projects" button. Confirm both navigate to `index.html#projects`.

- [ ] **Step 7: Verify the footer's live-app link**

Confirm the footer text shows "Live app → samsara-safety-pipeline.vercel.app" as a link with `target="_blank"`.

- [ ] **Step 8: Check mobile responsiveness**

Use `resize_window` (or equivalent) to a mobile width (375px) and take a screenshot of both `index.html`'s projects section and `samsara.html`. Confirm the new project card and the case study page's `.cs-footer` stack vertically without overflow, matching the existing `@media (max-width: 768px)` rules already present in both the shared `styles.css` and the page-local `<style>` block.

---

## Self-Review Notes (for the plan author, not a task)

- Spec coverage: card content (Task 1), full case study copy including all 5 sections from the spec (Task 2), honesty constraint on real-vs-simulated correctly reflects rule-based (not live-model) check (Task 2 Step 1), generic framing with no company name anywhere in the new copy (Task 1 + Task 2), link-icon-only to live app with no GitHub link (Task 1 Step 2) — all covered.
- No test runner exists in this repo; visual/browser verification (Task 3) is the correct substitute, matching this project's actual tooling (plain HTML, no build step).
