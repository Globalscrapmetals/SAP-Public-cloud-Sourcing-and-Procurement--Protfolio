# 📦 Operational Procurement

> **Wiki Navigation:** [Home](Home) › Operational Procurement

---

## Overview

Operational Procurement covers the day-to-day execution of purchasing — from recognizing a need through to paying the supplier. In SAP S/4HANA Public Cloud, this is the **Purchase-to-Pay (P2P)** process, supported by the Materials Management (MM) module and executed via SAP Fiori applications.

---

## Purchase-to-Pay (P2P) Process Flow

```
Business Need Identified
          │
          ▼
  Purchase Requisition (PR) Created
  (Manually, via MRP, or from Shopping Cart)
          │
          ▼
  PR Approval
  (Flexible Workflow — based on value & cost centre)
          │
          ▼
  Source of Supply Determination
  ├── Source List (fixed source)
  ├── Purchasing Info Record (preferred vendor)
  └── Outline Agreement / Contract (call-off)
          │
          ▼
  Purchase Order (PO) Created
  (Converted from PR or created manually)
          │
          ▼
  PO Approval
  (Flexible Workflow — based on value thresholds)
          │
          ▼
  PO Transmitted to Vendor
  (Print, EDI, email, or Ariba Network)
          │
          ▼
  Goods Receipt (GR) Posted
  or Service Entry Sheet (SES) Created
          │
          ▼
  Invoice Verification
  (3-Way Match: PO + GR + Invoice)
          │
          ▼
  Payment Processing (FI)
```

---

## Purchase Requisition (PR)

A **Purchase Requisition** is an internal document that communicates a need to the purchasing department. It does **not** go to the vendor — it is an internal authorization request.

### PR Header Fields
| Field | Description |
|---|---|
| Document Date | Date PR is created |
| Purchasing Group | Buyer responsible for processing |
| Document Type | NB (standard), or custom type |

### PR Line Item Fields
| Field | Description |
|---|---|
| Material / Short Text | What is needed |
| Quantity & UoM | How much is required |
| Delivery Date | When it is needed |
| Plant | Where it should be delivered |
| Storage Location | Exact storage area within plant |
| Account Assignment | Cost Centre (K), Asset (A), WBS (P) |
| Material Group | Category classification |

### PR Sources
- **Manual creation** — Buyer or requester creates PR in Fiori
- **MRP run** — System auto-generates PRs based on demand planning
- **Self-Service Procurement** — Employee creates shopping cart that converts to PR
- **Project system** — WBS element triggers material requirement

---

## Purchase Order (PO)

A **Purchase Order** is a legally binding document issued to a vendor to procure goods or services at agreed prices and terms.

### PO Document Types

| Type | Code | Use Case |
|---|---|---|
| Standard PO | `NB` | Default external procurement |
| Framework Order | `FO` | Blanket order with open qty/value |
| Stock Transport Order | `UB` | Inter-plant stock movement |
| Scheduling Agreement Release | `LP` | Delivery against scheduling agreement |

### PO Line Item Categories

| Item Category | Description | GR Required? |
|---|---|---|
| Standard (blank) | Physical goods | Yes |
| Consignment | `K` — Vendor owns until consumption | Yes |
| Subcontracting | `L` — Vendor processes your material | Yes |
| Third Party | `S` — Vendor ships directly to customer | No (confirmation) |
| Service | `D` — Non-stock services | Service Entry Sheet |
| Limit/Blanket | `B` — Open value limit for services | SES or GR |

### Account Assignment Categories

| Category | Code | Used For |
|---|---|---|
| Cost Centre | `K` | Operating expenses |
| Asset | `A` | Capital expenditure |
| WBS Element | `P` | Project costs |
| Sales Order | `C` | Make-to-order production |
| Network | `N` | Plant maintenance / project |
| Unknown | `U` | Assignment to be confirmed later |

### PO Pricing Elements
- **Net price** — Base vendor price per unit
- **Conditions** — Discounts, surcharges, freight added via condition records
- **Tax code** — Applied to determine GST/HST/VAT amount
- **Payment terms** — e.g., Net 30, 2/10 Net 30
- **Incoterms** — Delivery responsibility (EXW, FOB, DDP, CIF, etc.)

---

## Goods Receipt (GR)

A **Goods Receipt** records the physical receipt of goods against an open Purchase Order. Posting a GR updates inventory and triggers automatic financial accounting entries.

### GR Posting Effects
| System Area | Effect |
|---|---|
| Inventory | Stock quantity increased at plant/storage location |
| Accounting | Dr. Inventory/GR Expense → Cr. GR/IR Clearing |
| PO | Delivery quantity updated; PO history recorded |
| Invoice Verification | GR quantity now available for 3-way match |

### GR Movement Types
| Movement Type | Description |
|---|---|
| `101` | GR for Purchase Order (standard) |
| `103` | GR into Goods Receipt Blocked Stock |
| `105` | Release from Blocked Stock to unrestricted |
| `122` | Return to Vendor (reversal of GR) |
| `161` | Returns PO (vendor sends replacement) |

### Service Entry Sheet (SES)
For **service POs** (item category D), a Service Entry Sheet replaces the Goods Receipt:
- Created by the person who received/confirmed the service
- Records what service was performed, quantities, and value
- Requires acceptance before invoice can be processed
- Links back to the service PO line item

---

## Self-Service Procurement (SSP)

Self-Service Procurement (also called **Shopping Cart**) allows non-purchasing employees to request goods and services directly, without creating a formal PR.

### SSP Process
```
Employee Searches Catalog or Enters Free-Text Item
          │
          ▼
  Shopping Cart Created
  (Includes cost centre, plant, delivery address)
          │
          ▼
  Shopping Cart Approved
  (Line manager or budget owner)
          │
          ▼
  Automatic PR / PO Created in Background
          │
          ▼
  Vendor Ships / Delivers
          │
          ▼
  Employee Confirms Receipt (GR)
          │
          ▼
  Invoice Processed
```

### SSP Catalog Types
| Catalog Type | Description |
|---|---|
| Internal Catalog | Items pre-loaded by procurement team |
| External Punchout | Employee redirected to vendor website |
| Free-Text Request | Employee describes item manually |

---

## Key Business Rules

- A PO **must** reference a vendor, material (or short text), quantity, price, and delivery date as minimum
- **GR-based invoice verification** flag on the vendor master ensures invoices cannot be posted until GR is confirmed
- **Over-delivery tolerance** on the PO line controls whether excess deliveries are accepted
- **Final delivery indicator** closes a PO line to further GRs once marked
- POs can be **output** to vendors via print, fax, email, EDI, or Ariba Network
- **PO change management** — amendments to price or quantity above a threshold can re-trigger workflow

---

> ← [Strategic Sourcing](Strategic-Sourcing) | Next: [Invoice Verification](Invoice-Verification) →
