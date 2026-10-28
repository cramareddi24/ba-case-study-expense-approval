# Business Requirements Document

**Project:** Expense Report Approval Workflow
**Company:** Harborview Supply Co. (fictional)
**Sponsor:** Finance Controller
**Version:** 1.2 (updated after UAT decisions)

## 1. Executive summary

Expense reimbursement today runs on emailed spreadsheets. It's slow (about 14 business days end to end), error-prone (about 18% of reports are sent back), and invisible to the people waiting on it. This project replaces that process with a web-based workflow where employees submit reports with receipts, approvals route automatically, and Finance exports approved reports straight into the accounting system.

## 2. Business objectives

| ID | Objective | Measure | Target |
|---|---|---|---|
| OBJ-1 | Reimburse employees faster | Business days from submission to payment | 5 or fewer (from ~14) |
| OBJ-2 | Reduce rework | % of reports returned for missing info | Under 5% (from ~18%) |
| OBJ-3 | Remove manual data entry | Finance hours spent re-keying per month | 0 (from ~30) |
| OBJ-4 | Make status visible | % of reports with a trackable status | 100% |

## 3. Scope

**In scope**
- Web form for creating and submitting expense reports with line items
- Receipt upload
- Policy checks at the point of entry
- Approval routing based on report total
- Status tracking for submitters and approvers
- Email notifications and reminders
- Finance review and export to the accounting system
- Audit trail

**Out of scope (Phase 1)**
- Native mobile app (the web form will be mobile responsive)
- Corporate credit card feed integration
- Multi-currency reports
- GPS-based mileage tracking

## 4. Stakeholders

| Stakeholder | Role in project | Main concern |
|---|---|---|
| Employees (submitters) | Primary users | Fast, easy submission and knowing when they'll be paid |
| People managers (approvers) | Primary users | Quick approvals without chasing information |
| Department heads | Secondary approvers | Visibility into large expenses |
| Accounts Payable team | Primary users | Clean, complete reports and no re-keying |
| Finance Controller | Sponsor and decision maker | Policy compliance and audit readiness |
| Internal Audit | Reviewer | Complete, tamper-proof history |
| IT / Engineering | Build and support | Clear, testable requirements |

## 5. Current state pain points

Gathered from interviews with 6 employees, 4 managers, and the AP team, plus a review of 50 recent reports.

1. Receipts are missing or unreadable on a large share of reports, which drives most of the back-and-forth.
2. Managers lose approval requests in their inbox. There's no reminder and no way to delegate during PTO.
3. Policy violations (for example, meals over the daily limit) are caught by AP at the very end, after the manager has already approved.
4. AP re-types every approved report into the accounting system, which introduces typos.
5. Employees have no way to check status without emailing someone.

## 6. Business requirements

| ID | Requirement | Priority | Source |
|---|---|---|---|
| BR-01 | Employees can create, save as draft, and submit expense reports online, with line items for date, category, merchant, amount, and description. | Must | Pain point 5, OBJ-4 |
| BR-02 | A receipt is required for any line item of $25.00 or more. Accepted formats: JPG, PNG, PDF, up to 10 MB each. | Must | Pain point 1, OBJ-2 |
| BR-03 | The system checks policy limits at entry (meals $75/day, lodging $250/night). Over-limit items are flagged and require a written justification, but are not blocked. | Must | Pain point 3 |
| BR-04 | Submitted reports route to the submitter's direct manager. Reports with a total greater than $2,500.00 also require department head approval after the manager. | Must | Controller |
| BR-05 | Approvers can approve, reject (reason required), or return for changes (comment required). | Must | Pain point 2 |
| BR-06 | Submitters and approvers can see the current status and full approval history of each report. | Must | Pain point 5, OBJ-4 |
| BR-07 | Email notifications are sent on submission, on every approval action, and as a reminder when a report has been pending with one approver for 3 business days. | Should | Pain point 2, OBJ-1 |
| BR-08 | AP can review fully approved reports and export them as a CSV that matches the accounting system's import template. | Must | Pain point 4, OBJ-3 |
| BR-09 | Every action (create, edit, submit, approve, reject, return, export) is logged with user, timestamp, and details. Logs cannot be edited. | Must | Internal Audit |
| BR-10 | Users cannot approve their own reports, including when acting as a delegate. Managers can assign a delegate approver for a date range. | Must | Controller, Pain point 2 |

## 7. Non-functional requirements

| ID | Requirement |
|---|---|
| NFR-01 | Login through existing company single sign-on |
| NFR-02 | Role-based access: submitters see only their own reports, approvers see reports routed to them, AP sees approved reports |
| NFR-03 | Pages load in under 3 seconds for 95% of requests |
| NFR-04 | Receipts and audit logs retained for 7 years |
| NFR-05 | Usable on mobile browsers and meets WCAG 2.1 AA accessibility |

## 8. Assumptions and constraints

- The HR system is the source of truth for reporting lines (who each employee's manager and department head are).
- The accounting system's CSV import template will not change during the project.
- Phase 1 must go live before the start of the next fiscal quarter.

## 9. Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Reporting lines in HR data are out of date, so reports route to the wrong person | High | Data quality check on reporting lines before launch; manual reassign option for AP |
| Managers keep approving by email out of habit | Medium | Email notifications link directly to the approval screen; old process retired on a set date |
| Export doesn't match what accounting actually accepts | High | Include AP in UAT and test the export through the real import |

## 10. Success metrics (measured 90 days after launch)

Measured against the OBJ targets above, plus user satisfaction from a short survey of submitters and approvers.
