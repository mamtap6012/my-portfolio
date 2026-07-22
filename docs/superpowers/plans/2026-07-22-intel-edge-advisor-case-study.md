# Intel Edge Advisor Case Study Portfolio Addition Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a project card for the Edge AI Deployment Readiness Advisor to the portfolio homepage, and a full case study page (`intel-edge-advisor.html`) matching the existing case-study pages' visual system.

**Architecture:** Two files: one insertion into `index.html`'s existing `.projects-grid` (after the Fleet Safety Correction Pipeline card, before PM Ecosystem Job Board), and one new static HTML file (`intel-edge-advisor.html`) cloned structurally from `samsara.html` (same head/style/nav/theme-toggle boilerplate, new body copy). No JavaScript, no build step, no new CSS.

**Tech Stack:** Plain HTML + CSS (existing `styles.css` design tokens), vanilla JS theme toggle (copied verbatim, no changes).

**Testing approach:** No test runner or build step exists in this project. Verification is visual: serve the site locally via the project's `.claude/launch.json` `my-portfolio` config (already set up from the prior fleet-safety case study task) and check rendering, links, dark mode, and mobile layout in a real browser.

---

### Task 1: Add the project card to `index.html`

**Files:**
- Modify: `C:\Users\karth\my-portfolio\index.html` (around line 160, right after the Fleet Safety Correction Pipeline card's closing `</div>`)

- [ ] **Step 1: Locate the exact insertion point**

Open `C:\Users\karth\my-portfolio\index.html` and find this block (currently at lines 150-162):

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

        <div class="project-card">
          <div class="project-card-header">
            <span class="project-tag">Community · Real Users</span>
          </div>
          <h3 class="project-name">PM Ecosystem Job Board</h3>
```

The insertion point is between the Fleet Safety card's closing `</div>` and the PM Ecosystem Job Board card's opening `<div class="project-card">`.

- [ ] **Step 2: Insert the new project card**

Insert this new block between those two lines:

```html

        <div class="project-card">
          <div class="project-card-header">
            <span class="project-tag">Enterprise AI · Intel Open Edge</span>
            <a class="project-link-icon" href="https://intel-edge-advisor.vercel.app" target="_blank" rel="noopener noreferrer" aria-label="Open Edge AI Deployment Readiness Advisor">
              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
            </a>
          </div>
          <h3 class="project-name">Edge AI Deployment Readiness Advisor</h3>
          <p class="project-desc">A self-serve readiness assessment for teams evaluating Intel's Open Edge Platform — scores five deployment dimensions, surfaces blockers, and generates a personalized getting-started path across seven industry verticals.</p>
          <a class="project-cta" href="intel-edge-advisor.html">Read case study →</a>
        </div>
```

- [ ] **Step 3: Verify the HTML is well-formed**

```bash
grep -c 'class="project-card"' "C:\Users\karth\my-portfolio\index.html"
```

Expected: `6` (was `5` before this change: Navya, Fleet Safety Correction Pipeline, PM Ecosystem Job Board, Meditation App, Sadhana App, now plus Edge AI Deployment Readiness Advisor).

- [ ] **Step 4: Commit**

```bash
cd /c/Users/karth/my-portfolio
git add index.html
git commit -m "feat: add Intel Edge Advisor project card to homepage"
```

---

### Task 2: Create the `intel-edge-advisor.html` case study page

**Files:**
- Create: `C:\Users\karth\my-portfolio\intel-edge-advisor.html`

- [ ] **Step 1: Create the file with the following complete content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Edge AI Deployment Readiness Advisor — Case Study · Mamta Pandey</title>
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
        <span class="cs-label-tag">Enterprise AI</span>
        <span class="cs-label-tag">Intel Open Edge</span>
      </div>
      <h1 class="cs-page-title">Edge AI Deployment Readiness Advisor</h1>
      <p class="cs-page-subtitle">Turning a 30+ component platform into a five-minute self-assessment with one clear next step.</p>
      <div class="cs-divider"></div>
    </header>

    <div class="cs-body">

      <div class="cs-section">
        <h2>The Problem</h2>
        <p>Intel's Open Edge Platform is powerful but sprawling — OpenVINO for model optimization, DL Streamer for media pipelines, Edge Microvisor Toolkit for secure runtimes, Edge Manageability Framework for fleet orchestration, Geti for model training, SceneScape for multi-camera tracking, and vertical-specific AI suites spanning manufacturing, healthcare, retail, smart cities, robotics, federal, and education. For a team evaluating whether to build on it, that's a lot of surface area with no obvious entry point.</p>
        <p>Two questions come up constantly, and neither has a self-serve answer today: are we actually ready to move from pilot to production, and if not, what's the one thing to fix first? Teams without a good answer tend to guess — racing into infrastructure investment before their model is edge-ready, or stalling on infrastructure decisions while an already-optimized model sits idle.</p>
        <div class="cs-callout">
          <p>The right next step depends entirely on where a team's weakest link actually is — and that's rarely obvious from the outside, to the team or to whoever is trying to help them.</p>
        </div>
      </div>

      <div class="cs-section">
        <h2>What I Built</h2>
        <p>I designed this as a four-step assessment that produces a scored, prioritized report:</p>
        <ul class="cs-list">
          <li><strong>Use case & stage</strong> — what they're building, their industry vertical, and how far along they are (concept through active scaling).</li>
          <li><strong>Infrastructure & scale</strong> — target node count, network connectivity at the edge, and existing IT foundation (Kubernetes, on-prem, cloud, legacy OT, or greenfield).</li>
          <li><strong>AI model & data</strong> — model readiness (from "no model yet" to "already optimized for edge"), latency requirements, and data sensitivity.</li>
          <li><strong>Team & security</strong> — the team's hands-on experience with the Intel stack specifically, and compliance requirements.</li>
        </ul>
        <p>From those inputs, five dimensions get scored — infrastructure, model readiness, security, team skills, and scale/ops — each against a transparent, visible rubric. The overall score drives three outputs: the top blockers standing between the team and production, tailored Intel component recommendations (which suite, which tool, and why), and a personalized getting-started path — a five-step guide selected from fourteen tracks (one of two paths, model-optimization-first or team-onboarding-first, for each of seven verticals), chosen automatically based on whichever dimension scored weakest.</p>
      </div>

      <div class="cs-section">
        <h2>Key Product Decisions</h2>
        <p>Two decisions from actually building this were worth calling out:</p>
        <ul class="cs-list">
          <li><strong>Fully deterministic, rule-based scoring instead of an opaque model call.</strong> Every score comes from a visible, documented rubric — the report includes a "how each dimension is scored" methodology box, not just a number. For a B2B tool where a technical buyer is deciding whether to trust a recommendation, showing your work matters more than sounding sophisticated.</li>
          <li><strong>Branching the getting-started path on the weakest dimension, not just the industry vertical.</strong> A team with a strong model but zero Intel-stack experience needs a genuinely different next step than a team with an experienced team but an unoptimized model — even in the same industry. Personalizing on the actual bottleneck, not just the vertical, is what makes the recommendation feel earned instead of generic.</li>
        </ul>
      </div>

      <div class="cs-section">
        <h2>How It's Built</h2>
        <p>This tool is 100% client-side — no server, no database, nothing submitted or stored anywhere. Every input lives only in the browser tab for the duration of the session; refreshing the page clears it. All fourteen getting-started paths (seventy individually written steps across verticals and tracks) and every linked resource are real, genuine Intel documentation URLs — nothing here is placeholder content. The scoring itself is rule-based arithmetic, not a live model call — this is an assessment <em>of</em> AI deployment readiness, not itself an AI system.</p>
      </div>

      <div class="cs-section">
        <h2>What's Next</h2>
        <p>No persistence means a user loses their assessment on refresh — a real version of this would want to let someone save or share a report rather than re-answer nine questions if they close the tab. The scoring weights and the getting-started path content are also currently my own judgment calls, built from Intel's public documentation and product positioning, not validated against real deployment outcomes — the next honest step would be testing the recommendations against actual pilot-to-production journeys and adjusting the weights where reality disagrees with the model.</p>
      </div>

    </div>

    <footer class="cs-footer">
      <div class="cs-footer-meta">
        <div>Live app → <a href="https://intel-edge-advisor.vercel.app" target="_blank" rel="noopener noreferrer">intel-edge-advisor.vercel.app</a></div>
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
grep -c "cs-section" "C:\Users\karth\my-portfolio\intel-edge-advisor.html"
```

Expected: `10` (5 opening `<div class="cs-section">` + 5 `.cs-section` CSS selector references — if the count differs, re-check the file against Step 1's content for a missed/duplicated section).

- [ ] **Step 3: Commit**

```bash
cd /c/Users/karth/my-portfolio
git add intel-edge-advisor.html
git commit -m "feat: add Intel Edge Advisor case study page"
```

---

### Task 3: Visual verification

**Files:** none (verification only)

- [ ] **Step 1: Start the local static server**

The project already has a `.claude/launch.json` entry named `my-portfolio` (added during the fleet-safety case study task) serving this directory on port 5544. Use the `preview_start` MCP tool with name `my-portfolio` to start it (or confirm it's already running via `preview_list`).

- [ ] **Step 2: Confirm the new card renders in the Projects section**

Navigate to `http://localhost:5544/`. Use `read_page` (filter: all) to confirm the page contains "Edge AI Deployment Readiness Advisor" and "Enterprise AI · Intel Open Edge", positioned between the Fleet Safety Correction Pipeline card and the "PM Ecosystem Job Board" card.

- [ ] **Step 3: Confirm the card's external link icon points to the right URL**

In the same `read_page` output, confirm the link with `aria-label="Open Edge AI Deployment Readiness Advisor"` has `href="https://intel-edge-advisor.vercel.app"`, and the "Read case study →" link has `href="intel-edge-advisor.html"`.

- [ ] **Step 4: Click through to the case study**

Click "Read case study →" under the new card (or navigate directly to `http://localhost:5544/intel-edge-advisor.html`). Confirm the page renders: title "Edge AI Deployment Readiness Advisor", the three header tags (Case Study, Enterprise AI, Intel Open Edge), and all five section headings (The Problem, What I Built, Key Product Decisions, How It's Built, What's Next).

- [ ] **Step 5: Verify dark mode toggle works on the new page**

Click the theme toggle button. Confirm via `javascript_tool` (`document.documentElement.getAttribute('data-theme')` should return `"dark"`) and a screenshot that colors update correctly.

- [ ] **Step 6: Verify the "Back to Projects" links work**

Click both the top `cs-back` link and the bottom footer "← Back to Projects" button. Confirm both navigate to `index.html#projects`.

- [ ] **Step 7: Verify the footer's live-app link**

Confirm the footer shows "Live app → intel-edge-advisor.vercel.app" as a link with `target="_blank"`, matching the pattern on the other case study pages.

- [ ] **Step 8: Check mobile responsiveness**

Use `resize_window` to a mobile width (375px). Screenshot both the homepage's projects section (confirm the new card stacks cleanly with no overflow) and the case study page (confirm section headings and footer stack correctly, matching the existing `@media (max-width: 768px)` rules already present in the page).

- [ ] **Step 9: Stop the server**

Use `preview_stop` on the server started in Step 1.

---

## Self-Review Notes (for the plan author, not a task)

- Spec coverage: card content (Task 1), full case study copy including all 5 adapted sections (Task 2), Intel named explicitly per the approved design decision, no GitHub link (no repo exists), accuracy constraint on rule-based (not AI-powered) scoring correctly reflected in the "How It's Built" section copy — all covered.
- No test runner exists in this repo; visual/browser verification (Task 3) is the correct substitute, reusing the same `my-portfolio` launch.json server config already proven to work for the fleet-safety case study's verification.
