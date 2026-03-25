# 📱 SAP Fiori Apps Reference

> **Wiki Navigation:** [Home](Home) › Fiori Apps Reference

---

## Overview

SAP Fiori is the user experience (UX) framework for SAP S/4HANA Public Cloud. All procurement transactions are accessed via **Fiori apps** — role-based, browser-accessible tiles on the Fiori Launchpad. This page provides a reference of the key Fiori apps used in Sourcing and Procurement.

---

## Fiori Launchpad Overview

```
SAP Fiori Launchpad
├── Role: Operational Buyer
│   ├── Manage Purchase Requisitions
│   ├── Manage Purchase Orders
│   ├── Post Goods Receipt for PO
│   └── My Purchasing Document Worklist
│
├── Role: Accounts Payable Accountant
│   ├── Create Supplier Invoice
│   ├── Manage Supplier Invoices
│   └── Release Blocked Invoices
│
├── Role: Strategic Buyer
│   ├── Sourcing and Contracting (workspace)
│   ├── Manage Supplier Contracts
│   └── Supplier Evaluation
│
└── Role: Procurement Manager
    ├── Procurement Overview Page
    ├── Monitor Purchase Order Items
    └── Flexible Workflow Analytics
```

---

## Purchase Requisition Apps

| App ID | App Name | Description | User Role |
|---|---|---|---|
| `F0842` | Manage Purchase Requisitions | Create, edit, search, and track PRs. Full list view with filters. | Buyer, Requester |
| `F2603` | Create Purchase Requisition | Simplified creation app for requesters | Requester / SSP |
| — | My Purchase Requisitions | Requester's personal view of their own PRs | Requester |
| — | Approve Purchase Requisitions | Inbox view for PR approvers | Manager / Approver |

---

## Purchase Order Apps

| App ID | App Name | Description | User Role |
|---|---|---|---|
| `F1048` | Manage Purchase Orders | Full PO management — create, change, display, output | Buyer |
| `F2348` | Create Purchase Order | Simplified PO creation from scratch | Buyer |
| — | Approve Purchase Orders | Mobile-ready approval inbox for PO approvers | Approver |
| `F2173` | Display Purchasing Documents | Read-only view of all purchasing documents | All Procurement |
| `F3163` | My Purchasing Document Worklist | Task-based worklist — POs pending action | Buyer |
| — | Monitor Purchase Order Items | KPI-based view of PO item statuses | Procurement Manager |

---

## Goods Receipt & Inventory Apps

| App ID | App Name | Description | User Role |
|---|---|---|---|
| `F1062` | Post Goods Receipt for Purchase Order | Record delivery of goods against PO | Warehouse / Buyer |
| — | Manage Inbound Deliveries | Track expected deliveries and ASNs | Warehouse |
| — | Display Material Documents | View GR/GI material documents | Buyer / Warehouse |
| — | Stock Overview | Current stock levels by plant and material | Buyer / Planner |

---

## Invoice Verification Apps

| App ID | App Name | Description | User Role |
|---|---|---|---|
| `F1068` | Create Supplier Invoice | Enter vendor invoice (equivalent to MIRO) | AP Accountant |
| `F2142` | Manage Supplier Invoices | Monitor all invoices — posted, parked, blocked | AP Accountant |
| — | Release Blocked Invoices | Review and release payment-blocked invoices | Buyer / AP Lead |
| — | Display Supplier Invoice | Read-only display of posted invoice + accounting doc | All Finance |
| — | Supplier Invoice Worklist | Task-based view of invoices requiring action | AP Accountant |

---

## Contract Management Apps

| App ID | App Name | Description | User Role |
|---|---|---|---|
| `F4868` | Manage Supplier Contracts | Create, change, display contracts and scheduling agreements | Buyer / Contracts Team |
| — | Contract Monitoring | Track contract utilization — value and qty consumed | Procurement Manager |
| — | Contracts Expiring Soon | Alert list of contracts near expiry date | Buyer / Manager |

---

## Sourcing & Contracting Apps

| App | Name | Description | User Role |
|---|---|---|---|
| — | Sourcing and Contracting | All-in-one workspace for sourcing projects, RFx events, auctions, and award | Strategic Buyer |
| — | Manage Sourcing Projects | Create and track sourcing project lifecycle | Strategic Buyer |
| — | Publish RFx | Push sourcing events to SAP Business Network | Strategic Buyer |
| — | Evaluate Bids | Side-by-side bid comparison with scoring | Strategic Buyer |
| — | Supplier Evaluation | Structured supplier scoring and performance tracking | Strategic Buyer |

---

## Analytics & Reporting Apps

| App | Name | Description | User Role |
|---|---|---|---|
| — | Procurement Overview Page | Role-based cockpit — KPIs, exceptions, alerts | Procurement Manager |
| — | Spend Analysis | Spend by vendor, category, plant, time period | Procurement Manager |
| — | Supplier Delivery Performance | On-time delivery rate and trends | Buyer / Manager |
| — | Purchase Order Fulfillment | % of POs fully received and invoiced | Buyer |
| — | Operational Procurement | Cycle time analytics — PR to PO, PO to GR | Procurement Manager |

---

## Workflow & Approval Apps

| App | Name | Description | User Role |
|---|---|---|---|
| — | My Inbox | Unified inbox for all pending approvals | All Approvers |
| — | Flexible Workflow Configuration | Configure workflow rules and approval steps | Admin / Consultant |
| — | Workflow Monitor | View active and completed workflow instances | Admin |
| — | Substitution Rules | Set up delegation / substitution during absence | All Users |

---

## Fiori App Types

SAP Fiori apps come in three types:

| Type | Description | Examples |
|---|---|---|
| **Transactional** | Create, change, display documents | Manage Purchase Orders, Create Invoice |
| **Analytical** | KPIs, charts, drill-down reporting | Procurement Overview, Spend Analysis |
| **Fact Sheet** | 360° view of a master data object | Business Partner Fact Sheet, Material Fact Sheet |

---

## Access & Authorization

Fiori app access is controlled by **Business Roles** assigned to users:

| Business Role | Key Apps Included |
|---|---|
| Operational Purchaser | PR, PO, GR, Contracts |
| Strategic Purchaser | Sourcing, RFx, Contracts, Auctions |
| Accounts Payable Accountant | Invoice creation, release, monitoring |
| Procurement Manager | All of the above + analytics |
| Approver (any level) | My Inbox, document display |

> 💡 In SAP S/4HANA Public Cloud, business roles are pre-delivered by SAP and can be assigned directly in the **Maintain Business Users** app — no custom role development required for standard use cases.

---

> ← [Integration & Analytics](Integration-and-Analytics) | Next: [Glossary](Glossary) →
