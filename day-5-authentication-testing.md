
# Day 5 — Authentication and Session Management Testing

## Finding: Potential Account Data Exposure After Logout

**Target:** OWASP Juice Shop (Local Lab)

**Testing Area:** Authentication and Session Management

**Observation:** Account information appeared accessible after logout during initial testing.

**Validation Status:** Pending.

**Next Action:** Repeat the same account API request after logout and inspect the HTTP response to determine whether protected account data is actually returned.

**Severity:** Not yet determined.

**Evidence:** Firefox Developer Tools — Network tab, authenticated and unauthenticated request/response comparison.

## Test Results

| Test | Result |
|---|---|
| Login successful | Yes |
| JWT authentication observed | Not confirmed |
| Authorization header observed | Yes |
| Account data accessible while logged in | Yes |
| Account data accessible after logout | Needs validation |

## Tools Used
- Kali Linux
- OWASP Juice Shop
- Firefox Developer Tools
- Burp Suite Community Edition

## Conclusion

Initial authentication testing was completed.
Further validation is required to determine whether account information remains accessible after logout.
