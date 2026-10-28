# Process Flows

## Current state (as-is)

```mermaid
flowchart TD
    A[Employee fills out Excel expense form] --> B[Takes photos of receipts]
    B --> C[Emails form and photos to manager]
    C --> D{Manager sees email?}
    D -- No, buried in inbox --> E[Employee follows up by email]
    E --> D
    D -- Yes --> F{Manager approves?}
    F -- Questions --> G[Back-and-forth email thread]
    G --> F
    F -- Approves by reply --> H[Employee forwards approval to AP]
    H --> I{AP review: receipts and policy OK?}
    I -- No --> J[AP emails employee to fix]
    J --> A
    I -- Yes --> K[AP re-keys report into accounting system]
    K --> L[Reimbursement in next payment run]
```

**Problems visible in the flow:** two loops that send work back to the start, policy checked only at the end by AP, manual re-keying, and no status anywhere except email.

## Future state (to-be)

```mermaid
flowchart TD
    A[Employee creates report in web form] --> B[Adds line items and uploads receipts]
    B --> C{Policy check at entry}
    C -- Over limit --> D[Employee adds justification]
    D --> E
    C -- Within limit --> E[Submit]
    E --> F[Routed to direct manager]
    F --> G{Manager decision}
    G -- Return for changes --> B
    G -- Reject --> R[Rejected, employee notified]
    G -- Approve --> H{Total greater than 2,500.00?}
    H -- Yes --> I{Department head decision}
    I -- Return --> B
    I -- Reject --> R
    I -- Approve --> J
    H -- No --> J[Fully approved]
    J --> K[AP reviews]
    K --> L[Export CSV to accounting system]
    L --> M[Reimbursement in next payment run]
```

**What changed:** receipts and policy are checked before submission instead of at the end, routing is automatic, the only loop back is an intentional "return for changes," and the export replaces re-keying.

## Report status lifecycle

```mermaid
stateDiagram-v2
    [*] --> Draft
    Draft --> PendingManager: Submit
    PendingManager --> Draft: Returned for changes
    PendingManager --> Rejected: Rejected
    PendingManager --> PendingDeptHead: Approved and total > 2,500.00
    PendingManager --> Approved: Approved and total <= 2,500.00
    PendingDeptHead --> Draft: Returned for changes
    PendingDeptHead --> Rejected: Rejected
    PendingDeptHead --> Approved: Approved
    Approved --> Exported: AP exports
    Exported --> [*]
    Rejected --> [*]
```

Every transition writes an entry to the audit log (BR-09) and triggers a notification (BR-07).
