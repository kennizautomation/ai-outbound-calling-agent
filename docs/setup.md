# Configuration and verification guide

## Project-specific ownership
- **GHL:** outbound trigger/drip/webhook workflow and call-analysis webhook workflow.
- **Vapi:** Olivia assistant and exact configured appointment/transfer tools.
- **Make.com:** appointment checking and booking.
- **GHL Calendar:** availability and appointment storage.

## Supplied evidence
Eight screenshots and the owner-provided Olivia prompt. The screenshots are included as redacted configuration evidence; there is no importable Make blueprint or complete Vapi assistant export.

## Private values
Keep transfer numbers, contact identifiers, calendar IDs, account/location IDs, webhook URLs, credentials, real contact records, and health responses out of this public repository. The sanitized prompt uses [BUSINESS_NAME], [DEPARTMENT_NAME], and [ADVISOR_TRANSFER_NUMBER].

## Verify the actual setup
1. Inspect GHL's tag trigger, drip configuration, and outbound webhook privately.
2. Confirm Vapi assistant selection and exact callable names.
3. Inspect Make checking parameters, OpenAI completion instructions, HTTP settings, code, and response.
4. Inspect Make booking request and router filters.
5. Inspect GHL call-analysis payload and contact mapping.
6. Resolve [prompt conflicts](prompt-review.md) with the business owner.
7. Run the [test matrix](test-scenarios.md) and capture correlated evidence.

## Official reference links
These are implementation references, not proof that hidden settings match current API contracts.
- [Vapi server events](https://docs.vapi.ai/server-url/events)
- [Vapi tools](https://docs.vapi.ai/tools)
- [Make webhooks](https://help.make.com/webhooks)
- [GHL calendar events](https://marketplace.gohighlevel.com/docs/ghl/calendars/calendar-events/)

Publishing this repository changes portfolio files only. It does not modify GHL, Make.com, or Vapi production settings or place calls.
