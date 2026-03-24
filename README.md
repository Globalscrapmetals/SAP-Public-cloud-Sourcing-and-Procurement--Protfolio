# SAP S/4HANA Public Cloud — Sourcing & Procurement Portfolio

> A comprehensive knowledge portfolio demonstrating end-to-end expertise in SAP S/4HANA Public Cloud Sourcing & Procurement — covering business processes, system configuration, flexible workflows, and cross-module integration.

---

## 📋 Table of Contents

1. [About This Portfolio](#about)
2. [Certification](#certification)
3. [Core Domains](#core-domains)
4. [Business Process Flows](#business-process-flows)
   - [Purchase-to-Pay (P2P)](#1-purchase-to-pay-p2p)
   - [Source-to-Contract (S2C)](#2-source-to-contract-s2c)
   - [RFx Process](#3-rfx-process)
   - [Invoice Verification](#4-invoice-verification)
5. [System Configuration](#system-configuration)
   - [Organizational Structure](#organizational-structure)
   - [Master Data](#master-data)
   - [Document Configuration](#document-configuration)
6. [Flexible Workflows & Approval Processes](#flexible-workflows--approval-processes)
7. [Strategic Sourcing Deep Dive](#strategic-sourcing-deep-dive)
8. [Contract Management](#contract-management)
9. [Integration Knowledge](#integration-knowledge)
10. [SAP Fiori Apps Reference](#sap-fiori-apps-reference)
11. [Key Terminology](#key-terminology)
12. [Portfolio Website](#portfolio-website)

---

## About

This repository showcases my functional and technical knowledge of **SAP S/4HANA Public Cloud** with a focus on the **Sourcing and Procurement** module. It is designed to demonstrate:

- **Business Process Understanding** — How procurement and sourcing cycles work end-to-end
- **System Configuration Knowledge** — How SAP is configured to support those processes
- **Workflow Design Competency** — How flexible approval workflows are set up and managed
- **Integration Awareness** — How procurement connects to Finance, Sales, and external networks

This portfolio is intended for recruiters, hiring managers, and SAP project teams looking for a certified Sourcing & Procurement professional.

---

## Certification

| Certification | Status |
|---|---|
| SAP S/4HANA Public Cloud — Sourcing & Procurement | ✅ Certified |
| Focus Areas | MM , Sourcing, Flexible Workflow |

---

## Core Domains

| Domain | Key Capabilities |
|---|---|
| 🎯 Strategic Sourcing | RFI, RFP, RFQ, Auctions, Award Decisions, Sourcing Projects |
| 📦 Operational Procurement | PR, PO, GR, Service Entry, Invoice Verification, SSP |
| 📋 Contract Management | Outline Agreements, Release Orders, Compliance Monitoring |
| ⚙️ System Configuration | Org Structures, Master Data, Document Types, Account Determination |
| 🔀 Flexible Workflows | Condition-based Routing, Multi-level Approvals, Escalation |
| 🔗 Integration & Analytics | MM–FI, MM–SD, Ariba Network, SAP Analytics Cloud |

---

## Business Process Flows

### 1. Purchase-to-Pay (P2P)

The core operational procurement cycle from need identification through vendor payment.

```
Purchase Requisition (PR)
        │
        ▼
  PR Approval (Flexible Workflow)
        │
        ▼
  Source of Supply Determination
  (Info Record / Source List / Contract)
        │
        ▼
  Purchase Order (PO)
        │
        ▼
  PO Approval (Flexible Workflow)
        │
        ▼
  Goods Receipt (GR) / Service Entry Sheet
        │
        ▼
  Invoice Verification (3-Way Match: PO + GR + Invoice)
        │
        ▼
  Invoice Approval (if blocked/parked)
        │
        ▼
  Payment Run (FI)
```

**Key Process Points:**
- The **PR** captures the business need: material, quantity, required delivery date, cost centre, and plant
- **Source of supply** is determined from source list, purchasing info record, or existing contract — in that priority order
- **3-way match** ensures PO price, GR quantity, and invoice amount are within tolerance
- **GR/IR clearing** account reconciles goods received vs. invoiced amounts

---

### 2. Source-to-Contract (S2C)

Strategic sourcing lifecycle from spend identification through contract establishment.

```
Spend Analysis & Category Strategy
        │
        ▼
  Sourcing Project Creation
  (Define scope, team, milestones)
        │
        ▼
  RFx Publication
  (RFI → RFP → RFQ)
        │
        ▼
  Supplier Bid Collection
  (via SAP Business Network / Supplier Portal)
        │
        ▼
  Bid Evaluation & Scoring
  (Price + Technical + Compliance criteria)
        │
        ▼
  Negotiation Rounds / Auction
        │
        ▼
  Award Decision
  (Per lot, per item, or split award)
        │
        ▼
  Contract Creation
  (Auto-created or manually from award)
        │
        ▼
  Contract Release Orders / Call-offs
```

---

### 3. RFx Process

Detailed flow for managing competitive bidding events.

| Step | Action | Actor |
|---|---|---|
| 1 | Create RFx (RFI/RFP/RFQ) with line items, questionnaires, T&Cs | Buyer |
| 2 | Select and invite suppliers | Buyer |
| 3 | Publish event and notify suppliers | System |
| 4 | Q&A collaboration during open period | Buyer + Supplier |
| 5 | Supplier bid submission via portal | Supplier |
| 6 | Bid comparison (price, technical, compliance) | Buyer |
| 7 | Negotiation rounds (if needed) | Buyer + Supplier |
| 8 | Award decision + acceptance letters | Buyer |
| 9 | Contract / PO creation from award | System / Buyer |

**RFx Types:**
- **RFI** — Request for Information: Market research, no commitment
- **RFP** — Request for Proposal: Solution + pricing, qualitative evaluation
- **RFQ** — Request for Quotation: Pricing-focused, quantitative comparison

---

### 4. Invoice Verification

Three-way matching and exception handling in Logistics Invoice Verification.

```
Vendor Invoice Received
(Manual entry / EDI / Email / PDF)
        │
        ▼
  Reference PO in MIRO or Fiori App
        │
        ▼
  ┌─────────────────────────────────┐
  │     3-Way Match Check           │
  │  PO Price vs Invoice Price      │
  │  PO Quantity vs GR Quantity     │
  │  PO Conditions vs Invoice       │
  └─────────────────────────────────┘
        │
   ┌────┴────┐
   │         │
Within     Variance
Tolerance  Detected
   │         │
   ▼         ▼
Post       Block / Park Invoice
Invoice    ──────────────────────
           → Buyer Reviews
           → Vendor Queries
           → Approve or Reject
                │
                ▼
           Release & Post to FI
```

**Tolerance Types:**
- **Price Variance** — Invoice unit price vs PO price
- **Quantity Variance** — Invoiced qty vs GR qty
- **Date Variance** — Delivery date vs billing date

---

## System Configuration

### Organizational Structure

SAP S/4HANA Public Cloud uses a layered organizational hierarchy that controls where and how procurement happens.

```
CLIENT (SAP System)
└── COMPANY CODE (Legal Entity / Financial Books)
    └── PLANT (Operational Unit — Production / Warehouse / Office)
        ├── STORAGE LOCATION (Physical bin/area within a plant)
        └── PURCHASING ORGANIZATION (Negotiates contracts and pricing)
            └── PURCHASING GROUP (Buyer team managing day-to-day POs)
```

| Object | Description | Example |
|---|---|---|
| Client | Entire SAP system | `100` |
| Company Code | Legal entity with own balance sheet | `CA01` — Canada Ltd. |
| Plant | Operational unit for manufacturing/storage | `1000` — Toronto Plant |
| Storage Location | Physical stock area within plant | `0001` — Raw Materials |
| Purchasing Org | Contract & price negotiating entity | `1000` — Central Purch. |
| Purchasing Group | Individual buyer or buyer team | `001` — Indirect Goods |

---

### Master Data

#### Material Master
The central object describing what is being procured. Key views:

| View | Key Fields |
|---|---|
| Basic Data | Material number, description, material group, base UoM |
| Purchasing | Purchasing group, planned delivery time, overdelivery tolerance |
| MRP | MRP type, reorder point, lot size, safety stock |
| Accounting | Valuation class, standard price / moving average price |
| Plant Data | Plant, storage location, batch management |

#### Business Partner / Vendor Master
Supplier data managed as Business Partner (BP) with procurement-specific views:

- **General Data** — Name, address, tax number, bank details
- **Purchasing Data** — Currency, payment terms, incoterms, GR-based IV indicator
- **Partner Functions** — Ordering address, goods supplier, invoicing party

#### Purchasing Info Record
Links a specific material to a specific vendor with pricing and delivery conditions:

```
Material XYZ  +  Vendor ABC  →  Info Record
                               ├── Net Price: $45.00/EA
                               ├── Delivery Time: 5 days
                               ├── Minimum Order Qty: 10
                               └── Validity: 01.01.2024 – 31.12.2024
```

#### Source List
Defines approved sources of supply for a material at a plant level. Can:
- Block unauthorized vendors
- Mark fixed sources (MRP will always use this vendor)
- Set validity periods

#### Quota Arrangement
Splits procurement volume across multiple vendors by percentage:

```
Material: Steel Rods — Plant: 1000
├── Vendor A: 60% of requirements
├── Vendor B: 30% of requirements
└── Vendor C: 10% of requirements (backup)
```

---

### Document Configuration

#### Purchase Order Document Types

| Doc Type | Description | Use Case |
|---|---|---|
| `NB` | Standard PO | Default PO for external procurement |
| `FO` | Framework Order | Blanket PO with open value / quantity |
| `UB` | Stock Transport Order | Inter-plant / inter-company stock movement |
| `ZNB` | Custom Standard PO | Client-specific enhancements |

#### Account Assignment Categories

| Category | Code | Usage |
|---|---|---|
| Cost Centre | `K` | Operating expenses charged to a department |
| Asset | `A` | Capital expenditure for fixed assets |
| Project (WBS) | `P` | Project-based procurement |
| Sales Order | `C` | Customer-specific procurement (MTO) |
| Unknown | `U` | Used when assignment not yet known |

#### Item Categories

| Category | Description |
|---|---|
| Standard | Physical goods with GR requirement |
| Consignment | Goods owned by vendor until consumption |
| Subcontracting | Vendor processes your material, returns finished goods |
| Limit / Blanket | Service with overall value limit, no fixed qty |
| Third Party | Vendor ships directly to end customer |

---

## Flexible Workflows & Approval Processes

SAP S/4HANA Public Cloud uses **Flexible Workflow** (replacing classical release strategies) to route procurement documents for approval based on configurable business rules.

### How Flexible Workflow Works

```
Document Created / Changed
          │
          ▼
   Workflow Rule Engine
   (Evaluates conditions)
          │
   ┌──────┴──────────────────────┐
   │                             │
No Approval Needed          Approval Required
   │                             │
Auto-Approved               Approval Task sent
                            to Approver Inbox
                                 │
                         ┌───────┴───────┐
                         │               │
                      Approved        Rejected
                         │               │
                    Document          Returned to
                    Proceeds          Requester
```

### Sample Approval Conditions

**Purchase Order Approval Rules:**

| Rule | Condition | Approver |
|---|---|---|
| 1 | Net Value < $5,000 | Auto-approve |
| 2 | $5,000 – $25,000 | Line Manager |
| 3 | $25,000 – $100,000 | Manager + Department Head |
| 4 | $100,000 – $500,000 | Manager + Head + VP Procurement |
| 5 | > $500,000 | Full chain + CFO |
| 6 | New Vendor (any amount) | Compliance Officer + Manager |
| 7 | CapEx (Account Assignment A) | Finance Controller + Manager |

### Approval Features in Flexible Workflow

| Feature | Description |
|---|---|
| **Multi-Step** | Chain multiple approvers in sequence or parallel |
| **Condition-Based** | Route based on value, org unit, category, vendor type |
| **Escalation** | Auto-escalate to next level if not acted upon within deadline |
| **Delegation** | Approver delegates to substitute during absence |
| **Ad-Hoc Approver** | Add extra approver on the fly without changing base rules |
| **Mobile Approval** | Approve/reject via SAP Fiori Launchpad on any device |
| **Reminder Notifications** | Automated email reminders for pending approvals |
| **Audit Trail** | Full approval history logged on the document |

### Documents Supported by Flexible Workflow

- ✅ Purchase Requisition (PR)
- ✅ Purchase Order (PO)
- ✅ Supplier Invoice
- ✅ Contracts / Outline Agreements
- ✅ Sourcing Events (RFx)
- ✅ Goods Receipt (for high-value / sensitive items)

---

## Strategic Sourcing Deep Dive

### Sourcing Project Management

A **Sourcing Project** is the container for all sourcing activities:

- Define project type (New sourcing, Re-sourcing, Spot buy)
- Assign team members with roles (Lead buyer, approver, observer)
- Set milestones and deadlines
- Create RFx events within the project
- Track project status through to contract award

### Auction Types in SAP

| Auction Type | Description |
|---|---|
| **English (Forward)** | Price increases — used for selling |
| **Dutch (Reverse)** | Price decreases — vendors compete to offer lowest price |
| **Japanese** | All-or-nothing rounds, participants drop out |
| **Ranked** | Suppliers see their rank, not competitor prices |

> In procurement, **Reverse Auctions** (Dutch format) are most common — suppliers compete by lowering prices in real time.

### Supplier Evaluation

After bid collection, buyers score suppliers using weighted criteria:

```
Total Score = Σ (Criterion Weight × Supplier Score)

Example:
├── Price:           40% weight  ×  85 points  = 34.0
├── Quality:         25% weight  ×  90 points  = 22.5
├── Delivery:        20% weight  ×  78 points  = 15.6
├── Sustainability:  10% weight  ×  70 points  = 7.0
└── Innovation:       5% weight  ×  65 points  = 3.25
                              Total Score: 82.35 / 100
```

---

## Contract Management

### Contract Types in SAP

| Type | Transaction | Description |
|---|---|---|
| Quantity Contract | `MK` | Fixed total quantity to purchase from vendor |
| Value Contract | `WK` | Fixed total spend commitment with vendor |
| Scheduling Agreement | `LP` / `LPA` | Delivery schedule with planned dates and quantities |

### Contract Lifecycle

```
Award Decision (from RFx)
        │
        ▼
  Contract Created
  (Manually or auto-generated)
        │
        ▼
  Contract Approved
  (Flexible Workflow)
        │
        ▼
  Contract Active
  ├── Release Orders issued (call-offs)
  ├── Compliance monitored (qty / value consumed)
  └── Supplier performance tracked
        │
        ▼
  Contract Expiry Warning
  (Alert X days before end date)
        │
        ▼
  Renew / Renegotiate / Close
```

### Key Contract Fields

- **Validity period** — Start and end date
- **Target value / quantity** — Total commitment
- **Release documentation** — Whether POs need to reference this contract
- **Item conditions** — Negotiated price scales and discounts
- **Partner functions** — Ordering address, invoicing party, goods supplier

---

## Integration Knowledge

### MM → FI Integration

| Procurement Event | Financial Impact |
|---|---|
| Goods Receipt (GR) | Dr. Inventory / Expense Account → Cr. GR/IR Clearing |
| Invoice Verification | Dr. GR/IR Clearing → Cr. Vendor Account (AP) |
| Payment | Dr. Vendor Account → Cr. Bank Account |
| Invoice Variance | Dr./Cr. Price Difference Account |

### MM → SD Integration

- **Stock Transport Orders (STO)** — Move stock between plants, triggers SD delivery
- **Third-Party Orders** — Customer sales order triggers vendor PO
- **Intercompany Procurement** — Cross-company code purchasing with automatic billing

### SAP Business Network (Ariba) Integration

- Suppliers access orders and submit invoices via the **Ariba Network**
- Catalog punchout for guided buying
- Invoice status visibility for supplier self-service
- Automatic invoice status sync between Ariba and SAP S/4HANA

---

## SAP Fiori Apps Reference

| App ID | App Name | Function |
|---|---|---|
| `F0842` | Manage Purchase Requisitions | Create, edit, approve PRs |
| `F1048` | Manage Purchase Orders | Create, change, display POs |
| `F1062` | Post Goods Receipt for PO | Record GR against PO |
| `F1068` | Create Supplier Invoice | Enter vendor invoice (MIRO equivalent) |
| `F2142` | Manage Supplier Invoices | Monitor, block, release invoices |
| `F2173` | Display Purchasing Documents | View all procurement docs |
| `F3163` | My Purchasing Document Worklist | Buyer task list and follow-ups |
| `F4868` | Manage Supplier Contracts | Create and monitor contracts |
| — | Sourcing and Contracting | Full sourcing workspace (RFx, auctions) |
| — | Approve Purchase Orders | Mobile-ready approval inbox |
| — | Monitor Purchase Order Items | KPI-based procurement monitoring |
| — | Procurement Overview Page | Role-based analytical cockpit |

---

## Key Terminology

| Term | Definition |
|---|---|
| **PR** | Purchase Requisition — internal request to buy |
| **PO** | Purchase Order — legal document sent to vendor |
| **GR** | Goods Receipt — confirmation goods were received |
| **GR/IR** | Goods Receipt / Invoice Receipt clearing account |
| **MIRO** | SAP transaction for Logistics Invoice Verification |
| **RFx** | Generic term for RFI, RFP, and RFQ events |
| **Info Record** | Vendor-material combination with price and delivery data |
| **Source List** | Approved vendor list for a material/plant |
| **Outline Agreement** | Umbrella purchasing agreement (contract or scheduling agreement) |
| **Release Order** | Call-off order issued against a contract |
| **3-Way Match** | Verification of PO, GR, and Invoice alignment |
| **Flexible Workflow** | SAP's rule-based approval routing engine |
| **Business Partner (BP)** | Unified master data record for vendors, customers |
| **MRP** | Material Requirements Planning — auto-generates PRs |
| **Account Assignment** | Determines cost object charged (cost centre, asset, WBS) |
| **Valuation Class** | Links material to G/L accounts for automatic posting |
| **Incoterms** | International delivery terms (EXW, DDP, FOB, CIF, etc.) |

---

## Portfolio Website

This repository includes a full interactive portfolio website (`index.html`) that visually showcases all the knowledge areas above, including:

- ✅ Animated domain cards for each expertise area
- ✅ Interactive tabbed process flow diagrams (P2P, S2C, RFx, Invoice)
- ✅ Configuration reference tables (Org structure, Master Data, Fiori Apps)
- ✅ Visual flexible workflow approval diagram
- ✅ Skills inventory with proficiency indicators

**To view:** Open `index.html` in any web browser — no server or build step required.

---

*Portfolio created to showcase SAP S/4HANA Public Cloud Sourcing & Procurement certification knowledge.*
