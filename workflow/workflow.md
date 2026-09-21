# BikoWWW Workflow

Multi-persona workflow for developing/maintaining BikoWWW — a static,
no-build, dependency-free, 19-language site (see
`.github/copilot-instructions.md` for the technical structure this assumes:
`docs/` as site root, `docs/index/<lang>.json` +
`docs/formal/<doc-type>/<lang>.json` content models, one stylesheet per page
family).

## How to run

1. Match the request to a scenario in [Scenario Selection](#scenario-selection);
   open its file in `scenarios/` and load only the persona files it lists
   (from `personas/`).
2. Run **Process** as a real discussion — Reviewers give concrete critique,
   the **Lead** resolves disagreements and owns sign-off.
3. Any visual/artistic deliverable must clear the
   [Product Owner Approval Gate](#product-owner-approval-gate-hard-rule)
   before implementation, regardless of scenario.

Global Instructions below govern every scenario; a scenario file only states
what's scenario-specific.

## Scenario Selection

| Scenario | Trigger signals | File |
|---|---|---|
| Technical Implementation | New feature, bug fix, refactor, markup/script/behavior change with no look-and-feel impact | [scenario-technical-implementation.md](scenarios/scenario-technical-implementation.md) |
| Visual / Artistic Change | Redesign, new colors/typography/spacing/layout, imagery style, animation/micro-interaction, "make it look better", any creative visual proposal | [scenario-visual-artistic-change.md](scenarios/scenario-visual-artistic-change.md) |
| Content & Localization | New/edited copy, new language content, legal document text change, translation update, key additions to `index/` or `formal/` JSON | [scenario-content-localization.md](scenarios/scenario-content-localization.md) |
| SEO & Metadata Audit | Meta tags, sitemap, structured data, `hreflang`, canonical URLs, ranking/search-visibility concerns | [scenario-seo-metadata-audit.md](scenarios/scenario-seo-metadata-audit.md) |
| Performance & File Optimization | Reduce file/request count, dedupe CSS/JS across page families, asset/payload size concerns | [scenario-performance-file-optimization.md](scenarios/scenario-performance-file-optimization.md) |
| Trend Review | "What's new in HTML/CSS/JS", periodic trend scan, competitive/visual inspiration gathering | [scenario-trend-review.md](scenarios/scenario-trend-review.md) |
| Responsive / Cross-Device Audit | "Check this on mobile/tablet", full-site device sweep, layout-breakage reports | [scenario-responsive-audit.md](scenarios/scenario-responsive-audit.md) |

### Typical pipeline order

Trend Review (optional, advisory) → **Technical Implementation** or
**Visual/Artistic Change** (split mixed requests) → **Responsive/Cross-Device
Audit** (verification). **Content & Localization** and **SEO & Metadata
Audit** can run independently at any point.

- If a request is ambiguous about visual vs. technical intent, ask before
  picking a scenario.
- After a scenario completes, ask the user before continuing automatically to
  the next one — never continue silently.

## Global Instructions

Apply to every scenario unless it explicitly overrides them.

### Team composition

One **Lead** (confirms scope, resolves disagreements, owns sign-off) + one
**Author** (drafts/implements) + one or more **Reviewers** (concrete,
domain-specific critique — never a rubber stamp). A Reviewer that adds no
value for a given request is dropped explicitly, not silently. If a task
needs a persona that doesn't exist, add one under `personas/` in the same
format rather than stretching an existing one.

### Product Owner Approval Gate (hard rule)

**Product Owner** = the human user — no persona file for this role. Any
deliverable changing look-and-feel (colors, typography, spacing/layout,
imagery/iconography, animation, new visual components) must be presented to
the Product Owner as a description/mockup/diff and get **explicit approval
before implementation** — never assumed, never pre-implemented "to save a
round trip." Purely technical work (structure, code quality, performance,
SEO mechanics, i18n wiring, bug fixes) skips this gate even when done by a
persona who also does visual work. Split mixed requests: implement the
technical part directly, gate only the visual part.

### Cross-device responsiveness (hard rule)

Every page must render correctly at ~360px, ~768px, ~1024px, ~1440px+, both
orientations. Responsive/Cross-Device QA Reviewer
(`personas/responsive-qa-reviewer.md`) is a **mandatory** Reviewer for any
change touching `docs/*.html` or `docs/css/*` — never dropped for those.

### 19-language consistency (hard rule)

Every home-page key (`docs/index/<lang>.json`) and every formal document
(`docs/formal/<doc-type>/<lang>.json`) stays parallel across all 19
languages; a formal document's `version` is bumped identically everywhere
(`MINOR` = editorial, `MAJOR` = legal-meaning/scope change). Language
list/cookies/chrome UI strings live only in `docs/js/language.js`. Content
renders via `createElement`/`textContent` only, never `innerHTML`.

### No-build / dependency-free constraint

No bundler, package manager, or framework without explicit Product Owner
approval — treat that as an architecture decision escalated through Site
Architect, not a normal technical call.

### Ambiguity handling

Ask the user rather than guess, unless the ambiguity is trivial and the
default is safely reversible.

### Standard process

Unless a scenario overrides it: **Intake** (Author restates the request,
flags unknowns) → **Framing** (Lead confirms scope) → **Draft/Implement**
(Author produces the deliverable, flags open questions inline) → **Review**
(each Reviewer gives concrete critique) → **Resolve** (Author fixes;
unresolved disagreement escalates to Lead) → **Sign-off** (Lead approves or
sends back with specific feedback; visual deliverables additionally need the
Approval Gate).

### Commit message format

Short, imperative, no ticket-ID prefixes, matching existing `git log` style
(e.g. `Add sitemap.xml`, `Fix hreflang tags on support page`).

### Verification

No build/lint/test command exists. Validate by opening the affected
`docs/*.html` directly, or serving `docs/` with a static file server —
`fetch()` needs `http(s)://`, not `file://`. Scenario files add specifics
(viewport widths, metadata checks, locale parity).

### Output housekeeping

Changes land directly in `docs/...`; no planning/notes files unless the user
asks. Update `.github/copilot-instructions.md` in the same commit if a
documented convention changes.
