# Make.com scenario build plan

These are configuration instructions, not an importable blueprint. Use supported native modules where suitable, or Make HTTP modules with the current vendor API contracts. Connections and account identifiers must be configured privately.

## Scenario A: eligible lead to outbound call
1. Custom webhook or approved GHL trigger receives contact and campaign identifiers.
2. Retrieve the current GHL contact and relevant opportunity.
3. Filter out suppressed, ineligible, invalid-phone, outside-window, or attempt-limited leads.
4. Reserve the attempt using a serialized dispatch process or durable atomic mechanism.
5. Submit a Vapi outbound call request using the configured assistant and phone number.
6. Store the returned call ID alongside the GHL contact and attempt ID.
7. Mark dispatch status; route failures to reconciliation or manual review.

Do not retry ambiguous call-creation timeouts blindly. A successful submission also does not prove the prospect answered.

## Scenario B: real-time tool requests
1. Receive and validate the Vapi tool request.
2. Route by the configured tool name.
3. Resolve trusted contact, account, and calendar IDs from the call association.
4. Execute availability lookup, booking, callback persistence, or suppression.
5. Return the required Vapi tool response, preserving the original tool-call identifier.

Configure Make's Webhook Response module to return the actual tool result. A generic webhook acknowledgement is not an availability or booking result. Keep this path short enough for the configured Vapi timeout; move nonessential notifications to a separate path.

For booking, use a stable booking request key. Resolve an uncertain result before creating another appointment. For callbacks, save the requested time and a durable pending status. Any later scheduler must recheck suppression and the allowed calling window before dispatch.

## Scenario C: post-call synchronization
1. Receive the configured final call event.
2. Validate its association and deduplicate by call/event identity.
3. Normalize connection status, qualification fields, business outcome, and summary.
4. Update the matching GHL contact and intended opportunity.
5. Save a concise note and next action; notify the owner when configured.
6. Mark processing complete only after required updates succeed.

Apply monotonic state rules: final processing must not clear suppression, erase a confirmed appointment, or downgrade a manually completed follow-up.

## Error paths
| Failure | Handling |
| --- | --- |
| Authentication error | Stop the affected route and alert the owner |
| Rate limiting | Respect provider retry guidance and use bounded retry |
| Create-request timeout | Mark uncertain and reconcile |
| Invalid input | Record validation failure; do not dispatch |
| CRM update fails after booking | Retry CRM update using the existing appointment ID |
| Duplicate event | Return acknowledgement without repeating side effects |

## Make settings to validate
Webhook concurrency, scenario processing order, incomplete executions, error handlers, request timeouts, and log retention all need explicit configuration. Sequential processing in one scenario does not coordinate separate scenarios or external workers.
