> Global rules are in [`workflow.md`](../workflow.md).

## Scenario: Trend Review

**Objective**: produce a short, actionable digest of current HTML/CSS/JS and
visual/UX trends relevant to BikoWWW, routed to the right owners — this
scenario produces recommendations only, never an implemented change.

**Use for**: a periodic "what's new" scan, or gathering inspiration before a
Technical Implementation or Visual/Artistic Change. Not for: the user already
has a concrete change in mind (go straight to that scenario).

### Team

| Role | Persona | Responsibility |
|------|---------|-----------------|
| **Lead** | Site Architect | Filters technical items for fit with the no-build constraint, signs off |
| Author | Web Trends Researcher | Scans and drafts the digest (technical + visual/UX sections, each with a feasibility note) |
| Reviewer | Art Director | Reviews the visual/UX section for relevance/consistency fit; may later shape an item into a Visual/Artistic Change proposal (still subject to the Approval Gate) |

### Process

Simplified standard process: Web Trends Researcher scans and drafts the
digest; Site Architect checks technical feasibility, Art Director checks
visual relevance. No item is "approved for implementation" here — that only
happens inside Technical Implementation or Visual/Artistic Change.

### Output

A short digest (chat output or a session-workspace note — not a committed
repository file, per
[output housekeeping](../workflow.md#output-housekeeping)). No code or
content is changed by this scenario.
