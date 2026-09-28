# Product Requirements Document: Sales CRM with Distributor Portal

| Field        | Value                         |
|--------------|-------------------------------|
| Status       | Draft v0.3                    |
| Last updated | 2026-09-28                    |
| Owner        | sennuramamoorthy              |
| Scope        | MVP (Release 1)               |
| Market       | United States                 |

---

## 1. Summary

A web application for a US business that sells products, including products
supplied by **independent distributors across the USA**. Three groups of users
work in it:

1. **Executives** see what's going on across the business (pipeline, revenue,
   orders, who is dealing with what) and approve large discounts and quotes.
2. **The sales team** works with customers and deals, then creates **quotes**,
   turns accepted quotes into **orders**, and bills them with **invoices**.
3. **Distributors** log in to a separate **Distributor Portal**. There they
   manage their own products, fulfil their part of each order, and see how
   their products are selling. They never see other distributors' data, the
   business's customers, selling prices or margins.

The app combines a CRM (contacts, companies, deals, tasks), a product catalog
with type-specific details (food, electronics and more), a quote-to-invoice
sales flow, and role-based dashboards.

## 2. Problem Statement

- **Executives** have no single, current view of the pipeline, revenue, open
  orders, and which salesperson or distributor is handling what. Answers come
  from spreadsheets and status meetings.
- **Sales reps** build quotes and invoices by hand in documents or accounting
  tools. The result is pricing mistakes, unapproved discounts and no link
  between a quote and the deal or customer it belongs to.
- **Distributors** receive orders by email or phone, send product details as
  attachments, and have no way to confirm, ship or report on orders in one
  place. The business can't see whether a distributor has acted on an order.
- Product information (specs, ingredients, allergens, nutrition, weights and
  dimensions) is scattered, out of date or inconsistent between distributors.

## 3. Goals & Non-Goals

### 3.1 Goals (MVP)
1. **G1: One view of the business for executives.** Dashboards and record
   ownership show pipeline, revenue, orders, receivables, and who is handling
   each customer, deal and order.
2. **G2: Quote to cash in one flow.** Deal → quote → order → invoice with no
   re-typing, with totals and taxes calculated consistently.
3. **G3: Controlled discounting.** Quotes above set discount or value limits
   need executive approval before they can be sent.
4. **G4: Distributors run their own part.** Distributors keep their product
   listings current and fulfil their order lines themselves, and the business
   sees each fulfilment status in real time.
5. **G5: Strict data separation.** Each distributor sees only its own
   products, order lines and documents. Customer contact details, selling
   prices and margins are never shown to distributors.
6. **G6: Complete product information.** A catalog with categories and
   type-specific details (technical specs for electronics; ingredients,
   allergens and nutrition facts for food; weights and dimensions for all).
7. **G7: Relationship management.** Contacts, companies, deals, tasks and
   activities stay linked and visible on one timeline.

### 3.2 Non-Goals (MVP)
- Collecting payments online (card/ACH). Payments are recorded manually; see
  Phase 2.
- Paying distributors (payouts, commissions, settlement). The MVP only tracks
  the invoices distributors upload.
- Automatic sales-tax calculation by address (e.g., Avalara/TaxJar). The MVP
  uses tax rates set by the business.
- Inventory and stock management, warehouses and purchase orders.
- Two-way sync with accounting software (e.g., QuickBooks); the MVP offers a
  CSV export.
- Distributors selling to their own customers inside the app (see open
  question 1).
- Customer self-service portal and e-commerce storefront.
- Marketing automation, support ticketing, native mobile apps.
- Generating food labels that comply with labeling laws (the catalog stores
  the data but does not certify compliance).

## 4. Users, Roles & Access

### 4.1 User groups

| Group | Who they are | What they come to do |
|-------|--------------|----------------------|
| **Executive** | Owner, CEO, VP of Sales, finance lead. | See everything; track performance, workload and receivables; approve discounts, large quotes and distributor products. Rarely creates records. |
| **Sales** | Sales reps and account managers. | Manage customers and deals, log activities, build quotes, convert them to orders, issue invoices, record payments, follow up. |
| **Distributor** | Staff of an independent distributor company somewhere in the US. Each distributor company has one or more users. | Manage their own product listings, acknowledge and ship their order lines, upload documents, see their own sales. |

**Administrator** is a permission added to an Executive or Sales user, not a
separate group. Administrators manage settings, users, distributor accounts,
product types, categories and approval limits.

### 4.2 Personas

| Persona | Description | Key needs |
|---------|-------------|-----------|
| **Elena, Executive (CEO)** | Runs a 25-person company selling food and electronics products nationwide. | A dashboard she can read in 2 minutes; spotting stalled deals, late orders and overdue invoices; approving discounts from her phone. |
| **Marcus, Sales Rep** | Handles 60 customer accounts. | Fast quote building from the catalog, knowing when a quote is approved, seeing whether an order has shipped without calling the distributor. |
| **Dana, Distributor (Texas)** | Owns a 6-person distribution company that supplies 40 products. | Getting new orders immediately, marking them shipped with tracking, keeping product details current, seeing monthly volume. |

### 4.3 Permission matrix

✅ = full access · 👁 = view only · ✍ = own records only · — = no access

| Capability | Executive | Sales | Distributor |
|------------|:---------:|:-----:|:-----------:|
| Executive & team dashboards | ✅ | 👁 own + team totals | — |
| Distributor dashboard | 👁 any distributor | 👁 any distributor | ✍ own |
| Contacts & companies (customers) | ✅ | ✅ | — |
| Deals & pipeline | ✅ (can reassign) | ✍ edit own, 👁 all | — |
| Tasks & activities | ✅ | ✅ | — |
| Product catalog | ✅ | 👁 | ✍ own products |
| Create/edit products | ✅ | — (unless Administrator) | ✍ own, needs approval |
| Approve distributor products | ✅ | — (unless Catalog approver) | — |
| Product types & categories | ✅ (Administrator) | 👁 | 👁 (to pick from) |
| Selling price | ✅ | 👁 | — |
| Distributor supply price | ✅ | 👁 | ✍ own |
| Margin | ✅ | 👁 | — |
| Quotes | ✅ | ✍ create/edit own | — |
| Approve quotes over limits | ✅ | — | — |
| Sales orders (full) | ✅ | ✍ own, 👁 all | — |
| Fulfilment orders (distributor's lines) | 👁 | 👁 | ✍ own: acknowledge, ship, reject |
| Invoices & payments | ✅ | ✍ own | — |
| Distributor documents (their invoices, certificates) | 👁 | 👁 | ✍ own |
| Users, distributor accounts, settings | ✅ (Administrator) | — | Distributor admin: own company's users (P1) |
| Audit log | ✅ | — | — |

### 4.4 What a distributor can see on an order

A distributor sees a **fulfilment order**: only the lines for its own products
from a sales order.

| Visible to the distributor | Never visible to the distributor |
|----------------------------|----------------------------------|
| Fulfilment order number and date | The sales order's number, total, and other lines |
| Product, SKU, quantity, unit of sale | Other distributors' products or orders |
| Its own supply price and line total at supply price | Selling price, discount, tax, margin |
| Ship-to recipient name and delivery address, requested ship-by date, delivery notes | Customer email, phone, company details, deal, quote, invoice, activity history |
| Status history, tracking information, its own uploaded documents | Internal notes, the salesperson's name (it sees a "sales contact" set by the business instead) |

Ship-to name and address are shown because distributors ship directly to
customers. See open question 2.

## 5. Core Workflows

### 5.1 Quote to cash
```
Deal (Sales) ──► Quote (draft)
                   │ discount or total over limit?
                   ├─ yes ─► Pending approval ─► Executive approves / rejects (with comment)
                   ▼
                 Approved ─► Sent to customer (PDF by email) ─► Accepted / Declined / Expired
                                                                  │
                                                     Accepted ─► Sales Order
                                                                  │ split by product owner
                        ┌─────────────────────────────────────────┼──────────────────────┐
                        ▼                                         ▼                      ▼
             Fulfilment Order (Distributor A)     Fulfilment Order (Distributor B)   In-house lines
             New → Acknowledged → Shipped → Delivered (or Rejected)                  (fulfilled by staff)
                        └──────────────── all shipped ─────────────┘
                                                  ▼
                                   Invoice (Sales) ─► Sent ─► Paid (payments recorded manually)
```

### 5.2 Distributor product onboarding
```
Distributor creates product (Draft) ─► Submits for review ─► Approver reviews
   ─► Approved: product goes Active and can be quoted
   ─► Changes requested: back to distributor with comments
Edits to an Active product create a pending revision; the live version stays
unchanged until the revision is approved.
```

## 6. Functional Requirements

Priority: **P0** = must have for MVP, **P1** = should have, **P2** = nice to have.

### 6.1 Authentication, Users & Access
| ID | Requirement | Priority |
|----|-------------|----------|
| AUTH-1 | Sign in with email + password, with email verification and password reset. | P0 |
| AUTH-2 | Sign in with Google (internal users). | P1 |
| AUTH-3 | Two-factor authentication (TOTP); required for Executives and Administrators. | P1 |
| AUTH-4 | Sessions expire after 12 hours of inactivity; distributors after 8 hours. | P0 |
| USR-1 | Internal users are invited by an Administrator and given a group (Executive or Sales) plus optional permissions (Administrator, Catalog approver). | P0 |
| USR-2 | An Administrator creates a **distributor account** (company name, address, contact, states served, status) and invites its first user. | P0 |
| USR-3 | A distributor admin can invite and deactivate users of its own company. | P1 |
| USR-4 | Deactivating a user or a distributor account signs them out right away and blocks sign-in; their records remain. | P0 |
| USR-5 | Distributor users sign in to the **Distributor Portal**, a separate area of the app with its own navigation. They can't reach internal pages or data even by editing URLs or calling the API directly. | P0 |
| USR-6 | Executives can reassign ownership of customers, deals, quotes and orders (e.g., when a rep leaves), singly or in bulk. | P0 |

### 6.2 Contacts & Companies (customers)
Internal users only.

| ID | Requirement | Priority |
|----|-------------|----------|
| CON-1 | Contact fields: first/last name, email(s), phone(s), job title, company, address, owner, tags, source, notes. | P0 |
| CON-2 | Company fields: name, website, industry, size, phone, billing address, shipping addresses (several), payment terms, tax-exempt flag and certificate, owner, tags. | P0 |
| CON-3 | Many contacts per company; a contact belongs to at most one company. | P0 |
| CON-4 | List view with search, filters (owner, tag, state, last contacted), sort and pagination. | P0 |
| CON-5 | Detail page with one timeline: activities, deals, quotes, orders, invoices. | P0 |
| CON-6 | CSV import with column mapping, preview, validation and duplicate detection (by email / company name); CSV export. | P0 |
| CON-7 | "Last contacted" date derived from the latest logged activity. | P0 |
| CON-8 | Custom fields on contacts, companies and deals. | P1 |
| CON-9 | Merge duplicates; bulk tag, bulk reassign. | P1 |

### 6.3 Deals & Pipeline
| ID | Requirement | Priority |
|----|-------------|----------|
| DEAL-1 | Deal fields: title, company, primary contact, owner, stage, probability, expected close date, value, status (Open / Won / Lost), lost reason. | P0 |
| DEAL-2 | Kanban board with deal count and value per stage; drag and drop to change stage. | P0 |
| DEAL-3 | Default stages: Lead → Qualified → Quote Sent → Negotiation → Won / Lost. Administrators can add, rename, reorder and remove stages and set probabilities. | P0 |
| DEAL-4 | A deal can have several quotes; one is marked **primary**, and the deal value follows the primary quote's total. | P0 |
| DEAL-5 | When a quote is accepted, its deal is marked Won (it can be undone). | P1 |
| DEAL-6 | Stage history is recorded for cycle-time and conversion reports. | P0 |
| DEAL-7 | Board and list views filterable by owner, stage, close date and status. | P0 |

### 6.4 Tasks & Activities
| ID | Requirement | Priority |
|----|-------------|----------|
| TASK-1 | Tasks with title, due date/time, priority, assignee and a linked record (contact, company, deal, quote, order, invoice). | P0 |
| TASK-2 | "My Tasks" view: Overdue / Today / Upcoming. | P0 |
| TASK-3 | In-app notifications for due and assigned tasks; optional daily email digest. | P0 / P1 |
| ACT-1 | Log calls, meetings, emails and notes against records; they appear on every linked record's timeline. | P0 |
| ACT-2 | @mentions of colleagues in notes, with a notification. | P1 |

### 6.5 Products & Catalog

#### Ownership & review
| ID | Requirement | Priority |
|----|-------------|----------|
| OWN-1 | Every product has an owner: **In-house** (the business) or **one distributor**. | P0 |
| OWN-2 | Distributors can create, edit and archive only their own products; they can't delete a product that has been ordered. | P0 |
| OWN-3 | Products created by distributors start as **Draft** and must be **submitted for review**. A user with Executive or Catalog approver permission approves them or requests changes, with a comment. | P0 |
| OWN-4 | Edits to an Active product by a distributor create a **pending revision**. The live version stays unchanged until it is approved. The reviewer sees a side-by-side diff of what changed. | P0 |
| OWN-5 | The business sets the **selling price**; the distributor sets its **supply price** (what the business pays the distributor). A change to the supply price needs approval like any other edit. | P0 |
| OWN-6 | The same item supplied by two distributors is two separate products (each with its own SKU and supply price). | P0 |
| OWN-7 | Notifications: distributors are told when a product is approved or needs changes; approvers are told when something is submitted. | P0 |

#### Product types
A **product type** decides which detail fields a product has. Types answer "what
kind of thing is this?" and categories answer "where does it sit in the
catalog?". The two are independent.

| ID | Requirement | Priority |
|----|-------------|----------|
| PT-1 | Built-in types: **Food**, **Electronics**, **General** (common fields only). They can't be deleted, but fields can be added. | P0 |
| PT-2 | Administrators can create custom types with their own field definitions (label, data type, unit options, required, help text, display group). | P1 |
| PT-3 | Types in use can't be deleted, only archived. Changing a product's type keeps the old values hidden, not deleted. | P1 |

#### Categories
| ID | Requirement | Priority |
|----|-------------|----------|
| CAT-1 | Administrators create categories as a tree up to 5 levels deep (e.g., *Food › Beverages › Juices*); rename, reorder and move by drag and drop. A category can't be moved under its own descendant. | P0 |
| CAT-2 | Distributors choose from existing categories and can suggest a new one, which an Administrator creates or declines. | P0 / P1 |
| CAT-3 | A product has one primary category and may belong to more. | P0 / P1 |
| CAT-4 | Deleting a category requires moving its products and subcategories elsewhere; products are never deleted with it. | P0 |
| CAT-5 | Category names are unique among siblings (case-insensitive). | P0 |

#### Common product fields
| ID | Requirement | Priority |
|----|-------------|----------|
| PRD-1 | Name, SKU (unique across the catalog), type, category, owner (in-house or distributor), short and long description, status (Draft / Pending review / Active / Archived), tags. | P0 |
| PRD-2 | Pricing: selling price (USD), supply price (distributor products), unit of sale (each, lb, case…), tax category. Margin is calculated and shown to internal users only. | P0 |
| PRD-3 | Brand, manufacturer, manufacturer part number, GTIN/UPC (check digit validated), country of origin. | P1 |
| PRD-4 | Up to 10 images (JPEG/PNG/WebP, ≤ 5 MB), one marked primary. | P1 |
| PRD-5 | Attachments such as datasheets, certificates and safety data sheets (PDF, ≤ 20 MB). | P1 |

#### Weights & dimensions
| ID | Requirement | Priority |
|----|-------------|----------|
| DIM-1 | Product: net weight, length, width, height. | P0 |
| DIM-2 | Package: gross weight, length, width, height, units per case. | P0 |
| DIM-3 | Entry in imperial (oz, lb, in, ft) or metric (g, kg, mm, cm, m); stored in base units (g, mm); shown in imperial by default. | P0 |
| DIM-4 | Net volume for liquids (fl oz, ml, l); calculated package volume. | P1 |
| DIM-5 | Values must be positive; gross weight below net weight shows a warning. | P0 |

#### Electronics details
| ID | Requirement | Priority |
|----|-------------|----------|
| ELE-1 | Standard fields: model number, power source, voltage (V), power (W), battery capacity (mAh), connectivity (Wi-Fi, Bluetooth, USB-C, Ethernet…), color, warranty (months), certifications (FCC, UL, ETL, Energy Star, RoHS…). | P0 |
| ELE-2 | Free-form spec table of grouped name–value–unit rows (e.g., "Display": Size = 6.1 in). | P0 |
| ELE-3 | Copy specs from another product. | P1 |
| ELE-4 | Side-by-side spec comparison of up to 4 products. | P2 |

#### Food details
| ID | Requirement | Priority |
|----|-------------|----------|
| FOOD-1 | **Ingredients**: an ordered list (descending by weight, as on the label), each with an optional percentage, plus an "ingredients statement" field for text pasted from the label. | P0 |
| FOOD-2 | **Allergens**: for each of the 9 US major allergens (milk, eggs, fish, crustacean shellfish, tree nuts, peanuts, wheat, soybeans, sesame), mark *Contains*, *May contain* or *Free from*. Additional allergens (e.g., gluten, mustard, celery) can be tracked. Allergens are shown prominently. | P0 |
| FOOD-3 | **Nutrition facts** in US FDA format: serving size, servings per container, calories, total fat, saturated fat, trans fat, cholesterol, sodium, total carbohydrate, dietary fiber, total sugars, added sugars, protein, vitamin D, calcium, iron, potassium, each with amount and % Daily Value. Per-100 g values can also be stored. | P0 |
| FOOD-4 | Calculations: % Daily Value from the FDA reference values; per-serving values from per-100 g values and serving size. Calculated values can be overridden. | P1 |
| FOOD-5 | Dietary labels: vegetarian, vegan, gluten-free, dairy-free, halal, kosher, USDA organic, non-GMO. | P0 |
| FOOD-6 | Storage and shelf life: storage type (ambient, refrigerated, frozen), temperature range, shelf life, shelf life after opening. | P0 |
| FOOD-7 | Validation: a sub-nutrient can't exceed its parent (saturated fat ≤ total fat, sugars ≤ carbohydrate, added sugars ≤ total sugars). | P0 |
| FOOD-8 | A note shows that the product owner is responsible for label accuracy and compliance. | P0 |

#### Products page
| ID | Requirement | Priority |
|----|-------------|----------|
| PROD-1 | Table and grid views, with a category tree in a side panel. Internal users see all products; distributors see only their own. | P0 |
| PROD-2 | Search by name, SKU, UPC and brand; filter by type, category, owner/distributor, status and price. | P0 |
| PROD-3 | Detail page tabs: Overview, Details (type-specific), Weights & dimensions, Documents, Sales (orders containing it), History. | P0 |
| PROD-4 | "Pending review" queue for approvers. | P0 |
| PROD-5 | Duplicate a product; bulk change category, status or tags. | P1 |
| PROD-6 | CSV import and export per product type (internal users and distributors, each for the products they're allowed to manage). | P1 |

### 6.6 Quotes
| ID | Requirement | Priority |
|----|-------------|----------|
| QUO-1 | Create a quote from a deal or a company: customer, contact, billing and shipping address, payment terms, valid-until date (default 30 days), notes and terms. | P0 |
| QUO-2 | Line items from the catalog (Active products only): quantity, unit price (defaults to the selling price), discount (% or $), tax rate, line total. Free-text lines are allowed for services or fees. | P0 |
| QUO-3 | Totals: subtotal, discounts, shipping, sales tax, grand total. Tax rate per quote or per line; tax-exempt customers are charged no tax. | P0 |
| QUO-4 | Lines keep a snapshot of product name, SKU, price and supply price, so later product edits don't change the quote. | P0 |
| QUO-5 | Statuses: Draft → Pending approval → Approved → Sent → Accepted / Declined / Expired. Quotes past their valid-until date expire automatically. | P0 |
| QUO-6 | Approval rules (set by an Administrator): approval is required when any line's discount is over X%, the total discount is over Y%, the margin is under Z%, or the total is over $N. The reason for requiring approval is shown to the approver. | P0 |
| QUO-7 | Executives approve or reject with a comment; the rep is notified. Editing an approved quote sends it back for approval if it breaks a rule again. | P0 |
| QUO-8 | Branded PDF (logo, address, terms), emailed from the app to the customer; sending is logged as an activity. | P0 |
| QUO-9 | Revisions: a revised quote keeps the same number with a suffix (Q-1042-R2), and earlier versions stay viewable. | P1 |
| QUO-10 | The customer can view and accept the quote online through a secure link. | P2 |
| QUO-11 | Numbering: configurable prefix and sequence (e.g., Q-2026-0001). | P0 |

### 6.7 Orders & Fulfilment
| ID | Requirement | Priority |
|----|-------------|----------|
| ORD-1 | Marking a quote Accepted creates a **sales order** with the same lines, addresses and totals. Orders can also be created directly. | P0 |
| ORD-2 | The order is automatically split into one **fulfilment order** per distributor whose products it contains; in-house lines are fulfilled by internal staff. | P0 |
| ORD-3 | Fulfilment order statuses: New → Acknowledged → Shipped → Delivered, or Rejected (with a required reason) or Cancelled (by the business). | P0 |
| ORD-4 | Distributors are notified by email and in the portal about new fulfilment orders. The business sets how long they have to acknowledge (e.g., 1 business day); late orders are flagged to the sales owner. | P0 |
| ORD-5 | When shipping, the distributor enters carrier, tracking number and ship date; the sales owner is notified. | P0 |
| ORD-6 | A rejected fulfilment order alerts the sales owner, who can cancel the lines or move them to another distributor's equivalent product. | P0 / P1 |
| ORD-7 | The sales order's status is derived from its parts: Open → Partially shipped → Shipped → Delivered / Cancelled. | P0 |
| ORD-8 | Partial shipments (some quantity now, the rest later). | P1 |
| ORD-9 | Distributors can attach documents to a fulfilment order: packing slip, proof of delivery, and **their invoice to the business** (amount, invoice number, date). | P0 |
| ORD-10 | Internal users see the status of distributor invoices (Received → Approved → Paid) and can change it. | P1 |
| ORD-11 | Sales can edit or cancel an order until any part of it has shipped; affected distributors are notified. | P0 |

### 6.8 Invoices & Payments
| ID | Requirement | Priority |
|----|-------------|----------|
| INV-1 | Create an invoice from a sales order: the whole order, or shipped lines only (P1). Manual invoices are also allowed. | P0 |
| INV-2 | Invoice fields: number (sequential, never reused), dates, due date from payment terms (Net 15/30/60, due on receipt), bill-to, ship-to, lines, discounts, shipping, tax, total, balance due, notes. | P0 |
| INV-3 | Statuses: Draft → Sent → Partially paid → Paid, Overdue (automatic after the due date), Void. A sent invoice can't be edited, only voided and reissued. | P0 |
| INV-4 | Branded PDF, sent by email from the app; the send is logged. | P0 |
| INV-5 | Record payments by hand: date, amount, method (check, ACH, wire, card), reference. Several partial payments are allowed. | P0 |
| INV-6 | Automatic reminder emails before and after the due date (schedule configurable). | P1 |
| INV-7 | Credit notes. | P2 |
| INV-8 | CSV export of invoices and payments for the accountant. | P1 |

### 6.9 Dashboards & Reports
| ID | Requirement | Priority |
|----|-------------|----------|
| REP-1 | **Executive dashboard**: revenue invoiced and collected (month, quarter, year to date), open pipeline and weighted forecast, quotes awaiting approval, orders by status, overdue invoices and receivables aging (0–30 / 31–60 / 61–90 / 90+ days), top customers, products, categories and distributors. | P0 |
| REP-2 | **Who is dealing with what**: per sales rep, their open deals, quotes, orders, overdue tasks and last activity; per distributor, open fulfilment orders, late acknowledgements and on-time shipping rate. Click through to the records. | P0 |
| REP-3 | **Sales dashboard**: my pipeline, my quotes by status, my orders awaiting shipment, my overdue invoices, my tasks today. | P0 |
| REP-4 | **Distributor dashboard** (portal): new and open fulfilment orders, units shipped and value at supply price by month and product, on-time rate, products pending review. | P0 |
| REP-5 | Sales performance: win rate, average deal size, cycle time, quote-to-order conversion, by rep and date range. | P0 |
| REP-6 | Sales by US state (map or table). | P1 |
| REP-7 | CSV export of any report. | P1 |

### 6.10 Global
| ID | Requirement | Priority |
|----|-------------|----------|
| GLB-1 | Global search (Cmd/Ctrl+K) limited to the records the user may see. | P0 |
| GLB-2 | **Audit log** of sign-ins, approvals, price changes, status changes, ownership changes and exports: who, what, when, old and new values. Executives can view it. | P0 |
| GLB-3 | In-app notification center; email for important events (approval requests, new fulfilment orders, rejections). | P0 |
| GLB-4 | Responsive layout; approvals and fulfilment status updates work well on phones. | P0 |
| GLB-5 | Settings: company profile and logo, address, timezone, number formats, payment terms, tax rates, approval limits, acknowledgement deadline. | P0 |

## 7. Data Model (Conceptual)

```
Organization (the business) 1─* User (group: EXECUTIVE | SALES | DISTRIBUTOR; flags: admin, catalog_approver)
Distributor 1─* User (distributor users), states_served[]
Company 1─* Contact ; Company 1─* Address
Pipeline 1─* Stage ; Deal *─1 Stage, *─1 Company, *─1 User(owner) ; Deal 1─* DealStageHistory
ProductType 1─* FieldDefinition ; Category (parent_id tree)
Product *─1 ProductType, *─1 Category, *─1 Distributor? (null = in-house)
        + selling_price, supply_price, weights/dimensions (base units), attributes JSONB
Product 1─* ProductRevision (pending changes + review status)
FoodDetails 1─1 Product ; ElectronicsDetails 1─1 Product (spec rows)
Quote *─1 Deal?, *─1 Company, *─1 User(owner) ; Quote 1─* QuoteLine (product snapshot) ; Quote 1─* Approval
SalesOrder *─1 Quote? ; SalesOrder 1─* OrderLine
SalesOrder 1─* FulfilmentOrder *─1 Distributor ; FulfilmentOrder 1─* OrderLine, 1─* Shipment, 1─* Document
Invoice *─1 SalesOrder? ; Invoice 1─* InvoiceLine ; Invoice 1─* Payment
Task, Activity (linked to any record), Notification, AuditLogEntry
```

Every table carries `organization_id`, so the system can host more than one
business later. Distributor-owned data also carries `distributor_id`.

**How distributor separation is enforced (defence in depth):**
1. **Separate portal routes and API.** Distributor sessions can only call
   `/portal/*` endpoints, and internal endpoints reject them outright.
2. **Scoped queries.** Every portal query is filtered by the session's
   `distributor_id` in a shared data-access layer; handlers can't bypass it.
3. **Response shapes by role.** Portal endpoints return purpose-built response
   objects (e.g., `FulfilmentOrderForDistributor`) that don't contain selling
   price, customer contact fields or other lines. Full records are never
   serialized and then trimmed.
4. **Postgres Row-Level Security** on distributor-owned tables as a final
   backstop.
5. **Automated authorization tests** covering the full permission matrix in
   §4.3, including cross-distributor access attempts.

**Why product details are modeled this way:** fields that are filtered, sorted
and reported on (prices, SKU, weights) are real columns. Food and electronics
details have stable structure and validation rules, so they get typed tables.
Custom-type fields go in JSONB validated against field definitions. Order and
quote lines snapshot product data so documents never change after the fact.

## 8. Non-Functional Requirements

| Area | Requirement |
|------|-------------|
| Performance | p95 page load < 1.5 s and p95 API < 300 ms with 50k contacts, 20k products, 100k order lines. |
| Scale (MVP) | Up to 100 internal users and 500 distributor companies (2,000 distributor users). |
| Security | HTTPS only; Argon2 password hashing; distributor separation as in §7; OWASP Top 10 mitigations; rate limiting on sign-in; files stored privately with short-lived signed URLs; uploaded files checked for malware and allowed types. |
| Privacy | US privacy laws (e.g., CCPA/CPRA): export and deletion of personal data on request; customer personal data shown to distributors only where needed to deliver. |
| Money | Amounts stored as integer cents; rounding rules defined once and shared by quotes, orders and invoices; document numbers never reused. |
| Availability | 99.5% monthly uptime; daily backups kept 30 days, with point-in-time recovery. |
| Accessibility | WCAG 2.1 AA for core flows. |
| Browsers | Latest 2 versions of Chrome, Safari, Firefox and Edge; iOS Safari and Android Chrome for approvals and fulfilment. |
| Observability | Structured JSON logs with trace IDs; error tracking; timing of API, database and email calls. |
| Localization | US English, USD, US date format, imperial units by default; times shown in each user's timezone. |

## 9. Recommended Technical Approach

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Language | TypeScript end to end | One language, shared types for money and permissions. |
| Web framework | Next.js (App Router) + React | Internal app and distributor portal as route groups in one deployable, with separate layouts and middleware. |
| UI | Tailwind CSS + shadcn/ui; dnd-kit (Kanban, category tree); Recharts | Fast to build and accessible. |
| Database | PostgreSQL | Relational integrity for orders and money, Row-Level Security, full-text search. |
| ORM / migrations | Prisma (or Drizzle) | Type-safe queries and migrations. |
| Auth | Auth.js with credentials + Google; TOTP 2FA | Session handling; role and distributor in the session. |
| Authorization | One policy module (e.g., CASL or hand-written policies) used by every query and action | The permission matrix lives in one tested place. |
| PDFs | React-PDF or Playwright HTML-to-PDF | Branded quotes and invoices. |
| Files | S3-compatible storage with signed URLs | Images, documents, PDFs. |
| Background jobs | pg-boss | Emails, reminders, quote expiry, overdue invoices, late acknowledgements. |
| Email | Postmark / Resend / SES | Invites, notifications, sending quotes and invoices. |
| Validation | Zod | Shared client/server schemas. |
| Testing | Vitest (unit, permission matrix), Playwright (end-to-end for all three roles) | Guards the separation between roles. |
| Deployment | Docker; Vercel or Fly.io/Render + managed Postgres | Simple operations. |
| CI | GitHub Actions: lint, typecheck, test, build | Standard. |

## 10. Success Metrics

| Metric | Target (3 months after launch) |
|--------|-------------------------------|
| Quotes created in the app (vs. outside it) | ≥ 90% |
| Median time from quote request to quote sent | < 1 business day |
| Median approval turnaround | < 4 business hours |
| Fulfilment orders acknowledged on time | ≥ 90% |
| Distributor products with complete details (all required fields) | ≥ 95% |
| Executives using the dashboard weekly | 100% |
| Days sales outstanding (DSO) | 10% lower than before launch |
| Cross-distributor data exposure incidents | 0 |

## 11. Release Plan / Milestones

| Milestone | Scope | Est. |
|-----------|-------|------|
| M0 – Foundation | Repo, CI, auth, user groups and permissions module, distributor accounts, internal app and portal shells, audit log, design system | 3 wks |
| M1 – Customers | Contacts, companies, addresses, CSV import/export, timeline | 2 wks |
| M2 – Catalog | Categories, product types, products, weights & dimensions, food and electronics details, distributor product management and review | 3.5 wks |
| M3 – Pipeline | Deals, Kanban, tasks, activities, notifications | 2.5 wks |
| M4 – Quotes | Quote builder, taxes, approval rules and approvals, PDF, email | 2.5 wks |
| M5 – Orders & Fulfilment | Sales orders, split into fulfilment orders, distributor portal fulfilment, documents | 2.5 wks |
| M6 – Invoices | Invoices, payments, overdue handling, PDF, email | 2 wks |
| M7 – Dashboards | Executive, "who's dealing with what", sales, distributor dashboards; reports | 2 wks |
| M8 – Hardening & Pilot | Permission-matrix test suite, security review, performance, accessibility, pilot with 2–3 distributors | 2 wks |

Total ≈ 22 weeks for one small team. A pilot with a few friendly distributors
before full rollout is strongly recommended.

**Phase 2 candidates:** online payments (Stripe), automatic sales tax
(Avalara/TaxJar), QuickBooks/Xero sync, distributor payouts, inventory levels
reported by distributors, product variants, price lists and customer-specific
pricing, customer portal and online quote acceptance, email/calendar sync,
public API and webhooks, mobile app.

## 12. Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| A distributor sees another distributor's or the business's confidential data | The layered enforcement in §7, automated tests for the permission matrix, a security review before the pilot, and an audit log. |
| Distributors don't adopt the portal and keep using email | Email notifications with one-click links, mobile-friendly acknowledge/ship actions, a short onboarding guide, and pilot feedback before rollout. |
| Wrong totals or taxes on quotes and invoices | Integer-cent money handling, one shared calculation module with unit tests, snapshots on documents, non-editable sent invoices. |
| Wrong product data (e.g., allergens) from distributors reaches customers | Review before products go live, pending revisions for edits, validation rules, prominent allergen display, and a note on the owner's responsibility. |
| Approvals slow down sales | Clear rule reasons, mobile approvals, notifications, and turnaround shown on the dashboard. |
| Scope creep (payments, tax engines, inventory) | Hold the non-goals; everything else goes to the Phase 2 list. |

## 13. Open Questions

1. **Do distributors ever sell directly to their own customers inside this
   app?** The draft assumes no: the sales team sells, and distributors fulfil
   and manage their products.
2. **Delivery details:** is showing the ship-to recipient's name and address
   to distributors acceptable (needed for direct shipping)? Or do products
   ship to the business first?
3. **Who approves distributor products:** Executives only, or also specific
   sales users (the "Catalog approver" permission)?
4. **Approval limits:** starting values for max discount %, min margin % and
   max quote total without approval.
5. **Territories:** do distributors cover specific states? If two
   distributors carry the same product, should orders be routed by the ship-to
   state?
6. **Distributor payment:** does the business pay distributors per order from
   their uploaded invoices (as assumed), or on a monthly statement or
   commission basis?
7. **Sales tax:** is a manually set rate per quote acceptable for the MVP?
   In which states does the business collect tax?
8. **Single business or product:** is this app for your company only, or will
   it be offered to other businesses (SaaS)? This affects sign-up, billing
   and hosting.
9. **Accounting:** which accounting software is used today, and is an
   integration needed soon after the MVP?
10. **Products:** besides Food and Electronics, which types should be built in
    (e.g., clothing, cosmetics, household)? Are variants (sizes, flavors)
    needed in the MVP?
11. **Branding and name** of the application.
