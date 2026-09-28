# Product Requirements Document: Import, Inventory & Distribution Platform

| Field        | Value                                          |
|--------------|------------------------------------------------|
| Status       | Draft v0.4                                     |
| Last updated | 2026-09-28                                     |
| Owner        | sennuramamoorthy                               |
| Scope        | MVP (Release 1)                                |
| Market       | Importers selling in the United States and Canada |

---

## 1. Summary

A cloud application (SaaS) for **businesses that import products from India
and other countries and sell them in the United States and Canada** through a
network of regional distributors.

It covers the whole path of a product:

```
Overseas supplier ──► Import (PO, shipment, customs, landed cost)
   ──► Receiving into a warehouse (batch / lot, expiry)
   ──► Inventory across many locations (company warehouses + distributors)
   ──► Customer order ──► routed to the location that serves the customer's region
       and holds the stock ──► shipped from that location's inventory ──► invoiced
```

Four groups of people use it:

1. **Owners & executives** run the business. They manage imports from overseas
   suppliers, see stock and money across every location, and approve key
   decisions.
2. **Operations / warehouse staff** receive imported goods, record batches and
   expiry dates, move stock between locations and keep counts accurate.
3. **Sales** handle customers, quotes, orders and invoices.
4. **Distributors** in regions across the US and Canada hold stock in their
   area, fulfil the orders routed to them from their own inventory, and see
   only their own location, stock and orders.

Each business that signs up gets its own isolated account (tenant).

## 2. Problem Statement

- **Imports are tracked in email and spreadsheets.** Purchase orders, shipping
  documents, customs paperwork and ETAs are scattered. The true **landed cost**
  per unit (product + freight + duty + fees) is rarely known, so pricing and
  margins are guesses.
- **Stock is spread across many places**, from company warehouses to
  distributors' premises in different states and provinces. Nobody knows
  exactly how much of each product is where.
- **Batches and expiry dates aren't tracked**, especially for food. Stock
  expires on shelves, the wrong batch ships first, and a supplier recall can't
  be traced to the customers who received the affected batch.
- **Order fulfilment is decided by phone.** Someone has to work out which
  distributor is closest to the customer and actually has the product, then
  chase them to ship it.
- **Executives can't see the whole picture:** goods on the water, stock value
  by location, stock about to expire, sales by region, and which distributor
  is performing.

## 3. Goals & Non-Goals

### 3.1 Goals (MVP)
1. **G1: Import visibility and landed cost.** Every purchase order and
   shipment from overseas is tracked from order to warehouse, with documents,
   ETAs and a calculated landed cost per unit.
2. **G2: Accurate multi-location inventory.** Real-time stock by product,
   location and **batch**, with expiry dates, for company warehouses and
   distributor locations.
3. **G3: Nothing expires unnoticed; everything is traceable.** Stock is
   allocated first-expiry-first-out (FEFO), expiry alerts go out in advance,
   and any batch can be traced from supplier to customer in one click.
4. **G4: Orders fulfilled from the right place.** Each order is routed
   automatically to the location that serves the customer's region and has the
   stock, and staff can override the choice.
5. **G5: Distributors run their part.** Distributors receive stock transfers,
   fulfil routed orders from their inventory and report counts in their own
   portal, seeing only their own data.
6. **G6: One view for executives.** Dashboards for imports in transit,
   inventory value and expiry risk, sales by region, and distributor
   performance.
7. **G7: Quote to cash.** Customers, quotes, orders and invoices in USD and
   CAD, linked to the stock that fulfils them.

### 3.2 Non-Goals (MVP)
- Filing customs entries directly with US CBP or the CBSA, or FDA prior
  notice. The app stores filing references, documents and deadlines; a
  customs broker files them.
- Live tracking feeds from shipping lines or carriers (entered manually in the
  MVP; see Phase 2).
- Carrier rate shopping and shipping-label purchase.
- Full accounting (general ledger). The MVP provides inventory valuation and
  exports for the accountant.
- Online payment collection and automatic sales-tax calculation.
- Warehouse robotics features: bin/slot optimization, wave picking,
  handheld-scanner apps (browser barcode scanning is P1).
- A customer self-service portal or e-commerce storefront.
- Generating compliant food labels (the data is stored; label compliance is the
  business's responsibility).

## 4. Users, Roles & Access

### 4.1 User groups

| Group | Who they are | What they come to do |
|-------|--------------|----------------------|
| **Owner / Executive** | Business owner, directors, finance lead. | Manage overseas suppliers and imports; see stock, sales and money across all locations; approve purchase orders, large adjustments and discounts; manage settings. |
| **Operations / Warehouse** | Staff at the company's own warehouses (or a 3PL's staff given access). | Receive shipments, record batches and expiry dates, put stock on hold, transfer stock to distributors, pick and ship orders from their warehouse, run stock counts. |
| **Sales** | Sales reps and account managers. | Manage customers, create quotes and orders, check stock availability, follow up on invoices. |
| **Distributor** | Staff of an independent distributor responsible for a region of the US or Canada. | Receive stock transferred to them, fulfil orders routed to their location from their own stock, report stock counts and damages, see their performance. |

Permissions that can be added to internal users:
- **Administrator**: settings, users, locations, territories, distributors.
- **Import manager**: create and manage purchase orders, shipments and landed
  cost. Executives have it by default; it can be given to operations staff.
- **Approver**: approve purchase orders, inventory adjustments and quotes above
  set limits.

### 4.2 Personas

| Persona | Description | Key needs |
|---------|-------------|-----------|
| **Raj, Owner** | Imports spices, snacks and small appliances from India; sells to grocery stores and retailers in the US and Canada. | Know what's on the water and when it lands; the true landed cost per unit; stock and expiry risk at every location; which regions and distributors perform. |
| **Maria, Warehouse lead (New Jersey)** | Runs the main warehouse where containers arrive. | Receive a container quickly against its packing list; record batch and expiry for each line; send stock to distributors; know what to pick. |
| **Kevin, Sales rep** | Manages 80 retail accounts. | See available stock (and its expiry) before quoting; know which location will ship the order and when it ships. |
| **Dana, Distributor (Texas)** | Covers Texas, Oklahoma and Louisiana from her own storage facility. | See the orders she must ship today; pick the right batch; confirm stock transfers she received; report damaged or expired stock. |
| **Luc, Distributor (Ontario)** | Covers Ontario and Quebec. | Same as Dana, with Canadian addresses, CAD and bilingual product details. |

### 4.3 Permission matrix

✅ full · 👁 view · ✍ own location / own records only · — none

| Capability | Owner / Exec | Operations | Sales | Distributor |
|------------|:-----------:|:----------:|:-----:|:-----------:|
| Executive dashboards | ✅ | 👁 inventory only | 👁 own + team totals | — |
| Overseas suppliers | ✅ | 👁 | — | — |
| Purchase orders & import shipments | ✅ | 👁 (✅ with Import manager) | 👁 ETA only | — |
| Purchase cost & landed cost | ✅ | 👁 with Import manager | — | — |
| Receive shipments into a warehouse | ✅ | ✅ | — | — |
| Inventory, all locations | ✅ | ✅ | 👁 available qty & expiry | — |
| Inventory at own location | ✅ | ✅ | 👁 | ✍ view batches & expiry |
| Stock transfers | ✅ create/approve | ✅ create, ship, receive | — | ✍ receive inbound, request stock |
| Inventory adjustments (damage, expiry, count) | ✅ approve | ✍ create | — | ✍ request (needs approval) |
| Batch hold / recall | ✅ | ✅ place hold | 👁 | 👁 holds on own stock |
| Product catalog | ✅ | 👁 | 👁 | 👁 products they stock |
| Selling price | ✅ | — | ✅ | — |
| Customers & CRM | ✅ | 👁 ship-to only | ✅ | — |
| Quotes | ✅ | — | ✍ own | — |
| Sales orders | ✅ | 👁 | ✍ own, 👁 all | — |
| Routing override (change fulfilling location) | ✅ | ✅ | — (requests) | — |
| Fulfilment orders | ✅ | ✍ own warehouse | 👁 | ✍ own location |
| Invoices & payments | ✅ | — | ✍ own | — |
| Users, locations, territories, settings | ✅ (Administrator) | — | — | Distributor admin: own users (P1) |
| Audit log | ✅ | — | — | — |

### 4.4 What a distributor sees

| Visible | Never visible |
|---------|---------------|
| Its own location's stock by product and batch: quantity, expiry, status (available / reserved / on hold) | Other locations' stock, other distributors |
| Inbound stock transfers to its location | Purchase orders, suppliers, purchase cost, landed cost |
| Fulfilment orders routed to it: products, quantities, suggested batches, ship-to name and address, delivery notes, ship-by date | Selling prices, order totals, invoices, customer email/phone/account details, quotes, deals |
| Its product catalog: details, specs, ingredients, allergens, handling and storage instructions | Margins and sales figures of the business as a whole |
| Its own dashboard: orders shipped, on-time rate, stock on hand, stock near expiry | Internal notes |

## 5. Core Workflows

### 5.1 Import to stock
```
Supplier (India) ──► Purchase Order (Exec / Import manager)
   ──► Supplier confirms, proforma invoice, advance payment recorded
   ──► Import Shipment created (one or more POs, sea or air)
         Booked → Departed (ETD) → In transit → Arrived at port (ETA)
         → Customs: entry filed → Held / Cleared → Delivered to warehouse
         Documents attached at each step (commercial invoice, packing list,
         bill of lading, certificate of origin, FDA / CFIA documents, customs entry)
   ──► Receiving at warehouse (Operations)
         count each line against the packing list → record batch / lot,
         manufacturing date, expiry date, condition → discrepancies flagged
   ──► Landed cost finalized: freight, insurance, duty, broker and trucking
       fees allocated to each received batch → cost per unit
   ──► Stock available (or on QC hold until released)
```

### 5.2 Distributing stock to regions
```
Warehouse ──► Stock Transfer (batches chosen FEFO) ──► In transit
   ──► Distributor confirms receipt (quantities per batch; shortages or damages flagged)
   ──► Stock available at the distributor's location
Distributor can request stock (replenishment request); Ops / Exec approves and creates the transfer.
```

### 5.3 Order routing and fulfilment
```
Sales Order confirmed (customer ship-to address)
   ──► Routing engine suggests the fulfilling location(s):
        1. Locations whose territory covers the ship-to region (state / province / ZIP / postal code)
        2. …that have enough AVAILABLE stock in batches meeting the minimum
           remaining shelf life
        3. Ranked by: same country first → nearest distance → location priority
        4. If no single location can ship everything:
           split across locations, OR fall back to the main warehouse, OR backorder
           (per the business's routing settings)
   ──► Stock reserved by batch (FEFO) ──► Fulfilment Order sent to the location
   ──► Location picks (confirms or swaps batch, with a reason) → packs → ships
       (carrier + tracking) → stock deducted
   ──► Customer invoiced ──► payment recorded
Ops / Exec can override the suggested location before the location starts picking.
```

### 5.4 Recall
```
Supplier or regulator reports a problem with a batch
   ──► Exec / Ops puts the batch ON HOLD everywhere (can't be allocated or shipped)
   ──► Traceability report: where the batch is now (per location) and which
       customers received it (orders, quantities, dates, addresses)
   ──► Distributors are notified to quarantine their stock
   ──► Stock returned or written off; recall closed with notes
```

## 6. Functional Requirements

Priority: **P0** = must have for MVP, **P1** = should have, **P2** = nice to have.

### 6.1 Accounts, Users & Access
| ID | Requirement | Priority |
|----|-------------|----------|
| ACC-1 | A business signs up and creates its tenant account (company name, home country US or Canada, base currency USD or CAD, timezone). Each tenant's data is fully isolated. | P0 |
| ACC-2 | Email + password sign-in with email verification and password reset; Google sign-in for internal users (P1). | P0 |
| ACC-3 | Two-factor authentication, required for Owners/Executives and Administrators. | P1 |
| USR-1 | Administrators invite internal users with a group (Executive, Operations, Sales) and optional permissions (Administrator, Import manager, Approver). Operations users are assigned to one or more warehouses. | P0 |
| USR-2 | Administrators create **distributors** (legal name, contact, address, country) with one or more **locations**, and invite distributor users. | P0 |
| USR-3 | Distributor users use a separate **Distributor Portal** and can reach only their own locations' data, including through the API. | P0 |
| USR-4 | Deactivating a user or distributor signs them out right away; records remain. | P0 |
| USR-5 | Distributor admins manage their own company's users. | P1 |

### 6.2 Overseas Suppliers
| ID | Requirement | Priority |
|----|-------------|----------|
| SUP-1 | Supplier record: legal name, country, address, contacts, currency (e.g., INR, USD), payment terms, default Incoterm, bank details (visible to Executives only), notes. | P0 |
| SUP-2 | Compliance fields: exporter codes (e.g., India IEC), FSSAI licence, FDA food facility registration number, certifications (ISO, HACCP, organic…) with **expiry dates and reminders**. | P0 |
| SUP-3 | Supplier documents (licences, certificates, contracts) with expiry dates. | P0 |
| SUP-4 | Products supplied by a supplier with their supplier SKU and last purchase price. | P0 |
| SUP-5 | Supplier performance: on-time shipment rate, receiving discrepancy rate, quality holds. | P1 |

### 6.3 Import Management

#### Purchase orders
| ID | Requirement | Priority |
|----|-------------|----------|
| PO-1 | Create a purchase order: supplier, currency, exchange rate (rate on the PO date, editable), Incoterm (EXW, FOB, CFR, CIF, DDP…), port of loading, destination (country and warehouse), requested ship date, payment terms, notes. | P0 |
| PO-2 | Lines: product, quantity in purchase units (e.g., cartons) with the conversion to selling units, unit cost in supplier currency, line total; totals in supplier currency and the base currency. | P0 |
| PO-3 | Statuses: Draft → Pending approval → Approved → Sent → Confirmed by supplier → Partially shipped → Shipped → Received / Closed / Cancelled. | P0 |
| PO-4 | Approval required above a set value (Approver or Executive). | P0 |
| PO-5 | PO PDF to email to the supplier. | P0 |
| PO-6 | Record supplier payments manually (advance, balance) with date, amount, currency, exchange rate and reference; shows the balance owed. | P0 |
| PO-7 | Supplier documents per PO: proforma invoice, final commercial invoice. | P0 |
| PO-8 | Suggested purchase quantities based on stock on hand, stock in transit, sales velocity and lead time. | P2 |

#### Import shipments
| ID | Requirement | Priority |
|----|-------------|----------|
| SHP-1 | Create an import shipment containing lines from one or more POs (and a PO can be split over several shipments). | P0 |
| SHP-2 | Fields: mode (sea FCL, sea LCL, air, courier), carrier / shipping line, forwarder, customs broker, container number(s) and type, bill of lading or air waybill number, vessel/voyage or flight, port of loading, port of discharge, final destination warehouse, ETD, ETA, actual dates. | P0 |
| SHP-3 | Statuses with a timeline: Booked → Departed → In transit → Arrived at port → Customs entry filed → Customs hold / Cleared → Out for delivery → Delivered to warehouse → Received. Each change is dated, and users can add notes. | P0 |
| SHP-4 | **Customs and regulatory** (country-aware): for the US, ISF (10+2) filing reference and deadline (24 hours before loading for ocean), FDA Prior Notice confirmation number for food, CBP entry number and date, duties paid. For Canada, CBSA transaction number, CFIA/SFCR licence reference, duties and GST paid at import. | P0 |
| SHP-5 | Documents per shipment: commercial invoice, packing list, bill of lading/AWB, certificate of origin, phytosanitary or health certificates, lab/test reports, customs entry summary, delivery order, and others. | P0 |
| SHP-6 | Reminders for approaching deadlines (ISF filing, arrival, free days at port before demurrage) and alerts when an ETA changes. | P0 |
| SHP-7 | HS / HTS tariff code per product per destination country, with a duty rate used to estimate duty before the actual customs entry. | P0 |
| SHP-8 | Tracking link-out to the carrier's website using the container or AWB number. | P1 |
| SHP-9 | Automatic tracking updates from a container-tracking provider. | P2 |

#### Landed cost
| ID | Requirement | Priority |
|----|-------------|----------|
| LC-1 | Add cost lines to a shipment: ocean/air freight, insurance, customs duty, customs broker fees, port and terminal charges, trucking (drayage), inspection fees, demurrage, other. Each has an amount, currency, exchange rate and vendor. Duty can be entered per product line. | P0 |
| LC-2 | Allocate shared costs to shipment lines by **value, weight, volume or quantity** (chosen per cost line). | P0 |
| LC-3 | Calculate **landed cost per unit** for each received batch = product cost (converted to base currency) + allocated costs. | P0 |
| LC-4 | Costs can be estimated before arrival and finalized later. When final costs differ, the batch cost is updated and the change is recorded. | P0 |
| LC-5 | Landed cost report per shipment and per product over time; margin = selling price − landed cost (internal users with cost permission only). | P0 |

### 6.4 Receiving
| ID | Requirement | Priority |
|----|-------------|----------|
| RCV-1 | Receive a shipment (or a transfer) at a location: for each line, received quantity, **batch / lot number**, supplier's batch number (if different), **manufacturing date**, **expiry / best-before date**, condition (good, damaged, short). One line can be split over several batches. | P0 |
| RCV-2 | Batch and expiry are **required** for products marked "batch-tracked" (default for food). Expiry can be calculated from manufacturing date + shelf life. | P0 |
| RCV-3 | Differences from the packing list (shortages, overages, damage) are flagged, can have photos attached, and create a discrepancy record for the supplier or insurer. | P0 |
| RCV-4 | Received stock can go straight to **Available** or to **QC hold** (per product or per receipt) until released by an authorized user. | P0 |
| RCV-5 | Partial receipts are allowed; the shipment shows received versus expected. | P0 |
| RCV-6 | Print batch labels with barcodes (product, batch, expiry). | P1 |
| RCV-7 | Scan barcodes with a phone or tablet camera during receiving. | P1 |
| RCV-8 | Receiving a batch that expires within the minimum shelf life (e.g., under 6 months) triggers a warning. | P0 |

### 6.5 Inventory Management

#### Locations & territories
| ID | Requirement | Priority |
|----|-------------|----------|
| LOC-1 | Location types: **Company warehouse**, **3PL warehouse**, **Distributor location**. Each has a name, code, address (geocoded), country, timezone, contacts, operating status and fulfilment priority. | P0 |
| LOC-2 | **Territories**: each location serves a set of regions, defined by US states / Canadian provinces and optionally ZIP / postal code prefixes. Territories may overlap; overlaps are resolved by routing rules. | P0 |
| LOC-3 | A map view of locations and their territories, highlighting regions nobody serves. | P1 |
| LOC-4 | Optional sub-locations (zone / aisle / bin) inside warehouses. | P2 |

#### Stock, batches & expiry
| ID | Requirement | Priority |
|----|-------------|----------|
| INVT-1 | Stock is held per **product × location × batch**, with quantity in the base unit and display in cases where configured (e.g., 1 case = 24 units). | P0 |
| INVT-2 | Stock statuses: **Available**, **Reserved** (allocated to an order or transfer), **In transit**, **On hold** (QC, recall, investigation), **Damaged**, **Expired**. Only Available stock can be allocated. | P0 |
| INVT-3 | Every change is recorded as an **immutable stock movement** (receipt, transfer out/in, reservation, shipment, adjustment, return, write-off) with who, when, why and reference document. Stock on hand is always rebuildable from movements. | P0 |
| INVT-4 | Stock can never go negative. Two people can't reserve the same units at the same time. | P0 |
| INVT-5 | **FEFO**: allocation always suggests the batch that expires first, as long as it meets the order's minimum remaining shelf life. | P0 |
| INVT-6 | **Expiry alerts** at configurable thresholds (e.g., 90, 60, 30 days) per location, sent to Ops, Execs and the distributor holding the stock. Expired batches automatically become Expired and can't be allocated. | P0 |
| INVT-7 | **Minimum remaining shelf life** at dispatch: a default per product, overridable per customer (e.g., a grocery chain requires 75% of shelf life remaining). | P1 |
| INVT-8 | Inventory views: by product (all locations), by location (all products), by batch; filters for status, expiry window and low stock. Export to CSV. | P0 |
| INVT-9 | **Reorder points** per product per location; low-stock alerts; days of cover based on recent sales. | P1 |
| INVT-10 | Stock value by location and in total, at landed cost per batch. | P0 |

#### Transfers, adjustments & counts
| ID | Requirement | Priority |
|----|-------------|----------|
| TRF-1 | **Stock transfer** between any two locations (e.g., warehouse → distributor): lines with products and batches (FEFO suggested), statuses Draft → Approved → Shipped (in transit) → Received (full / partial with discrepancies) / Cancelled. Batch identity and expiry travel with the stock. | P0 |
| TRF-2 | Distributors can send a **replenishment request** for products; Ops or Execs turn it into a transfer or decline it. | P1 |
| TRF-3 | Cross-border transfers (US ↔ Canada) are flagged as exports/imports requiring customs documents. | P1 |
| ADJ-1 | **Inventory adjustments** with reason codes (damaged, expired, lost, found, count correction, sample, quality reject). Adjustments above a set quantity or value need approval. Distributors can only request adjustments. | P0 |
| ADJ-2 | **Stock counts**: count all or selected products at a location (blind count option), compare to the system and post differences as adjustments after review. Distributors can submit counts for their location. | P0 |
| ADJ-3 | **Batch hold / recall** as in §5.4: hold a batch everywhere, see all locations and customers affected, notify distributors, close with notes. | P0 |
| ADJ-4 | Customer **returns** (RMA): receive back to a batch as Available, On hold or Damaged, and link to a credit. | P1 |

### 6.6 Product Catalog
Owned by the business; distributors see the products they stock but don't
edit them.

#### Structure
| ID | Requirement | Priority |
|----|-------------|----------|
| PRD-1 | Common fields: name, SKU (unique), product type, category, brand, descriptions, status (Draft / Active / Discontinued), tags, images (P1), documents (spec sheets, safety data sheets, certificates) (P1). | P0 |
| PRD-2 | **Units**: base unit (each), purchase unit (e.g., carton of 48), selling units (e.g., case of 24), with conversions. | P0 |
| PRD-3 | **Import fields**: country of origin, default supplier(s) and supplier SKU, HS code and duty rate per destination country (US, Canada), shelf life (days), batch-tracked flag, storage requirements (ambient / chilled / frozen). | P0 |
| PRD-4 | **Pricing**: selling price per currency (USD, CAD) and per price list (P1); last landed cost and average landed cost shown to users with cost permission. | P0 |
| PRD-5 | **Barcodes**: UPC/EAN/GTIN per unit level (each, case), check-digit validated. | P1 |
| PRD-6 | **Canada fields**: French product name and description, since bilingual labeling is required for many consumer goods. | P1 |
| PT-1 | **Product types** decide the detail fields: built-in Food, Electronics, General; custom types defined by Administrators (P1). | P0 |
| CAT-1 | **Categories** as a tree up to 5 levels deep (e.g., *Food › Spices › Whole Spices*), independent of type; create, rename, reorder, move; deleting a category moves its products elsewhere. | P0 |

#### Weights & dimensions
| ID | Requirement | Priority |
|----|-------------|----------|
| DIM-1 | Net weight and dimensions of the product; gross weight and dimensions of each packaging level (case, carton, pallet: units and cases per pallet). | P0 |
| DIM-2 | Entered in imperial or metric and stored in base units (g, mm). Shown in the unit system of the user's country (US: imperial, Canada: metric). | P0 |
| DIM-3 | Carton volume (CBM) used for landed cost allocation and container planning. | P0 |

#### Electronics details
| ID | Requirement | Priority |
|----|-------------|----------|
| ELE-1 | Model number, power source, voltage (V), frequency (Hz), power (W), plug type, battery (type, capacity), connectivity, warranty, certifications (FCC, UL/ETL, CSA for Canada, Energy Star, RoHS…). | P0 |
| ELE-2 | A free-form grouped spec table (group / name / value / unit). | P0 |
| ELE-3 | Flags for regulated items (e.g., lithium batteries for shipping). | P1 |

#### Food details
| ID | Requirement | Priority |
|----|-------------|----------|
| FOOD-1 | **Ingredients**: ordered list (descending by weight) with optional percentages, plus the label's ingredients statement in English (and French for Canada, P1). | P0 |
| FOOD-2 | **Allergens**: *Contains* / *May contain* / *Free from* for the US major allergens (milk, eggs, fish, crustacean shellfish, tree nuts, peanuts, wheat, soybeans, sesame) and Canada's priority allergens (adds mustard, sulphites, molluscs and gluten sources). | P0 |
| FOOD-3 | **Nutrition facts**: US FDA format (serving size, servings per container, calories, fats, cholesterol, sodium, carbohydrate, fiber, sugars, added sugars, protein, vitamin D, calcium, iron, potassium, with % Daily Value). Canadian Nutrition Facts table values stored alongside. | P0 / P1 |
| FOOD-4 | Validation: sub-nutrients can't exceed their parent (e.g., saturated fat ≤ total fat); % Daily Value calculated from reference values. | P0 |
| FOOD-5 | Dietary labels (vegetarian, vegan, gluten-free, halal, kosher, organic, non-GMO), storage instructions, shelf life and shelf life after opening. | P0 |
| FOOD-6 | A note that the business is responsible for the accuracy and compliance of labels. | P0 |

### 6.7 Customers (CRM)
| ID | Requirement | Priority |
|----|-------------|----------|
| CUS-1 | Customer companies and contacts: name, type (retailer, grocery chain, wholesaler, restaurant…), billing address, **multiple ship-to addresses** (geocoded), currency, payment terms, tax status and exemption certificate, minimum shelf-life requirement, sales owner. | P0 |
| CUS-2 | Customer timeline: activities, quotes, orders, shipments, invoices. | P0 |
| CUS-3 | Tasks and activities (calls, meetings, notes) with reminders. | P0 |
| CUS-4 | Deals and pipeline (Kanban) for larger opportunities. | P1 |
| CUS-5 | CSV import/export. | P0 |

### 6.8 Quotes
| ID | Requirement | Priority |
|----|-------------|----------|
| QUO-1 | Quote for a customer and ship-to address with products, quantities (in selling units), prices, discounts, taxes and totals in the customer's currency. | P0 |
| QUO-2 | While quoting, sales sees **available stock in the region that serves the ship-to address** and the earliest expiry that would ship. | P0 |
| QUO-3 | Approval when discounts or margins break set limits; approvers see the reason. | P0 |
| QUO-4 | Statuses: Draft → Pending approval → Approved → Sent → Accepted / Declined / Expired; PDF by email. | P0 |
| QUO-5 | Accepting a quote creates a sales order. | P0 |

### 6.9 Order Management & Routing
| ID | Requirement | Priority |
|----|-------------|----------|
| ORD-1 | Sales orders from a quote or created directly: customer, ship-to address, requested delivery date, lines, prices, taxes, totals, currency, customer PO number. | P0 |
| ORD-2 | On confirmation, the **routing engine** suggests fulfilling location(s) using the rules in §5.3: territory coverage of the ship-to region → enough Available stock meeting minimum shelf life → same country → nearest (straight-line distance from geocoded addresses) → location priority. | P0 |
| ORD-3 | The suggestion is shown with its reason (e.g., "Houston distributor: covers TX, 180 mi away, all 6 lines in stock, earliest expiry 2027-03"). Alternatives are listed with what they lack. | P0 |
| ORD-4 | Routing settings per business: **auto-assign** or **suggest and confirm**; whether orders may be **split** across locations; fallback location (e.g., main warehouse); whether cross-border fulfilment is allowed (default: no). | P0 |
| ORD-5 | Operations or Executives can **override** the location, or the batches, before picking starts; the override and its reason are logged. | P0 |
| ORD-6 | When no location can fulfil a line: backorder it (fulfilled automatically when stock arrives at a serving location), or suggest a transfer to the serving location. | P1 |
| ORD-7 | Confirmed orders **reserve** stock by batch (FEFO); cancelled or edited orders release it. | P0 |
| ORD-8 | Each location gets a **fulfilment order** with its lines: statuses New → Acknowledged → Picking → Packed → Shipped → Delivered, or Rejected (with a reason, which re-routes the order). | P0 |
| ORD-9 | While picking, the location confirms the batch shipped per line; picking a different batch than reserved needs a reason and must still meet shelf-life rules. | P0 |
| ORD-10 | Shipping records carrier, tracking number, ship date, number of cartons and weight; stock is deducted from the batch on shipment; the customer can be emailed a shipping notification. | P0 |
| ORD-11 | Acknowledgement and ship-by deadlines per location; overdue fulfilment orders are flagged to Ops and the sales owner. | P0 |
| ORD-12 | Packing slip and pick list PDFs. | P0 |
| ORD-13 | The sales order status is derived from its fulfilment orders: Confirmed → Partially shipped → Shipped → Delivered / Cancelled. | P0 |

### 6.10 Invoices & Payments
| ID | Requirement | Priority |
|----|-------------|----------|
| INV-1 | Invoice from a sales order (all lines or shipped lines), in the order's currency (USD or CAD). | P0 |
| INV-2 | Taxes: US sales tax rate per invoice/line (manual, with exemptions); Canada GST/HST and PST/QST by the customer's province. | P0 |
| INV-3 | Statuses: Draft → Sent → Partially paid → Paid / Overdue / Void; sent invoices can only be voided and reissued; numbers are never reused. | P0 |
| INV-4 | PDF and email; payments recorded manually (check, ACH, EFT, wire, card) with partial payments. | P0 |
| INV-5 | Receivables aging report; reminder emails (P1). | P0 |
| INV-6 | CSV export of invoices, payments and inventory valuation for the accountant. | P1 |

### 6.11 Distributor Portal
| ID | Requirement | Priority |
|----|-------------|----------|
| DP-1 | **Today** view: new fulfilment orders to acknowledge, orders to ship today, overdue orders, inbound transfers, expiring stock. | P0 |
| DP-2 | **Fulfilment orders**: acknowledge, pick (confirm batches), pack, ship (carrier, tracking), reject (with reason); print pick list and packing slip. | P0 |
| DP-3 | **My inventory**: stock by product and batch with expiry and status; expiry alerts. | P0 |
| DP-4 | **Inbound transfers**: see what's coming and when; receive with quantities per batch; report shortages and damage with photos. | P0 |
| DP-5 | **Adjustments & counts**: request adjustments (damaged, expired…) and submit stock counts for approval. | P0 |
| DP-6 | **Replenishment requests**. | P1 |
| DP-7 | **Performance**: orders shipped, on-time acknowledgement and shipping rate, stock accuracy (from counts). | P1 |
| DP-8 | Works on phones and tablets; barcode scanning with the camera. | P0 / P1 |

### 6.12 Dashboards & Reports
| ID | Requirement | Priority |
|----|-------------|----------|
| REP-1 | **Executive home**: purchase orders open, shipments in transit with ETA, stock value by location, stock expiring in 30/60/90 days (quantity and value), sales this month by region (state/province) and by distributor, open orders and late fulfilment, receivables overdue. | P0 |
| REP-2 | **Import report**: shipments by status, delays vs ETA, landed cost per unit by product and shipment, duty and freight as a % of product cost. | P0 |
| REP-3 | **Inventory reports**: stock on hand by location/product/batch, movement history, aging, expiry risk, write-offs by reason, stock value. | P0 |
| REP-4 | **Batch traceability**: supplier → PO → shipment → receipt → transfers → customers, for any batch. | P0 |
| REP-5 | **Distributor performance**: orders fulfilled, on-time rates, rejections, stock accuracy, write-offs, sales volume in their territory. | P0 |
| REP-6 | **Sales**: by customer, product, category, region, sales rep; margin at landed cost (restricted). | P0 |
| REP-7 | **Operations**: receipts pending, transfers in transit, fulfilment orders by status and location. | P0 |
| REP-8 | CSV export of any report. | P1 |

### 6.13 Global
| ID | Requirement | Priority |
|----|-------------|----------|
| GLB-1 | Global search limited to what each user may see. | P0 |
| GLB-2 | **Audit log** of approvals, stock movements, cost changes, routing overrides, price changes, user changes and exports. | P0 |
| GLB-3 | Notification center plus email for key events (approvals, new fulfilment orders, ETA changes, expiry alerts, holds). | P0 |
| GLB-4 | Multi-currency: base currency per business (USD or CAD); supplier currencies (INR, USD, EUR…) on POs; customer currency USD or CAD; exchange rates entered manually or fetched daily (P1). | P0 |
| GLB-5 | Settings: company profile, currencies, tax rates, approval limits, routing rules, expiry alert thresholds, document numbering. | P0 |

## 7. Data Model (Conceptual)

```
Tenant (business) 1─* User (group: EXEC | OPS | SALES | DISTRIBUTOR; permissions)
Distributor 1─* Location ; Location (type: WAREHOUSE | 3PL | DISTRIBUTOR) 1─* TerritoryRule (country, state/province, postal prefix)
Supplier 1─* SupplierProduct *─1 Product ; Supplier 1─* PurchaseOrder 1─* POLine
ImportShipment *─* POLine (via ShipmentLine) ; ImportShipment 1─* CostLine, 1─* ShipmentEvent, 1─* Document
Receipt *─1 ImportShipment | StockTransfer ; Receipt 1─* ReceiptLine ─► creates Batch
Batch: product, lot no., supplier lot no., mfg date, expiry date, landed unit cost, origin shipment
StockBalance: (location, product, batch, status) → quantity        ← derived from StockMovement
StockMovement: immutable ledger (type, qty, from/to location, batch, reference, user, time)
StockTransfer 1─* TransferLine (batch) ; Adjustment ; StockCount 1─* CountLine ; Hold/Recall
Product *─1 ProductType, *─1 Category ; units & conversions ; FoodDetails / ElectronicsDetails ; HsCode per country
Customer 1─* Contact, 1─* ShipToAddress (geocoded)
Quote 1─* QuoteLine ; SalesOrder 1─* OrderLine
SalesOrder 1─* FulfilmentOrder *─1 Location ; FulfilmentOrder 1─* Allocation (order line × batch × qty) ; 1─* Shipment
Invoice 1─* InvoiceLine, 1─* Payment
Task, Activity, Notification, AuditLogEntry, ExchangeRate
```

**Key design decisions**
- **Ledger-based inventory.** Stock balances are derived from an append-only
  movement ledger, so every quantity is explainable and auditable. Reservations
  and deductions happen in database transactions with row locks, so stock
  can't go negative or be double-allocated.
- **Batch as the unit of truth.** Expiry, landed cost, supplier and origin
  shipment live on the batch, so FEFO, valuation and recalls all work from the
  same record.
- **Routing as a pure, testable function:** `(order, locations, territories,
  stock, settings) → ranked options with reasons`. It is unit-tested with
  fixtures and can be changed without touching order code.
- **Tenant and distributor isolation:** every row has `tenant_id`, and
  distributor-owned data is scoped by `location_id`/`distributor_id`. This is
  enforced in a shared data-access layer and backed by Postgres Row-Level
  Security. The portal API returns distributor-specific shapes without prices,
  costs or customer contact details.
- **Money:** integer minor units per currency; the exchange rate used is stored
  on every foreign-currency document.

## 8. Non-Functional Requirements

| Area | Requirement |
|------|-------------|
| Performance | p95 page load < 1.5 s and p95 API < 300 ms; routing a 50-line order in < 1 s with 100 locations and 20k products. |
| Inventory integrity | No negative stock or double allocation under concurrent use (tested); balances always equal the sum of movements (daily automated check). |
| Scale (MVP) | Per tenant: 200 internal users, 300 distributor locations, 20k products, 1M stock movements per year. |
| Security | HTTPS only, Argon2 passwords, 2FA for executives, tenant and distributor isolation (§7), OWASP Top 10, rate limiting, private file storage with signed URLs, malware checks on uploads. |
| Privacy | US (CCPA/CPRA) and Canada (PIPEDA; Quebec Law 25) privacy requirements; customer personal data shared with distributors only as needed to deliver. |
| Data residency | Hosted in North America; Canadian tenants may require Canadian hosting (open question). |
| Availability | 99.5% monthly; daily backups, 30-day retention, point-in-time recovery. |
| Offline tolerance | Receiving and picking screens tolerate brief connection drops without losing entered data (P1). |
| Accessibility | WCAG 2.1 AA for core flows. |
| Localization | English UI; French product content for Canada; USD/CAD; imperial or metric by country; each user's own timezone. |
| Observability | Structured JSON logs with trace IDs; error tracking; timing of API, database and external calls. |

## 9. Recommended Technical Approach

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Language | TypeScript end to end | Shared types for money, units and permissions. |
| Web | Next.js (App Router) + React | Internal app and Distributor Portal as separate route groups with their own layouts and middleware. |
| UI | Tailwind CSS + shadcn/ui; TanStack Table; Recharts; MapLibre for location/territory maps | Data-heavy screens, accessible components. |
| Database | PostgreSQL | Transactions and row locking for stock, Row-Level Security, PostGIS or earthdistance for distance-based routing. |
| ORM | Prisma (or Drizzle) | Type-safe queries and migrations. |
| Auth | Auth.js + TOTP 2FA | Sessions carry tenant, group, permissions and locations. |
| Authorization | One policy module used by every query and action | The permission matrix in one tested place. |
| Geocoding | Address geocoding at save time (e.g., Mapbox, Google, or Geocodio for US/Canada) with ZIP/postal centroid fallback | Distances for routing. |
| Barcodes | Browser camera scanning (e.g., ZXing) and label PDFs | Receiving and picking on phones. |
| PDFs | React-PDF | POs, quotes, invoices, pick lists, packing slips, labels. |
| Files | S3-compatible storage with signed URLs | Shipping, customs and compliance documents. |
| Jobs | pg-boss | Expiry checks, reminders, overdue flags, exchange rates, emails. |
| Testing | Vitest (routing engine, stock ledger, money, permissions), Playwright (end-to-end per user group) | Covers the logic where mistakes cost the most. |
| Deployment | Docker; managed Postgres in North America | Simple operations. |

## 10. Success Metrics

| Metric | Target (6 months after launch) |
|--------|-------------------------------|
| Import shipments tracked in the app | 100% |
| Received batches with batch number and expiry recorded | 100% for batch-tracked products |
| Inventory accuracy (system vs. counted) | ≥ 98% |
| Value of stock written off as expired | 50% lower than before launch |
| Orders routed automatically without override | ≥ 80% |
| Fulfilment orders shipped by the ship-by date | ≥ 95% |
| Time to trace a batch to all affected customers | < 5 minutes |
| Executives using the dashboard weekly | 100% |

## 11. Release Plan / Milestones

Operations first (import → inventory → routing), then selling and billing.

| Milestone | Scope | Est. |
|-----------|-------|------|
| M0 – Foundation | Tenant sign-up, users, groups and permissions, distributors and locations, territories, portal shell, audit log, design system, CI | 3 wks |
| M1 – Catalog | Products, types, categories, units, weights & dimensions, food and electronics details, HS codes | 3 wks |
| M2 – Suppliers & Imports | Suppliers, purchase orders and approvals, import shipments, documents, deadlines, landed cost | 3.5 wks |
| M3 – Receiving & Inventory | Receiving with batches and expiry, stock ledger, statuses, FEFO, expiry alerts, stock views, valuation | 3.5 wks |
| M4 – Transfers & Control | Stock transfers, distributor receiving, adjustments, counts, holds and recalls, traceability | 2.5 wks |
| M5 – Customers & Orders | Customers, ship-to geocoding, sales orders, routing engine, reservations, fulfilment orders, distributor portal fulfilment, pick/pack/ship | 4 wks |
| M6 – Quotes & Invoices | Quotes with regional availability, approvals, invoices, US/Canada taxes, payments, aging | 3 wks |
| M7 – Dashboards | Executive, import, inventory, distributor and sales reports | 2 wks |
| M8 – Hardening & Pilot | Concurrency and permission test suites, security review, performance, pilot with one importer and 2–3 distributors | 2.5 wks |

Total ≈ 27 weeks for one small team.

**Phase 2 candidates:** live container and carrier tracking, customs broker
integration, carrier rate shopping and labels, QuickBooks/Xero sync, online
payments, automatic sales tax, demand forecasting and purchase suggestions,
bin locations, native mobile scanning app, customer portal, EDI with grocery
chains, deals pipeline v2.

## 12. Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| Inventory numbers drift from reality (especially at distributors) | Ledger-based stock, mandatory batch confirmation on pick, regular counts in the portal, accuracy shown on the distributor dashboard. |
| Wrong location chosen for an order | Routing reasons shown, suggest-and-confirm mode by default at first, easy override, routing unit tests from real scenarios. |
| Distributors don't record receipts and shipments promptly | Mobile-friendly portal, email/SMS nudges, acknowledgement deadlines, performance reporting. |
| Missed customs or compliance deadlines (ISF, prior notice, licence expiry) | Deadline fields with reminders; documents required before status can advance (configurable). |
| Landed cost wrong because final costs arrive late | Estimated vs. final costs, recalculation with history, flag on shipments with unfinalized costs. |
| Food safety incident without traceability | Batch required for food, recall workflow, traceability report tested in the pilot. |
| Data leakage between tenants or distributors | Layered isolation, automated cross-tenant and cross-distributor tests, security review before pilot. |
| Scope is large | Operations-first milestones; CRM pipeline and advanced features deferred to P1/Phase 2. |

## 13. Open Questions

1. **Who owns stock held by distributors?** The draft assumes the business
   still owns it (distributors store it on its behalf, like consignment).
   If distributors buy the stock, it leaves our inventory on transfer and the
   model changes.
2. **How are distributors paid?** A fee per order, a margin, a monthly fee?
   Should the app calculate it?
3. **Territories:** are they exclusive (one distributor per state/province), or
   can several distributors overlap? Are they defined by state/province only,
   or also by ZIP/postal code?
4. **Routing:** fully automatic, or suggest-and-confirm by staff? May one order
   be split across several locations? Are orders ever shipped across the
   US/Canada border?
5. **Canada supply:** does stock for Canada arrive directly from India into
   Canada, or is it moved from US warehouses?
6. **Company warehouses:** does the business run its own warehouses, use 3PLs,
   or both? Should 3PL staff log in?
7. **Who takes customer orders?** Only your sales team, or do distributors also
   take orders from customers in their region? (Earlier the answer was the
   sales team.)
8. **Minimum shelf life:** are there standard rules by customer type (e.g.,
   grocery chains)?
9. **Supplier currency:** do you pay Indian suppliers in INR or USD?
10. **Costing method:** landed cost per batch (specific identification) is
    assumed. Does your accountant need FIFO or weighted average instead?
11. **SaaS model:** pricing (per user, per location, per order volume) and
    whether a free trial is needed.
12. **Branding and name** of the application.
