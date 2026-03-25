# ⚙️ System Configuration

> **Wiki Navigation:** [Home](Home) › System Configuration

---

## Overview

System Configuration in SAP S/4HANA Public Cloud defines how the system is structured to reflect a company's legal entities, operational units, and procurement controls. Unlike SAP ECC/on-premise, SAP S/4HANA Public Cloud uses a **pre-configured best-practice baseline** — customization is done through guided configuration apps rather than raw ABAP/IMG customizing.

---

## Organizational Structure

The organizational hierarchy controls *where* procurement happens and *who* is responsible for it.

```
CLIENT
(Entire SAP system — single instance)
    │
    └── COMPANY CODE
        (Legal entity — own financial books, balance sheet)
            │
            ├── PLANT
            │   (Operational unit — factory, warehouse, office)
            │       │
            │       └── STORAGE LOCATION
            │           (Physical area within plant — bin, rack, area)
            │
            └── PURCHASING ORGANIZATION
                (Negotiates prices and contracts with vendors)
                    │
                    └── PURCHASING GROUP
                        (Individual buyer or buyer team)
```

### Organizational Objects Reference

| Object | Code Example | Purpose |
|---|---|---|
| Client | `100` | Entire SAP landscape |
| Company Code | `CA01` | Canada Ltd. — legal entity |
| Plant | `1000` | Toronto Manufacturing Plant |
| Storage Location | `0001` | Raw Materials Warehouse |
| Purchasing Org | `1000` | Central Purchasing |
| Purchasing Group | `001` | Indirect Goods Buyers |
| Purchasing Group | `002` | Raw Materials Buyers |

### Purchasing Org Assignment Models

| Model | Description | Use Case |
|---|---|---|
| **Plant-Specific** | Each plant has its own Purchasing Org | Decentralized procurement |
| **Cross-Plant** | One Purchasing Org serves multiple plants | Centralized procurement |
| **Cross-Company** | Purchasing Org spans multiple company codes | Shared services / SSC |

---

## Master Data

### Material Master

The Material Master is the central object describing what is procured, stored, or produced. It is organized by **views** — each view relevant to a different organizational level.

| View | Org Level | Key Fields |
|---|---|---|
| Basic Data 1 | Client | Material number, description, material group, base UoM |
| Basic Data 2 | Client | Gross weight, net weight, dimensions, shelf life |
| Purchasing | Purchasing Org / Plant | Purchasing group, planned delivery time, overdelivery tolerance, GR processing time |
| MRP 1 | Plant | MRP type (PD, VB, etc.), reorder point, lot sizing procedure |
| MRP 2 | Plant | Safety stock, minimum/maximum stock levels, scheduling |
| MRP 3 | Plant | Availability check, planning calendar |
| Accounting 1 | Plant | Valuation class, price control (S/V), standard/MAP price |
| Accounting 2 | Plant | Tax classification, LIFO/FIFO data |
| Plant Data / Stor. 1 | Plant / SLoc | Hazardous material indicator, temperature conditions |

### Price Control Types
| Type | Code | Description |
|---|---|---|
| Standard Price | `S` | Fixed price — variances go to price difference account |
| Moving Average Price | `V` | Price updates with each GR — reflects actual costs |

---

### Business Partner / Vendor Master

In SAP S/4HANA, vendor data is managed via the **Business Partner (BP)** framework — a unified master record for all partner roles.

```
Business Partner (BP)
    │
    ├── General Role (BP000)
    │   └── Name, address, tax numbers, bank details
    │
    ├── FI Vendor Role (FLVN00)
    │   └── Reconciliation account, payment terms, dunning
    │
    └── MM Purchasing Role (FLVN01)
        └── Currency, incoterms, GR-based IV, ERS flag
```

### Key Vendor Master Fields

| Area | Field | Description |
|---|---|---|
| General | Name / Address | Legal vendor name and registered address |
| General | Tax Number | VAT / GST / HST registration |
| General | Bank Details | Account for payment runs |
| Purchasing | Purchasing Currency | Currency for PO and invoices |
| Purchasing | Payment Terms | Net 30, 2/10 Net 30, etc. |
| Purchasing | Incoterms | EXW, FOB, DDP, CIF, etc. |
| Purchasing | GR-Based IV | Invoices only processable after GR |
| Purchasing | ERS Indicator | Enable Evaluated Receipt Settlement |
| Purchasing | ABC Indicator | Vendor classification for reporting |

---

### Purchasing Info Record (PIR)

The **Purchasing Info Record** links a specific material to a specific vendor and stores pricing and delivery conditions for that combination.

```
Material: Steel Sheets (MAT-001)
    +
Vendor: Acme Steel Inc. (V-10045)
    =
Info Record:
    ├── Net Price: $145.00 / 100 kg
    ├── Minimum Order Qty: 500 kg
    ├── Planned Delivery Time: 7 days
    ├── Purchasing Group: 001
    └── Validity: 01.01.2024 – 31.12.2024
```

### PIR Types
| Type | Description |
|---|---|
| Standard | Regular external procurement |
| Subcontracting | Vendor processes materials on behalf of company |
| Consignment | Vendor holds stock on your premises |
| Pipeline | Continuous supply (utilities, gas, fluids) |

---

### Source List

The **Source List** defines which vendors are approved to supply a specific material at a specific plant. It enforces procurement compliance.

| Field | Description |
|---|---|
| Material | What material this applies to |
| Plant | Supplying to which plant |
| Vendor | Approved supplier |
| Validity Dates | Active period for this source |
| Fixed Source | If checked, MRP always uses this vendor |
| Blocked | Vendor blocked for this material/plant |

> 💡 **Best Practice:** Enable "Source List Required" on the material master to prevent buyers from ordering from unapproved vendors.

---

### Quota Arrangement

Used to split procurement volume across multiple approved vendors by percentage.

```
Material: Packaging Cardboard — Plant: 1000

┌─────────────────┬────────┬──────────────────────────┐
│ Vendor          │ Quota% │ Rationale                 │
├─────────────────┼────────┼──────────────────────────┤
│ PackRight Co.   │  60%   │ Primary — best price      │
│ BoxWorld Inc.   │  30%   │ Secondary — backup supply │
│ EcoPack Ltd.    │  10%   │ Tertiary — sustainability │
└─────────────────┴────────┴──────────────────────────┘
```

MRP automatically distributes planned requirements across vendors according to quota.

---

## Document Configuration

### PO Document Types

| Type | Code | Description |
|---|---|---|
| Standard PO | `NB` | Default — external procurement |
| Framework Order | `FO` | Blanket order, open qty/value |
| Stock Transport Order | `UB` | Inter-plant / inter-company |
| Custom Type | `ZNB` | Client-specific document type |

### Number Ranges
Each document type has a **number range** that determines how document numbers are assigned:

| Method | Description |
|---|---|
| Internal | SAP assigns the next sequential number |
| External | User enters the number manually |

### Tolerance Keys
Configured per company code to control invoice verification behavior:

| Key | Type | Typical Setting |
|---|---|---|
| `PP` | Price variance % | ±2% |
| `BD` | Small differences (absolute) | ±$1.00 |
| `QU` | Quantity variance % | ±5% |

### Account Determination
SAP automatically determines G/L accounts for procurement postings based on:
- **Valuation Class** (from material master)
- **Movement Type** (GR, reversal, etc.)
- **Transaction Key** (BSX, WRX, PRD, etc.)

| Transaction Key | Description |
|---|---|
| `BSX` | Inventory posting |
| `WRX` | GR/IR clearing account |
| `PRD` | Price difference account |
| `GBB` | Offsetting entry for GI (goods issue) |

---

> ← [Contract Management](Contract-Management) | Next: [Flexible Workflows & Approvals](Flexible-Workflows-and-Approvals) →
