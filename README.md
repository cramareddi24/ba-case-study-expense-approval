# BA Case Study: Expense Report Approval Workflow

A full set of business analysis deliverables for replacing an email-and-spreadsheet expense process with a web-based submission and approval workflow, from requirements through UAT sign-off.

The company and numbers are fictional, and I play the BA in the scenario. The work itself mirrors what I've done in QA and product roles: figure out what the business actually needs, write it down clearly enough that engineering can build it without guessing, trace every requirement to a test, and run validation until stakeholders can sign off.

## The scenario

**Harborview Supply Co.** (fictional, ~450 employees) reimburses expenses through a manual process. Employees email an Excel form and receipt photos to their manager, managers approve by replying to the email, and Finance re-keys everything into the accounting system.

| Problem | Baseline |
|---|---|
| Time from submission to reimbursement | ~14 business days |
| Reports sent back for missing info or receipts | ~18% |
| Finance time spent re-keying reports | ~30 hours/month |
| Visibility into where a report is | None (email threads) |

**Goal:** cut reimbursement time to 5 business days or less, get returns under 5%, and eliminate manual re-keying.

## Deliverables

| # | Document | What it shows |
|---|---|---|
| 1 | [Business Requirements Document](01_business_requirements_document.md) | Objectives, scope, stakeholders, 10 business requirements, non-functional requirements, risks |
| 2 | [Process Flows](02_process_flows.md) | Current vs future state flowcharts and a report status lifecycle (Mermaid diagrams) |
| 3 | [User Stories and Acceptance Criteria](03_user_stories.md) | 11 user stories with Given/When/Then criteria and MoSCoW priority |
| 4 | [Requirements Traceability Matrix](04_requirements_traceability_matrix.md) | Every requirement linked to stories, test cases, and final status |
| 5 | [UAT Plan and Test Cases](05_uat_plan_and_test_cases.md) | Entry/exit criteria, roles, and 18 test cases including edge cases |
| 6 | [UAT Execution Log](06_uat_execution_log.md) | Results, 5 defects found and resolved, retest, and sign-off |
| 7 | [Decision Log and Open Questions](07_decision_log.md) | How ambiguous requirements were resolved and who owns what's still open |

## Highlights

- **Caught a requirements gap before go-live.** The routing rule said reports "over $2,500" go to a department head, but nobody had defined what happens at exactly $2,500.00. A boundary test exposed it, I took it to the Finance Controller, and the decision was documented (D-03) and fixed before release.
- **Found a control gap in delegation.** A delegate approver could approve their own report, bypassing the self-approval rule. Logged as Critical, fixed, and retested before sign-off.
- **Tested the handoff, not just the screens.** The finance export looked correct but used a date format the accounting system would reject on import. Running the export through the real import path caught it.
- **Full traceability.** All 10 business requirements map to user stories and test cases, with 18 of 18 test cases passing after retest.

## Viewing the diagrams

The process flows use Mermaid, which GitHub renders automatically in the browser.
