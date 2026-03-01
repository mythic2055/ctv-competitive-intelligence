# Fix Log - CTV Competitive Intelligence

**Date:** March 1, 2026

## Open Fix Items
| ID | Priority | Area | Issue | Required Action | Owner | Status |
|---|---|---|---|---|---|---|
| FIX-001 | High | Step 2 reports | Six company deep-dives are below planned depth target (1,500-2,500 words each). | Expand `mntn.md`, `tatari.md`, `vibe.md`, `tvscientific_pinterest.md`, `viant.md`, `the_trade_desk.md` to target range while preserving evidence discipline. | Research Agent | Open |
| FIX-002 | Medium | Citation traceability | Some inference statements in Markdown are not directly linked to claim IDs. | Add inline claim-ID references for inference-heavy paragraphs and cross-map to corresponding `*_claims.csv` rows. | Research Agent | Open |
| FIX-003 | Medium | Evidence quality | Private-company self-reported metrics remain weakly validated. | Add independent corroboration where available; otherwise keep downgraded confidence and caveat language. | Research Agent | Open |
| FIX-004 | Medium | Comparative benchmarking | Limited standardized incrementality comparisons across all six competitors. | Add a methodology-normalized benchmark appendix in Step 3 update cycle. | Research Agent | Open |
| FIX-005 | Low | Terminology polish | Minor narrative style differences across reports. | Final editorial pass for uniform tone and section transition style. | Research Agent | Open |

## Completed in This QA Pass
| ID | Area | Resolution |
|---|---|---|
| DONE-001 | File structure | Verified complete phase-based folder structure and expected artifact presence. |
| DONE-002 | CSV schema integrity | Verified all claim CSV files include required schema fields. |
| DONE-003 | Synthesis deliverables | Verified final memo, one-pager, top-50 claims, and uncertainty register are present. |
| DONE-004 | Contradiction handling | Verified source hierarchy and conflict disposition logic is documented in synthesis. |

## Exit Condition for Full QA Pass
All high-priority items closed, especially `FIX-001` (Step 2 depth compliance).
