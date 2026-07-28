# AfricaNenda Foundation — Portal Profile

## Portal Characteristics

| Attribute | Value |
|-----------|-------|
| **CMS** | WordPress |
| **ATS Platform** | None (PDF-based postings) |
| **Curl Accessibility** | Good — WordPress pages render full HTML |
| **Cloudflare** | No |
| **Job Detail Format** | PDF files linked from careers page |
| **Deadline Location** | In PDF body text (last page, "no later than [date]") |
| **Application Method** | Email to applications@africanenda.org |
| **Careers URL** | https://africanenda.org/work-with-us-category/careers/ |
| **ORG Code** | AFN |

## PDF Extraction Pattern

```bash
curl -sL "https://africanenda.org/wp-content/uploads/[FILENAME].pdf" -o /tmp/afn-job.pdf
python3 -c "
import subprocess
result = subprocess.run(['pdftotext', '/tmp/afn-job.pdf', '-'], capture_output=True, text=True)
if result.returncode == 0:
    print(result.stdout)
else:
    import fitz
    doc = fitz.open('/tmp/afn-job.pdf')
    for page in doc:
        print(page.get_text())
"
```

## Scan Results (2026-06-22)

| Title | Posted | Status | Notes |
|-------|--------|--------|-------|
| Consultant - Programme Manager (DRC) | 10 Jun 2026 | **Open** | Deadline 26 Jun 2026. Requires fluent French. |
| Payment Specialist (Consultant) | May 2026 | Closed | Closed 8 Jun 2026 |
| Program Support Intern | May 2026 | Closed | Internship — filtered |
| Bilingual Payments Project Manager (Guinea) | Jan 2026 | Closed | |

## Relevance to User

Very high — AfricaNenda's mission (digital payments, IIPS, financial inclusion in Africa) directly matches User's payment systems experience (BusPlus, mParking, mobile money, MVNO). However, the French language requirement on the DRC role is a SOFT_NO_REQUIRED_LANGUAGE_GAP blocker.

## ORG Code

`NG-AFN-{NNN}` — e.g., NG-AFN-001 for the Programme Manager DRC role.
