---
name: ngo-jobs-search
description: >
  Searches NGO sector vacancies using SearXNG meta-search and direct browser
  verification. Targets senior-level ICT, digital transformation, AI, telecom,
  and connectivity roles at the world's largest NGOs. Maintains
  NGO_JOBS_TRACKER.TXT in tracker-file-format.
triggers:
  - "ngo"
  - "ngo jobs"
  - "ngo search"
  - "NGO_JOBS_TRACKER"
  - "non-governmental"

---

# NGO Jobs Search Agent

## Role
Autonomous agent that scans the web for NGO sector vacancies matching User's senior profile. Targets senior-level roles in ICT, digital transformation, AI, telecom, connectivity, and digital development at the world's largest NGOs. Maintains a clean tracking file with scored, verified entries.

**This skill handles:** NGO staff/contract positions, senior advisory roles, ICT/Digital leads, programme management with tech components, expert consulting for NGOs.

**Does NOT handle:** UN/IO permanent staff roles (P-3+, fixed-term) — those go to `un-jobs-search-minimaltoken`. Does NOT handle freelance consulting — those go to `freelance-consulting-search`.

---

## ⛔ MANDATORY: Tracker File Format — TABLE-ONLY MODE

**BEFORE ANY write to `NGO_JOBS_TRACKER.TXT`, load `tracker-file-format`:**
```
skill_view(name='tracker-file-format')
```

The file uses the **TABLE-ONLY format** — identical to all other tracker files. The file contains ONLY the summary table. Entry blocks are NOT written.

**Table structure (exact):**
```
================================================================================
NGO SECTOR VACANCIES TRACKER
Generated: YYYY-MM-DD
================================================================================

🔵 VACANCY SUMMARY TABLE

#     Organization           Position Title                               Deadline        Score    Vacancy ID                    Applied
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
[row data]
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total: N active vacancies
Last updated: YYYY-MM-DD
Color coding: 🔴 90+ STRONG FIT  |  🟠 80-89 COMPETITIVE  |  🟡 70-79 STRETCH  |  🟢 <70 LOW FIT
================================================================================
```

**Column widths (FIXED — same as UN tracker):**
- `#`: 5 chars left-aligned
- `Organization`: 22 chars, truncate with … if longer, pad to 22
- `Position Title`: 44 chars, truncate at 44, pad to 44
- `Deadline`: 16 chars (e.g. `2026-06-15      ` or `TBD             ` or `Open            `)
- `Score`: 10 chars — emoji + space + 2-digit number (e.g. `🟠 88      `)
- `Vacancy ID`: 30 chars left-aligned, truncate if longer
- `Applied`: 7 chars (`NO     ` or `YES    `)

**Separator line:** 196 dashes (`-` × 196)

**Sorting:** By deadline ascending. TBD/Open at bottom.

**Opportunity ID Convention:** `NG-{ORG_CODE}-{NNN}` where:
- NG = NGO
- ORG_CODE = 3-5 char org abbreviation (NRC, DRC, CARE, WVI, BRAC, SCI, IRC, MSF, OXF, etc.)
- NNN = sequential 3-digit number

**Never append or patch — always full rebuild** via `execute_code` Python with `Path().write_text()`, then `sync`.

Template reference: `~/Downloads/DATA_REPOSITORY/UN_SECTOR_VACCANCIES_TEMPLATE.txt`

---

## Candidate Profile

- **MASTER DATABASE (2026-05-27):** `~/CV_REPOSITORY_DATABASE.md` — Load via `skill_view(name='cv-repository')`.
- **Profile Skill:** `skill_view(name='cv-repository')` — Retrieval protocol, TAGS reference, key metrics
- **Scoring:** `skill_view(name='vacancy-compatibility-scoring-engine')` — MUST use for all scoring, requires FULL JD
- Expertise: AI Product Leadership | LLMs, Agentic Systems, RAG | ICT/Telecom (4G/5G/FTTX/GPON/WIFI) | Digital Transformation | ISP/MVNO/MVNE | Payment Systems | Tech Due Diligence ($500M+) | UN/Africa/EU Advisory
- **Nationality: EU citizen (Czech Republic)** — qualifies for ALL EU-funded positions, tenders, and framework contracts
- **Nationality: Serbian** — qualifies for Serbian nationals-only positions
- Target: P-3 equivalent or above | Daily rate $350+/day for consultant roles

---

## 📋 TARGET NGO PORTALS — COMPLETE LIST

### 🟢 Tier 1 — Specific Portals Requested (direct browser verification priority)

| # | NGO | Careers/Vacancies URL | Notes |
|---|-----|----------------------|-------|
| 1 | **Norwegian Refugee Council (NRC)** | nrc.no/careers | NORCAP deployable pool also at ekum.fa.em2.oraclecloud.com |
| 2 | **Danish Refugee Council (DRC)** | drc.ngo/en/jobs/ | Also job.drc.ngo |
| 3 | **CARE International** | care-international.org/careers | Also care.org/careers |
| 4 | **Unconnected.org** | unconnected.org/careers | Small org, connectivity mission — high relevance |
| 5 | **Internet Society** | internetsociety.org/careers/ | Digital rights, connectivity — high relevance |
| 6 | **Internet Society Foundation** | isocfoundation.org/careers/ | Grants, digital resilience |
| 7 | **World Vision International** | wvi.org/careers | Workday: worldvision.wd1.myworkdayjobs.com. **Many roles say "Applicant Types Accepted: Local Applicants Only" — HARD DISQUALIFIER for User. Always check this field before scoring.** |
| 8 | **Turing Trust** | turingtrust.co.uk/about-us/careers/ | UK-based, ICT for education |
| 9 | **NetHope** | nethope.org | Remote consultancy, AI Accelerator for Nonprofits + Digital Hub for Emergency Coordination. **PDF ToR format:** `nethope.org/wp-content/uploads/YYYY/MM/AI-Accelerator_Digital-Hub_Lead-Consultant-ToR.pdf`. Very high relevance — scored 93/100. Deadline Jul 15, 2026. Check PDF ToR directly; ReliefWeb listing may show "Gone" even when role is still live. |
| 10 | **BRAC International** | bracinternational.org/career/ | Also careers.brac.net |
| 10 | **Oxfam International** | oxfam.org/en/take-action/jobs | Also oxfam.current-vacancies.com, jobs.oxfam.org.uk |
| 11 | **Médecins Sans Frontières (MSF)** | msf.org/work-msf | Also msf.org/jobs |
| 12 | **AfricaNenda Foundation** | africanenda.org/work-with-us-category/careers/ | Digital payments, Africa — high relevance to payment systems & digital transformation |
| 13 | **Bill & Melinda Gates Foundation** | gatesfoundation.org/careers | Workday ATS — digital finance, global health ICT, Africa programs — very high relevance |
| 14 | **Clinton Foundation / CHAI** | clintonfoundation.org/careers | Also clintonhealthaccess.org/careers — global health ICT, digital health, data systems — high relevance |

### 🟡 Tier 2 — 25 Largest NGOs (additional)

| # | NGO | Careers/Vacancies URL | Notes |
|---|-----|----------------------|-------|
| 15 | **Save the Children International** | savethechildren.net/careers | Also savethechildren.net/careers/apply |
| 16 | **International Rescue Committee (IRC)** | careers.rescue.org | Also rescue.org/careers |
| 17 | **Plan International** | jobs.plan-international.org | Also plan-international.org/about/jobs/ |
| 18 | **Mercy Corps** | mercycorps.org/careers | Country-specific boards also |
| 19 | **Catholic Relief Services (CRS)** | crs.org/about-us/careers | Country-specific: crsegyptjobs.crs.org |
| 20 | **Action Against Hunger (ACF)** | actionagainsthunger.org/careers | Also actionagainsthunger.org/careers/current-openings |
| 21 | **Practical Action** | practicalaction.org/careers/ | UK-based development tech |
| 22 | **PATH** | path.org/who-we-are/careers/ | Global health tech |
| 23 | **WWF (World Wildlife Fund)** | worldwildlife.org/about/careers/ | Environmental, ICT cross-over |
| 24 | **Amnesty International** | careers.amnesty.org/jobs/ | Also amnesty.org/en/careers/ |
| 25 | **Human Rights Watch** | hrw.org/careers | Senior advocacy/research roles |
| 26 | **Transparency International** | transparency.org/en/career-tender-opportunities | Anti-corruption, digital governance |
| 27 | **WaterAid** | wateraid.org/uk/careers-wateraid | WASH, ICT4D |
| 28 | **IFRC (International Federation of Red Cross/Red Crescent)** | ifrc.org/get-involved/work-us | Also careers.ifrc.org |

### 🟠 Supplementary Sources (scan if tokens available)

| Source | URL | Notes |
|--------|-----|-------|
| **ReliefWeb NGO Jobs** | reliefweb.int/jobs | Filter by organization type: NGO |
| **Impactpool (NGO filter)** | impactpool.org/jobs | Filter OUT UN agencies, keep INGOs |
| **NGO Jobs in Africa** | ngojobsinafrica.com | Regional focus |
| **DevelopmentAid** | developmentaid.org | IFI/NGO tenders |
| **UNjobs (NGO section)** | unjobs.org/non-un-organizations/ | Aggregator — verify on official portal |

---

## 🔍 SEARCH METHOD HIERARCHY (updated 2026-07-17)

**Priority — try each before moving to the next. web_search_plus is now PRIMARY.**

### 1. web_search_plus (PRIMARY — always works)
When Camoufox, SearXNG, and all automated tools are blocked, `web_search_plus` with `mode=research` auto-routes around failures. Use this FIRST.

```
web_search_plus(count=15, mode='research', query='NGO ICT digital technology lead director 2026 site:nrc.no OR site:drc.ngo OR site:care-international.org OR site:savethechildren.net')
web_search_plus(count=10, mode='research', query='digital transformation ICT AI NGO senior vacancy 2026 site:reliefweb.int OR site:impactpool.org')
```

After finding a vacancy URL, use **web_answer_plus (mode=deep)** to extract the full JD:
```
web_answer_plus(mode='deep', output='json', query='[position title] job description responsibilities qualifications deadline', sources=3)
```
This extracts structured JD data from aggregator sites (untalent.org, uncareer.net, etc.) even when the original portal is inaccessible.

### 2. Direct NGO PDF ToR extraction (for consultancies)
Many NGOs publish consultancy ToRs as PDFs on their own domains, bypassing aggregator listings. Pattern:
```
https://{org}.org/wp-content/uploads/YYYY/MM/{slug}-ToR.pdf
```
Use `curl -sL [URL] -o /tmp/file.pdf && pdftotext /tmp/file.pdf -` to extract.

**Critical:** A vacancy showing "Gone" on ReliefWeb does NOT mean the role is closed — always check the direct NGO source. NetHope's ReliefWeb listing was "Gone" on 2026-07-17 but the PDF ToR was live and the deadline was 2 days away.

### 3. Direct curl to NGO portals (Workday/Oracle fallback)
Workday-based NGO portals (World Vision, Gates Foundation, IRC, Save the Children) return JD metadata in raw HTML. Use:
```bash
curl -s --max-time 20 -L -A "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36" "[URL]" | python3 -c "
import sys, re; c=sys.stdin.read()
text = re.sub(r'<script[^>]*>.*?</script>', ' ', c, flags=re.DOTALL)
text = re.sub(r'<style[^>]*>.*?</style>', ' ', text, flags=re.DOTALL)
text = re.sub(r'<[^>]+>', ' ', text); text = re.sub(r'\s+', ' ', text)
print(text[:8000])
"
```

### 4. ❌ SearXNG — DEPRECATED (all engines blocked)
Brave suspended, DuckDuckGo CAPTCHA, Google 0 results, Startpage blocked. Do not rely on. Retain only as historical reference.

### 5. ❌ ReliefWeb API — DEPRECATED
`api.reliefweb.int` is Cloudflare-blocked. Returns empty HTTP 200. Do not retry.

### 6. ❌ Camoufox — UNRELIABLE (M4 Mac arch mismatch)
`better-sqlite3` native module is x86_64, M4 Mac runs arm64e. Every tab creation fails with `dlopen(...incompatible architecture...)`. Go straight to `web_search_plus`; do not wait for Camoufox.

### 7. ❌ scrapling / curl_cffi — BROKEN on this Mac
`curl_cffi` fails on both Python 3.11 (x86_64) and Python 3.13 (arm64e). `scrapling` depends on it. Do not attempt `uv run --with scrapling`.

### 8. ❌ ReliefWeb browser extraction — LEGACY fallback
If Camoufox were working, navigate to `https://reliefweb.int/jobs?search=ICT+OR+digital+OR+telecom+OR+information+technology` and extract via `browser_console` JS. But since Camoufox is down and the API is blocked, this is no longer viable as a primary method.

---

## 🚫 HARD FILTERING

**Immediately discard:**
- Irrelevant domains (healthcare clinical, WASH engineering, protection, shelter, logistics, supply chain, HR, finance, fundraising, communications)
- Junior or entry-level roles (< P-3 equivalent or < 5 years experience)
- Volunteer or unpaid positions
- Ukraine duty station
- National/local positions restricted to country nationals (EXCEPTION: Serbia = PASS)
- **"Local Applicants Only" / "Applicant Types Accepted: Local Applicants Only" — this is a HARD DISQUALIFIER even if the role is otherwise senior. User is international (Belgrade-based EU citizen) and does not qualify for local-hire roles. Exceptions: Serbian nationals-only positions (User has Serbian citizenship).**
- Internships
- Consultant roles with daily rate < $350/day
- Vague requirements, spam postings

**Only keep:**
- ICT / Digital / AI / Telecom / Connectivity / Technology
- Strategy / advisory / architecture / senior leadership
- Digital transformation, EdTech, innovation (tech-focused only)
- Data systems, enterprise architecture, cloud, cybersecurity
- Programme management with substantial tech component

---

## 🧠 SCORING MODEL

**MUST use `vacancy-compatibility-scoring-engine`** for all scoring with FULL JD.

1. Load the scoring engine: `skill_view(name='vacancy-compatibility-scoring-engine')`
2. Load CV Repository for evidence: `skill_view(name='cv-repository')` + `read_file(path='~/CV_REPOSITORY_DATABASE.md')`
3. Extract the full job description from the NGO portal (never score from title alone)
4. Apply the 7-parameter scoring framework (P1–P7, max 100)
5. Run hard filters first in order
6. Show arithmetic explicitly: P1+P2+P3+P4+P5+P6+P7 = TOTAL
7. Produce full verdict with Application Strategy

**Color coding:**
- 🔴 RED (90+): STRONG FIT — apply immediately
- 🟠 ORANGE (80-89): COMPETITIVE — apply within 48h
- 🟡 YELLOW (70-79): STRETCH — evaluate carefully
- 🟢 GREEN (<70): LOW FIT — marginal

**Auto-discard:** Score < 65

---

## 💾 FILE MANAGEMENT

### File Location
`~/Downloads/DATA_REPOSITORY/NGO_JOBS_TRACKER.TXT`

### Write Method
**Never append or patch. Always full rebuild.** Use `write_file` to create a Python script, then run it via `terminal`:
```python
# Save to /tmp/ngo_tracker_rebuild.py via write_file, then run: python3 /tmp/ngo_tracker_rebuild.py
from pathlib import Path
path = Path("~/Downloads/DATA_REPOSITORY/NGO_JOBS_TRACKER.TXT")
path.write_text(new_content, encoding='utf-8')
```

Then `sync` and verify with `wc -l`.

**⚠️ NEVER use `execute_code` for file writes.** The execute_code sandbox has an isolated filesystem — `write_file` inside it destroys real files by writing nothing back. Use `write_file` (Hermes tool) to create the script, then `terminal` to execute it.

### POST-WRITE VERIFICATION
After every write, verify ALL of:
1. Line count ≈ N + 12 where N = number of active opportunities
2. Count of numbered rows = N
3. `"MATCH ANALYSIS"` does NOT appear anywhere in the file
4. `"Applied"` DOES appear in the header row
5. Every data row ends with `"NO     "` (or `"YES    "` if any YES remain)
6. Run `sync` after write

---

## EXECUTION PHASES

### Phase 1: Initialize & Load State
1. Get Belgrade time: `TZ='Europe/Belgrade' date '+%Y-%m-%d %H:%M:%S'`
2. Ensure SearXNG is running
3. Read existing `NGO_JOBS_TRACKER.TXT`
4. Extract all existing Vacancy IDs for dedup
5. Load skills: `tracker-file-format`, `cv-repository`, `vacancy-compatibility-scoring-engine`

### Phase 2: Portal Discovery — ReliefWeb Browser Extraction (Primary)
1. Navigate to `https://reliefweb.int/jobs?search=ICT+OR+digital+OR+telecom+OR+information+technology`
2. Extract all articles via browser_console JS (see PRIMARY SEARCH METHOD section)
3. Filter for ICT-relevant titles
4. For each viable lead: navigate to JD page, extract full description, save to NGO_JD_FILES/
5. Optionally: try SearXNG queries (legacy) — expect 0 results, do not retry

### Phase 3: Direct Portal Verification
For viable leads from Tier 1 (highest priority): browser_navigate to verify on official source.
Extract: title, org, deadline, grade, contract type, URL, eligibility.
Discard expired or inaccessible entries.

### Phase 4: Score & Filter
1. Run hard filters first
2. For surviving entries: load full JD from portal
3. Score using `vacancy-compatibility-scoring-engine` (7-parameter model)
4. Deduplicate against existing entries by (title.lower(), org.lower())

### Phase 4b: PRE-SAVE EXPIRATION CHECK — MANDATORY
**CRITICAL: Before adding any entry to the tracker, verify the vacancy has not expired.**

For every candidate being added:
- Extract the closing/deadline date from the JD or portal page
- Compare to today's date (Belgrade time: `TZ='Europe/Belgrade' date '+%Y-%m-%d'`)
- If `closing_date < today`: DISCARD. Do NOT add to tracker.
- Exception: Only keep expired entries if the user explicitly asks.

**Why this matters (2026-07-17 case study):** The NetHope Lead Consultant (NG-NHP-001, deadline 2026-07-15) was scanned on 2026-07-17 — already 2 days expired. It was found via cached ReliefWeb results and saved at 93/100 before expiration was caught. Always check the deadline BEFORE scoring, not after.

This is especially critical for:
- Consultancy roles with compressed timelines (1-year contracts, rolling deadlines)
- ReliefWeb-aggregated listings (cache lag shows expired roles as live)
- Short-deadline postings (< 7 days from scan date)

### Phase 5: Rebuild & Write
1. Backup existing file: `cp ... BACKUP_YYYYMMDD_HHMM.txt`
2. Merge new entries with existing active entries
3. Rebuild summary table sorted by deadline (ascending)
4. Write full file via `execute_code` Python `Path().write_text()`
5. `sync && wc -l`

### Phase 6: Report
- Sources scanned (which NGO portals)
- New entries added with scores
- Total active opportunities
- Top 5 matches with scores, deadlines
- Excluded entries with filter reasons
- Blocked/inaccessible portals

### 🤖 Orchestrator-Delegate Mode (Cross-Agent with AGENT)

When the user asks to delegate scanning to a cheaper agent (AGENT/DeepSeek V4 Flash):

**Orchestrator (AGENT, this agent):**
- Prepares dispatch prompt with exact SearXNG queries, ReliefWeb URL, filter rules, JD file naming convention, output directory
- Loads CV repository + scoring engine while AGENT scans (parallel work)
- Receives AGENT results, reads saved JD files, scores each entry using V5.0.0 engine
- Rebuilds and writes tracker file

**Delegate (AGENT, cheaper agent):**
- Runs SearXNG queries + ReliefWeb browser extraction
- Filters results for ICT relevance
- Navigates to each JD page, extracts full description
- Saves JD text files to shared `NGO_JD_FILES/` directory
- Writes `_SCAN_SUMMARY.txt` with metadata
- Replies back to orchestrator via cmux when done

**Dispatch Protocol (see FORWARD skill for details):**
1. Verify AGENT is at `─ ready │` prompt BEFORE dispatching (capture pane first)
2. Write dispatch prompt to temp file, then 3-step cmux send: text → newline → Enter
3. Use UUID (`--workspace <UUID>`), not workspace:N ref (refs shift between sessions)
4. Monitor every 60-90s via `cmux capture-pane --workspace <UUID> --scrollback --lines 50`
5. After AGENT reports done: read all JD files from `NGO_JD_FILES/`, score each, rebuild tracker

**Reference:** `references/scan-20260704-reliefweb-orchestrator.md` for the full worked example.

---

## KNOWN PITFALLS

- **Camoufox server pre-flight**: Before any browser_navigate, verify `curl -s http://localhost:9377/health` returns `{"ok":true,...}`. If not running, start with `camofox server start --port 9377`.
- **Camoufox frequently down — have a curl-only fallback**: When Camoufox is not running (very common!), do NOT stall. Fall back to curl+regex for portal verification. Workday sites (World Vision) return JSON-LD via curl. Save the Children returns full HTML with closure markers ("no longer accepting applications"). DRC, Plan International, MSF, fundsforngos, ngojobsinafrica return 0 bytes or Cloudflare — mark as BLOCKED and move on. See `references/scan-20260606-yield.md` per-portal curl accessibility.
- **SearXNG ALL ENGINES BLOCKED (as of 2026-07-04)**: Brave is suspended (too many requests), DuckDuckGo and Startpage return CAPTCHA, KarmaSearch returns access denied, Google returns 0 results. The SearXNG container is running and the JSON API responds, but every upstream engine blocks automated queries. **Do not expect SearXNG to return any web results.** Pivot immediately to direct browser navigation on known aggregator portals instead of spending tokens on SearXNG queries.
- **ReliefWeb direct browser extraction is the primary fallback**: When SearXNG fails (which is now the norm), navigate directly to `https://reliefweb.int/jobs?search=ICT+OR+digital+OR+telecom+OR+information+technology` in the browser. This returns 92+ results across 5 pages. Extract all articles via `browser_console` JS (`Array.from(document.querySelectorAll('article')).map(...)`), filter for ICT-relevant titles, then navigate to each viable JD page to extract the full description. This yields ~10-15 viable leads per scan. Save JDs as text files to `NGO_JD_FILES/` with filename pattern `NG_{ORG}_{NNN}.txt`.
- **SearXNG returns snippets, not full pages**: Always verify by visiting actual URL before recording.
- **Some NGO careers portals require login** (e.g., Oxfam recruitment.oxfam.org) — use SearXNG for discovery, browser only for public pages.
- **NGO portals often use third-party ATS**: Taleo, Workday, Oracle Cloud, SmartRecruiters, Greenhouse — each has different bot-friendliness.
- **Keywords are unreliable in NGO contexts**: "Digital" may mean fundraising/comms, "Technology" may be health tech, "Innovation" may be grants. Always verify actual accountabilities.
- **Aggregator sites show expired listings**: Verify deadline date on actual portal before adding.
- **ReliefWeb and UNjobs aggregate NGO listings** — useful for discovery but always verify on official portal.
- **Score only from full JD** — never from 44-char tracker title (16pt average error).
- **NGO salary bands are generally lower than UN/IFI**: P-3 equivalent may be CHF 70-90K. Flag salary step-downs but don't auto-discard.
- **Unconnected.org is a small org** — vacancies may be rare but high relevance (connectivity mission).
- **Turing Trust is UK-based** — mostly UK roles, ICT for education focus.
- **NORCAP (NRC) deployable expert pool** is a high-leverage entry point — register if not already.
- **Gates Foundation US work authorization trap**: ALL Gates Foundation roles in the US require unrestricted US work authorization without visa sponsorship. This is a HARD NO for User (no US work visa). Even Nairobi-based roles may require Kenya work authorization without sponsorship. Check the "Must have unrestricted work authorization" line in every Gates Foundation JD before scoring.
- **CHAI uses iCIMS ATS**: The CHAI careers portal (clintonhealthaccess.org/join-our-team/) redirects to careers-chai.icims.com via an iframe. SearXNG cannot index iCIMS content. Direct browser navigation to the iCIMS search URL is required: `https://careers-chai.icims.com/jobs/search?ss=1&searchKeyword=digital+OR+ICT+OR+technology+OR+AI+OR+data`
- **AfricaNenda uses PDF-based postings**: Job details are in PDF files, not HTML. Use `curl -sL [URL] -o /tmp/file.pdf && pdftotext /tmp/file.pdf -` or pymupdf to extract. The careers page shows Open/Closed status with dates.
- **Save the Children listings persist in search results long after expiry**: The Director of Digital Systems (deadline 7 Apr 2026) still appeared in SearXNG results on 22 Jun 2026. Always verify deadline on the actual portal page before scoring.
- **World Vision has multiple Digital Transformation PM postings**: Different job requisition IDs (JR44972 vs JR50119) for similar titles. Deduplicate by job requisition ID, not just title. Check the Workday job ID field.
- **Clinton Foundation careers page uses an iframe**: The /careers/apply/ page embeds an iframe that loads the actual job listings. Browser_navigate may not see the content. Try navigating to the iframe src URL directly, or use the "See open positions" link target.
- **ReliefWeb single-query high-yield discovery**: A single SearXNG query to `reliefweb.int/jobs?search=digital+OR+ict+OR+technology+connectivity` returned 13 live vacancies across 7 NGOs. ReliefWeb is the highest-yield NGO aggregator found. Use it FIRST before per-portal crawl. Its `api.reliefweb.int` endpoint has longer query processing — expect 15-30s response time. If the terminal command times out and triggers a Consent BLOCK, do NOT retry the same curl command. Switch to `browser_navigate` directly on the ReliefWeb search URL instead.
- **Himalaya config needs Gmail Trash folder paths**: When using Himalaya CLI to move emails to Gmail Trash, the command `himalaya message delete` may fail. Add to `~/.config/himalaya/config.toml`: `message.delete.folder = "[Gmail]/Trash"` and `message.trash.folder = "[Gmail]/Trash"`. The working command is then `himalaya message move -f "[Gmail]/All Mail" "[Gmail]/Trash" <id>`.
- **Tracker emoji codepoints (2026-07-04)**: When building tracker rows in Python, use the correct Unicode codepoints: 🔴=`\U0001F534`, 🟠=`\U0001F7E0`, 🟡=`\U0001F7E1`, 🟢=`\U0001F7E2`. Do NOT use `\U0001F736` — that renders as 🜶 (alchemical symbol), not 🟠 (orange circle). The score column format is: `f"{emoji} {score}".ljust(10)`.
- **Orchestrator-delegate dispatch verification (2026-07-04)**: When delegating to AGENT, ALWAYS verify the target is at `─ ready │` prompt before dispatching. A dispatch to a busy agent is silently lost. After dispatch, capture the pane within 30s to confirm the agent started processing YOUR prompt. See FORWARD skill for full protocol.

## 🛠️ MAINTENANCE: Adding a New NGO Portal

When the user asks to add a new NGO to the scan list:

1. **Visit the careers URL** via browser_navigate to verify it exists and see the portal type
2. **Check portal characteristics:** CMS type, ATS platform, Cloudflare presence, curl accessibility, job detail format (HTML vs PDF), deadline location
3. **Check for open vacancies** — note any relevant ones with deadlines
4. **Add to the Tier 1 table** in SKILL.md (insert at the end of Tier 1, renumber Tier 2 entries)
5. **Create a reference file** at `references/{org-code}-portal-profile.md` with:
   - Portal characteristics table (CMS, ATS, curl accessibility, Cloudflare, deadline location, application method)
   - Current open/closed vacancies table
   - Relevance assessment to User's profile
   - PDF extraction pattern (if applicable)
   - ORG code for tracker (NG-{CODE}-{NNN})
6. **Update the References section** in SKILL.md to point to the new file
7. **Update the description** if the "25 largest" count changes

**ORG Code convention:** `NG-{CODE}-{NNN}` where CODE is 3-5 chars (e.g., AFN for AfricaNenda, GTF for Gates Foundation).

## References
- `references/scan-20260717-calibration.md` — **2026-07-17 scan:** CHAI Director AI Transformation (96/100), NetHope Lead Consultant (93/100, EXPIRED — not tracked), NRC Digital Systems Technical Officer (72/100). Includes Gates Foundation US auth trap, World Vision Local Applicants Only trap, calibration arithmetic.
- `references/portal-yields-2026-05-30.md` — First-scan yield by portal: which NGOs returned ICT-relevant leads, which were empty/gated/redirected. Consult before re-scanning to avoid repeating dead-end portals.
- `references/portal-yields-2026-06-06.md` — Second scan: World Vision yielded 2 entries, Save/DRC/Oxfam/MSF yielded none (closed/blocked/irrelevant).
- `references/scan-20260606-yield.md` — Jun 6 scan: curl-verification patterns per portal, ATS bot-friendliness table, yield rate ~1.7%, Save the Children closure detection via HTML patterns.
- `references/scan-20260622-reliefweb.md` — Jun 22 ReliefWeb scan: 13 jobs across 7 NGOs from a single query, terminal timeout mitigation, browser fallback chain for ReliefWeb extraction when curl fails.
- `references/scan-20260622-yield.md` — Jun 22 scan: Gates Foundation work authorization trap, AfricaNenda French gap, World Vision PMII scored at 78.
- `references/scan-20260704-reliefweb-pivot.md` — 2026-07-04 scan: SearXNG all engines blocked, ReliefWeb direct browser extraction pattern, extraction JS, yield analysis.
- `references/scan-20260704-reliefweb-orchestrator.md` — 2026-07-04 orchestrator-delegate scan: AGENT+AGENT division of labor, dispatch protocol, SearXNG engine status table, 9 JD files scored, 4 new tracker entries.
- `references/scan-20260717-discovery-methods.md` — Search method hierarchy (2026-07-17): web_search_plus PRIMARY, PDF ToR extraction, direct curl fallback, deprecated tools documented.
- `references/africanenda-portal-profile.md` — AfricaNenda Foundation portal profile: WordPress, PDF-based postings, email applications, French language filter.
- `references/gates-foundation-portal-profile.md` — Gates Foundation portal profile: Workday ATS, US work authorization trap, scan results.
- `references/clinton-chai-portal-profile.md` — Clinton Foundation / CHAI portal profile: iCIMS ATS, iframe issues, scan results.
- `references/save-the-children-portal-profile.md` — Save the Children portal profile: Oracle Cloud ATS, curl accessibility, apply-button detection pattern, current open ICT vacancies (Jul 2026).

---

## THIS SKILL vs OTHER SKILLS

- **This skill:** NGO staff and consultant vacancies at the world's 25 largest NGOs
- **UN-JOBS-SEARCH:** UN/IO permanent/FT staff roles (P-3+, fixed-term), UN agency consultancy
- **FREELANCE-CONSULTING-SEARCH:** Non-UN freelancing, IFI procurement, development consulting firms
- **Overlap:** Impactpool spans all three — entries classified by source organization type
- **Scoring:** ALL skills use `vacancy-compatibility-scoring-engine` for every evaluation
