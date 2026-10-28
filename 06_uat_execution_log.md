# UAT Execution Log

## Round 1 results (Mar 10 to Mar 14, 2025)

| ID | Tester role | Result | Defect | Notes |
|---|---|---|---|---|
| TC-01 | Employee | Pass | | |
| TC-02 | Employee | Pass | | |
| TC-03 | Employee | Pass | | |
| TC-04 | Employee | Pass | | |
| TC-05 | Employee | Pass | | |
| TC-06 | Employee | **Fail** | DEF-03 | Files were rejected, but message just said "Upload failed" |
| TC-07 | Employee | Pass | | |
| TC-08 | Manager | Pass | | |
| TC-09 | Manager | Pass | | |
| TC-10 | Manager | **Fail** | DEF-01 | 2,500.00 report went to department head |
| TC-11 | Manager | Pass | | |
| TC-12 | Manager | Pass | | |
| TC-13 | Manager | Pass | | |
| TC-14 | Employee | Pass | | |
| TC-15 | Manager | **Fail** | DEF-04 | Reminder sent Monday, counted weekend days |
| TC-16 | AP | **Fail** | DEF-05 | Accounting import rejected the file |
| TC-17 | AP | Pass | | |
| TC-18 | Manager | **Fail** | DEF-02 | Delegate was able to approve their own report |

**Round 1: 13 of 18 passed (72%).**

## Defect log

| ID | Severity | Test | Summary | Root cause | Resolution |
|---|---|---|---|---|---|
| DEF-01 | High | TC-10 | Report totaling exactly 2,500.00 routed to department head | Requirements ambiguity. Draft BR-04 said "over $2,500" and dev implemented it as 2,500 or more. | Took it to the Controller, who confirmed strictly greater than 2,500.00 (D-03). BR-04 reworded, logic fixed. |
| DEF-02 | Critical | TC-18 | Delegate could approve a report they submitted | Self-approval check compared submitter only to the assigned approver, not to active delegates | Check now applies to anyone acting on the report. Added to regression suite. |
| DEF-03 | Medium | TC-06 | Unsupported file upload shows generic "Upload failed" | Error handling didn't distinguish file type, size, and network errors | Specific messages for each case. HEIC support raised separately as CR-01. |
| DEF-04 | Medium | TC-15 | 3-day reminder counted weekends | Reminder used calendar days | Switched to business days using the company holiday calendar |
| DEF-05 | High | TC-16 | Export dates formatted MM/DD/YYYY; accounting import requires YYYY-MM-DD | Export format built from a sample screenshot, not the actual import template | Export now built from the official template spec. Re-tested through the real import. |

## Retest (Mar 17 to Mar 18, 2025)

| Defect | Retest case | Result |
|---|---|---|
| DEF-01 | TC-10, plus TC-09 and TC-11 for regression | Pass |
| DEF-02 | TC-18, plus a manager approving a delegate's report (should be allowed) | Pass |
| DEF-03 | TC-06 | Pass |
| DEF-04 | TC-15, plus a holiday week scenario | Pass |
| DEF-05 | TC-16, full import of 5 reports | Pass |

**Final: 18 of 18 passed. 0 open defects.**

## Change requests raised during UAT

| ID | Request | Raised by | Decision |
|---|---|---|---|
| CR-01 | Accept HEIC images (default iPhone photo format) | Employee testers | Approved for release 1.1. Not a defect since BR-02 specifies JPG, PNG, PDF. |

## Sign-off

| Name / role | Decision | Date |
|---|---|---|
| Finance Controller (sponsor) | Approved for release | Mar 19, 2025 |
| AP Lead | Approved | Mar 19, 2025 |
| Manager representative | Approved | Mar 19, 2025 |

Exit criteria met: all test cases executed, no open Critical or High defects, sign-offs received.
