# QA Report - CTV Competitive Intelligence Package

**Date:** March 1, 2026  
**Scope audited:**
- `research/01_market_baseline/*`
- `research/02_company_deep_dives/*`
- `research/03_synthesis/*`

## Audit Method
- File inventory and naming verification
- Schema checks on all CSV outputs
- Section consistency checks across all Step 2 deep-dive reports
- Word-count checks against planned depth targets
- Manual review of citation/disclosure discipline (self-reported vs validated claims)

## Checklist Results (Pass/Fail)
| Checklist Item | Status | Evidence | Notes |
|---|---|---|---|
| No uncited non-trivial claims | **Pass (with caveat)** | Claims tables include source-level evidence; deep-dive narrative includes source sections | Most material/numeric claims are traceable. Caveat: some inference statements in prose are not claim-ID linked. |
| Source dates captured for all citations | **Pass** | All claim CSV files include `source_date` | Date normalization is present across Step 1-3 claim tables. |
| Confidence score present for all key claims | **Pass** | All claim CSV files include `confidence_score` | Self-reported private metrics are appropriately downgraded in confidence. |
| Contradictions flagged and dispositioned | **Pass** | Step 1 caveats + Step 3 normalization/conflict section | Source hierarchy (`SEC/IR > Official > Media`) applied and documented. |
| Terminology consistent across all reports | **Pass** | Consistent use of CTV/convergent/performance framing | Minor stylistic variation only; no taxonomy-breaking inconsistencies found. |
| File names and structure standardized | **Pass** | Folder layout aligns with planned structure | Outputs are grouped correctly by phase with expected naming patterns. |

## Additional QA Gate Checks
| Gate | Status | Notes |
|---|---|---|
| Step 2 depth target (1,500-2,500 words per company report) | **Fail** | Current range is ~882-1,236 words. Functional but below target depth. |
| Step 3 final synthesis target (2,500-4,000 words) | **Pass** | Final synthesis is 2,863 words. |
| Top claims table output generated | **Pass** | `top_50_claims_table.csv` has 50 claims + header. |
| Uncertainty register generated | **Pass** | `uncertainty_register.csv` present with prioritized unresolved items. |

## File-Level Summary
- Step 1 outputs: complete and citation-rich.
- Step 2 outputs: complete and structurally consistent; depth expansion needed to fully match target spec.
- Step 3 outputs: complete; scorecard, ranking, scenarios, and evidence tables present.

## Overall QA Verdict
**Conditional Pass** for repository publication and internal use.  
**Condition to close for full spec compliance:** expand all six Step 2 deep-dive articles to the planned 1,500-2,500 word depth and strengthen claim-ID linkage for key inference statements.

## Recommended Next Action
Execute fixes listed in `research/04_qa/FIX_LOG.md` and rerun this QA checklist.
