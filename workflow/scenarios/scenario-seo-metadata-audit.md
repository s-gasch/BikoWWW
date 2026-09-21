> Global rules are in [`workflow.md`](../workflow.md).

## Scenario: SEO & Metadata Audit

**Objective**: audit and improve discoverability/ranking signals — titles,
descriptions, canonical/`hreflang`, structured data, sitemap/robots — across
all pages and all 19 languages, without changing visible copy or visual
design.

**Use for**: search ranking, metadata, structured data, sitemap coverage, a
periodic SEO health check. Not for: fix requires visible-copy change (route
the copy part to Content & Localization, keep the metadata part here); fix
requires a visual change (→ Visual/Artistic Change).

### Team

| Role | Persona | Responsibility |
|------|---------|-----------------|
| **Lead** | Site Architect | Confirms scope, signs off |
| Author | SEO & Metadata Specialist | Audits current state, drafts fix/addition |
| Reviewer | Frontend Developer | Implements `<head>`/markup changes; flags anything needing a build step (disallowed) |
| Reviewer | Content Localization Specialist | Confirms `hreflang`/locale metadata matches the real 19-language set |
| Reviewer | Performance & Optimization Engineer | Confirms added script/data doesn't meaningfully hurt Core Web Vitals |

### Process

Standard process. SEO & Metadata Specialist audits current `<title>`/
description/canonical/`hreflang`/structured-data/sitemap/robots state, then
drafts fixes keeping `hreflang` count and structured-data fields strictly
accurate to real content. Site Architect signs off only once no structured-
data field describes nonexistent content and no `hreflang` entry points at a
language without that content.

### Output

Changes committed under `docs/...` (and `sitemap.xml`/`robots.txt` if
present/introduced), per
[commit format](../workflow.md#commit-message-format).
