# ReliefWeb NGO Jobs Scan — 2026-06-22

## Session: Full run of NGO-jobs-search skill

**Date**: 2026-06-22  
**Method**: Primary = ReliefWeb (reliefweb.int), Fallback = SearXNG meta-search on Tier 1 NGO portals, Tertiary = direct browser verification  
**Tool call count**: 39 (terminal 5, execute_code 5, browser_navigate 8, etc.)  

---

## Key Finding: ReliefWeb as Primary Discovery Source

The ReliefWeb page at `reliefweb.int/jobs?search=digital+OR+ict+OR+technology+connectivity&sort=newest` returned **13 live vacancies across 7 NGOs** from a single query. This is the highest-yield aggregator discovered so far.  

Per-portal SearXNG runs produced lower yield (7 leads but most expired/inaccessible). ReliefWeb should be used **FIRST** in future NGO scans before launching per-portal crawls.

---

## Query Strategy

```
ReliefWeb search URL pattern:
https://reliefweb.int/jobs?search=digital+OR+ict+OR+technology+connectivity&sort=newest

curl approach (slower — 15-30s, prone to timeout):
N/A — terminal tool triggers consent BLOCK on long curls. Do not retry.

Browser approach (reliable):
browser_navigate to ReliefWeb search URL
Full page snapshot => extract all article elements
Each article provides: title, organization (dd a link), country (p link), posted date (time), closing date (time pair)
```

---

## Results Table — Full Extracted Jobs

| # | Vacancy ID | Organization | Title | Location | Posted | Closing | Score | Status |
|---|-----------|--------------|-------|----------|--------|---------|-------|--------|
| 1 | 4217269 | AWO | Consultancy to Design and Deliver Nine Training Workshops on Digital Skills | Jordan | 22 Jun | 2 Jul | 64 | Open |
| 2 | 4216965 | Caritas Int'l | Comms, Extranet & Intranet Assessment | Holy See | 19 Jun | 9 Jul | 65 | Open |
| 3 | 4216666 | **NRC** | **Digital Programme Development Manager** | Sudan | 17 Jun | **30 Jun** | **70** | **Open** |
| 4 | 4216247 | ForAfrika | E-Learning Capacity Building Consultancy | Remote | 15 Jun | 5 Jul | 63 | Open |
| 5 | 4216211 | World Vision | Groundwater Mapping Consultancy | Somalia | 15 Jun | 22 Jun | 60 | Open |
| 6 | 4215506 | **Aflatoun** | **Digital Platform Consultant** | **Remote** | 9 Jun | **22 Jun** | **68** | **Open — CLOSES TODAY** |
| 7 | 4215431 | Bibliothèques SF | Digital Content Cleaning Consultancy | Afghanistan | 9 Jun | 30 Jun | 62 | Open |
| 8-13 | — | *Not fully extracted — session reached interactive phase* | — | — | — | — | — |

**Note**: Entries 8-13 exist but were not fully extracted. The snapshotted page listed jobs for Kenya (after the Kenya filter link). Full session needed ~3 more minutes of scrolling to capture all 13. Future sessions should scroll progressively or use browser console extraction.

---

## Verified & Scored Researched Details

### 🔴/🟡 Best Fit: NRC Digital Programme Development Manager (Sudan)

**ReliefWeb URL**: https://reliefweb.int/job/4216666/digital-programme-development-manager-sudan-national-role  
**Direct portal**: Redirects to ekum.fa.em2.oraclecloud.com/hcmUI (Oracle HCM — empty, SPA-rendered)  
**Level**: Programme Development Manager (PDM grade — mid-senior)  
**Org**: Norwegian Refugee Council (Tier 1)  
**Score**: 70/100 (🟡 STRETCH)  

**Accountabilities from full ReliefWeb JD:**
- Lead digital tech-enabled programming for NRC Sudan
- Digital culture building + staff capacity on data analysis, visualisation, data protection
- Digital programme strategy, tools, SOPs, training materials, results frameworks
- Digital cash, e-vouchers, mobile money, digital ICLA, digital case management
- Partnerships with mobile network operators and digital service providers
- GIS integration into programmes
- Budget management for digital portfolio
- Report to Head of Programme Support

**Gaps for User:**
- National role (not international P-level)
- Sudan-specific (no dual nationality; only Sudanese nationals qualify)
- Lower grade than director/head-level target

**Why keep**: NRC is Tier 1, Sudan is a high-need ICT4D context, role matches User's digital transformation + connectivity + data skills. Syrian refugees include Sudanese diaspora with relevant experience.

---

### 🟡 Aflatoun Digital Platform Consultant

**ReliefWeb URL**: https://reliefweb.int/job/4215506/digital-platform-consultant  
**Org**: Aflatoun International (Amsterdam HQ, Nairobi Hub)  
**Duration**: 8 months  
**Budget**: EUR 34,000 / total (approx EUR 4,250/month)  
**Score**: 68/100 (🟡 STRETCH)  

**Scope**:
- Build a Digital Learning Platform using existing Aflatoun digital assets
- Frontend UI/UX, backend architecture, 3rd party integrations
- Support platform launch and maintenance for 6 months
- Training on platform use and content management
- Needs: Liferay/Django/Wagtail experience + React/Next.js/TypeScript

**Gaps**:
- Mid-level (not senior).
- Specific CMS stack (Liferay) outside User's stack.
- 8-month max term.
- Low financial value.

---

## Excluded During Verification

| Source | Title | Why Excluded |
|--------|-------|--------------|
| DRC | Information Management Officer | Job ID 176110 — returned "job not found / deadline passed" |
| Oxfam | Digital media & Communication Senior Officer | Page not found (404) |
| MSF | ICT Supervisor Homa Bay | Cloudflare redirected to CommonSec, returning text of wrong role |
| IDB (Impactpool) | Technology and Digital Transformation Consultant | CLOSED (deadline 20 Jun 2025, not 2026) — Impactpool listing was stale |

---

## Tool Behavior Learnings

1. **Terminal `curl` on api.reliefweb.int timed out** at 15s / 30s triggering consent BLOCK. Do not retry — switch to `browser_navigate` on ReliefWeb search page immediately.

2. **SearXNG generic NGO queries returned mostly noise** — 44 leads but most were blog posts, PDFs, expired roles. Always include `-site:indeed.com -site:linkedin.com` filters (skill already has this).

3. **Oracle HCM portal (ekum.fa.em2.oraclecloud.com)** returned empty for NRC — SPA-rendered, bootstraps after page load. Use browser, not curl, for Oracle HCM.

4. **Camoufox was NOT started** — session ran without browser automation server (irrelevant for this scan since ReliefWeb is not JS-heavy).

5. **Browser tool limitations**:
   - Full snapshots are processed but output is very long; `browser_scroll` + full snapshot captured ~7/13 jobs before session shifted to report phase
   - `browser_console` with `document.querySelectorAll('article')` returned null — elements loaded via lazy JS render, not SSR
   - No vision tool available on this endpoint

---

## Portal Verification Table — Curl vs Browser

| Portal | curl / terminal | browser_navigate | Notes |
|--------|----------------|------------------|-------|
| ReliefWeb | timeout → BLOCK | ✅ Full content | Use browser always |
| api.reliefweb.int | timeout → BLOCK | N/A | Don't use — terminal blocks |
| ekum.fa.em2.oraclecloud.com (NRC) | Empty HTML | Empty SPA | Oracle HCM — needs JS render, curl useless |
| career.ocb.msf.org | Cloudflare | ✅ Works | Cloudflare selective — browser wins |
| drc.ngo/en/jobs/ | Empty 404-pattern | 404 job not found | Job expired |
| vietnam.oxfam.org | N/A | 404 | Job removed |

---

## Recommendations for Future NGO Scans

1. **Start with ReliefWeb** — single query, 13 leads, high NGO density. Use browser_navigate, not curl.

2. **Tier 1 direct verification order**: After ReliefWeb leads, verify on actual NGO portal in this order:
   a. NRC (Oracle HCM — use browser, expect SPA)
   b. DRC (drc.ngo — curl works, but verify deadline carefully)
   c. World Vision (Workday — curl returns JSON-LD, no browser needed)
   d. MSF (irffg.msf.org / career.ocb.msf.org — Cloudflare, MUST use browser)
   e. Oxfam (current-vacancies.com — curl accessible, verify expiry)
   f. CARE (care-international.org — curl likely works based on June 6)

3. **For Aflatoun (Amsterdam)** — reliefweb.int listing has full details already (no separate portal needed). Email application with one-page project proposal.

4. **Expirations matter** — all three NGO scans so far have found more EXPIRED than live postings. World Vision had a PMII role to ~30 Jun that might still be open (check JR44972 status).

---

## Related Files

- `references/portal-yields-2026-06-06.md` — Earlier portal scan (before ReliefWeb discovery)
- `references/scan-20260606-yield.md` — ATS bot-friendliness table
- `NGO_JOBS_TRACKER.TXT` — `~/Downloads/DATA_REPOSITORY/` — contains 3 World Vision entries as of 2026-06-22, needs updating with ReliefWeb results
