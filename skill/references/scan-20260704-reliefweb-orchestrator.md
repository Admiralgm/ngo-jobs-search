# ReliefWeb NGO Jobs Scan — 2026-07-04 (Orchestrator + Delegate Pattern)

## Session: AGENT (GLM 5.2) orchestrator + AGENT (DeepSeek V4 Flash) scanner

**Date**: 2026-07-04
**Method**: AGENT ran SearXNG queries + ReliefWeb browser extraction; AGENT scored and wrote tracker
**Yield**: 9 JD files, 4 new tracker entries (scores 80-92), 5 excluded

---

## Orchestrator-Delegate Pattern (First Successful Cross-Agent NGO Scan)

### Division of Labor
| Phase | Agent | Task | Cost |
|-------|-------|------|------|
| Phase 2-3 (Scan + Extract) | AGENT (DeepSeek V4 Flash) | SearXNG queries, ReliefWeb browsing, JD file saving | 3x cheaper |
| Phase 4-5 (Score + Write) | AGENT (GLM 5.2) | V5.0.0 7-parameter scoring, tracker rebuild/write | Orchestrator |

### Dispatch Protocol
1. Orchestrator (AGENT) prepares dispatch prompt with exact SearXNG queries, filter rules, JD file naming convention, and output directory
2. Verify AGENT is at `─ ready │` prompt BEFORE dispatching (see FORWARD skill pitfall 2026-07-04)
3. Send via 3-step cmux sequence: `cmux send --workspace <UUID> "$(cat /tmp/h2_prompt.txt)"` → `cmux send --workspace <UUID> "\n"` → `cmux send-key --workspace <UUID> Enter`
4. Monitor every 60-90s via `cmux capture-pane --workspace <UUID> --scrollback --lines 50`
5. AGENT replies back to orchestrator's workspace UUID when done
6. Orchestrator reads saved JD files, scores each, rebuilds tracker

### What Worked Well
- AGENT autonomously pivoted from dead SearXNG to direct ReliefWeb browsing (92 results scanned)
- AGENT correctly filtered: skipped Ukraine roles, junior positions, non-ICT roles
- AGENT saved full JD text files (not just snippets) for accurate scoring
- AGENT wrote a comprehensive _SCAN_SUMMARY.txt with all metadata
- Orchestrator loaded CV repository + scoring engine while AGENT worked in parallel

### What Could Be Better
- Initial dispatch was lost because AGENT was mid-task (busy with a previous UNTalent scan) — see FORWARD pitfall
- All SearXNG engines were down (Brave/DDG/Startpage/KarmaSearch all CAPTCHA'd/suspended) — ReliefWeb is the reliable fallback
- Google engine returned 0 results with no error (silently rate-limited, not marked as unresponsive)
- Bing engine worked for generic queries but returned non-NGO results (Croatia NGO directories, Wikipedia)

---

## SearXNG Engine Status (2026-07-04 22:31 CEST)

| Engine | Status | Notes |
|--------|--------|-------|
| Brave | Suspended: too many requests | Rate-limited |
| DuckDuckGo | CAPTCHA | Blocked |
| Startpage | CAPTCHA | Blocked |
| KarmaSearch | Suspended: access denied | Blocked |
| Google | 0 results, no error message | Silently rate-limited |
| Bing | Working | Returns generic results, not NGO-specific |

**Conclusion**: SearXNG meta-search is unreliable for NGO job scanning. ReliefWeb direct browsing is the primary reliable method. SearXNG should be treated as a secondary discovery tool, not primary.

---

## ReliefWeb Direct Browsing Results (92 results scanned)

### JD Files Saved (9 total)
| File | Org | Title | Deadline | Score | Status |
|------|-----|-------|----------|-------|--------|
| NG_OAF_001.txt | One Acre Fund | Tupande AI Engineering Lead | 2026-09-26 | 🔴 92 | TRACKER |
| NG_OAF_002.txt | One Acre Fund | Tupande Automation Engineering Lead | 2026-09-26 | 🟠 89 | TRACKER |
| NG_IRC_002.txt | IRC | AI Program Manager (Governance) | 2026-08-31 | 🟠 83 | TRACKER |
| NG_WV_001.txt | World Vision Intl | Director, Innovation & GC Continuous A&A | 2026-07-19 | 🟠 80 | TRACKER |
| NG_ADPC_001.txt | ADPC | Technical Analyst, Geospatial AI | 2026-07-15 | 🟡 71 | Excluded (<75) |
| NG_AG_001.txt | Altamont Group | IT Proposal Writer (Remote) | 2026-07-10 | 🟡 67 | Excluded (<75) |
| NG_IRC_001.txt | IRC | Information Management Senior Officer - Damascus | 2026-07-07 | 🟡 65 | Excluded (<75) |
| NG_RI_001.txt | Relief International | Global IT Support Coordinator | Rolling | 🟢 57 | Excluded (<75) |
| NG_WHH_001.txt | Welthungerhilfe | Application Manager CRM Solutions | 2026-07-24 | DISQUALIFIED | Below P-3 (1-3 yrs) |

### Top Score Justification: NG_OAF_001 (92/100)
- P1(25) Domain: AI/ML/Agentic Systems — full cap, production AI engineering
- P2(13) Seniority: Lead role, team mentoring, P-3 equivalent
- P3(14) UN/IFI: INGO + Africa mention (+3)
- P4(8) Education: MSc Elec Eng, Master's implied preferred
- P5(10) Language: English only required
- P6(10) Logistics: Flexible EU locations (Poland/Spain/Portugal/Estonia/Romania)
- P7(12) Competitive: Direct AI engineering + current Hermes/Olivia alignment

### Excluded Entries with Reasons
- Ukraine positions (Team Leader - Mykolaiv, NP) — HARD_NO_UKRAINE
- Junior Project Officer Cybersecurity (DCAF) — Below P-3 equivalent
- Data Entry Clerks (AKF) — Junior/admin
- Education Technical Advisor (ForAfrika) — Not ICT
- Sudan national-only role — HARD_NO_NATIONALS_ONLY
- WHH Application Manager — HARD_NO_BELOW_P3_EQUIVALENT (1-3 years experience)

---

## Tracker After Update
- File: `~/Downloads/DATA_REPOSITORY/NGO_JOBS_TRACKER.TXT`
- Total entries: 7 (3 existing World Vision + 4 new)
- Backup: `NGO_JOBS_TRACKER_BACKUP_20260704_2245.txt`
- All verification checks passed