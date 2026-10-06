# URLSentinel

A phishing and URL threat scanner that runs entirely in your browser.

Paste a link and click Scan. URLSentinel checks it against a set of rule-based detection checks, gives a threat score from 0 to 100, and shows exactly which indicators fired and why.

**Live demo:** https://tanushpradhan.com/tools/urlsentinel.html

**Status:** In progress (live and usable, still being developed)

![URLSentinel result screen](screenshots/scan-result.png)

## Why I built it

Most phishing links look harmless until you read the address closely. I wanted a tool that explains why a link looks suspicious, not one that only says "safe" or "unsafe". It applies what I studied in my B.Tech in Cybersecurity and Networks.

## What it does

- Scores a pasted URL from 0 to 100 and labels it from Clean to Critical threat
- Lists every indicator that fired, ordered by severity, with a plain-language explanation
- Includes sample links to try: a phishing pattern, a legitimate site and a suspicious URL
- Runs from one HTML page with no install, account or backend

## Detection checks

Each check looks at one property of the URL and adds points to the score.

| # | Check | Severity |
|---|-------|----------|
| 1 | IP address used as the host | Critical |
| 2 | High-risk top-level domain (.xyz, .tk, .top and similar) | High |
| 3 | "@" symbol in the URL | Critical |
| 4 | URL shortener | Medium |
| 5 | No TLS encryption (HTTP) | Medium |
| 6 | Deep subdomain nesting | Medium |
| 7 | Brand impersonation and typosquatting (for example paypa1) | Critical |
| 8 | Irregular letter and digit pattern in the domain | Medium |
| 9 | Credential-harvesting keywords in the path (login, verify, secure) | Medium or Low |
| 10 | Hyphen-packed domain | Low |
| 11 | Abnormally long URL | Low |
| 12 | Non-standard port | Medium |
| 13 | Heavy percent-encoding | Medium |
| 14 | Another site's domain embedded in the path | High or Critical |

Two or more critical indicators raise the final label to Critical threat.

## How it works

The scan is plain JavaScript in the page. It parses the URL with the browser's built-in `URL` parser, runs the checks, adds up the points and caps the score at 100. It makes no network requests and sends the URL nowhere, so nothing you paste leaves your browser. There are no API keys or secrets in this project.

## Run it yourself

1. Download or clone this repository.
2. Open `index.html` in a browser.
3. Paste a URL and click Scan.

The page loads three fonts from Google Fonts. Without internet it still works, using fallback fonts.

## Limitations

- URLSentinel is rule-based. It can miss new attacks and can flag harmless links.
- It looks only at the text of the URL. It does not visit the link, check domain age or look up reputation lists.
- Treat the result as a warning sign, not a verdict.

## Roadmap

- [ ] Test the checks against a larger set of known phishing and legitimate URLs
- [ ] Add more lookalike brands and homoglyph detection
- [ ] Add domain-age and reputation checks through a small server-side function

## Author

Tanush Pradhan
Portfolio: https://tanushpradhan.com
LinkedIn: https://linkedin.com/in/tanushpradhan
