# 2026-07-04 NGO Scan: SearXNG All Engines Blocked → ReliefWeb Pivot

## Situation
All 8 SearXNG queries returned 0 results. Every upstream engine blocked the instance:
- Brave: "Suspended: too many requests"
- DuckDuckGo: CAPTCHA
- Startpage: CAPTCHA
- KarmaSearch: "Suspended: access denied"
- Google: 0 results (rate limited)

The SearXNG container was healthy (`docker ps` confirmed running, JSON API responded with `{"number_of_results": 0, "results": []}`). This is a persistent upstream blocking state, not a transient rate-limit.

## Pivot: ReliefWeb Direct Browser Extraction

Navigated directly to:
```
https://reliefweb.int/jobs?search=ICT+OR+digital+OR+telecom+OR+information+technology
```

### Extraction Pattern
1. **Get all articles from the search results page:**
```js
Array.from(document.querySelectorAll('article')).map(a => {
  const title = a.querySelector('h3')?.textContent?.trim();
  if (!title) return null;
  const url = a.querySelector('h3 a')?.href;
  const org = a.querySelector('dd a')?.textContent?.trim();
  const dds = a.querySelectorAll('dd');
  const closing = dds[1]?.querySelector('time')?.textContent?.trim();
  const countryEl = a.querySelector('p a');
  const country = countryEl?.textContent?.trim();
  return {title, url, org, closing, country};
}).filter(x => x !== null)
```

2. **Filter for ICT-relevant titles** using keywords: ICT, digital, technology, information systems, AI, connectivity, telecom, network, data, transformation, CIO, CTO, director, lead, innovation, cybersecurity, software, cloud, automation.

3. **Navigate to each viable JD page** via `browser_navigate(url)` and extract full description via `browser_console` with `document.body.innerText`.

4. **Save as text files** to `NGO_JD_FILES/` with pattern `NG_{ORG}_{NNN}.txt`.

### Results
- 92 results across 5 pages on ReliefWeb
- 9 viable ICT-relevant JDs saved
- Yield: ~10% (9/92)

### Blocked Portals (SearXNG unavailable)
NRC, DRC, CARE, WVI, Save the Children, Internet Society, BRAC, MSF, World Vision careers, Rescue.org, Plan International, Impactpool, Gates Foundation, Clinton Health Access — all unreachable via SearXNG.

### Key Insight
ReliefWeb is the highest-yield single source for NGO ICT vacancies. A single browser_navigate to its search page with ICT keywords yields more viable leads than all per-portal SearXNG queries combined. **Start here, skip SearXNG entirely.**
