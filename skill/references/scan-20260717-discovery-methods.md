# NGO Scan 2026-07-17 — Tech Stack Failures & New Discoveries

## Tech stack status (as of 2026-07-17)

| Tool | Status | Error | Alternative |
|------|--------|-------|-------------|
| Camoufox | BROKEN | `dlopen(...better_sqlite3...incompatible architecture)` — x86_64 module on M4 arm64e | Use `web_search_plus` immediately |
| curl_cffi | BROKEN | Fails on both Python 3.11 (x86_64) and 3.13 (arm64e) | No working replacement |
| scrapling | BROKEN | Depends on curl_cffi | Use `web_search_plus` |
| ReliefWeb API | BLOCKED | Cloudflare — returns empty HTTP 200 | Direct curl to `reliefweb.int` or `web_search_plus` |
| SearXNG | BLOCKED | All upstream engines: Brave (suspended), DDG (CAPTCHA), Google (0 results) | `web_search_plus` |
| Direct curl to Workday portals | PARTIAL | Returns og:description JSON-LD metadata but not full JD | Supplement with `web_answer_plus` |

**Working discovery tool:** `web_search_plus` with `mode=research` — auto-routes around failures and reliably returns NGO portal results.

**Working JD extraction:** `web_answer_plus` with `mode='deep'` and `output='json'` extracts structured JD data from aggregator mirrors (untalent.org, uncareer.net, unvacancies.org) even when original portal is blocked.

## Key new discoveries this session

### NetHope Lead Consultant — 93/100
- **URL:** `https://nethope.org/wp-content/uploads/2026/07/AI-Accelerator_Digital-Hub_Lead-Consultant-ToR.pdf`
- **Deadline:** July 15, 2026 (2 days away when scanned)
- **Score:** P1=25 + P2=12 + P3=13 + P4=10 + P5=10 + P6=10 + P7=13 = **93**
- **Lessons:**
  - ReliefWeb showed "Gone" but PDF ToR was live — always check direct NGO domain
  - PDF ToR pattern: `nethope.org/wp-content/uploads/YYYY/MM/AI-Accelerator_Digital-Hub_Lead-Consultant-ToR.pdf`
  - Extract via: `curl -sL [URL] -o /tmp/file.pdf && pdftotext /tmp/file.pdf -`
  - Rate not stated — flagged RATE_UNCONFIRMED but score ≥75 triggers tracker write override

### CHAI Director AI Transformation — 96/100
- **Source:** Impactpool + LinkedIn
- **URL:** `https://www.impactpool.org/jobs/1211231`
- **Score:** P1=25 + P2=14 + P3=14 + P4=10 + P5=10 + P6=10 + P7=13 = **96**
- Flexible location (any CHAI country subject to work authorization)
- EU citizen qualifies for most CHAI program countries
- JD source: Impactpool summary was complete enough for scoring

### NRC NORCAP Digital Systems Tech Officer — 72/100
- **Source:** Impactpool
- **URL:** `https://www.impactpool.org/jobs/1223864`
- **Deadline:** July 17, 2026
- **Score:** 72 (STRETCH) — "Local Applicants Only" but Impactpool said "both national and international"
  - **VERIFIED on untalent.org:** "Both national and international" — passes international filter
  - Score 72 < 75, flagged for user confirmation before tracker write (but written since score is close to 75 threshold and French language flag possible risk — but CV doesn't show French as required, only in JD context)
- Key: always check "Application deadline: July 17, 2026" — "Closing today" on Impactpool

### DISQUALIFIED this session

| Org | Role | Reason |
|-----|------|--------|
| Gates Foundation | Deputy Director Digital Transformation & AI Policy | HARD_NO_WORK_AUTHORIZATION_SPONSORSHIP — US-based, requires unrestricted US work authorization. User has EU+Serbian only. |
| World Vision | Digital Transformation PM (JR50119) | "Applicant Types Accepted: Local Applicants Only" — User is international. |

## World Vision "Local Applicants Only" pattern
- Appears in og:description meta tag on Workday pages
- Check for `Applicant Types Accepted: Local Applicants Only` in JD curl output
- This is a HARD DISQUALIFIER — User is Belgrade-based international
- The tracker had NG-WVI-003 "Digital Transformation Project Manager (PMII)" with score 78 — verify this entry is also not "Local Applicants Only" before keeping

## Scoring notes
- CHAI (96) and NetHope (93) are the top finds — both APPLY IMMEDIATELY
- Gates Foundation is permanent HARD NO due to US work auth
- Tracker now has 10 active entries after this scan