# GHL data mapping — supplied variables and proposed checks

The owner's source prompt provides these variable names. Actual GHL custom-field IDs and webhook mappings were not included.

| Prompt variable | Meaning |
| --- | --- |
| {{client_name}} | Contact display name |
| {{phone_number}} | Contact phone |
| {{address}} | Contact address |
| {{email}} | Contact email |
| {{Contact_ID}} | GHL contact reference |
| {{current_time}} | Current/local time supplied to the agent |
| {{timezone}} | Timezone |
| {{timeoffset}} | Time offset |
| {{allslot}} | Ten-day availability data |

The Vapi booking-tool screenshot visibly includes LastName, Timezone, datetime, and FirstName fields. It is only a partial schema; other inputs must not be inferred as configured.

## Qualification information in the supplied script
Existing coverage, desired monthly payment and explanation, family motivation, an emotional descriptor, smoking status, health-history response, height, weight, and ZIP code.

These are question topics, not verified GHL field mappings. No real answers are published. Treat any collected health responses as restricted information and keep them out of public examples.

## Recommended integration checks
Confirm how the GHL analysis webhook associates a call with a contact, what the Create contact action does for an existing contact, and which fields are updated. Keep actual appointment IDs separate from an intent to book. Do not claim opportunity/pipeline updates until their configuration is supplied.
