# Fleet safety correction pipeline — portfolio addition design

## Problem

The portfolio (`my-portfolio`) doesn't yet include the fleet-safety AI correction
pipeline project (deployed separately at `samsara-safety-pipeline`). It should get
the same treatment as the Navya project: a card on the homepage and a full case
study page.

## Scope

Two files in `my-portfolio`:
- `index.html` — add one new `.project-card` to the `.projects-grid` (after the
  Navya card, before the PM Ecosystem Job Board card).
- `samsara.html` (new file) — a case study page cloned structurally from
  `navya.html` (same `<head>`, dark-mode script, nav, theme toggle, `.cs-page`
  layout), with new copy.

No changes to `styles.css` — all classes needed (`cs-page`, `cs-back`, `cs-header`,
`cs-label`, `cs-label-tag`, `cs-page-title`, `cs-page-subtitle`, `cs-divider`,
`cs-body`, `cs-section`, `cs-callout`, `cs-list`, `cs-footer`, `cs-footer-meta`,
`btn btn-resume`, `.project-card`, `.project-card-header`, `.project-tag`,
`.project-link-icon`, `.project-name`, `.project-desc`, `.project-cta`) already
exist and are reused as-is.

## Constraints from user decisions

- **Framing:** generic — do not name the target company. Describe it as a
  fleet-safety / driver-monitoring AI correction pipeline.
- **Tag:** `Fleet Safety · AI/Ops`
- **Link:** the project card's external link icon points to the live app
  (`https://samsara-safety-pipeline.vercel.app`) only. No GitHub link — the repo
  is private.
- **Honesty constraint:** the source README claims (in one section) that the
  secondary check is "a real, live model call," while another section of the
  same README and the actual code (`api/secondary-check.js`) confirm it's a
  pure rule-based keyword scorer with no external API call. The case study must
  describe the deployed check as rule-based (the verified-accurate claim), and
  may mention that a separate live-model version exists as a disconnected
  Claude.ai artifact for interview walkthroughs — it must not claim the
  deployed app itself makes a live model call.
- **No fabricated research:** unlike Navya (13 real user conversations from a
  buildathon), this project has no user interviews behind it — it's a
  self-directed solo build. The case study must not imply user research that
  didn't happen. Frame the "problem" section around well-known, publicly
  documented patterns in AI-flagged driver-monitoring systems (false positive
  rates, driver trust erosion, lack of feedback loops) rather than claimed
  primary research.

## Content — index.html project card

Insert after the Navya `.project-card` closing `</div>` (currently ends at line
148) and before the PM Ecosystem Job Board card:

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

(exact SVG icon reused verbatim from the Navya card, same viewBox/paths — it's a
generic "external link" glyph, not brand-specific)

## Content — samsara.html case study

Same `<head>` boilerplate as `navya.html` (dark-mode init script, `styles.css`
link, same inline `<style>` block for `.cs-*` classes — copy verbatim, this is
shared page-scoped CSS that both case study pages currently duplicate rather
than sharing a stylesheet, matching the existing pattern in this codebase), same
nav/theme-toggle markup, same `.cs-footer` / closing `<script>` for the toggle.

Title: `Fleet Safety Correction Pipeline — Case Study · Mamta Pandey`

**Header:**
- Tags: `Case Study`, `Fleet Safety`, `AI/Ops`
- Title: `Fleet Safety Correction Pipeline`
- Subtitle: `Designing the workflow that turns an AI false positive into a training signal instead of a dead end.`

**Section: The Problem**
```
Camera-based driver monitoring systems flag behaviors like phone use or
inattentive driving automatically — but a meaningful share of those flags are
false positives. A driver reaching for a water bottle, checking a mirror, or
driving into low light and sun glare can look identical to a genuine
phone-use event to a model trained on visual patterns alone.

Two things tend to go wrong in these systems. First, every flag costs a human
review cycle regardless of how obviously wrong it is — nobody's time gets
saved on the easy cases. Second, once a flag gets dismissed as a false
positive, that judgment usually evaporates. Nothing captures which patterns
the model keeps getting wrong, so the same false positives keep recurring
indefinitely instead of shrinking over time.
```
(callout)
```
The fix isn't a better model on day one. It's a workflow that captures every
human correction as a labeled data point — so "the model was wrong" becomes
something the system can act on, not just something a driver has to shrug off.
```

**Section: The Pipeline I Designed**
```
I designed this as four stages, each with a specific job:
```
- `cs-list`:
  - **Secondary AI check** — before any human sees the flag, a second pass
    re-analyzes the scene description for the cheapest, most obvious false
    positives (an object near the face, a mirror check, a briefly obstructed
    camera). High-confidence false positives get auto-cleared here and never
    reach a person at all.
  - **Driver dispute** — anything the secondary check isn't confident about
    goes to the driver, who was actually in the vehicle. They confirm the
    flag is accurate, or say what actually happened, from a fixed set of
    reason codes.
  - **Manager adjudication** — escalation only for the genuinely ambiguous
    cases, where the model's confidence and the driver's account disagree.
    This is the expensive path, reserved for judgment calls that actually
    need a human with authority.
  - **Correction dashboard** — every decision (dismissed or upheld) at every
    stage rolls up into a pattern-level view: which flag types have the
    highest false-positive rate, at what confidence the model's stated
    certainty stops matching its actual accuracy, and which patterns have
    enough volume to justify a retraining pass.

**Section: Key Product Decisions**
```
Two decisions from actually building this were worth calling out:
```
- `cs-list`:
  - **A free, rule-based secondary check instead of a live model call.** The
    deployed check is pure keyword-pattern scoring against the scene
    description — no external API, no per-request cost. That was a deliberate
    trade: this pipeline is meant to run against every flagged event, not a
    sampled subset, so a paid model call on every single flag doesn't scale
    the way a cheap, honestly-labeled rule-based pass does. A live-model
    version of the same check exists separately, for walkthroughs where
    showing a genuine model call matters more than production cost.
  - **Gating the driver's dispute behind an explicit yes/no choice.**
    Originally, "is this accurate?" was a single confirm button, with dispute
    reason chips sitting directly below it, already clickable. That layout
    let a driver select a dispute reason without the system ever recording
    that they'd actively said the flag was wrong — confirm and dispute were
    two paths with only one of them requiring a real decision. Replacing it
    with an explicit yes/no dropdown that gates the reason chips closed a
    small but real gap between "the driver did this" and "the driver clicked
    near this."

**Section: What's Real vs. Simulated**
```
Transparency on what this demo actually is:
```
- `cs-list`:
  - **Real:** the four-stage pipeline logic, the rule-based secondary check
    (genuinely runs server-side on every request, not canned per-event), and
    the persistence layer — every stage transition and correction is written
    to and read back from a real Postgres database, so progress survives a
    page refresh.
  - **Simulated:** the confidence scores, scene descriptions, and the
    backfilled correction history shown on the pipeline dashboard are
    synthetic — built to reflect realistic false-positive patterns, not pulled
    from real fleet telemetry.

**Section: What's Next**
```
The biggest gap right now: the driver and manager stages currently render in
the same single screen, swapping content based on an event's stage — fine for
a demo where one person clicks through the whole pipeline, but a real
deployment would need these as genuinely separate views with their own access
control, since a driver and a fleet manager are different people with
different permissions. Beyond that: real telemetry instead of synthetic
backfill data, and a second look at edge cases in the rule-based check as
real-world scene descriptions turn out messier than the patterns it was
tuned against.
```

**Footer:**
```html
<div>Live app → <a href="https://samsara-safety-pipeline.vercel.app" target="_blank" rel="noopener noreferrer">samsara-safety-pipeline.vercel.app</a></div>
<div>Status: Deployed prototype</div>
```
Back-to-projects button identical to Navya's.

## Out of scope

- No changes to `navya.html`, `styles.css`, or any other existing content.
- No changes to the `samsara-safety-pipeline` project itself (already deployed;
  this task only adds portfolio content that links to it).
- No new shared stylesheet extraction for the duplicated `.cs-*` CSS block —
  matches the existing pattern where `navya.html` already duplicates this
  rather than sharing a file. Not this task's job to refactor that.
