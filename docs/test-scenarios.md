# Acceptance test plan — Olivia

These tests are **not recorded as passed**. Screenshots are configuration evidence only. Use controlled test contacts; do not publish health responses or personal details.

| # | Test | Acceptance criterion |
| --- | --- | --- |
| 1 | GHL tag trigger | Correct contact reaches drip action and outbound webhook |
| 2 | GHL webhook to Vapi | One intended call is created and associated with the contact |
| 3 | Repeated trigger | No unintended duplicate call |
| 4 | GHL analysis webhook | Correct call/contact mapping and intended contact action |
| 5 | Direct booking request | Qualification questions bypassed; ZIP handling follows the approved rule |
| 6 | Qualification path | Questions follow approved order without repeated answers |
| 7 | Budget exactly $20 | Explicit approved branch exists |
| 8 | Availability tool | Exact KappointmentAvailability name; next ten days requested |
| 9 | Requested slot exists | Actual returned slot offered and confirmed |
| 10 | Requested slot unavailable | Up to three actual closest alternatives; no invented availability |
| 11 | No slots | Clear unavailable result and approved next action |
| 12 | Booking tool | Exact KAppointment_booking name; confirmed selection passed |
| 13 | Booking succeeds | One GHL appointment; success spoken only after confirmation |
| 14 | Booking fails or times out | No false success; uncertain creation reconciled before retry |
| 15 | Three confirmed failures | Approved transfer offer; no automatic transfer |
| 16 | Advisor request | Clear immediate-transfer agreement and verified transferCall attachment |
| 17 | Transfer completes | No false appointment confirmation afterward |
| 18 | Transfer unavailable | Accurate fallback without an invented booking |
| 19 | Date/time handling | Month, day, and time spoken without year; timezone correct internally |
| 20 | ZIP handling | Approved resolution of ask-once versus confirmation conflict is followed |
| 21 | Wrong person or no-request objection | Approved truthful response; no fabricated referral source |
| 22 | Do-not-call request | GHL suppression behavior verified before any subsequent dispatch |
| 23 | One-question rule | Objection handling and height/weight obey approved turn-taking |
| 24 | Correlated evidence | GHL contact, Vapi call, Make execution, and GHL appointment linked privately |

Record expected result, actual result, date, configuration version, and redacted evidence per test. Do not infer test success from Published, Active, enrollment counts, or unrelated appointment rows.
