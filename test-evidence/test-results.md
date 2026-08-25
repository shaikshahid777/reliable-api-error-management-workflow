# Test Results / Execution Evidence

## Test 1 — Successful API Request
- Expected: HTTP 200 response is handled by `Log_Success`.
- Observed: Workflow completed successfully with statusCode 200.

## Test 2 — HTTP 404
- Expected: `IF_IsError404` routes the record to `Log_ProfileNotFound`.
- Observed: 404 is treated as a handled profile-not-found condition.

## Test 3 — HTTP 429
- Expected: Retry strategy handles transient rate limiting where the endpoint permits retry.
- Verification: Confirm retry attempts and final response in the n8n execution log.

## Test 4 — HTTP 503
- Expected: Temporary service failure is retried according to configured retry policy.
- Verification: Confirm attempts, backoff timing, and final outcome in execution history.

## Test 5 — Timeout / Slow Response
- Expected: Request terminates at the configured timeout instead of blocking indefinitely.
- Verification: Run against a deliberately slow test endpoint and capture execution evidence.

## Test 6 — Centralized Error Trigger
- Expected: Unhandled workflow errors invoke `Error Trigger → Build_Incident_Report → Log_SlackAlert`.
- Incident fields: failedNode, executionId, workflowName, errorMessage, incidentTime.

## Evidence

Screenshots should be stored in this directory and referenced from the LMS submission. Never include API keys, bearer tokens, OAuth client secrets, or Slack credentials in screenshots.