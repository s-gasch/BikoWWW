# BikoWWW — Copilot instructions

Marketing/support website for **BikePilot** (iOS cycling computer app), published at
`bike-pilot.eu` via GitHub Pages. There is no build step, package manager, bundler,
test suite, or CI — it is deliberately a static, dependency-free site.

Always use the multi-persona workflow in
[`workflow/workflow.md`](../workflow/workflow.md) when working on this
project — it defines the persona team, process, and required approvals
(notably: any visual/artistic change requires explicit Product Owner
sign-off before implementation; purely technical work does not).

## Structure

- Pages source is the `docs/` folder (GitHub Pages serves from `docs/` on the default
  branch; `docs/CNAME` pins the custom domain). Treat `docs/` as site root — all
  relative links/fetches (`css/...`, `js/...`, `index/...`, `formal/...`) resolve
  from there.
- Top-level pages: `docs/index.html` (home), `docs/privacy-policy.html`,
  `docs/terms-of-use.html`, `docs/support.html`.
- `docs/js/language.js` — shared runtime: supported-language list, language
  detection/resolution, the `bp_lang`/`bp_consent` cookies, and the UI-string table
  used for chrome text (nav, footer, consent banner) in all 19 locales.
- `docs/js/home.js` — renders the home page from `docs/index/<lang>.json` using
  `data-i18n` (text content) / `data-i18n-attr="attr:path"` (attribute) hooks in the
  HTML.
- `docs/js/formal.js` — renders privacy-policy/terms-of-use/support pages from
  `docs/formal/<doc-type>/<lang>.json` using a structured block/run document model
  (see below). `docs/js/support.js` just imports `formal.js` and is the extension
  point for support-page-only behavior.
- `docs/css/` — one stylesheet per page family (`index.css`, `formal.css`,
  `support.css`); `formal.css` is shared by privacy-policy/terms-of-use/support.

## Content model (formal documents)

`docs/formal/<doc-type>/<lang>.json` (doc-type: `privacy-policy`, `terms-of-use`,
`support`) has the shape:
```
{ title: string, version: "MAJOR.MINOR", blocks: Block[] }
```
- `Block` is one of `heading` (`level: 2|3`), `paragraph` (`runs`), `list`
  (`ordered`, `items: Run[][]`), `table` (`headers`, `rows: Run[][][]`).
- `Run` is `{ text, bold?, italic?, code?, href?, break? }` — never raw HTML.
- **Every one of the 19 language files for a given doc-type must share the same
  `version`.** Bump `MINOR` for editorial/cosmetic changes, `MAJOR` when the legal
  meaning/scope changes.
- Content is rendered via `document.createElement`/`textContent` only — never
  `innerHTML` — to keep the model injection-safe (`validateDocumentModel` in
  `formal.js` fails fast on unknown block/run keys or a malformed `version`).
- When adding/editing a formal document, update all 19 language JSON files under
  that `doc-type` together, keeping the same `version`.

## i18n conventions

- Supported languages/cookie/consent logic live only in `language.js`; don't
  duplicate language lists or cookie handling elsewhere.
- Home page copy keys are addressed by dotted path (e.g. `hero.lead`,
  `features.0.title`) matching the JSON structure in `docs/index/<lang>.json` —
  keep new keys consistent across all 19 files.
- Language switching falls back to `en` (`DEFAULT_LANGUAGE`) if a fetch for the
  active language fails.
- The language-preference cookie is only persisted after consent
  (`hasConsent`/`renderConsentBanner`) — don't set `bp_lang` unconditionally.

## Conventions

- Plain JS modules (`type="module"`), no framework, no external JS dependencies
  (`index.js` states this explicitly: "intentionally small, dependency-free
  JavaScript").
- Some comments reference internal `TASK-###`/`REQ-###` tracking IDs from prior
  work — informational only, not a scheme you need to continue unless asked.
- `docs/img/resizer.sh` is a one-off asset-resizing script, not part of any
  pipeline.

## Verification

There is no build/lint/test command. Validate changes by opening the HTML files
directly (or serving `docs/` with any static file server) and checking the page
in a browser, since `fetch()` calls for JSON content require `http(s)://`, not
`file://`.
