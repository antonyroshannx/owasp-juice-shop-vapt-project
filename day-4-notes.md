# Day 4 — VAPT Lab Notes: XSS Testing

## Objective
Investigate how OWASP Juice Shop handles HTML-like input in its search bar and capture browser-side evidence.

## Environment
- Target: `http://127.0.0.1:3000`
- Application: OWASP Juice Shop
- Tools: Firefox Developer Tools, Burp Suite
- Test input: `<img src=x onerror=alert(1)>`

## Testing Performed
1. Submitted the test input through the search bar.
2. Inspected requests in Firefox Developer Tools.
3. Observed `logo.png` and `noresults.png` highlighted in red in the Network tab.
4. Attempted to inspect the HTTP response and application behavior.

## Observations
- Network requests observed: `logo.png`, `noresults.png`
- Status codes: To be confirmed from the request details.
- Browser alert execution: Not confirmed.
- Confirmed XSS vulnerability: Not established.

## Evidence
- `01-search-test.png`
- `02-network-requests.png`
- `03-request-details.png`
- `04-console.png` (if applicable)

## Conclusion
The test input was submitted and browser network activity was observed. The red highlighting of image requests alone does not establish an XSS vulnerability. Further analysis of the request status, DOM behavior, and JavaScript execution is required before making a security finding.

## Recommendation
Use context-appropriate output encoding and safe DOM APIs. Avoid inserting untrusted input into HTML without proper sanitization.

## Scope
Testing was conducted against the local OWASP Juice Shop training environment.
