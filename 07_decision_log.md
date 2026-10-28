# Decision Log and Open Questions

Requirements rarely arrive complete. This log captures where they were ambiguous, what was decided, and who made the call, so nobody has to rely on memory later.

## Decisions

| ID | Date | Question | Decision | Decided by | Why |
|---|---|---|---|---|---|
| D-01 | Feb 3, 2025 | Should over-policy expenses be blocked or allowed? | Allowed with required justification, flagged to approvers | Finance Controller | Legitimate exceptions happen (for example, client dinners in high-cost cities). Blocking would push people back to email. |
| D-02 | Feb 3, 2025 | What's the receipt threshold? | $25.00 and above | Finance Controller | Matches existing written policy, so no policy change needed |
| D-03 | Mar 12, 2025 | Does "over $2,500" include exactly $2,500.00? | No. Department head approval applies only to totals strictly greater than $2,500.00 | Finance Controller | Matches how the written policy has always been applied. Found through boundary testing (DEF-01). |
| D-04 | Feb 10, 2025 | Mobile app in Phase 1? | No. Mobile-responsive web form instead | Sponsor and IT | Most submissions happen at a desk after trips; an app would delay launch past the fiscal quarter |
| D-05 | Mar 14, 2025 | Support HEIC uploads? | Yes, in release 1.1 (CR-01) | Sponsor | Common iPhone format; not blocking for launch since users can export as JPG |

## Open questions

| ID | Question | Owner | Needed by |
|---|---|---|---|
| Q-01 | Should reports with expenses older than 60 days be blocked or just flagged? | Finance Controller | Before release 1.1 |
| Q-02 | How long should rejected reports be retained? The 7-year rule covers approved reports. | Internal Audit | Before release 1.1 |
| Q-03 | Who approves reports for department heads themselves? HR data shows some reporting to the CFO, some to the COO. | HR and Finance Controller | Before release 1.1 |
