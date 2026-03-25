# 🔗 Integration & Analytics

> **Wiki Navigation:** [Home](Home) › Integration & Analytics

---

## Overview

SAP S/4HANA Public Cloud Procurement does not operate in isolation — it is tightly integrated with Financial Accounting (FI), Sales & Distribution (SD), and external networks. Understanding these integration touchpoints is critical for any SAP Procurement professional, as configuration errors at these boundaries are the most common source of posting errors and reconciliation problems.

---

## MM → FI Integration (Materials Management to Finance)

Every procurement event that changes stock value or creates a liability automatically generates an **accounting document** in FI — no manual journal entry is required.

### Accounting Flow by Event

| Procurement Event | Debit | Credit | Account Type |
|---|---|---|---|
| **Goods Receipt (GR)** | Inventory or Expense Account | GR/IR Clearing | Balance Sheet / P&L |
| **Invoice Verification (matched)** | GR/IR Clearing Account | Vendor Account (AP) | Balance Sheet |
| **Invoice — Price Variance** | Price Difference Account | Vendor Account | P&L |
| **Invoice — Quantity Variance** | GR/IR Clearing Account | Vendor Account | Balance Sheet |
| **Payment Run** | Vendor Account (AP) | Bank Account | Balance Sheet |
| **GR Reversal** | GR/IR Clearing | Inventory Account | Reverse of GR |
| **Invoice Cancellation** | Vendor Account | GR/IR Clearing | Reversal |

### GR/IR Clearing Account Explained

The **GR/IR (Goods Receipt / Invoice Receipt) Clearing Account** is a control account that sits between the warehouse and accounts payable:

```
Goods Received (GR posted)
    → Debit: Inventory $10,000
    → Credit: GR/IR Clearing $10,000

Invoice Received (LIV posted)
    → Debit: GR/IR Clearing $10,000
    → Credit: Vendor Account $10,000

Result: GR/IR Clearing = $0 (balanced)
```

> ⚠️ An unbalanced GR/IR account indicates either a GR without an invoice, or an invoice without a GR — both require investigation.

### Account Determination Logic

SAP determines which G/L accounts to post to automatically based on:

```
Movement Type  +  Valuation Class  +  Plant  →  G/L Account
    (101)             (3000)           (1000)  →  Inventory Raw Materials
```

Key configuration objects:

| Object | Purpose |
|---|---|
| **Valuation Class** | Set on material master; groups materials for accounting |
| **Transaction Key** | SAP-defined posting event code (BSX, WRX, PRD...) |
| **Chart of Accounts** | G/L structure assigned to company code |
| **Account Modification** | Further subdivision within a transaction key |

---

## MM → SD Integration (Materials Management to Sales & Distribution)

### Stock Transport Orders (STO)

Used to move stock between plants — triggers a delivery in SD for the receiving plant.

```
Sending Plant 1000 (Toronto)  →  Receiving Plant 2000 (Vancouver)

Step 1: STO created (UB document type) in MM
Step 2: Outbound Delivery created in SD (from sending plant)
Step 3: Goods Issue posted at sending plant (stock leaves)
Step 4: Goods Receipt posted at receiving plant (stock arrives)
Step 5: (Inter-company only) SD billing document created
```

### Third-Party Orders

A customer places a sales order, but the goods are shipped directly from the vendor to the customer — no stock passes through your warehouse.

```
Customer Sales Order (SD)
          │
          ▼
  Purchase Requisition auto-created (MM)
          │
          ▼
  Purchase Order created to vendor
          │
          ▼
  Vendor ships directly to customer
          │
          ▼
  PO confirmation triggers SD delivery confirmation
          │
          ▼
  Vendor invoice → your company
  Your invoice   → customer
```

### Intercompany Procurement

When one company code buys from another within the same SAP system:
- Purchasing company code issues a standard PO
- Supplying company code creates a sales order in SD
- Goods are shipped and SD billing creates an intercompany invoice
- MM processes the intercompany invoice in LIV

---

## SAP Business Network (Ariba) Integration

The **SAP Business Network** (formerly Ariba Network) connects SAP S/4HANA with supplier systems for digital procurement collaboration.

### Integration Scope

| Feature | Description |
|---|---|
| **PO Transmission** | Purchase Orders sent electronically to supplier via network |
| **Order Confirmation** | Supplier confirms PO receipt and delivery date |
| **Advanced Shipping Notification (ASN)** | Supplier notifies shipment before goods arrive |
| **Catalog Punchout** | Employee browses supplier catalog; items pulled back to SAP |
| **Invoice Submission** | Supplier submits electronic invoice directly into SAP |
| **Invoice Status** | Supplier tracks payment status in real time |
| **Supplier Registration** | New vendor onboarding via network profile |

### Integration Architecture

```
SAP S/4HANA Public Cloud
          │
          │  (API / middleware)
          ▼
  SAP Integration Suite (Cloud Integration)
          │
          │  (Ariba Network Protocol)
          ▼
  SAP Business Network
          │
          │  (Supplier Portal Access)
          ▼
  Supplier Systems / Supplier Portal
```

### Benefits
- **Eliminates paper invoices** — reduces AP processing costs
- **Reduces invoice errors** — supplier-entered data validated before submission
- **Improves supplier relationships** — real-time payment visibility
- **Supports compliance** — enforces procurement policy via network rules

---

## Analytics & Reporting

### Embedded Analytics in SAP S/4HANA

SAP S/4HANA Public Cloud includes built-in analytical apps — no separate BI tool required for standard procurement reporting.

#### Key Procurement KPIs

| KPI | Description | Fiori App |
|---|---|---|
| **On-Time Delivery Rate** | % of POs delivered by requested date | Supplier Delivery Performance |
| **Invoice Exception Rate** | % of invoices blocked or requiring intervention | Monitor Supplier Invoices |
| **Maverick Buying Rate** | % of spend outside contracts | Spend Analysis |
| **Contract Coverage** | % of spend under active contract | Contract Monitoring |
| **PO Cycle Time** | Avg days from PR to PO | Operational Procurement |
| **Approval Cycle Time** | Avg days from document creation to approval | Flexible Workflow Analytics |
| **Supplier Spend Distribution** | Spend concentration by supplier | Spend Analytics |

### Procurement Overview Page

The **Procurement Overview Page** is a role-based Fiori app providing a consolidated cockpit for procurement managers:

```
Procurement Overview Page
├── 📊 Open POs by status (ordered, GR pending, invoice pending)
├── 📈 Spend trend (monthly/quarterly)
├── ⚠️  Exception alerts (blocked invoices, delayed deliveries)
├── 📋 Contracts expiring in 30/60/90 days
├── 🔔 Approval inbox shortcut
└── 📉 KPI tiles with drill-down capability
```

### SAP Analytics Cloud (SAC) Integration

For advanced analytics beyond standard embedded apps, SAP Analytics Cloud connects to S/4HANA for:
- **Custom dashboards** with drag-and-drop visualization
- **Predictive analytics** — demand forecasting, price trend analysis
- **What-if scenarios** — procurement simulation modeling
- **Cross-module reports** — Procurement + Finance + Operations combined

---

> ← [Flexible Workflows & Approvals](Flexible-Workflows-and-Approvals) | Next: [Fiori Apps Reference](Fiori-Apps-Reference) →
