# Intel Edge Advisor — portfolio addition design

## Problem

The portfolio doesn't yet include the Edge AI Deployment Readiness Advisor
(deployed separately at `intel-edge-advisor`, live at
`https://intel-edge-advisor.vercel.app`). It should get the same card + case
study treatment already established for the Fleet Safety Correction Pipeline
and Navya, with sections adapted where this project's actual shape differs
(no backend, no database, purely client-side).

## Scope

Two files in `my-portfolio`:
- `index.html` — add one new `.project-card` to the `.projects-grid`, after
  the Fleet Safety Correction Pipeline card and before the PM Ecosystem Job
  Board card.
- `intel-edge-advisor.html` (new file) — a case study page, structurally
  cloned from `samsara.html`/`navya.html` (same head/style/nav/theme-toggle
  boilerplate), with new copy.

No changes to `styles.css` or any other existing file.

## Constraints from user decisions

- **Framing:** name Intel explicitly. Unlike the fleet-safety project, this
  tool is inherently and inseparably Intel-branded (Intel blue `#0068B5`,
  Intel logo mark, and direct references throughout to real Intel products —
  OpenVINO, DL Streamer, Edge Microvisor Toolkit, Edge Manageability
  Framework, Geti, SceneScape, the Open Edge Platform vertical AI suites).
  Genericizing it would misrepresent what was built and create an
  inconsistency between the live tool and the case study.
- **Tag:** `Enterprise AI · Intel Open Edge`
- **Link:** the project card's external link icon points to the live app
  (`https://intel-edge-advisor.vercel.app`) only. No source-code link — the
  project has no GitHub repo (confirmed: no `.git` directory exists locally).
- **Section adaptation:** the established case-study template's "What's Real
  vs. Simulated" section doesn't map cleanly onto this project — it has no
  backend, no database, and no synthetic/simulated data (unlike the
  fleet-safety pipeline's synthetic confidence scores and backfilled
  correction history). Replace that section with "How It's Built," honestly
  describing the tool as 100% client-side with no persistence — this is
  still a transparency section in spirit, just answering a different
  question (what's the tool's actual architecture) rather than "what's fake."
- **Accuracy constraint:** the tool's scoring engine (verified by reading
  `intel-edge-advisor/index.html`'s `sInfra`, `sModel`, `sSec`, `sSkills`,
  `sOps` functions) is pure deterministic arithmetic over form inputs — no
  API call, no model inference, nothing external. The case study must
  describe this as rule-based/deterministic scoring, not as an "AI-powered"
  assessment engine, even though the tool's subject matter is AI deployment.
  This mirrors the same honesty standard already applied to the fleet-safety
  pipeline's rule-based secondary check.

## Content — index.html project card

Insert after the Fleet Safety Correction Pipeline card's closing `</div>`
and before the PM Ecosystem Job Board card:

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

(same generic external-link SVG glyph reused verbatim from the other cards)

## Content — intel-edge-advisor.html case study

Same head boilerplate, dark-mode script, nav, theme-toggle, `.cs-page`
layout, and footer script as `samsara.html`, copied verbatim (matches the
already-accepted pattern of duplicating this shared block rather than
extracting it, per the fleet-safety case study's precedent).

Title: `Edge AI Deployment Readiness Advisor — Case Study · Mamta Pandey`

**Header:**
- Tags: `Case Study`, `Enterprise AI`, `Intel Open Edge`
- Title: `Edge AI Deployment Readiness Advisor`
- Subtitle: `Turning a 30+ component platform into a five-minute self-assessment with one clear next step.`

**Section: The Problem**
```
Intel's Open Edge Platform is powerful but sprawling — OpenVINO for model
optimization, DL Streamer for media pipelines, Edge Microvisor Toolkit for
secure runtimes, Edge Manageability Framework for fleet orchestration, Geti
for model training, SceneScape for multi-camera tracking, and
vertical-specific AI suites spanning manufacturing, healthcare, retail,
smart cities, robotics, federal, and education. For a team evaluating
whether to build on it, that's a lot of surface area with no obvious entry
point.

Two questions come up constantly, and neither has a self-serve answer
today: are we actually ready to move from pilot to production, and if not,
what's the one thing to fix first? Teams without a good answer tend to
guess — racing into infrastructure investment before their model is
edge-ready, or stalling on infrastructure decisions while an
already-optimized model sits idle.
```
(callout)
```
The right next step depends entirely on where a team's weakest link
actually is — and that's rarely obvious from the outside, to the team or to
whoever is trying to help them.
```

**Section: What I Built**
```
I designed this as a four-step assessment that produces a scored,
prioritized report:
```
- `cs-list`:
  - **Use case & stage** — what they're building, their industry vertical,
    and how far along they are (concept through active scaling).
  - **Infrastructure & scale** — target node count, network connectivity at
    the edge, and existing IT foundation (Kubernetes, on-prem, cloud,
    legacy OT, or greenfield).
  - **AI model & data** — model readiness (from "no model yet" to "already
    optimized for edge"), latency requirements, and data sensitivity.
  - **Team & security** — the team's hands-on experience with the Intel
    stack specifically, and compliance requirements.

```
From those inputs, five dimensions get scored — infrastructure, model
readiness, security, team skills, and scale/ops — each against a
transparent, visible rubric. The overall score drives three outputs: the
top blockers standing between the team and production, tailored Intel
component recommendations (which suite, which tool, and why), and a
personalized getting-started path — a five-step guide selected from
fourteen tracks (one of two paths, model-optimization-first or
team-onboarding-first, for each of seven verticals), chosen automatically
based on whichever dimension scored weakest.
```

**Section: Key Product Decisions**
```
Two decisions from actually building this were worth calling out:
```
- `cs-list`:
  - **Fully deterministic, rule-based scoring instead of an opaque model
    call.** Every score comes from a visible, documented rubric — the
    report includes a "how each dimension is scored" methodology box, not
    just a number. For a B2B tool where a technical buyer is deciding
    whether to trust a recommendation, showing your work matters more than
    sounding sophisticated.
  - **Branching the getting-started path on the weakest dimension, not just
    the industry vertical.** A team with a strong model but zero Intel-stack
    experience needs a genuinely different next step than a team with an
    experienced team but an unoptimized model — even in the same industry.
    Personalizing on the actual bottleneck, not just the vertical, is what
    makes the recommendation feel earned instead of generic.
```

**Section: How It's Built**
```
This tool is 100% client-side — no server, no database, nothing submitted
or stored anywhere. Every input lives only in the browser tab for the
duration of the session; refreshing the page clears it. All fourteen
getting-started paths (seventy individually written steps across verticals
and tracks) and every linked resource are real, genuine Intel documentation
URLs — nothing here is placeholder content. The scoring itself is rule-based
arithmetic, not a live model call — this is an assessment *of* AI deployment
readiness, not itself an AI system.
```

**Section: What's Next**
```
No persistence means a user loses their assessment on refresh — a real
version of this would want to let someone save or share a report rather
than re-answer nine questions if they close the tab. The scoring weights
and the getting-started path content are also currently my own judgment
calls, built from Intel's public documentation and product positioning, not
validated against real deployment outcomes — the next honest step would be
testing the recommendations against actual pilot-to-production journeys and
adjusting the weights where reality disagrees with the model.
```

**Footer:**
```html
<div>Live app → <a href="https://intel-edge-advisor.vercel.app" target="_blank" rel="noopener noreferrer">intel-edge-advisor.vercel.app</a></div>
<div>Status: Deployed prototype</div>
```
Back-to-projects button identical to the other case study pages.

## Out of scope

- No changes to `navya.html`, `samsara.html`, `styles.css`, or any other
  existing content.
- No changes to the `intel-edge-advisor` project itself (already deployed;
  this task only adds portfolio content that links to it).
- No git repo setup for `intel-edge-advisor` — the user only asked to add
  this project to the portfolio, not to replicate the full deployment
  pipeline (git init, GitHub push) that `samsara-safety-pipeline` went
  through. If that's wanted later, it's a separate request.
- No new shared stylesheet extraction for the duplicated `.cs-*` CSS block —
  same accepted tradeoff as the fleet-safety case study.
