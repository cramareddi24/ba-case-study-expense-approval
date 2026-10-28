# User Stories and Acceptance Criteria

Priority uses MoSCoW: **M**ust, **S**hould, **C**ould.

---

### US-01: Create and submit an expense report
**As an** employee, **I want to** enter my expenses as line items in a web form and submit them, **so that** I don't have to fill out and email a spreadsheet.
**Traces to:** BR-01 | **Priority:** M

- **Given** I'm logged in, **when** I create a report and add line items with date, category, merchant, amount, and description, **then** the report total updates automatically.
- **Given** a required field is blank, **when** I click Submit, **then** submission is blocked and the missing field is highlighted.
- **Given** a complete report, **when** I submit, **then** its status changes to Pending Manager and I can no longer edit it.

### US-02: Save a report as a draft
**As an** employee, **I want to** save an unfinished report, **so that** I can add expenses as they happen during a trip.
**Traces to:** BR-01 | **Priority:** S

- **Given** a partially filled report, **when** I click Save Draft, **then** it's saved with status Draft and appears in My Reports.
- **Given** a draft, **when** I reopen it, **then** all previously entered line items and receipts are still there.

### US-03: Upload receipts
**As an** employee, **I want to** attach receipt images to line items, **so that** my report isn't sent back for missing receipts.
**Traces to:** BR-02 | **Priority:** M

- **Given** a line item of $25.00 or more, **when** I try to submit without a receipt, **then** submission is blocked with the message "Receipt required for items $25.00 or more."
- **Given** a line item under $25.00, **when** I submit without a receipt, **then** submission is allowed.
- **Given** a file that is not JPG, PNG, or PDF, or is over 10 MB, **when** I upload it, **then** it's rejected with a message that names the allowed formats and size limit.

### US-04: See policy warnings while entering expenses
**As an** employee, **I want to** know right away if an expense is over policy, **so that** I can explain it before my manager or AP has to ask.
**Traces to:** BR-03 | **Priority:** M

- **Given** meal expenses on one date total more than $75.00, **when** I enter them, **then** the items are flagged and a justification field becomes required.
- **Given** a lodging line over $250.00 per night, **when** I enter it, **then** it's flagged and requires justification.
- **Given** a flagged item with a justification, **when** I submit, **then** submission is allowed and the flag and justification are visible to approvers.

### US-05: Automatic approval routing
**As a** Finance Controller, **I want** reports to route to the right approvers based on amount, **so that** large expenses always get a second review.
**Traces to:** BR-04 | **Priority:** M

- **Given** a submitted report, **then** it routes to the submitter's direct manager from the HR system.
- **Given** a report total greater than $2,500.00, **when** the manager approves, **then** it routes to the department head.
- **Given** a report total of $2,500.00 or less, **when** the manager approves, **then** it's marked Approved with no department head step.

### US-06: Approve, reject, or return a report
**As a** manager, **I want to** act on a report from one screen, **so that** I don't need an email thread to ask questions.
**Traces to:** BR-05 | **Priority:** M

- **Given** a report pending with me, **when** I approve, **then** it moves to the next step.
- **Given** I choose Reject, **then** a reason is required before I can confirm.
- **Given** I choose Return for Changes, **then** a comment is required, and the report goes back to Draft with my comment visible to the submitter.

### US-07: Track report status
**As an** employee, **I want to** see where my report is and who has it, **so that** I don't have to email anyone to find out.
**Traces to:** BR-06 | **Priority:** M

- **Given** any report I submitted, **when** I open it, **then** I see the current status, the current approver, and a timeline of every past action.

### US-08: Notifications and reminders
**As an** approver, **I want** an email when something needs my action and a reminder if I forget, **so that** reports don't stall.
**Traces to:** BR-07 | **Priority:** S

- **Given** a report is routed to me, **then** I get an email with a direct link to it.
- **Given** a report has been pending with me for 3 business days, **then** I get a reminder email. Weekends and company holidays don't count.
- **Given** any approval action, **then** the submitter gets an email with the new status.

### US-09: Export approved reports for accounting
**As an** AP specialist, **I want to** export approved reports in the accounting import format, **so that** I never re-key expenses.
**Traces to:** BR-08 | **Priority:** M

- **Given** fully approved reports, **when** I select them and click Export, **then** a CSV is generated that matches the accounting import template exactly (column order, names, and formats, including dates as YYYY-MM-DD).
- **Given** a report has been exported, **then** its status changes to Exported and it can't be exported again without an override.

### US-10: Audit history
**As an** internal auditor, **I want** a complete, uneditable history of every report, **so that** I can verify who did what and when.
**Traces to:** BR-09 | **Priority:** M

- **Given** any action on a report, **then** an audit entry is written with user, action, timestamp, and changed values.
- **Given** any user, including admins, **when** they try to edit or delete an audit entry, **then** the action isn't possible.

### US-11: Delegate approvals without self-approval
**As a** manager, **I want to** assign a delegate while I'm out, **so that** my team's reports don't wait on my PTO.
**Traces to:** BR-10 | **Priority:** M

- **Given** I set a delegate for a date range, **then** reports routed to me during that range also go to my delegate.
- **Given** any user, **when** a report they submitted is routed to them (directly or as a delegate), **then** they can't approve it and it routes to the next approver up the reporting line.
