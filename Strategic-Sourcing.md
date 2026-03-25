# 🎯 Strategic Sourcing

> **Wiki Navigation:** [Home](Home) › Strategic Sourcing

---

## Overview

Strategic Sourcing in SAP S/4HANA Public Cloud covers the end-to-end process of identifying, evaluating, and awarding business to suppliers — from initial spend analysis through to contract creation. It replaces manual, email-based tendering with a structured, auditable digital process.

---

## Source-to-Contract (S2C) Process Flow

```
Spend Analysis & Category Strategy
          │
          ▼
  Sourcing Project Creation
  (Define scope, team members, milestones)
          │
          ▼
  RFx Event Creation
  (RFI → RFP → RFQ)
          │
          ▼
  Supplier Invitation & Portal Access
  (SAP Business Network / Supplier Portal)
          │
          ▼
  RFx Publication & Q&A Period
          │
          ▼
  Supplier Bid Submission
          │
          ▼
  Bid Comparison & Evaluation
  (Price + Technical + Compliance scoring)
          │
          ▼
  Negotiation Rounds / Reverse Auction
          │
          ▼
  Award Decision
  (Full, partial, or split across suppliers)
          │
          ▼
  Contract Auto-Creation
          │
          ▼
  Contract Release Orders (Call-offs)
```

---

## Sourcing Projects

A **Sourcing Project** is the master container that organizes all activities for a sourcing initiative.

### Project Types
| Type | Use Case |
|---|---|
| New Sourcing | First-time procurement of a category |
| Re-Sourcing | Existing category going back to market |
| Spot Buy | One-time purchase outside standard contracts |
| Benchmark | Market pricing check, no award intended |

### Project Setup Elements
- **Project name, type, and description**
- **Category / Material Group** being sourced
- **Team assignment** — Lead Buyer, approver, observers, legal
- **Milestones** — RFx open date, close date, award date
- **Linked RFx events** — one project can contain multiple RFx rounds

---

## RFx Management

### RFx Types Compared

| Type | Full Name | Purpose | Evaluation Basis |
|---|---|---|---|
| **RFI** | Request for Information | Market research, capability check | Qualitative only |
| **RFP** | Request for Proposal | Solution + pricing, complex categories | Weighted scoring |
| **RFQ** | Request for Quotation | Price-focused, commodity items | Price comparison |

### RFx Lifecycle

| Step | Action | Responsible |
|---|---|---|
| 1 | Create RFx with items, questions, T&Cs, attachments | Buyer |
| 2 | Select suppliers from master data or invite externally | Buyer |
| 3 | Set submission deadline and rules (sealed bids, etc.) | Buyer |
| 4 | Publish event — suppliers notified automatically | System |
| 5 | Q&A open period — buyers answer supplier questions | Buyer |
| 6 | Supplier bids submitted via SAP Business Network portal | Supplier |
| 7 | Bid opening — all bids visible after deadline | Buyer |
| 8 | Side-by-side comparison across suppliers | Buyer |
| 9 | Negotiation rounds initiated if needed | Buyer |
| 10 | Award decision made — award letters sent | Buyer |
| 11 | Contract / PO created from award | System / Buyer |

### Key RFx Configuration Elements
- **Questionnaires** — Technical, commercial, sustainability questions
- **Bid validity period** — How long supplier bids remain valid after award
- **Currency** — Bids can be submitted in supplier's currency, converted for comparison
- **Lot structure** — RFx can be organized by lots (groups of line items)
- **Weighted criteria** — Each evaluation criterion assigned a weight percentage

---

## Auction Management

SAP S/4HANA supports live competitive bidding events (auctions) as part of the sourcing process.

### Auction Types

| Auction Type | Mechanism | Common Use |
|---|---|---|
| **Reverse Auction (Dutch)** | Suppliers lower prices in real time | Commodity procurement — most common in purchasing |
| **Forward Auction (English)** | Prices rise — used for selling | Asset disposal, not procurement |
| **Japanese Auction** | All-or-nothing rounds; suppliers drop out each round | Strategic categories with few qualified suppliers |
| **Ranked Auction** | Suppliers see their rank but not competitor prices | Sensitive categories requiring partial confidentiality |

### Reverse Auction Flow
```
Auction Created (linked to RFx or standalone)
          │
          ▼
  Auction Rules Set
  (Reserve price, bid decrement, overtime rules)
          │
          ▼
  Suppliers Invited & Trained
          │
          ▼
  Live Auction Event
  ├── Real-time bid leaderboard
  ├── Countdown timer
  ├── Automatic overtime extension if bid placed near deadline
          │
          ▼
  Auction Closes → Best Bid Identified
          │
          ▼
  Award / Negotiation
```

---

## Supplier Evaluation & Scoring

After bid collection, buyers evaluate suppliers using a weighted scorecard.

### Scoring Formula

```
Total Score = Σ (Criterion Weight % × Supplier Score out of 100)

Example Evaluation:
┌─────────────────┬────────┬──────────┬───────┐
│ Criterion       │ Weight │ Score    │ Total │
├─────────────────┼────────┼──────────┼───────┤
│ Price           │ 40%    │ 85 / 100 │ 34.0  │
│ Quality         │ 25%    │ 90 / 100 │ 22.5  │
│ Delivery        │ 20%    │ 78 / 100 │ 15.6  │
│ Sustainability  │ 10%    │ 70 / 100 │  7.0  │
│ Innovation      │  5%    │ 65 / 100 │  3.25 │
├─────────────────┼────────┼──────────┼───────┤
│ TOTAL           │ 100%   │          │ 82.35 │
└─────────────────┴────────┴──────────┴───────┘
```

### Award Options
- **Full Award** — 100% to one supplier
- **Partial Award** — Percentage split across suppliers
- **Split Award by Lot** — Different suppliers win different lots
- **No Award** — RFx cancelled; resourcing initiated

---

## Supplier Collaboration

SAP S/4HANA Public Cloud integrates with the **SAP Business Network** (formerly Ariba Network) for supplier-facing interactions:

| Feature | Description |
|---|---|
| Supplier Portal | Suppliers register, view RFx events, submit bids |
| Q&A Messaging | Buyer-supplier questions visible to all (or private) |
| Bid Revision | Suppliers can revise bids before deadline |
| Award Notification | System automatically sends award/rejection letters |
| Document Sharing | NDA, T&Cs, specifications shared securely |

---

## Key Business Rules & Best Practices

- Always use a **Sourcing Project** to maintain audit trail and stakeholder visibility
- Set **bid validity periods** to protect against price withdrawals after award
- Use **RFI before RFP** for new categories to qualify the market first
- Configure **evaluation criteria** before publishing — changing criteria after publication reduces fairness
- Enable **sealed bidding** for high-value tenders to prevent collusion
- Document **award rationale** in the system for compliance and audit purposes

---

> ← [Project Overview](Project-Overview) | Next: [Operational Procurement](Operational-Procurement) →
