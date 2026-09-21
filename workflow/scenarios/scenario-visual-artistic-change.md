> Global rules are in [`workflow.md`](../workflow.md) — this scenario exists
> to enforce the
> [Product Owner Approval Gate](../workflow.md#product-owner-approval-gate-hard-rule).

## Scenario: Visual / Artistic Change

**Objective**: turn a creative/visual idea into an approved, implemented
change without breaking the cohesion across the four pages — and never
implementing anything visual before the Product Owner has explicitly
approved it.

**Use for**: restyle/redesign; new colors, typography, spacing/layout;
imagery/animation; "make it look better/more modern" requests. Not for:
no look-and-feel impact (→ Technical Implementation); copy/translation only,
with layout impact left to the Responsive/Cross-Device Audit (→ Content &
Localization).

### Team

| Role | Persona | Responsibility |
|------|---------|-----------------|
| **Lead (creative)** | Art Director | Drafts the proposal, ensures cross-page consistency; **cannot self-approve** |
| Reviewer | Site Architect | Technical feasibility within the no-build constraint |
| Reviewer | Responsive/Cross-Device QA Reviewer | Confirms the direction can hold up across viewport widths |
| Reviewer (advisory) | Web Trends Researcher | Trend input; drop if the request is already fully specified |
| **Approver** | **Product Owner** (human — no persona file) | Explicit approval required before implementation; cannot be delegated |
| Implementer | Frontend Developer | Implements only after approval is recorded |

### Process

Replaces the standard sign-off with a hard external gate:

1. Art Director restates the idea/constraints (which pages, what must stay
   consistent).
2. Web Trends Researcher contributes trend input if useful.
3. Art Director drafts a concrete proposal (description/mockup/diff) stating
   what changes and what stays the same across the four pages.
4. Site Architect + Responsive/Cross-Device QA Reviewer flag feasibility/
   device risk.
5. **Present to the Product Owner and wait for explicit approval** — never
   proceed on an assumed yes; if changes are requested, return to step 3.
6. Frontend Developer implements the approved direction exactly; any
   impractical detail discovered during implementation goes back to the
   Product Owner, not decided unilaterally.
7. Responsive/Cross-Device QA Reviewer re-checks the implemented result.

### Output

A recorded approval referencing what the Product Owner approved, before any
implementation commit. Commits per
[commit format](../workflow.md#commit-message-format), noting the approved
change. No visual/artistic change is ever marked done without that recorded
approval preceding its implementation commit.
