# Save the Children International — Portal Profile

## Portal Characteristics
| Property | Value |
|----------|-------|
| **Careers URL** | savethechildren.net/careers |
| **Job detail URL** | savethechildren.net/careers/apply/details?jid={N} |
| **ATS Platform** | Oracle Cloud (hcri.fa.em2.oraclecloud.com) |
| **Curl accessibility** | ✅ Job listing pages return full HTML via curl |
| **Full JD via curl** | ❌ Oracle ATS preview pages are JS-rendered ("SCI Career Site" title only) |
| **Cloudflare** | No |
| **Deadline location** | On the Oracle ATS preview page (JS-rendered, not accessible via curl) |
| **Application method** | Oracle Cloud Candidate Experience portal |
| **Apply button detection** | Search HTML for `class="apply-button"` and `href="https://hcri.fa.em2.oraclecloud.com/..."` |

## Curl Verification Pattern
```bash
# Check if a job is still live (look for apply button)
curl -sL "https://www.savethechildren.net/careers/apply/details?jid={JID}" | grep -c "apply-button"
# Returns 1 if live, 0 if expired/closed
```

## Current Open ICT/Digital Vacancies (2026-07-04)
| JID | Title | Grade | Status |
|-----|-------|-------|--------|
| 14898 | Director, Digital Systems | Director | Live |
| 10944 | Senior Lead, Transformation IT Delivery | Senior Lead | Live |
| 16221 | Senior Lead, Information Security Technology and Architecture | Senior Lead | Live |
| 273 | Technology and Digital Solutions Manager | Manager | Live |
| 14579 | Technology for Development (T4D) Technical Advisor | Advisor | Live |

## Known Issues
- **Listings persist after expiry**: Jobs remain searchable with Apply button even after deadline. Always verify deadline on the Oracle ATS page (requires browser).
- **Oracle ATS blocks curl**: Full JD text is loaded via JavaScript. Use browser_navigate when Camoufox is available, or accept snippet-only extraction from SearXNG results.
- **SearXNG returns good snippets**: The SearXNG content field often contains the first 300 chars of the actual JD, enough for initial filtering.

## Relevance to User
- Director, Digital Systems — senior ICT leadership, directly relevant
- Senior Lead, Transformation IT Delivery — digital transformation, directly relevant
- Senior Lead, InfoSec Architecture — cybersecurity leadership, relevant
- T4D Technical Advisor — ICT4D, directly relevant
- Tech & Digital Solutions Manager — more operational, less relevant
