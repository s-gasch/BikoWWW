> Global rules are in [`workflow.md`](../workflow.md), especially the
> [19-language consistency rule](../workflow.md#19-language-consistency-hard-rule).

## Scenario: Content & Localization

**Objective**: add or edit copy — home-page (`index/<lang>.json`) or a
formal document (`formal/<doc-type>/<lang>.json`) — across all 19 languages,
with no unrelated behavior or visual change.

**Use for**: new/changed home-page copy, formal-document section, legal-text
update, translation correction/re-translation. Not for: also changes layout
(split that part to Visual/Artistic Change); only `<head>` metadata, not
visible copy (→ SEO & Metadata Audit).

### Team

| Role | Persona | Responsibility |
|------|---------|-----------------|
| **Lead** | Site Architect | Confirms scope (surface, languages — normally all 19), signs off |
| Author | Content Localization Specialist | Drafts source copy, updates all 19 language files, bumps `version` |
| Reviewer | Frontend Developer | Confirms keys wired correctly / block-run model stays valid |
| Reviewer (if applicable) | SEO & Metadata Specialist | Locale-metadata implications (e.g. new doc type needing its own `hreflang` set) |
| Reviewer | Responsive/Cross-Device QA Reviewer | Longer/shorter translated strings don't break layout at narrow widths |

### Process

Standard process. Content Localization Specialist identifies every file the
change touches (all 19 locales); drafts source-language text first, gets it
confirmed, then produces the other 18; bumps `version` identically for
formal-document edits (`MINOR` editorial, `MAJOR` legal-meaning change).
Site Architect signs off only once all 19 files are present, parallel, and
in sync.

### Output

Content committed under `docs/index/` or `docs/formal/<doc-type>/` for all
19 languages in the same commit — never a partial-language commit — per
[commit format](../workflow.md#commit-message-format).
