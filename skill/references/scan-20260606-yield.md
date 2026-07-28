# NGO Scan Yield — 2026-06-06

Scanned 12 SearXNG queries across all 25 target NGOs. 2 new entries found.

## Portal Verification Notes

| Portal | Accessibility | Method | Notes |
|--------|-------------|--------|-------|
| **Save the Children** (savethechildren.net) | ✅ curl works | curl + regex | Closure detection: HTML contains "no longer accepting applications" and "closed earlier than advertised" patterns. Director Digital Systems → CLOSED. Senior Lead InfoSec → CLOSED. |
| **World Vision** (Workday) | ✅ curl works | curl + JSON-LD | worldvision.wd1.myworkdayjobs.com returns structured LD+JSON. Can extract: title, datePosted, validThrough, employmentType, description, jobLocation. 2 open entries found. |
| **DRC** (drc.ngo) | ❌ curl returns empty | Needs Camoufox | Both job detail pages (id=176021, 176022) returned 0 bytes. Likely Cloudflare or JS-rendered single-page app. SearXNG snippets confirm AI Engineer + Director of Global IT exist but deadlines could not be verified via curl. |
| **Plan International** (jobs.plan-international.org) | ❌ curl returns empty | Needs Camoufox | Workday-based but blocked. SearXNG returned IT job category page only. |
| **Oxfam** (oxfam.current-vacancies.com) | ⚠️ Partial curl | curl works for HTML, deadline in JS | D365 F&O Systems Engineer found but ERP role, not relevant. Site uses JS for deadline rendering ("Expired" string detection available). |
| **NRC** (nrc.no) | ⚠️ Partial curl | curl works for careers pages | Careers pages return HTML but individual job listings are deeper. No relevant ICT/AI roles found via SearXNG. |
| **MSF** (irffg.msf.org) | ❌ Cloudflare | Blocked | Returns "Just a moment..." Cloudflare challenge. |
| **FundsForNGOs** (fundsforngos.org) | ❌ Cloudflare | Blocked | CTO at AKDN listing blocked. |
| **NGO Jobs Africa** (ngojobsinafrica.com) | ❌ Cloudflare | Blocked | Both CTO and Digital Strategy Consultancy pages blocked. |
| **ReliefWeb** | ⚠️ Only category pages | curl | Returns category-listing pages, not individual jobs. Cannot extract specific NGO ICT listings. |
| **Internet Society** (internetsociety.org) | ✅ curl works | curl | No job listings found — only program pages, blog, grants. |

## Common NGO ATS Patterns

| ATS Platform | Examples | Bot-friendliness |
|-------------|----------|-----------------|
| **Workday** | World Vision, IRC, many others | ⚠️ JSON-LD available via curl on detail pages; search/index pages may be empty |
| **Recruitee** | See freelance skill — Oxfam uses separate vendor | ✅ Full JSON-LD, accessible |
| **Oracle Cloud** | NORCAP (NRC deployments) | ❌ JS-rendered, curl empty |
| **SmartRecruiters** | Some NGOs | Variable |
| **Custom Drupal** | Save the Children | ✅ curl works, closure text detectable |

## Yield Summary

- **Total SearXNG queries:** 12
- **Total results examined:** ~120
- **Viable leads after hard filter:** 2 (World Vision only)
- **Expired/closed/blocked/irrelevant:** 18+
- **Effective yield rate:** ~1.7%