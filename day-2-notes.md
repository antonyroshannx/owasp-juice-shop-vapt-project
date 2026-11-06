- Target: Local OWASP Juice Shop
## WebSocket observation
- Observed push-notification subprotocol header.
- Received HTTP 400 Bad Request.
- Security impact not established.

## Next investigation
- Identify the API request loading the Administration table.
- Inspect its response and assess authorization.
- Tool: Burp Suite Community Edition
- Status: HTTP 400 Bad Request
- Endpoint:  /v4/threatListUpdates:fetch
- Observation: Server rejected the request as malformed or invalid.
- Security impact: Not yet established.
- Next step: Review the request format and determine why it was rejected.
