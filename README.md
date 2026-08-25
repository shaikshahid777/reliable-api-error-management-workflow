# Reliable API Error Management Workflow — Lesson 5 Assessment

Production-style n8n workflow for retry protection, timeout handling, inline API error trapping, status-code routing, centralized error monitoring, and structured incident reporting.

## Main Workflow

```text
Manual Trigger
      ↓
HTTP_RetryOnFailure
      ↓
HTTP_TrapErrorsInline
      ↓
IF_IsError404
   ↙          ↘
404           Other / Success
 ↓                 ↓
Log_ProfileNotFound  Log_Success
```

## Centralized Error Monitoring

```text
Error Trigger
      ↓
Build_Incident_Report
      ↓
Log_SlackAlert
```

## Reliability Features

- Retry on Failure with maximum 3 attempts
- 2-second retry interval
- Timeout protection configured at 10 seconds
- Inline error continuation and full response handling
- HTTP 404 conditional routing
- Structured Profile Not Found logging
- Centralized Error Trigger workflow
- Incident fields: failedNode, executionId, workflowName, errorMessage, incidentTime
- Slack alert integration

## Testing

Recommended test cases:

- HTTP 200 successful response
- HTTP 404 profile-not-found response
- HTTP 429 rate limiting
- HTTP 503 temporary service failure
- Network interruption
- Authentication failure
- Slow API response / timeout
- Unhandled workflow failure through Error Trigger

## Important Verification Note

The exported workflow JSON contains placeholder API URLs that must be replaced with valid test endpoints before final reproduction. The Slack alert step requires a valid Slack credential and destination channel.

Before final LMS submission, verify that exponential backoff is explicitly enabled in the n8n HTTP Retry node UI if required by the assessment rubric.

## Repository Structure

```text
reliable-api-error-management-workflow/
├── README.md
├── workflow/
│   ├── Reliable_API_Workflow.json
│   └── Centralized_Error_Monitor.json
├── documentation/
│   └── Reliable_API_Error_Management_Workflow_Documentation.pdf
├── screenshots/
│   ├── workflow.png
│   ├── execution-success.png
│   └── centralized-error-monitor.png
└── test-evidence/
    └── test-results.md
```

## Security

Do not commit API keys, tokens, passwords, Slack secrets, or other credentials. Store credentials in n8n Credential Manager and mask sensitive values in screenshots and documentation.

## Setup

1. Import the two exported n8n workflow JSON files.
2. Replace placeholder API URLs with valid test endpoints.
3. Verify retry, timeout, and inline error settings.
4. Configure Slack credentials/channel for centralized alerts.
5. Run success and 404 tests plus the required reliability scenarios.
6. Capture evidence and export the final workflow JSON after validation.
