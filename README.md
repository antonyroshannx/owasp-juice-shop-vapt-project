# owasp-juice-shop-vapt-project
A practical web application security assessment conducted in an authorized local lab environment.

This repository documents a hands-on Vulnerability Assessment and Penetration Testing (VAPT) project using OWASP Juice Shop. The work focuses on learning and documenting a repeatable web security testing workflow: reconnaissance, HTTP traffic inspection, input-handling tests, authentication/session review, and access-control investigation.
Assessment note: This is a learning project, not a production penetration test. Findings are reported according to the evidence collected. Potential issues that have not been fully validated are explicitly marked as pending rather than claimed as confirmed vulnerabilities.

Project Overview
Field	Details
Project	Web Application Vulnerability Assessment & Penetration Testing
Target	OWASP Juice Shop
Environment	Local lab on Kali Linux
Target URL	http://127.0.0.1:3000
Approach	Manual, evidence-driven testing
Tools	Nmap, Burp Suite Community Edition, Firefox Developer Tools
Documentation	Day-wise notes, evidence, and final assessment report


Objectives
- Perform reconnaissance against the locally hosted application.
- Capture and analyze HTTP requests and responses.
- Investigate potential Cross-Site Scripting (XSS) behavior.
- Review authentication and session behavior, including post-logout access.
- Explore API behavior and access-control boundaries within the authorized lab.
- Document observations, validation status, evidence, and remediation guidance.
- Build practical skills in web application security testing and professional reporting.
Scope and Authorization
In scope
- OWASP Juice Shop running locally.
- Local host 127.0.0.1, with TCP port 3000 observed open.
- Manual testing of application-generated traffic and responses.
- Reconnaissance and testing using the tools listed in this repository.
Out of scope
- Public websites or systems belonging to other parties.
- Real user accounts or production data.
- Destructive testing, denial-of-service activity, or any testing without authorization.
All testing documented here was conducted against a local OWASP Juice Shop training instance.
Lab Setup
The assessment environment used:
- Kali Linux
- OWASP Juice Shop
- Firefox
- Burp Suite Community Edition
- Nmap
The application was accessed at:
http://127.0.0.1:3000
A local Nmap service-detection scan was performed against TCP port 3000:
nmap -sV -p 3000 -oN evidence/nmap-local.txt 127.0.0.1
The recorded scan showed the host up and port 3000/tcp open. Nmap returned the application HTML in its service fingerprint but did not identify a definitive service/version. This is a reconnaissance observation, not a vulnerability finding.
Methodology
The project follows a practical assessment cycle:
1. Reconnaissance — identify the local target and exposed service.
2. Traffic inspection — capture application requests and responses.
3. Input testing — submit controlled test inputs and inspect reflection and browser behavior.
4. Authentication/session testing — compare behavior in authenticated and logged-out states.
5. API/access-control investigation — inspect selected endpoint responses and authorization behavior.
6. Evidence and reporting — document what was observed, what remains unverified, and recommended next steps.
Day-wise Assessment Progress
The day-wise notes preserve the learning and testing progression. They are supporting records; the consolidated report provides the overall project summary.
Day	Focus	Recorded status
Day 1	Local reconnaissance and service discovery	Nmap evidence recorded
Day 2	WebSocket/API observations and Administration data investigation	HTTP 400 responses recorded; authorization follow-up identified
Day 3	Preliminary XSS testing and HTTP security-header review	Payload reflection and browser alert reported; execution context requires validation
Day 4	Search input handling and browser network observations	Input submitted; XSS execution not confirmed
Day 5	Authentication and session management	Post-logout account-data exposure requires validation
Day 6	IDOR / access-control assessment	Investigation in progress; confirm impact with request/response evidence


Update this table as testing progresses. Do not mark a suspected vulnerability as confirmed until the request, response, behavior, and impact have been validated.

Assessment Observations
The current notes document the following observations and test leads:
Reconnaissance
- Local host 127.0.0.1 was reachable.
- TCP port 3000 was open.
- The response contained the OWASP Juice Shop application HTML.
XSS and input handling
- A test payload was found in an HTTP response during preliminary testing.
- A browser alert displaying xss was reported.
- A separate <img> input test produced network activity involving logo.png and noresults.png; JavaScript execution was not confirmed.
- The observed X-XSS-Protection: 0 header is not, by itself, proof of a vulnerability.
Authentication and session behavior
- Login was successful.
- An authorization header was observed.
- JWT usage was not confirmed in the recorded notes.
- Account data was available while logged in.
- Post-logout access remains to be validated by comparing the same API request and response.
API / WebSocket behavior
- A WebSocket push-notification request returned HTTP 400 Bad Request.
- /v4/threatListUpdates:fetch returned HTTP 400 Bad Request.
- The security impact of these responses has not been established.
- Authorization testing of the Administration table request was identified as a follow-up.
These are recorded as observations or pending validation items, not as a list of confirmed vulnerabilities.
Findings and Validation Status
ID	Item	Status
OBS-01	Local service responding on TCP/3000	Observed
OBS-02	X-XSS-Protection: 0 response header	Observed; informational by itself
VULN-01	Potential XSS in input/search handling	Validation pending
VULN-02	Potential account-data exposure after logout	Validation pending
OBS-03	API/WebSocket requests returning HTTP 400	Observed; impact not established
TEST-01	Administration table authorization	Follow-up assessment pending
TEST-02	IDOR / resource access-control behavior	Investigation in progress


Severity ratings are intentionally omitted for unvalidated issues. Severity should be assigned only after exploitability and impact are demonstrated.
Recommendations
Recommendations are provided as general defensive guidance for the areas being assessed:
- Use context-aware output encoding and safe DOM APIs.
- Avoid inserting untrusted input into HTML without appropriate sanitization.
- Use Content Security Policy as a defense-in-depth control.
- Enforce authentication and authorization on every protected API request.
- Invalidate sessions or tokens appropriately during logout.
- Verify user- and role-specific access controls server-side.
- Capture reproducible request/response evidence before confirming findings.
- Redact session cookies, authorization tokens, and personal data from public evidence.
Repository Structure
A suggested organization for this project:
owasp-juice-shop-vapt/
├── README.md
├── reports/
│   └── Final-VAPT-Report.md
├── methodology/
│   ├── Day-01-Reconnaissance.md
│   ├── Day-02-API-WebSocket-Observations.md
│   ├── Day-03-XSS-Testing.md
│   ├── Day-04-Input-Validation.md
│   ├── Day-05-Authentication-Testing.md
│   └── Day-06-IDOR-Assessment.md
├── evidence/
│   ├── reconnaissance/
│   ├── xss/
│   ├── authentication/
│   └── access-control/
└── tools/
    └── tools-used.md
This is a suggested structure. Keep only files and folders that exist, and align each day’s filename and status with the work actually performed.
Evidence Handling
Evidence may include:
- Nmap output
- Burp Suite request/response captures
- Browser Network and Console screenshots
- Authenticated versus logged-out API comparisons
- Screenshots demonstrating reproducible behavior
Before publishing evidence:
- Remove or mask cookies and authorization headers.
- Redact personal or account information.
- Avoid publishing secrets, tokens, or sensitive data.
- Include enough context to make each screenshot understandable.


The report includes the project summary, scope, methodology, observations, validation status, recommendations, limitations, and references.
Skills Demonstrated
- Web application security testing fundamentals
- Network/service reconnaissance with Nmap
- HTTP request and response analysis
- Burp Suite Proxy and HTTP history
- Firefox Developer Tools
- Preliminary XSS assessment
- Authentication and session-management testing
- API and access-control investigation
- Evidence collection and technical documentation
- Responsible testing in an authorized lab
References
- OWASP Juice Shop
- OWASP Web Security Testing Guide
- OWASP Cross Site Scripting Prevention Cheat Sheet
- OWASP Authorization Cheat Sheet
- OWASP Session Management Cheat Sheet
Disclaimer
This repository is intended for educational and portfolio purposes only. Testing was performed against a local OWASP Juice Shop instance in an authorized environment. Do not use these techniques against systems without explicit permission.
