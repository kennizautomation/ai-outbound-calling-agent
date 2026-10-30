# Suggested GHL field mapping

These are logical names. Create or map fields in the actual GHL location and store their real IDs privately. The names below are not built-in API property names.

| Logical value | Suggested destination | Rule |
| --- | --- | --- |
| contact_id | Existing contact ID | Primary association; do not match by name alone |
| call_id | Call note or custom field | Preserve call history; a latest-call field alone is insufficient |
| campaign_id | Custom field or tag | Identify the approved campaign |
| connection_status | Custom field | queued, connected, no_answer, busy, voicemail, failed |
| business_outcome | Custom field | qualified, not_qualified, not_interested, callback_requested, opt_out, unknown |
| service_interest | Custom field | Actual stated interest |
| qualification_summary | Contact note | Factual concise summary |
| preferred_timeline | Custom field | Preserve uncertainty |
| appointment_id | Appointment reference | Present only after confirmed creation |
| callback_at | Custom datetime or task | Include timezone and pending/completed state |
| suppression | Appropriate DND/suppression controls | Map to the relevant channel controls and campaign exclusion |
| next_action | Task or workflow state | Explicit owner and due time when applicable |

## Example opportunity stages
New Lead → Contact Attempted → Qualified → Appointment Booked.
Callback Requested and Not Interested can be separate stages if the business uses them.

Map by configured stage IDs, not display text. Keep the relationship between the contact and intended opportunity explicit; do not overwrite unrelated deals. Do not create duplicate opportunities for repeated call events.

## Booking ownership
GHL Calendar is the appointment source of truth. Confirmed appointment details should include calendar ID, contact ID, appointment ID, start/end time, and timezone. A CRM tag such as "booked" is not proof of an appointment.

## Suppression
Persist opt-out immediately. Check current suppression before every dispatch, retry, or callback. A failed suppression write requires urgent manual review and a local block on further dispatch.
