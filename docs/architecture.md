# Architecture and call lifecycle

## Ownership
GHL owns contact, opportunity, suppression, and appointment records. Vapi owns the call session. Make coordinates them and retains a durable processing ledger.

## Lifecycle
1. Receive a lead identifier and campaign identifier from a selected GHL trigger.
2. Fetch current contact data. Check calling permission, suppression, valid phone, local calling window, attempt limit, and whether a call is already pending.
3. Reserve a unique attempt in a durable ledger before requesting a Vapi call. Use a campaign/contact/attempt identifier. Store the returned call ID.
4. Handle real-time tools separately from post-call processing.
5. Reconcile final call events using the call ID. Store outcomes without reverting confirmed booking or opt-out state.

## Proposed application tools
These are project-defined names, not claims about existing configured tools.

| Tool | Required input | Result |
| --- | --- | --- |
| check_availability | Calendar ID resolved server-side, date range, IANA timezone | Available slots with explicit offsets |
| book_appointment | Contact ID, selected slot, caller confirmation, booking key | Confirmed appointment ID or explicit failure |
| schedule_callback | Contact ID, desired time, timezone | Persisted callback ID or failure |
| record_opt_out | Contact ID, call ID | Persisted suppression status |

Use Vapi's configured transfer capability for live transfers. Define the destination and availability rules in the actual assistant setup.

## Time handling
Resolve the prospect's timezone before offering times. Keep timezone and offset data in storage; use readable 12-hour times in speech. Recheck availability before creation. Never bypass slot validation to force an appointment. Confirm success only after GHL returns a successful appointment result.

## Reliability
- Authenticate inbound requests using mechanisms supported by the chosen integration; validate expected event types and call/contact associations.
- Scope tool requests to the configured account and calendar; never trust arbitrary caller-provided account IDs.
- Deduplicate post-call events by call ID and event identity. Track processing state and retries.
- Use an atomic reservation or serialized queue for call dispatch. A search followed by a write is not a concurrency lock.
- Treat timeouts on call or appointment creation as uncertain outcomes. Reconcile against provider records before retrying.
- Persist booking success before later CRM notes or notifications. Retry those downstream steps without creating another booking.
- Keep opt-out processing independent of final-summary delivery.
- Record API errors and alert the owner when retries are exhausted.

## Outcomes
Keep connection status, business outcome, and booking status separate. A connected call is not automatically a qualified lead. No answer, voicemail, busy, and failed are connection results; callback requested, not interested, qualified, and opt-out are business outcomes. Booking status is confirmed only when an appointment ID exists.
