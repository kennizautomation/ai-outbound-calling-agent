# Olivia prompt review

The sanitized source retains the owner's behavior. The following changes are recommendations, not changes to the running Vapi assistant.

| Issue in supplied script | Recommended resolution |
| --- | --- |
| ZIP may never be repeated, but booking explicitly repeats it for confirmation | Choose one rule: ask once and reuse the stored answer; confirm only if corrected or unclear, if approved |
| Transfer only on an explicit request, but later a yes to an either/or question triggers transfer | Ask one unambiguous question: “Would you like me to connect you with an advisor now?” Transfer only after clear agreement |
| The same number is described as an advisor and customer support | Verify the actual destination and use an accurate label |
| Closing says a booking is confirmed after any transfer | Use a booking closing only after booking success; use a transfer-specific closing before handoff |
| One question at a time conflicts with bundled objection questions and height/weight | Split each into separate turns and preserve answered-question state |
| “I already have insurance” jumps to height/weight | Define whether objection handling resumes at the next unanswered qualification question |
| Exactly $20 has no defined budget branch | Define the equality branch explicitly rather than inventing one |
| No-request objection guesses that a family member signed the person up | Acknowledge the dispute without inventing a source; stop or route according to the approved contact-permission policy |
| Claimed state program, guaranteed tax-free coverage, pricing formula, employer-policy rule, and eligibility opinion | Have the business substantiate and approve wording; do not present these claims as verified portfolio facts |
| AI identity is not explained in the opening | Use an accurate AI-assistant introduction in an approved revised script |
| “Not interested” continues qualification | Define a respectful stop path and a do-not-call handling path |
| Three booking failures can include uncertain API results | Reconcile ambiguous results before another booking attempt to avoid duplicates |
| No slots or fewer than three alternatives are unspecified | Return only actual available slots; do not invent times |
| Prompt says transferCall, while the tool-list screenshot also shows TtransferCall | Confirm the exact attached transfer tool and callable name; do not rename from a screenshot alone |

## Boundaries of the review
This review identifies internal logic and unsupported assertions. It does not certify insurance terms, contact permissions, or legal compliance. No actual caller health information is included in the repository.

## Function names retained
`KappointmentAvailability`, `KAppointment_booking`, and `transferCall` remain exactly as supplied. No callback or opt-out function is invented. Any approved additional behavior needs matching workflow implementation.
