# UAT Plan and Test Cases

## Purpose

Confirm the expense workflow meets the business requirements in the BRD before it replaces the email process. UAT is run by the people who will actually use it: employees, managers, a department head, and AP.

## Entry criteria
- All Must-have user stories are dev complete and passed QA
- UAT environment is loaded with test users that mirror real reporting lines (including one manager with a delegate set)
- Accounting system test instance is available to receive exports

## Exit criteria
- 100% of test cases executed
- 0 open Critical or High defects
- Medium and Low defects either fixed or accepted by the sponsor with a target date
- Written sign-off from the Finance Controller, AP Lead, and a manager representative

## Roles

| Role | Who | Responsibility |
|---|---|---|
| UAT lead | Business Analyst | Plan, coordinate testers, log and triage defects, track to sign-off |
| Testers | 2 employees, 2 managers, 1 department head, 2 AP specialists | Execute test cases in their own role |
| Defect owner | Engineering lead | Fix and deploy to UAT |
| Approver | Finance Controller | Final sign-off and decisions on open items |

## Schedule (fictional)
- UAT round 1: Mar 10 to Mar 14, 2025
- Fixes deployed: Mar 17
- Retest: Mar 17 to Mar 18
- Sign-off: Mar 19

## Test cases

Edge cases are included on purpose: boundary amounts, weekends, delegation, and the real accounting import.

| ID | Story | Scenario | Steps | Expected result |
|---|---|---|---|---|
| TC-01 | US-01 | Create report, total calculates | Add 3 line items: 42.10, 18.00, 120.00 | Total shows 180.10 |
| TC-02 | US-01 | Required field missing | Leave merchant blank on one line, click Submit | Submit blocked, merchant field highlighted |
| TC-03 | US-02 | Save and reopen draft | Add 2 items with 1 receipt, Save Draft, log out, reopen | Both items and receipt still present, status Draft |
| TC-04 | US-03 | Receipt required at boundary | Add item of exactly 25.00 with no receipt, Submit | Blocked with "Receipt required for items $25.00 or more" |
| TC-05 | US-03 | Receipt not required just under | Add item of 24.99 with no receipt, Submit | Submission allowed |
| TC-06 | US-03 | Invalid file | Upload a .heic photo, then a 12 MB PDF | Both rejected with a message naming allowed formats and 10 MB limit |
| TC-07 | US-04 | Meal limit across items | Add two meals on same date: 48.00 and 31.00 | Both flagged (79.00 > 75.00), justification required |
| TC-08 | US-04 | Lodging over limit with justification | Add hotel 289.00/night, enter justification, Submit | Submission allowed; flag and justification visible to manager |
| TC-09 | US-05 | Routes to dept head above threshold | Submit report totaling 2,500.01, manager approves | Status moves to Pending Dept Head |
| TC-10 | US-05 | Exactly at threshold | Submit report totaling 2,500.00, manager approves | Status moves to Approved, no dept head step |
| TC-11 | US-05 | Under threshold | Submit report totaling 640.25, manager approves | Status moves to Approved |
| TC-12 | US-06 | Reject requires reason | Manager clicks Reject with empty reason | Can't confirm until reason entered; submitter sees reason |
| TC-13 | US-06 | Return for changes | Manager returns with comment "Missing hotel folio" | Report back to Draft; comment visible to submitter |
| TC-14 | US-07 | Status timeline | Submit, return, resubmit, approve one report | Timeline shows all 4 actions with user and time |
| TC-15 | US-08 | Reminder skips weekend | Report routed Friday 9am; manager takes no action | Reminder sent Wednesday (3 business days), not Monday |
| TC-16 | US-09 | Export imports cleanly | Export 5 approved reports, import CSV into accounting test instance | Import succeeds with 0 errors; amounts and dates match |
| TC-17 | US-10 | Audit log is complete and locked | Perform submit, approve, export; then try to edit a log entry as admin | All 3 actions logged; edit not possible |
| TC-18 | US-11 | Delegate can't approve own report | Delegate submits own report while covering for their manager | Delegate can't approve; report routes to next approver up |
