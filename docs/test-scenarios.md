# Acceptance test plan

Status: **not executed against live platforms**. Use synthetic contacts and controlled test numbers. Record actual results and redacted evidence after configuration.

| # | Scenario | Expected result |
| --- | --- | --- |
| 1 | Eligible lead trigger | One Vapi call request; call ID linked to the GHL contact |
| 2 | Duplicate lead trigger | No second call for the same reserved attempt |
| 3 | Suppressed lead | Call skipped with a recorded reason |
| 4 | Outside local calling window | No immediate call; deferred state recorded |
| 5 | Invalid phone | Validation failure; no dispatch |
| 6 | Interested lead | Answers stored accurately; no inferred qualification facts |
| 7 | Confirmed available slot | One GHL appointment; confirmation spoken only after success |
| 8 | Slot taken before creation | No false confirmation; new availability offered |
| 9 | Ambiguous booking timeout | Reconciliation before retry; no duplicate appointment |
| 10 | Callback requested | Exact date/time/timezone saved with pending state |
| 11 | Opt-out mid-call | Suppression persisted promptly and future dispatch blocked |
| 12 | Wrong person | Polite ending and correction flag; no qualification invented |
| 13 | No answer, busy, voicemail | Accurate connection status; no false booking or qualification |
| 14 | Requested transfer fails | Callback offered; no completed-transfer claim |
| 15 | Duplicate final event | No duplicate note, task, appointment, or opportunity |
| 16 | CRM error after booking | Existing appointment retained; CRM update retried separately |
| 17 | Unknown or forged tool request | Rejected without CRM or calendar mutation |
| 18 | Callback becomes suppressed | Scheduled retry skipped |
| 19 | Daylight-saving boundary | Correct local time, offset, and calendar slot |
| 20 | Call dispatch timeout | Uncertain attempt reconciled before another request |

## Evidence record
For each test capture: date, configuration version, synthetic contact ID, call ID where available, expected result, observed result, pass/fail, and redacted evidence link. Do not mark a test passed from the expected result alone.
