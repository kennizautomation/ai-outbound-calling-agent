# Setup and implementation checklist

## Required private configuration
- Vapi assistant, connected calling number, configured tools, and server credentials.
- Make scenarios and private connections.
- GHL location, calendar, pipeline, stage, and custom-field IDs.
- Approved campaign purpose, lead eligibility, calling windows, timezone rules, attempt limits, transfer destination, and callback policy.

Do not commit credentials, webhook secrets, private phone numbers, contact exports, or unredacted recordings.

## Implementation order
1. Configure a test GHL contact, pipeline mapping, and calendar.
2. Build availability and booking tool handling in Make.
3. Connect the tools to a test Vapi assistant using the example prompt.
4. Build call dispatch with eligibility and duplicate protection.
5. Build post-call synchronization and callback persistence.
6. Execute the acceptance test matrix using controlled test contacts.
7. Add redacted screenshots and actual test outcomes to the repository.

The configured campaign must meet the business's applicable permission and calling requirements. This repository does not establish those requirements or authorize calls.

## Evidence still needed
Actual Make blueprint, redacted Vapi configuration, GHL field mappings, platform test results, and any authorized demo recording. Add only artifacts matching the implemented system.

## Official technical references
Reviewed as design references on 2026-10-30. Verify current request fields and authentication while implementing.
- [Vapi server events](https://docs.vapi.ai/server-url/events)
- [Vapi tools](https://docs.vapi.ai/tools)
- [Make webhooks](https://help.make.com/webhooks)
- [Make scenario settings](https://help.make.com/scenario-settings)
- [GHL free slots](https://marketplace.gohighlevel.com/docs/ghl/calendars/get-slots/index.html)
- [GHL calendar events](https://marketplace.gohighlevel.com/docs/ghl/calendars/calendar-events/)

## Validation scope
This repository contains documentation and internal synthetic examples. It does not include executable integration code, verified API credentials, or an importable automation. Publishing these files does not configure the platforms or place calls.
