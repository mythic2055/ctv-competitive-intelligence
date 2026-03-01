# CTV Competitive Intelligence - Agentic Research Execution Plan

## Purpose
Build a defensible, citation-rich competitive intelligence package for CTV advertising with a focus on **MNTN** and **Tatari**, plus adjacent competitors (**Vibe.co**, **tvScientific/Pinterest**, **Viant**, **The Trade Desk**).

## Scope
- Geography: United States
- Date window: January 1, 2024 to present
- Output style: Analyst-grade, source-attributed, contradiction-aware
- Source priority:
  1. SEC filings, investor relations releases, earnings transcripts/decks
  2. Official company press releases and product documentation
  3. Reputable trade/financial media

---

## Step 1 - Market Baseline and Evidence Registry

### Objective
Create a current-state market baseline and a structured evidence table before company-level deep dives.

### Execution Prompt
```text
You are a senior AdTech market analyst.

Task:
Build a U.S. CTV advertising baseline (Jan 1, 2024 to present) and produce an evidence registry.

Coverage:
- Market growth and ad spend trajectory
- Viewing behavior shifts (streaming share, linear decline)
- Measurement and attribution trends (incrementality, MMM, MTA limitations)
- Supply-path and inventory access trends
- Buyer behavior by segment (SMB, mid-market, enterprise)

Method:
- Prioritize primary sources:
  A) SEC/IR filings and earnings materials
  B) Official company announcements/docs
  C) Reputable media
- For each claim, capture:
  - claim_id
  - claim_text
  - metric_value
  - period/date
  - source_url
  - source_date
  - source_tier (A/B/C)
  - confidence_score (High/Medium/Low)
  - notes_on_limitations

Output:
1) 1,000-1,500 word market baseline memo (Markdown)
2) `market_claims.csv` with all claims and citations
3) A "Known Unknowns" section with data gaps and how to close them
```

### Exit Criteria
- At least 30 cited claims in `market_claims.csv`
- No uncited non-trivial claim in the memo
- Contradictions explicitly flagged

---

## Step 2 - Per-Company Deep-Dive Articles

### Objective
Generate one detailed, consistently structured research article per target company.

### Execution Prompt
```text
You are a competitive intelligence specialist for AdTech.

Company under analysis: <COMPANY_NAME>
Peer anchors: MNTN and Tatari
Date window: Jan 1, 2024 to present

Deliverables:
1) Executive summary (max 10 bullets)
2) Company profile:
   - Core product, target customers, business model
3) Product and technical analysis:
   - Buying workflow, targeting, optimization, attribution, incrementality
4) Supply-path analysis:
   - Direct publisher relationships, SSP/DSP dependencies, transparency posture
5) GTM strategy:
   - Segment focus (SMB/mid-market/enterprise), agency channel, vertical wins
6) Commercial and financial signals:
   - Public metrics where available, funding/M&A indicators if private
7) Competitive assessment versus MNTN and Tatari:
   - Differentiators, weaknesses, likely head-to-head outcomes
8) 12-24 month outlook with 3 testable predictions
9) "Known Unknowns" and information gaps

Citation and quality requirements:
- Every material claim must include source URL and date.
- Mark claim confidence: High/Medium/Low.
- Explicitly label company self-reported metrics as self-reported.
- Flag contradictory claims and resolve using source priority:
  SEC/IR > Official PR/docs > Media

Output format:
- Markdown article, 1,500-2,500 words
- Companion CSV: `<company_slug>_claims.csv`
```

### Run Order
1. MNTN
2. Tatari
3. Vibe.co
4. tvScientific (include Pinterest integration context)
5. Viant
6. The Trade Desk

### Exit Criteria
- 6 completed company articles
- 6 companion claim CSV files
- Consistent section headings across all companies

---

## Step 3 - Cross-Company Scoring and Synthesis

### Objective
Normalize findings, rank threat levels, and extract strategic implications.

### Execution Prompt
```text
You are preparing a board-level competitive intelligence synthesis.

Inputs:
- 6 company deep-dive Markdown reports
- 6 company claim CSV files
- market_claims.csv

Tasks:
1) Normalize and deduplicate claims across all inputs.
2) Resolve conflicts by source hierarchy:
   SEC/IR > Official PR/docs > Media.
3) Build a weighted scorecard (0-10) per company using:
   - Product depth
   - Measurement credibility
   - Supply-path control
   - GTM efficiency
   - Financial durability
4) Produce:
   - Threat ranking (highest to lowest) relative to MNTN/Tatari
   - Win zones and risk zones by segment (SMB, mid-market, enterprise)
   - 3 market scenarios through 2027 with trigger indicators
   - 90-day intelligence monitoring plan (weekly/monthly/quarterly)
5) Build an uncertainty register:
   - unresolved_claim
   - impact_level
   - missing_evidence
   - verification_plan

Output:
1) `FINAL_CTV_COMPETITIVE_SYNTHESIS.md` (2,500-4,000 words)
2) `EXECUTIVE_BRIEF_1PAGER.md`
3) `top_50_claims_table.csv`
4) `uncertainty_register.csv`
```

### Exit Criteria
- All outputs generated
- Every major conclusion linked to at least one cited claim
- Clear recommendations for monitoring and next research cycle

---

## Step 4 - QA, Packaging, and Repository Readiness

### Objective
Ensure package quality and make the research bundle ready for version control and sharing.

### Execution Prompt
```text
You are a research QA editor.

Task:
Audit all generated files for methodological quality, citation integrity, and internal consistency.

Checklist:
- No uncited non-trivial claims
- Source dates captured for all citations
- Confidence score present for all key claims
- Contradictions flagged and dispositioned
- Terminology consistent across all reports
- File names and structure standardized

Output:
1) `QA_REPORT.md` with pass/fail per checklist item
2) `FIX_LOG.md` listing required revisions
3) Final publish-ready file manifest
```

### Exit Criteria
- QA report passes all critical checks
- Fixes applied and documented
- Repository tree is clean and ready to commit

---

## Suggested Repository Structure
```text
research/
  01_market_baseline/
    market_baseline.md
    market_claims.csv
  02_company_deep_dives/
    mntn.md
    mntn_claims.csv
    tatari.md
    tatari_claims.csv
    vibe.md
    vibe_claims.csv
    tvscientific_pinterest.md
    tvscientific_pinterest_claims.csv
    viant.md
    viant_claims.csv
    the_trade_desk.md
    the_trade_desk_claims.csv
  03_synthesis/
    FINAL_CTV_COMPETITIVE_SYNTHESIS.md
    EXECUTIVE_BRIEF_1PAGER.md
    top_50_claims_table.csv
    uncertainty_register.csv
  04_qa/
    QA_REPORT.md
    FIX_LOG.md
```

---

## GitHub Push Preparation (PAT via `.env`)

### 1) `.env` format (local only)
```bash
# Either variable name works:
GH_TOKEN=your_personal_access_token_here
# or:
GITHUB_PAT=your_personal_access_token_here
GITHUB_USERNAME=your_github_username
GITHUB_REPO=your_repo_name
```

### 2) Safe push script (manual run)
```bash
set -a
source .env
set +a

# Normalize token variable (supports GH_TOKEN or GITHUB_PAT)
TOKEN="${GH_TOKEN:-$GITHUB_PAT}"
if [ -z "$TOKEN" ]; then
  echo "Missing GH_TOKEN/GITHUB_PAT in .env"
  exit 1
fi

git init
git add .
git commit -m "Add CTV competitive intelligence execution plan"
git branch -M main
git remote add origin "https://${GITHUB_USERNAME}:${TOKEN}@github.com/${GITHUB_USERNAME}/${GITHUB_REPO}.git"
git push -u origin main
```

### Security Notes
- Never commit `.env` to Git.
- Add `.env` to `.gitignore` before push.
- Prefer fine-grained PAT with minimum required repo scopes.
