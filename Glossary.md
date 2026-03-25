# 📖 Glossary

> **Wiki Navigation:** [Home](Home) › Glossary

---

## A–Z Reference of SAP Sourcing & Procurement Terms

This glossary covers all key terms, acronyms, and concepts used across this portfolio. Click any linked term to jump to the relevant wiki page.

---

## A

**Account Assignment Category**
A one-character code that determines which cost object is charged when a purchase is made. Common categories: `K` (Cost Centre), `A` (Asset), `P` (WBS/Project), `C` (Sales Order). See [System Configuration](System-Configuration).

**AP (Accounts Payable)**
The finance function responsible for paying vendor invoices. Procurement feeds AP through invoice verification posting.

**Ariba Network**
SAP's cloud-based supplier collaboration network. Used for PO transmission, supplier invoicing, catalog punchout, and bid submission. See [Integration & Analytics](Integration-and-Analytics).

**ASN (Advanced Shipping Notification)**
A supplier-sent notification indicating that goods have been shipped, including shipment details and expected arrival. Sent via SAP Business Network.

**Auction**
A competitive bidding event in SAP. Types include Reverse (Dutch), Forward (English), Japanese, and Ranked. Most common in procurement: Reverse Auction. See [Strategic Sourcing](Strategic-Sourcing).

**Award Decision**
The formal selection of a supplier following an RFx event. Can be full award, partial award, or split across multiple suppliers.

---

## B

**Bid**
A supplier's response to an RFx event, including prices, terms, and questionnaire answers.

**Blocked Invoice**
An invoice that has been posted in SAP but has a payment block set — either automatically (tolerance exceeded) or manually. See [Invoice Verification](Invoice-Verification).

**BP (Business Partner)**
The unified master data record in SAP S/4HANA that represents vendors, customers, and other partners. Replaces separate vendor/customer master records from older SAP versions.

**BSX (Transaction Key)**
SAP internal key for inventory account postings. Used in account determination to map GR events to inventory G/L accounts.

---

## C

**Call-Off**
Informal term for a **Release Order** — a PO issued against an existing contract or scheduling agreement to draw down committed volume.

**Chart of Accounts**
The structured list of G/L accounts assigned to a company code. Defines the account numbers and descriptions used in financial postings.

**Client**
The highest organizational level in SAP — the entire system instance. All company codes exist within a client.

**Company Code**
An independent legal entity within SAP with its own balance sheet and P&L. Example: `CA01` = Canada Ltd.

**Condition Record**
A stored pricing condition (discount, surcharge, freight, tax) that is automatically applied when a PO or contract is created.

**Contract**
A long-term agreement with a vendor for goods or services at agreed terms. Types: Quantity Contract (`MK`), Value Contract (`WK`). See [Contract Management](Contract-Management).

**Credit Memo**
A document issued to reduce a previously posted invoice — either initiated by the vendor (supplier credit) or buyer (returns processing).

---

## D

**Delegation**
The assignment of approval authority to a substitute during an approver's absence. Set up via substitution rules in SAP Fiori.

**Document Type**
A configuration object that categorizes SAP documents (e.g., `NB` = Standard PO, `WK` = Value Contract) and controls number ranges, partner functions, and field behaviors.

---

## E

**EDI (Electronic Data Interchange)**
A structured digital format for exchanging business documents between systems (e.g., POs, invoices). Alternative to Ariba Network for supplier integration.

**Escalation**
An automatic action triggered when an approval task is not actioned within a set deadline — forwards the task to the next level approver.

**ERS (Evaluated Receipt Settlement)**
An automated invoicing mechanism where SAP generates the vendor invoice automatically upon Goods Receipt, eliminating the need for a vendor-submitted invoice. See [Invoice Verification](Invoice-Verification).

---

## F

**Fiori**
SAP's modern UX framework. All SAP S/4HANA transactions are accessed via Fiori apps in a browser — no SAP GUI required. See [Fiori Apps Reference](Fiori-Apps-Reference).

**Fixed Source**
A source list entry where a specific vendor is the mandatory source of supply for a material. MRP will always assign PRs to this vendor.

**Flexible Workflow**
SAP S/4HANA's built-in, rule-based approval engine. Replaces classical release strategies. See [Flexible Workflows & Approvals](Flexible-Workflows-and-Approvals).

**FO (Framework Order)**
A Purchase Order document type used for blanket orders — a pre-approved open value/quantity order for recurring purchases.

---

## G

**GR (Goods Receipt)**
The SAP posting that records the physical arrival of goods against a Purchase Order. Updates inventory and triggers the GR/IR accounting entry. See [Operational Procurement](Operational-Procurement).

**GR/IR Clearing Account**
A balance sheet control account that sits between inventory and accounts payable. Debited on GR, credited on invoice posting. Should reconcile to zero. See [Integration & Analytics](Integration-and-Analytics).

**GR-Based IV (Invoice Verification)**
A vendor master setting that prevents invoice posting until a matching Goods Receipt has been posted. Ensures 3-way match is enforced.

---

## I

**Incoterms**
International Commercial Terms — standardized delivery terms defining who bears cost and risk at each stage of transport. Examples: EXW (Ex-Works), FOB (Free on Board), DDP (Delivered Duty Paid), CIF (Cost, Insurance & Freight).

**Info Record (Purchasing Info Record / PIR)**
A master data object that stores the commercial relationship between a material and a vendor — including price, delivery time, and conditions. See [System Configuration](System-Configuration).

**Invoice Verification**
The SAP process of validating and posting a vendor invoice against PO and GR data. Performed in MIRO or Fiori App `F1068`. See [Invoice Verification](Invoice-Verification).

---

## L

**LIV (Logistics Invoice Verification)**
The SAP module and process for verifying vendor invoices — synonym for Invoice Verification in the MM context.

**Lot**
A grouping of items within an RFx or auction. Suppliers can bid on individual lots or the full package.

**LP / LPA (Scheduling Agreement Types)**
Document types for scheduling agreements. `LP` = standard; `LPA` = with release documentation (JIT).

---

## M

**Maverick Buying**
Procurement spend that bypasses approved contracts, vendors, or processes. High maverick buying rates indicate poor procurement compliance.

**MIRO**
The legacy SAP transaction code for Logistics Invoice Verification. Equivalent to Fiori App `F1068` in S/4HANA.

**Movement Type**
A 3-digit code that controls how an inventory transaction is processed. Key types: `101` (GR for PO), `122` (Return to Vendor), `201` (GI to Cost Centre).

**MRP (Material Requirements Planning)**
An SAP planning function that calculates material requirements based on demand and generates Purchase Requisitions automatically.

---

## N

**NB (Normalbestellung)**
The standard Purchase Order document type in SAP. `NB` is the default for external procurement.

**Net Price**
The base vendor price per unit, before any additional conditions (taxes, freight, discounts) are applied.

**Number Range**
A configuration object that controls how document numbers are assigned — either internally (system-assigned) or externally (user-entered).

---

## O

**Outline Agreement**
SAP's collective term for long-term vendor agreements, including Contracts (quantity and value) and Scheduling Agreements.

**Overdelivery Tolerance**
A configurable PO field that controls how much more than the ordered quantity can be received. Example: 10% overdelivery allowed.

---

## P

**Parked Invoice**
An invoice saved in SAP but not yet posted — used when information is incomplete. A parked invoice has no accounting impact until it is posted.

**Payment Terms**
Agreed conditions for when and how an invoice will be paid. Example: `Net 30` = full payment within 30 days. `2/10 Net 30` = 2% discount if paid within 10 days, otherwise full amount due in 30.

**PIR (Purchasing Info Record)**
See *Info Record*.

**Plant**
An operational unit in SAP — can represent a factory, warehouse, retail location, or office. Procurement and inventory are managed at plant level.

**PO (Purchase Order)**
A legally binding procurement document sent to a vendor to order goods or services at agreed prices and terms. See [Operational Procurement](Operational-Procurement).

**PR (Purchase Requisition)**
An internal SAP document requesting the purchase of goods or services. Not sent to vendors — triggers the purchasing process internally. See [Operational Procurement](Operational-Procurement).

**PRD (Transaction Key)**
SAP internal key for price difference postings — used when invoice price differs from PO price and the variance exceeds tolerance.

**Purchasing Group**
A buyer or buyer team responsible for processing day-to-day purchasing documents. Assigned to POs, PRs, and info records.

**Purchasing Organization**
The SAP organizational unit responsible for negotiating contracts and prices with vendors. Can serve one or multiple plants/company codes.

---

## Q

**Quota Arrangement**
A master data object that splits procurement volume for a material across multiple approved vendors by percentage. See [System Configuration](System-Configuration).

---

## R

**Release Order**
A Purchase Order issued against an existing contract or scheduling agreement that draws down the committed value or quantity. Also called a call-off.

**Release Strategy**
The classical SAP approval mechanism (used in ECC). Replaced by Flexible Workflow in S/4HANA Public Cloud.

**RFI (Request for Information)**
A sourcing document used for market research — assessing supplier capabilities without requesting firm pricing or commitment.

**RFP (Request for Proposal)**
A sourcing document requesting a proposed solution with pricing. Used for complex categories with qualitative evaluation requirements.

**RFQ (Request for Quotation)**
A sourcing document requesting firm pricing from suppliers. Used for commodity items where price is the primary evaluation criterion.

**RFx**
Generic umbrella term covering RFI, RFP, and RFQ events. See [Strategic Sourcing](Strategic-Sourcing).

---

## S

**SAC (SAP Analytics Cloud)**
SAP's cloud-based analytics platform for advanced dashboards, planning, and predictive analytics. Connects to S/4HANA for procurement reporting.

**Scheduling Agreement**
A long-term vendor agreement with planned delivery dates and quantities. Used in manufacturing environments with regular, predictable supply needs. See [Contract Management](Contract-Management).

**SES (Service Entry Sheet)**
The SAP document that confirms services have been performed against a service PO. Equivalent to a Goods Receipt for service line items.

**Source List**
A master data object listing approved vendors for a material at a specific plant. Enforces procurement compliance. See [System Configuration](System-Configuration).

**Sourcing Project**
The organizational container in SAP for managing a complete sourcing initiative — from RFx creation through to contract award. See [Strategic Sourcing](Strategic-Sourcing).

**SSP (Self-Service Procurement)**
A procurement model where non-buyers can request goods/services via a shopping cart interface. See [Operational Procurement](Operational-Procurement).

**STO (Stock Transport Order)**
An inter-plant or inter-company purchase order (`UB` document type) used to move stock between locations.

---

## T

**3-Way Match**
The process of verifying that a vendor invoice aligns with the corresponding Purchase Order and Goods Receipt. See [Invoice Verification](Invoice-Verification).

**Tolerance**
A configured threshold defining acceptable variance between PO and invoice values. If exceeded, invoices are automatically blocked.

**Transaction Key**
An SAP-internal code (e.g., BSX, WRX, PRD) used in automatic account determination to map procurement events to G/L accounts.

---

## U

**UB (Umlagerungsbestellung)**
The SAP document type for Stock Transport Orders — used for inter-plant stock movements.

---

## V

**Valuation Class**
A field on the material master that links a material to a group of G/L accounts for automatic posting. Different material types use different valuation classes.

**Value Contract**
An outline agreement committing to spend a total dollar value with a vendor over a validity period (doc type `WK`).

**Vendor Account**
The accounts payable sub-ledger account for a specific vendor. Credits are posted here when invoices are verified; debits when payments are made.

---

## W

**WBS Element (Work Breakdown Structure)**
A project hierarchy element used as a cost object in account assignment (`P`). Links procurement costs to specific project activities.

**WK (Wertkontrakt)**
SAP document type code for a Value Contract.

**WRX (Transaction Key)**
SAP internal key for GR/IR clearing account postings. Used in automatic account determination.

---

## Z

**Z-Objects**
SAP naming convention for customer-created / custom configuration objects. For example, `ZNB` = custom standard PO type; `Z001` = custom number range. In SAP S/4HANA Public Cloud, custom Z-objects are limited due to the clean-core principle.

---

> ← [Fiori Apps Reference](Fiori-Apps-Reference) | [Back to Home](Home) →
