# 📋 Contract Management

> **Wiki Navigation:** [Home](Home) › Contract Management

---

## Overview

Contract Management in SAP S/4HANA Public Cloud enables procurement teams to establish, maintain, and monitor long-term vendor agreements. Contracts serve as the source of supply for repeat procurement, ensuring negotiated prices and terms are consistently applied across all purchase orders.

In SAP terminology, contracts are called **Outline Agreements** and come in two primary forms: **Contracts** and **Scheduling Agreements**.

---

## Types of Outline Agreements

| Type | SAP Doc Type | Description | Key Differentiator |
|---|---|---|---|
| **Quantity Contract** | `MK` | Commit to buy a total quantity from a vendor | Tracks qty consumed vs. target |
| **Value Contract** | `WK` | Commit to spend a total value with a vendor | Tracks value consumed vs. budget |
| **Scheduling Agreement** | `LP` / `LPA` | Planned delivery schedule with dates and quantities | Delivery lines with specific dates |
| **Distributed Contract** | `WK` with distribution | Central contract available to multiple plants | Shared enterprise-wide agreement |

---

## Contract Lifecycle

```
Award Decision (from RFx / Sourcing Event)
          │         OR
          │    Direct Contract Creation
          ▼
  Contract Document Created
  (Auto from award, or manually created)
          │
          ▼
  Contract Approval
  (Flexible Workflow — procurement + legal sign-off)
          │
          ▼
  ┌─────────────────────────────────────┐
  │         CONTRACT ACTIVE             │
  │  ├── Validity period running        │
  │  ├── Release orders issued          │
  │  ├── Value / qty consumed tracked   │
  │  └── Supplier performance logged    │
  └─────────────────────────────────────┘
          │
          ▼
  Contract Expiry Warning
  (Configurable X days before end date — alert to buyer)
          │
     ┌────┴────────────────┐
     │                     │
  Renew Contract      Close / Expire
  (New validity,       (Archive in system,
   updated pricing)     no further call-offs)
```

---

## Key Contract Header Fields

| Field | Description |
|---|---|
| **Vendor** | Supplier this agreement is with |
| **Purchasing Organization** | Org unit responsible for the contract |
| **Validity Start / End Date** | Active period of the contract |
| **Target Value** | Total spend commitment (value contract) |
| **Target Quantity** | Total quantity commitment (quantity contract) |
| **Payment Terms** | Agreed payment terms (e.g., Net 30, 2/10 Net 30) |
| **Incoterms** | Delivery terms and risk transfer point |
| **Currency** | Contract pricing currency |
| **Release Documentation** | Whether release POs must reference this contract |

---

## Contract Line Items

Each contract has line items defining what is covered:

| Field | Description |
|---|---|
| Material / Service | What is being contracted |
| Target Quantity | Quantity committed per item (qty contract) |
| Net Price | Negotiated price per unit |
| Price Unit | Quantity per price unit (e.g., price per 100 units) |
| Material Group | Category classification |
| Plant | Delivering plant (if plant-specific) |
| Conditions | Additional pricing: discounts, scales, surcharges |

---

## Release Orders (Call-Offs)

A **Release Order** is a standard Purchase Order that references a contract and draws down the committed value or quantity.

### Release Order Creation
```
Open Contract in Fiori
          │
          ▼
  Create Release Order
  (Reference contract number)
          │
          ▼
  Prices Auto-Populated from Contract
          │
          ▼
  Release PO Approved (if required by workflow)
          │
          ▼
  PO Sent to Vendor
          │
          ▼
  Contract Target Value/Qty Updated
  (Remaining balance reduced)
```

### Release Order Rules
- If **Release Documentation** is active, all POs for that material/vendor **must** reference the contract
- If a contract is **expired**, release orders cannot be created against it
- **Over-fulfillment** — system warns (or blocks) if release orders exceed target value/qty

---

## Scheduling Agreements

A **Scheduling Agreement** is used when the procurement plan is known in advance — for example, in manufacturing environments with regular deliveries.

### Structure
```
Scheduling Agreement Header
  (Vendor, validity, pricing)
          │
          ▼
  Scheduling Agreement Lines
  (Material, quantity per delivery)
          │
          ▼
  Delivery Schedule Lines
  ├── 2024-01-15: 500 units
  ├── 2024-02-15: 500 units
  ├── 2024-03-15: 500 units
  └── 2024-04-15: 500 units
          │
          ▼
  Schedule Lines Transmitted to Vendor
  (As delivery forecasts or firm orders)
```

### SA Types
| Type | Code | Description |
|---|---|---|
| Standard SA | `LP` | Non-release documentation required |
| SA with Release | `LPA` | Requires scheduling agreement releases (JIT delivery) |

---

## Contract Compliance & Monitoring

### Compliance Tracking
SAP tracks contract utilization in real time:
- **% of target value consumed** — visible in contract header
- **% of target quantity consumed** — per line item
- **Open release order values** — commitments not yet invoiced
- **Actual spend vs. committed** — comparison view

### Expiry Management
| Alert Type | Trigger |
|---|---|
| Expiry Warning | Contract end date approaching (configurable days in advance) |
| Budget Warning | Contract value 80% / 90% / 100% consumed |
| No-Release Warning | Contract active but no orders placed |

### Reporting
Key analytics available:
- Contracts expiring in next 30/60/90 days
- Contracts with low utilization (potential savings loss)
- Spend under contract vs. off-contract (maverick buying rate)
- Vendor performance against contracted SLAs

---

## Supplier Collaboration on Contracts

Via **SAP Business Network**, suppliers can:
- View their active contracts and release order history
- Acknowledge contract terms
- Submit invoices directly against contract release orders
- Receive notifications for upcoming renewals

---

## Key Business Rules & Best Practices

- Always set a **Release Documentation** flag on contracts for strategic categories — this forces buyers to use the contract and prevents off-contract purchasing
- Use **Distributed Contracts** for enterprise-wide agreements to avoid duplicate contracts per plant
- Link contracts to **sourcing projects** for full audit trail from RFx to contract
- Set **expiry alerts** with sufficient lead time (60–90 days) to allow re-tendering before expiry
- Regularly run **contract utilization reports** — underutilized contracts signal maverick buying or demand forecast inaccuracies

---

> ← [Invoice Verification](Invoice-Verification) | Next: [System Configuration](System-Configuration) →
