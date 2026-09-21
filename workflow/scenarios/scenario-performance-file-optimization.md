> Global rules are in [`workflow.md`](../workflow.md), especially the
> [no-build/dependency-free constraint](../workflow.md#no-build--dependency-free-constraint).

## Scenario: Performance & File Optimization

**Objective**: reduce request count, duplicated code, and payload weight —
without introducing a build step and without changing behavior or visual
output.

**Use for**: reducing file count, deduping CSS/JS across page families,
shrinking asset weight, a general "make it leaner" ask. Not for: a fix that
would require a bundler/minifier/framework (escalate as an architecture
decision to Site Architect + Product Owner instead).

### Team

| Role | Persona | Responsibility |
|------|---------|-----------------|
| **Lead** | Site Architect | Confirms which file/architecture boundaries may be touched, signs off |
| Author | Performance & Optimization Engineer | Identifies duplication/waste, drafts the consolidation |
| Reviewer | Frontend Developer | Confirms functional correctness after consolidation |
| Reviewer | Responsive/Cross-Device QA Reviewer | Confirms zero visual/layout regression |
| Reviewer | SEO & Metadata Specialist | Confirms no canonical/asset-path/sitemap reference breaks |

### Process

Standard process. Performance & Optimization Engineer maps current
file/request count and duplication, then proposes the smallest change that
removes it without altering behavior or appearance. If it touches the
one-stylesheet-per-page-family boundary, Site Architect must approve that
specifically and `.github/copilot-instructions.md` gets updated. Sign-off
confirms the change is a pure optimization (same behavior/appearance, fewer
resources) that doesn't introduce a build dependency.

### Output

Consolidated files committed under `docs/...`, per
[commit format](../workflow.md#commit-message-format), noting the request/
byte-weight reduction achieved. No optimization is marked done if it changed
visible behavior or appearance — that becomes a Visual/Artistic or Technical
Implementation change instead, with its own approval requirements.
