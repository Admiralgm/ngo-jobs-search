# Clinton Foundation / CHAI — Portal Profile

## Portal Characteristics

### Clinton Foundation

| Attribute | Value |
|-----------|-------|
| **CMS** | Custom WordPress |
| **ATS Platform** | Unknown (iframe-based) |
| **Curl Accessibility** | Poor — careers page uses iframe for job listings |
| **Cloudflare** | No |
| **Job Detail Format** | Hidden behind iframe |
| **Deadline Location** | Unknown |
| **Application Method** | Via iframe portal |
| **Careers URL** | https://www.clintonfoundation.org/careers/apply/ |
| **ORG Code** | CLF |

### CHAI (Clinton Health Access Initiative)

| Attribute | Value |
|-----------|-------|
| **CMS** | Custom WordPress |
| **ATS Platform** | iCIMS (careers-chai.icims.com) |
| **Curl Accessibility** | Poor — iCIMS uses iframe, hard to scrape |
| **Cloudflare** | No |
| **Job Detail Format** | iCIMS job detail pages |
| **Deadline Location** | In iCIMS job detail |
| **Application Method** | iCIMS online application |
| **Careers URL** | https://www.clintonhealthaccess.org/join-our-team/ |
| **iCIMS Search URL** | https://careers-chai.icims.com/jobs/search?ss=1&searchKeyword=digital+OR+ICT+OR+technology+OR+AI+OR+data |
| **ORG Code** | CHAI |

## iCIMS Scraping Notes

- iCIMS loads job listings inside an iframe. `browser_navigate` to the iCIMS URL directly may work better than navigating to the CHAI careers page.
- SearXNG cannot index iCIMS content.
- The iCIMS search URL supports query parameters: `searchKeyword=digital+OR+ICT+OR+technology+OR+AI+OR+data`
- Job detail pages are standard HTML once you navigate to a specific job.

## Scan Results (2026-06-22)

**Clinton Foundation:** No ICT-relevant vacancies visible. The careers/apply/ page shows an iframe that may require JavaScript to load.

**CHAI:** No ICT/AI/digital vacancies found in iCIMS search. Most CHAI roles are health program management, clinical, or supply chain.

## Relevance to User

Moderate. CHAI is a large global health NGO with significant digital health programs, but their ICT vacancies are rare. The iCIMS ATS makes automated discovery difficult. Worth checking manually every 2-3 months.
