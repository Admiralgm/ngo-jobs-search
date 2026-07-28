# NGO Jobs Search

Scans 28+ NGO career portals for senior-level ICT, digital transformation, AI, telecom, and connectivity vacancies. Uses SearXNG meta-search, direct browser verification, and PDF ToR extraction. Maintains a scored tracker file.

## Architecture

```
ngo-jobs-search/
├── skill/
│   ├── SKILL.md              # Full operational skill (30KB)
│   └── references/           # 13 technical reference docs
│       ├── scan-20260717-calibration.md
│       ├── scan-20260717-discovery-methods.md
│       ├── scan-20260704-reliefweb-pivot.md
│       ├── scan-20260704-reliefweb-orchestrator.md
│       ├── scan-20260622-reliefweb.md
│       ├── scan-20260622-yield.md
│       ├── scan-20260606-yield.md
│       ├── portal-yields-2026-05-30.md
│       ├── portal-yields-2026-06-06.md
│       ├── africanenda-portal-profile.md
│       ├── gates-foundation-portal-profile.md
│       ├── clinton-chai-portal-profile.md
│       └── save-the-children-portal-profile.md
├── .gitignore
├── LICENSE
└── README.md
```

## Portals Covered (28+)

### Tier 1 — High-Priority (14)
- Norwegian Refugee Council (NRC) — Oracle Cloud
- Danish Refugee Council (DRC) — Custom
- CARE International — Custom
- Unconnected.org — Connectivity focus
- Internet Society — Digital rights
- Internet Society Foundation — Grants
- World Vision International — Workday
- Turing Trust — ICT for education
- NetHope — AI Accelerator, Digital Hub (PDF ToR)
- BRAC International — Custom
- Oxfam International — Custom
- Médecins Sans Frontières (MSF) — Custom
- AfricaNenda Foundation — Digital payments
- Bill & Melinda Gates Foundation — Workday
- Clinton Foundation / CHAI — iCIMS

### Tier 2 — 25 Largest NGOs (14)
- Save the Children International
- International Rescue Committee (IRC)
- Plan International
- Mercy Corps
- Catholic Relief Services (CRS)
- Action Against Hunger (ACF)
- Practical Action
- PATH
- WWF
- Amnesty International
- Human Rights Watch
- Transparency International
- WaterAid
- IFRC

### Supplementary Sources
- ReliefWeb NGO Jobs
- Impactpool (NGO filter)
- NGO Jobs in Africa
- DevelopmentAid
- UNjobs (NGO section)

## Search Method Hierarchy

1. **web_search_plus** (PRIMARY) — auto-routes around blocked engines
2. **Direct NGO PDF ToR extraction** — `curl -sL [URL] -o /tmp/file.pdf && pdftotext`
3. **Direct curl to NGO portals** — Workday/Oracle HTML parsing
4. ~~SearXNG~~ (DEPRECATED — all engines blocked)
5. ~~ReliefWeb API~~ (DEPRECATED — Cloudflare blocked)
6. ~~Camoufox~~ (UNRELIABLE — M4 Mac arch mismatch)
7. ~~Scrapling/curl_cffi~~ (BROKEN on this Mac)

## Scoring

Uses a 7-parameter vacancy compatibility scoring engine:
1. Domain alignment (ICT/AI/telecom/digital)
2. Seniority match
3. Technical skill overlap
4. Language requirements
5. Location/remote eligibility
6. Education equivalence
7. Transferable skills bridge

Color coding: 🔴 90+ STRONG FIT | 🟠 80-89 COMPETITIVE | 🟡 70-79 STRETCH | 🟢 <70 LOW FIT

## Known Pitfalls

- World Vision: "Local Applicants Only" = hard disqualifier for international candidates
- Gates Foundation: US work authorization required = hard disqualifier without US visa
- Save the Children: Listings persist in search results after expiry — verify on portal
- ReliefWeb: "Gone" status doesn't mean closed — check direct NGO source
- SearXNG: All engines blocked since 2026-07-04 — use web_search_plus instead
- Camoufox: broken on M4 Mac (x86_64 native module vs arm64e)

## License

MIT — see [LICENSE](LICENSE)
