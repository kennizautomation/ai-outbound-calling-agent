# Actual system architecture

Updated from the owner's clarification and eight supplied screenshots.

## Responsibility map
| Platform | Role in this project |
| --- | --- |
| GHL workflows | Outbound call initiation and call-analysis handling |
| Vapi | Olivia's conversation, qualification, appointment-tool requests, and advisor transfer |
| Make.com | Appointment availability checking and appointment booking |
| GHL Calendar | Calendar availability and appointment records |

## Outbound path
The supplied GHL workflow shows **Contact Tag → Drip mode → Custom webhook**. The owner identifies this as the Vapi outbound-call workflow. The webhook URL, headers, body, and precise batching settings are not visible, so this repository does not invent them.

## Call-analysis path
The supplied GHL “Vapi Agent Call Analysis” workflow shows **Inbound Webhook → Create contact**. The owner confirms call-analysis handling is in GHL. The screenshot does not expose the webhook payload, analysis generation, field mapping, or contact deduplication behavior. No Make post-call scenario is claimed.

## Appointment tools
- `KappointmentAvailability`: Olivia requests the next ten days of slots through the Make checking scenario.
- `KAppointment_booking`: Olivia submits the selected, confirmed time through the Make booking scenario.
- `transferCall`: advisor transfer as specified in the supplied prompt; destination redacted.

These names are case-sensitive. See [prompt review](prompt-review.md) for the transfer-name discrepancy visible in the tool list.

## Checking scenario
**Custom webhook → OpenAI completion → HTTP availability lookup → Make Code → Webhook response.**
The screenshot shows the module order and a GHL free-slots path. The calendar ID has been redacted. The OpenAI prompt and Make Code source are not visible; their exact transformations are not asserted.

## Booking scenario
**Custom webhook → HTTP (legacy) → Router → Booked / Not Booked webhook responses.**
The screenshot labels the request POST /v1/appointments. This is documented as observed, not recommended as a current API endpoint. The full URL, API version, authentication, and branch filters are not visible. A 200 response label on the module is not proof that a booking executed successfully.

## Evidence limits
Screenshots demonstrate configuration views and calendar entries. They do not provide a correlated lead → call ID → booking ID execution trace. Published/Active UI states are recorded as shown, not treated as end-to-end test results.

## Recommended validation, not established implementation
Check suppression and calling windows in the GHL dispatch path; prevent duplicate dispatch; validate webhook associations; reconcile uncertain booking results; preserve timezone data; and map call outcomes to the correct contact. None of those hidden settings can be verified from these screenshots alone.
