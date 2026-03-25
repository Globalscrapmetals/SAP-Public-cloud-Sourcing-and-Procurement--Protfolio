# 🔀 Flexible Workflows & Approvals

> **Wiki Navigation:** [Home](Home) › Flexible Workflows & Approvals

---

## Overview

**Flexible Workflow** is SAP S/4HANA Public Cloud's built-in, configurable approval engine. It replaces the classical SAP release strategy (which required ABAP configuration) with a no-code/low-code rule builder that business users and functional consultants can manage directly.

Flexible Workflow drives approval decisions based on configurable business rules — routing documents to the right people, at the right time, with full audit trail.

---

## How Flexible Workflow Works

```
Document Created or Changed
(PR, PO, Invoice, Contract, RFx)
          │
          ▼
  Workflow Rule Engine Evaluates
  (Checks all configured conditions)
          │
     ┌────┴───────────────────────────┐
     │                                │
No Rule Matches                  Rule Matches
     │                                │
Auto-Approved / No Approval      Approval Task Created
(Document proceeds)              in Approver's Inbox
                                         │
                                 ┌───────┴───────────┐
                                 │                   │
                              Approved           Rejected
                                 │                   │
                            Document            Document
                            Released            Returned
                            (Proceeds)          to Requester
                                                (with reason)
```

---

## Supported Document Types

Flexible Workflow can be configured to control approvals for:

| Document | Trigger Events |
|---|---|
| **Purchase Requisition (PR)** | Creation, value increase, cost centre change |
| **Purchase Order (PO)** | Creation, price change, new line item, value increase |
| **Supplier Invoice** | High-value invoices, blocked invoices, first-time vendors |
| **Contracts / Outline Agreements** | New contract, renewal, value change |
| **Sourcing Events (RFx)** | Before publication to suppliers |
| **Goods Receipt** | High-value items, specific material groups |

---

## Approval Rule Conditions

Rules are built by combining **conditions** — when all conditions in a rule are true, the approval path is triggered.

### Available Condition Fields

| Condition Category | Examples |
|---|---|
| **Value / Amount** | Net PO value, PR value, invoice amount |
| **Organizational Unit** | Company code, plant, purchasing org |
| **Vendor Attributes** | New vendor, blocked vendor, strategic supplier class |
| **Material / Category** | Material group, spend category, material type |
| **Account Assignment** | Cost centre, asset (CapEx), WBS element |
| **Document Attributes** | Document type, purchasing group, payment terms |
| **Change-Based** | Triggered only when specific field changes (e.g., price increase > X%) |

---

## Sample Approval Matrices

### Purchase Order — Value-Based Approval

| Net PO Value | Approval Path |
|---|---|
| < $5,000 | Auto-approve — no human approval needed |
| $5,000 – $25,000 | Line Manager (1 step) |
| $25,001 – $100,000 | Line Manager → Department Head (2 steps) |
| $100,001 – $500,000 | Line Manager → Dept Head → VP Procurement (3 steps) |
| > $500,000 | Full chain → VP Procurement → CFO (4 steps) |

### Special Condition Rules (overlaid on value matrix)

| Condition | Additional Approver Required |
|---|---|
| New Vendor (never used before) | Compliance Officer must also approve |
| CapEx (Account Assignment = A) | Finance Controller required |
| Single Source (no competition) | Procurement Director sign-off |
| Sensitive Material Group | Legal review required |
| IT Procurement | IT Security Officer included |

---

## Multi-Step Approval Configuration

Each approval step in a workflow can be configured with:

```
Step Configuration
├── Approver Determination
│   ├── Fixed User (always this person)
│   ├── Job Position (whoever holds this role)
│   ├── Organizational Hierarchy (manager of requester)
│   └── Custom Rule (formula-based determination)
│
├── Step Type
│   ├── Sequential — approvers act one after another
│   └── Parallel — all approvers act simultaneously
│
├── Deadline Settings
│   ├── Reminder notification after X days
│   └── Escalation after Y days (sends to next level)
│
└── Actions Available to Approver
    ├── Approve
    ├── Reject (with mandatory comment)
    ├── Return for Revision
    └── Add Ad-Hoc Approver
```

---

## Escalation & Delegation

### Escalation
When an approver does not act within the configured deadline:

```
Task assigned to Approver A
          │
    Deadline reached (no action)
          │
          ▼
  Reminder email sent to Approver A
          │
    Extended deadline reached
          │
          ▼
  Escalation: Task forwarded to Approver A's Manager
          │
    Final deadline reached
          │
          ▼
  Auto-approve or Auto-reject
  (configurable per workflow)
```

### Delegation
When an approver is on leave or unavailable:

| Method | Description |
|---|---|
| **Substitution** | Approver sets a substitute in their profile — all tasks automatically redirect |
| **Manual Forward** | Approver manually forwards a specific task to a colleague |
| **Ad-Hoc Approver** | Requester or buyer adds an extra approver to a specific document |

---

## Approver Experience

### SAP Fiori Approval Inbox
Approvers access pending items via the **My Inbox** Fiori tile:

```
My Inbox (Approver's view)
├── 📄 PO #4500001234 — $45,000 — Acme Steel
│   ├── Requested by: J. Smith | Dept: Manufacturing
│   ├── Due: 2024-02-15
│   └── Actions: [Approve] [Reject] [Forward] [View Details]
│
├── 📋 Contract #5000000456 — $250,000 — Tech Supplies Ltd.
│   ├── Validity: 01.03.2024 – 28.02.2025
│   └── Actions: [Approve] [Reject] [Request Revision]
│
└── 🧾 Invoice #5105001789 — $78,000 — blocked (price variance)
    ├── Variance: +3.2% above PO price
    └── Actions: [Release Block] [Keep Block] [Query Vendor]
```

### Mobile Approval
Approvals can be completed via:
- **SAP Fiori Launchpad** (browser on any device)
- **SAP Mobile Start** app (iOS / Android)
- **Email approval links** (configurable — click to approve from email)

---

## Audit Trail

Every workflow action is logged automatically on the document:

| Log Entry | Captured Data |
|---|---|
| Approval step started | Timestamp, approver assigned, step description |
| Approval action taken | Approver name, action (Approved/Rejected), timestamp |
| Comment added | Full text of any approver comments |
| Escalation triggered | Who was escalated to and when |
| Delegation used | Original approver + substitute who acted |
| Document changed | What changed after approval was requested |

> 💡 The audit trail is immutable — it cannot be deleted or modified, ensuring full compliance and traceability.

---

## Configuration Steps (Functional Overview)

1. **Define Workflow Scenarios** — Identify which document types need approval
2. **Build Condition Rules** — Define the business rules for when approval is triggered
3. **Configure Approval Steps** — Set approver determination, sequence, deadlines
4. **Assign Organizational Roles** — Map job positions to approval authority levels
5. **Test in Quality System** — Run test documents through all workflow paths
6. **Enable in Production** — Activate for live use
7. **Monitor & Iterate** — Review workflow analytics, adjust thresholds as needed

---

> ← [System Configuration](System-Configuration) | Next: [Integration & Analytics](Integration-and-Analytics) →
