# NGO Portal Scan Results — 2026-06-06

Batch scan across 25 target NGOs. 12 SearXNG queries + direct curl verification.

## Entries Found (added to tracker)

| ID | Org | Title | Deadline | Score |
|----|-----|-------|----------|-------|
| NG-WVI-001 | World Vision Intl | Digital Platform Engineer (Armenia, home) | Open | 🟡 70 |
| NG-WVI-002 | World Vision Intl | Digital Transformation PM (Philippines, home) | Open | 🟡 73 |

## Expired / Closed / Excluded

| Portal | Role | Reason |
|--------|------|--------|
| Save the Children | Director, Digital Systems | CLOSED (no longer accepting) |
| Save the Children | Senior Lead, InfoSec | CLOSED |
| Oxfam International | Senior D365 F&O Systems Engineer | ERP, not relevant profile |
| Oxfam International | Head of Brand, Communications & Digital Engagement | Comms, not tech |
| World Vision | Information Communication & Technology Officer Tanzania | Posted 2023, expired |
| NGO Jobs Africa | CTO | Cloudflare blocked |
| NGO Jobs Africa | Digital Strategy Consultancy | Expired Sep 2024 |
| MSF | ICT Supervisor | Cloudflare blocked |
| MSF | Digital Health Promotion Officer Gaza | Health-specific, irrelevant |
| Internet Society | Community-Centered Connectivity | Grants/Programs — not job |
| Internet Society Foundation | Grant Programs | Not employment |

## Platforms Verified Working (curl-accessible)
- World Vision (Workday) ✅ structured JSON-LD via curl
- Save the Children (Drupal) ✅ curl-accessible
- Oxfam (current-vacancies.com) ✅ curl-accessible, JS-rendered expiry
- DRC (drc.ngo) ✅ curl-accessible but requires JS for deadlines

## Platforms Blocked (Cloudflare / login-gated)
- MSF (irffg.msf.org) ❌ Cloudflare
- fundsforngos.org ❌ Cloudflare
- Plan International (Workday) ❌ Cloudflare redirect
- WBIF ❌ Cloudflare
- Expert360 ❌ Cloudflare

## Oxfam Scan Detail
All 3 Oxfam portal URLs verified as functional:
- `oxfam.org/en/take-action/jobs` — redirects to current-vacancies.com
- `oxfam.current-vacancies.com` — working, 2 tech-adjacent roles found (neither relevant)
- `jobs.oxfam.org.uk` — UK-specific roles, none ICT

No ongoing ICT/Digital/AI/Connectivity vacancies found at Oxfam.