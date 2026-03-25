# 🧾 Invoice Verification

> **Wiki Navigation:** [Home](Home) › Invoice Verification

---

## Overview

**Logistics Invoice Verification (LIV)** in SAP S/4HANA Public Cloud is the process of validating and posting a vendor's invoice against the corresponding Purchase Order and Goods Receipt. It is the final step before payment is released and is central to Accounts Payable accuracy.

---

## 3-Way Match Principle

The foundation of invoice verification is the **3-Way Match** — ensuring three documents align:

```
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│  Purchase Order  │     │  Goods Receipt   │     │ Vendor Invoice   │
│                  │     │                  │     │                  │
│  Material: X     │ ──► │  Qty Received: Y │ ──► │  Qty Billed: Y   │
│  Qty Ordered: Z  │     │  Date: DD/MM/YY  │     │  Price: $ P      │
│  Price: $ P      │     │                  │     │                  │
└──────────────────┘     └──────────────────┘     └──────────────────┘
         ↑                        ↑                        ↑
    Agreed Price             Confirmed             Must Match Both
```

### What is Checked
| Check | Description |
|---|---|
| **Price Check** | Invoice unit price vs PO net price (within tolerance) |
| **Quantity Check** | Invoiced quantity vs quantity on GR (within tolerance) |
| **Date Check** | Invoice date vs delivery date (for payment terms calculation) |
| **Tax Check** | Tax code and amount vs PO tax conditions |

---

## Invoice Verification Flow

```
Vendor Invoice Received
(Paper, email, EDI, PDF, or Ariba Network)
          │
          ▼
  Invoice Entry
  (MIRO transaction or Fiori App F1068)
          │
  Reference PO Number
          │
          ▼
  System Proposes Values from PO + GR
          │
          ▼
  ┌───────────────────────────────────┐
  │         Tolerance Check           │
  │  Compare Invoice vs PO vs GR      │
  └───────────────────────────────────┘
          │
     ┌────┴──────────┐
     │               │
  Within           Variance
  Tolerance        Detected
     │               │
     ▼               ▼
  Post Invoice    ┌──────────────────────────┐
  to FI           │ Block Invoice             │
                  │ (Automatic or Manual)     │
                  └──────────────────────────┘
                             │
                    ┌────────┴──────────┐
                    │                   │
               Buyer Reviews       Vendor Queried
                    │                   │
               Resolve Exception        │
                    └───────────────────┘
                             │
                             ▼
                    Release & Post to FI
                             │
                             ▼
                    Vendor Account Credited
                    → Payment Run
```

---

## Tolerance Configuration

Tolerances define how much variance is acceptable before an invoice is automatically blocked.

### Tolerance Keys

| Key | Description | Example Setting |
|---|---|---|
| `BD` | Form small differences (absolute) | ±$1.00 per invoice |
| `AN` | Amount for item without order reference | Maximum $500 |
| `AP` | Amount for item with order reference | ±$50 |
| `PP` | Price variance (percentage) | ±2% of PO price |
| `QU` | Quantity variance | ±5% of GR qty |
| `DQ` | Exceed amount: quantity variance | Dollar limit on qty variance |
| `VP` | Moving average price variance | ±$10 per unit |

### Tolerance Behaviour
- **Within tolerance** → Invoice posts automatically
- **Outside tolerance** → Invoice is **blocked** (payment block set)
- **Configurable per company code** → Each legal entity can have different limits

---

## Invoice Blocking

When an invoice cannot be automatically matched, SAP applies a **payment block** or **parking** status.

### Block vs. Park vs. Post

| Status | Description | Can Pay? |
|---|---|---|
| **Posted** | Fully verified and posted to FI | Yes — payment run will pick up |
| **Parked** | Saved but not posted — in progress | No |
| **Blocked** | Posted but payment withheld | No — must be released |

### Automatic Block Reasons

| Block Key | Reason |
|---|---|
| `R` | Invoice received before GR (timing block) |
| `Q` | Quantity variance exceeds tolerance |
| `P` | Price variance exceeds tolerance |
| `D` | Date variance (delivery date issue) |
| `A` | Amount exceeds configured limit |

### Manual Blocking
Buyers can manually set a payment block for:
- Vendor disputes
- Incorrect banking details
- Pending credit note from supplier
- Quality issue with delivered goods

---

## Invoice Release Process

```
Blocked Invoice in System
          │
          ▼
  Buyer Reviews Block Reason
          │
     ┌────┴───────────────────────────┐
     │                                │
  Issue Resolved               Issue Unresolved
  (Price agreed, GR posted,    (Debit note, return,
   tolerance adjusted)          vendor to re-issue)
     │                                │
     ▼                                ▼
  Remove Block                  Keep Block / Cancel Invoice
  Post to FI                    Issue Credit Memo Request
```

---

## Credit Memos & Subsequent Debits

| Document Type | Description |
|---|---|
| **Credit Memo** | Vendor issues credit to reduce an already-posted invoice |
| **Subsequent Debit** | Additional charge added to a previously posted invoice |
| **Subsequent Credit** | Reduction applied to previously posted invoice (not a full reversal) |
| **Invoice Cancellation** | Full reversal of a posted invoice |

---

## Evaluated Receipt Settlement (ERS)

**ERS** is an automated invoicing mechanism where SAP generates the invoice automatically upon Goods Receipt — no vendor invoice needed.

### ERS Requirements
- ERS indicator enabled on vendor master (Business Partner)
- ERS indicator enabled on PO line item
- Price must be clearly defined in PO (no price variance expected)
- GR-based IV must be active

### ERS Benefits
- Eliminates invoice processing effort for high-volume, stable-price vendors
- Reduces AP workload and invoice exceptions
- Improves payment accuracy and on-time payment rates

---

## Accounting Entries Summary

| Event | Debit | Credit |
|---|---|---|
| Goods Receipt posted | Inventory / GR Expense | GR/IR Clearing Account |
| Invoice posted (matched) | GR/IR Clearing Account | Vendor Account (AP) |
| Payment run | Vendor Account (AP) | Bank Account |
| Price variance (invoice > PO) | Price Difference Account | Vendor Account |
| Invoice reversal | Vendor Account | GR/IR Clearing Account |

---

## Key Fiori Apps for Invoice Verification

| App | Function |
|---|---|
| Create Supplier Invoice (`F1068`) | Enter vendor invoice against PO |
| Manage Supplier Invoices (`F2142`) | Monitor status, block, release invoices |
| Release Blocked Invoices | Review and release payment-blocked invoices |
| Display Invoice Documents | View posted invoice with accounting document |

---

> ← [Operational Procurement](Operational-Procurement) | Next: [Contract Management](Contract-Management) →
