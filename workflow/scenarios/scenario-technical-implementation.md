> Global rules (team, approval gate, cross-device, i18n, verification) are in
> [`workflow.md`](../workflow.md); only scenario-specific detail is below.

## Scenario: Technical Implementation

**Objective**: implement a feature, fix, or refactor with **no** look-and-feel
change. If a visual component is hiding in the request, split it out to
[Visual/Artistic Change](scenario-visual-artistic-change.md).

**Use for**: functional/behavioral/structural/accessibility changes. Not for:
look-and-feel change (→ Visual/Artistic Change), copy-only change with no
behavior change (→ Content & Localization), metadata-only change (→ SEO &
Metadata Audit).

### Team

| Role | Persona | Responsibility |
|------|---------|-----------------|
| **Lead** | Site Architect | Scope, flags any hidden visual component, arbitrates, signs off |
| Author | Frontend Developer | Implements following existing conventions |
| Reviewer (mandatory) | Responsive/Cross-Device QA Reviewer | No regression across viewport widths |
| Reviewer (if markup/`<head>` changed) | SEO & Metadata Specialist | — |
| Reviewer (if new files/assets added) | Performance & Optimization Engineer | — |
| Reviewer (if new copy keys introduced) | Content Localization Specialist | Confirms all 19 languages got the key |

### Process

Standard process (see `workflow.md`). At intake, Site Architect explicitly
checks for a hidden visual component and splits it out if found.

### Output

Commits under `docs/...`, one per completed unit, per
[commit format](../workflow.md#commit-message-format). Update
`.github/copilot-instructions.md` in the same commit if a convention changed.
Never sign off before the mandatory Responsive/Cross-Device review passes.
