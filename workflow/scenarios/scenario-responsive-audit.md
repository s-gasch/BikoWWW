> Global rules are in [`workflow.md`](../workflow.md) — this scenario is the
> periodic/full-site enforcement of the
> [cross-device responsiveness rule](../workflow.md#cross-device-responsiveness-hard-rule).

## Scenario: Responsive / Cross-Device Audit

**Objective**: sweep the whole site (all four pages, plus relevant languages
for long-string edge cases) for layout breakage across device widths, and
file concrete fixes — independent of any single feature change.

**Use for**: a periodic full-site device check, a reported "broken on my
phone/tablet" issue, or the verification pass after a batch of changes. Not
for: replacing the mandatory per-change reviewer pass (use this for a
broader sweep in addition to it).

### Team

| Role | Persona | Responsibility |
|------|---------|-----------------|
| **Lead** | Site Architect | Confirms scope (pages/languages), signs off |
| Author | Responsive/Cross-Device QA Reviewer | Runs the full sweep, files concrete reproducible issues |
| Reviewer | Frontend Developer | Implements fixes |
| Reviewer | Content Localization Specialist | Consulted when a break is caused by a language's string length, to judge CSS fix vs. copy tweak |

### Process

Site Architect confirms scope; Responsive/Cross-Device QA Reviewer checks
every in-scope page at ~360/768/1024/1440px+ (both orientations where
relevant), noting concrete issues. For each issue, triage with Content
Localization Specialist whether it's a pure CSS fix (Frontend Developer
implements directly) or better solved by shortening/rewording a translation
(routes through Content & Localization to keep all 19 languages in sync).
Fix and re-check until clean at every width.

### Output

Fixes committed under `docs/...` per
[commit format](../workflow.md#commit-message-format); translation-driven
fixes go through the Content & Localization scenario's all-19-languages
rule. No page is marked "swept clean" while it still overflows, clips, or
overlaps at any checked width.
