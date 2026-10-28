# Requirements Traceability Matrix

Every business requirement traces forward to at least one user story and test case, and every defect traces back to the requirement it affected. Final status reflects the end of UAT retest.

| Business req | Summary | User stories | Test cases | Defects | Final status |
|---|---|---|---|---|---|
| BR-01 | Create, draft, and submit reports | US-01, US-02 | TC-01, TC-02, TC-03 | None | Passed |
| BR-02 | Receipts required at $25.00+ | US-03 | TC-04, TC-05, TC-06 | DEF-03 | Passed after retest |
| BR-03 | Policy checks at entry | US-04 | TC-07, TC-08 | None | Passed |
| BR-04 | Routing by amount | US-05 | TC-09, TC-10, TC-11 | DEF-01 | Passed after retest |
| BR-05 | Approve, reject, return | US-06 | TC-12, TC-13 | None | Passed |
| BR-06 | Status and history | US-07 | TC-14 | None | Passed |
| BR-07 | Notifications and reminders | US-08 | TC-15 | DEF-04 | Passed after retest |
| BR-08 | Export to accounting | US-09 | TC-16 | DEF-05 | Passed after retest |
| BR-09 | Audit trail | US-10 | TC-17 | None | Passed |
| BR-10 | No self-approval, delegation | US-11 | TC-18 | DEF-02 | Passed after retest |

## Coverage summary

| | Count |
|---|---|
| Business requirements | 10 |
| Requirements with at least one test case | 10 (100%) |
| User stories | 11 |
| Test cases | 18 |
| Defects found in UAT | 5 |
| Requirements passed at sign-off | 10 (100%) |
