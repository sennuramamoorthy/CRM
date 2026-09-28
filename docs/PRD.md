# Product Requirements Document: Lightweight CRM for Small Businesses & Freelancers

| Field        | Value                         |
|--------------|-------------------------------|
| Status       | Draft v0.2                    |
| Last updated | 2026-09-28                    |
| Owner        | sennuramamoorthy              |
| Scope        | MVP (Release 1)               |

---

## 1. Summary

A simple, fast CRM for freelancers and small businesses (1–10 users). It keeps
contacts and companies, deals in a visual pipeline, tasks and activities, a
product catalog, and a few dashboards in one place. Salesforce and HubSpot are built for large sales
organizations. This product is for people who sell on the side of doing the
work. It should be set up in under 10 minutes and need no admin.

## 2. Problem Statement

Freelancers and small businesses track clients across spreadsheets, email
inboxes, sticky notes and memory. As a result:

- Follow-ups get forgotten, and deals go cold.
- Nobody has a single view of a client's history (calls, emails, notes, deals).
- Owners can't answer basic questions: *"What's in my pipeline this month?"*,
  *"Who haven't I contacted in 30 days?"*
- Existing CRMs are too expensive, too complex, or take days to configure.

## 3. Goals & Non-Goals

### 3.1 Goals (MVP)
1. **G1: One place for client relationships.** Contacts, companies, deals and
   activities are linked and shown on a single timeline.
2. **G2: Never miss a follow-up.** Tasks carry due dates and reminders, and a
   "Today" view shows what needs attention.
3. **G3: Visible pipeline.** A drag-and-drop Kanban board with deal values and
   a weighted forecast.
4. **G4: Instant insight.** Out-of-the-box dashboards with no configuration.
5. **G5: Know what you sell.** A product catalog with categories and
   type-specific details (e.g., technical specs for electronics, ingredients
   and nutrition facts for food) that can be added to deals as line items.
6. **G6: Fast onboarding.** A new user can import contacts from CSV and create
   a first deal within 10 minutes.

### 3.2 Non-Goals (MVP)
- Marketing automation (email campaigns, drip sequences, landing pages).
- Customer support ticketing.
- Invoicing, payments and accounting (possible later integration).
- Two-way email/calendar sync (Phase 2).
- Native mobile apps (the MVP is a responsive web app).
- Inventory and stock management, warehouses, purchase orders and supplier
  management.
- E-commerce storefront or online ordering.
- Generating regulatory-compliant food labels (the catalog stores the data but
  does not certify compliance with labeling laws).
- Enterprise features: territories, complex role hierarchies, SSO/SAML, sandboxes.

## 4. Target Users & Personas

| Persona | Description | Key needs |
|---------|-------------|-----------|
| **Fiona the Freelancer** | Solo designer/consultant with 20–100 active clients. | Remember who to follow up with, track proposals, see monthly income pipeline. |
| **Sam the Small Business Owner** | Runs a 3–8 person agency or services firm. | Shared client list, assign deals/tasks to staff, see team pipeline and performance. |
| **Tara the Team Member** | Salesperson or account manager at Sam's company. | Quickly log calls/meetings, see their own tasks and deals. |

## 5. User Stories

### Contacts & Companies
- As a user, I can create, edit and delete contacts (people) and companies
  (organizations), and link a contact to a company.
- As a user, I can import contacts and companies from CSV and export them to CSV.
- As a user, I can search, filter (by tag, owner, company, last-contacted date)
  and sort my contacts.
- As a user, I can tag records and add custom fields.
- As a user, I can see a contact's full timeline: notes, activities, tasks and deals.

### Deals & Pipeline
- As a user, I can create a deal with a value, expected close date, stage,
  owner and linked contact/company.
- As a user, I can drag deals between stages on a Kanban board.
- As an owner, I can customize pipeline stages and their win probabilities.
- As a user, I can mark a deal Won or Lost (with a reason).
- As a user, I can switch between board and list views of deals.

### Tasks & Activities
- As a user, I can create tasks with a due date/time, priority and assignee,
  linked to a contact, company or deal.
- As a user, I get an in-app (and optionally email) reminder when a task is due.
- As a user, I can log activities (call, meeting, email, note) against a record.
- As a user, I see a "Today" view of overdue and due-today tasks.

### Reports & Dashboards
- As a user, I see a home dashboard with pipeline value, weighted forecast,
  deals won this month, overdue tasks and recent activity.
- As an owner, I can see win rate, average deal size, sales cycle length and
  per-member performance for a chosen date range.
- As a user, I can see stale contacts (not contacted in N days).

### Products & Catalog
- As a user, I can open a Products page listing all products, with search and
  filters by product type, category, status and tag.
- As a user, I can create a product of a given **product type** (Food,
  Electronics, General, or a custom type), and the form shows the fields that
  belong to that type.
- As an owner, I can create, rename, nest, reorder and delete **categories**
  (e.g., *Food › Beverages › Juices*) and assign products to them.
- As an owner, I can create custom product types and define their fields
  (e.g., a "Clothing" type with size, material and care instructions).
- As a user, I can record **technical specifications** for an electronics
  product (e.g., processor, memory, battery, connectivity, power rating).
- As a user, I can record **ingredients, allergens and nutritional facts** for
  a food product.
- As a user, I can record **weight and dimensions** for any product, for both
  the product itself and its package.
- As a user, I can add products to a deal as line items with quantity, unit
  price and discount, and the deal value is calculated from them.
- As a user, I can import and export products via CSV.

### Workspace & Users
- As an owner, I can sign up, create a workspace, and invite team members by email.
- As an owner, I can assign roles (Owner, Member).
- As a user, I can sign in with email/password or Google.

## 6. Functional Requirements

Priority: **P0** = must have for MVP, **P1** = should have, **P2** = nice to have.

### 6.1 Authentication & Workspace
| ID | Requirement | Priority |
|----|-------------|----------|
| AUTH-1 | Sign up / sign in with email + password, with email verification. | P0 |
| AUTH-2 | Sign in with Google OAuth. | P1 |
| AUTH-3 | Password reset via email. | P0 |
| WS-1 | Each account belongs to a workspace; all data is isolated per workspace (multi-tenant). | P0 |
| WS-2 | Owner can invite members by email; invites expire after 7 days. | P0 |
| WS-3 | Roles: **Owner** (full access, billing, settings, user management) and **Member** (CRUD on CRM data, no settings). | P0 |
| WS-4 | Workspace settings: name, currency, timezone, date format. | P0 |

### 6.2 Contacts & Companies
| ID | Requirement | Priority |
|----|-------------|----------|
| CON-1 | Contact fields: first/last name, email(s), phone(s), job title, company, address, owner, tags, source, notes, created/updated timestamps. | P0 |
| CON-2 | Company fields: name, domain/website, industry, size, phone, address, owner, tags. | P0 |
| CON-3 | Many contacts per company; a contact belongs to at most one company. | P0 |
| CON-4 | List view with search (name, email, company), filters, sort and pagination. | P0 |
| CON-5 | Detail page with a unified activity timeline and related deals/tasks. | P0 |
| CON-6 | CSV import with column mapping, preview, validation errors and duplicate detection (by email). | P0 |
| CON-7 | CSV export of the current filtered list. | P0 |
| CON-8 | Custom fields (text, number, date, dropdown, checkbox) on contacts, companies and deals. | P1 |
| CON-9 | Merge duplicate contacts. | P1 |
| CON-10 | Bulk actions: tag, assign owner, delete. | P1 |
| CON-11 | "Last contacted" date derived from the latest logged activity. | P0 |

### 6.3 Deals & Pipeline
| ID | Requirement | Priority |
|----|-------------|----------|
| DEAL-1 | Deal fields: title, value, currency, stage, probability, expected close date, owner, primary contact, company, status (Open/Won/Lost), lost reason. | P0 |
| DEAL-2 | Kanban board: columns per stage showing deal count and total value; drag and drop changes the stage. | P0 |
| DEAL-3 | Default pipeline: Lead → Qualified → Proposal → Negotiation → Won / Lost. | P0 |
| DEAL-4 | Owner can add, rename, reorder and delete stages and set each stage's default probability. | P0 |
| DEAL-5 | List/table view with filters (owner, stage, close date, status). | P0 |
| DEAL-6 | Stage change history is recorded (for sales cycle and conversion reports). | P0 |
| DEAL-7 | Multiple pipelines. | P2 |

### 6.4 Tasks & Activities
| ID | Requirement | Priority |
|----|-------------|----------|
| TASK-1 | Task fields: title, description, due date/time, priority (Low/Med/High), assignee, status (Open/Done), linked record (contact/company/deal). | P0 |
| TASK-2 | "My Tasks" view grouped by Overdue / Today / Upcoming / No date. | P0 |
| TASK-3 | In-app notifications for due and assigned tasks. | P0 |
| TASK-4 | Daily email digest of due and overdue tasks (opt-in). | P1 |
| TASK-5 | Recurring tasks. | P2 |
| ACT-1 | Log activities of type Call, Meeting, Email, Note, with date, duration (optional), body and linked records. | P0 |
| ACT-2 | Activities appear on the timeline of every linked record. | P0 |
| ACT-3 | Rich-text notes with @mentions of team members (mention triggers a notification). | P1 |

### 6.5 Reports & Dashboards
| ID | Requirement | Priority |
|----|-------------|----------|
| REP-1 | Home dashboard: open pipeline value, weighted forecast (Σ value × probability), deals won/lost this month, overdue task count, recent activity feed. | P0 |
| REP-2 | Pipeline report: value and count by stage. | P0 |
| REP-3 | Sales performance: win rate, average deal size, average sales cycle (days), by owner and date range. | P0 |
| REP-4 | Activity report: activities logged by type and user over time. | P1 |
| REP-5 | Stale contacts report (no activity in N days, N configurable). | P1 |
| REP-6 | Export report data to CSV. | P1 |
| REP-7 | Members see their own numbers by default and can switch to team view; owners see everyone. | P0 |

### 6.6 Products & Catalog

#### Product types
A **product type** is a template that decides which detail fields a product
has. Types answer "what kind of thing is this?" and categories answer "where
does it sit in my catalog?". They are independent: a *Food* product can sit in
a *Gift Hampers* category next to an *Electronics* product.

| ID | Requirement | Priority |
|----|-------------|----------|
| PT-1 | Built-in types are **Food**, **Electronics** and **General** (common fields only). Built-in types can't be deleted, but their fields can be extended. | P0 |
| PT-2 | Owners can create custom product types with a name, icon and a list of field definitions. | P1 |
| PT-3 | Field definition: label, key, data type (text, long text, number, number + unit, boolean, date, single select, multi select, URL), unit options, required flag, help text and display group (e.g., "Display", "Battery"). | P0 for built-in types, P1 for custom types |
| PT-4 | A product's type is chosen at creation. Changing it later warns that values of fields the new type doesn't have will be hidden, and those values are kept (not deleted) so the change can be reversed. | P1 |
| PT-5 | A type that is in use can't be deleted; it can be archived, which hides it from new-product forms. | P1 |

#### Categories
| ID | Requirement | Priority |
|----|-------------|----------|
| CAT-1 | Owners can create categories with a name, optional description and optional parent, forming a tree up to 5 levels deep. | P0 |
| CAT-2 | Categories can be renamed, reordered (drag and drop) and moved to another parent; a category can't be moved under its own descendant. | P0 |
| CAT-3 | A product has one primary category and may belong to additional categories. | P0 (primary), P1 (additional) |
| CAT-4 | Deleting a category requires choosing what happens to its products and subcategories: move them to another category or to "Uncategorized". Products are never deleted with a category. | P0 |
| CAT-5 | Category names are unique among siblings (case-insensitive). | P0 |
| CAT-6 | The Products list can be filtered by category, including products in subcategories. | P0 |

#### Common product fields (all types)
| ID | Requirement | Priority |
|----|-------------|----------|
| PRD-1 | Name, SKU (unique per workspace), product type, category, short description, long description (rich text), status (Draft / Active / Archived), tags, owner. | P0 |
| PRD-2 | Pricing: unit price, currency (defaults to the workspace currency), unit of sale (each, kg, pack, box…), optional cost price, tax rate. | P0 |
| PRD-3 | Up to 10 images per product, with one marked as primary; JPEG/PNG/WebP, max 5 MB each. | P1 |
| PRD-4 | Barcode fields: GTIN/EAN/UPC (validated check digit), manufacturer part number, brand, manufacturer, country of origin. | P1 |
| PRD-5 | Attachments (e.g., datasheets, certificates, PDFs), max 20 MB each. | P2 |

#### Weights & dimensions (all types)
| ID | Requirement | Priority |
|----|-------------|----------|
| DIM-1 | **Product** measurements: net weight, length, width, height. | P0 |
| DIM-2 | **Package** (shipping) measurements: gross weight, length, width, height, and units per package. | P0 |
| DIM-3 | Users enter values in either metric (g, kg, mm, cm, m) or imperial (oz, lb, in, ft) units. Values are stored in base units (grams, millimetres) and shown in the workspace's default unit system, with the original unit remembered. | P0 |
| DIM-4 | Volume is calculated from dimensions and shown read-only; liquids can also record a net volume (ml, l, fl oz). | P1 |
| DIM-5 | Values must be positive numbers; gross weight smaller than net weight shows a warning, not an error. | P0 |

#### Electronics details
| ID | Requirement | Priority |
|----|-------------|----------|
| ELE-1 | Default spec fields: brand, model number, power source, voltage (V), power consumption (W), battery capacity (mAh), connectivity (multi select: Wi-Fi, Bluetooth, USB-C, Ethernet, NFC, cellular…), color, warranty period (months), certifications (CE, FCC, UL, RoHS…). | P0 |
| ELE-2 | A free-form **spec table** of grouped name–value–unit rows (e.g., group "Display": Size = 6.1 in, Resolution = 2532 × 1170), so any spec can be recorded without a schema change. | P0 |
| ELE-3 | Specs can be copied from another product to speed up entry of similar models. | P1 |
| ELE-4 | Products can be compared side by side on their specs (up to 4). | P2 |

#### Food details
| ID | Requirement | Priority |
|----|-------------|----------|
| FOOD-1 | **Ingredients**: an ordered list (in descending order of weight, as printed on labels), each with a name and an optional percentage; also a single "ingredients statement" text field for pasting a label as printed. | P0 |
| FOOD-2 | **Allergens**: for each of the 14 EU major allergens (which cover the 9 US major allergens), mark *Contains*, *May contain (traces)* or *Free from*. Allergens are shown prominently on the product page. | P0 |
| FOOD-3 | **Nutrition facts**: serving size (value + unit), servings per package, and values per 100 g/100 ml **and** per serving for energy (kcal and kJ), total fat, saturated fat, trans fat, cholesterol, carbohydrates, total sugars, added sugars, dietary fibre, protein, salt and sodium. | P0 |
| FOOD-4 | Entering energy in kcal fills kJ (× 4.184) and vice versa; entering salt fills sodium (÷ 2.5) and vice versa; entering per-100 g values plus serving size fills per-serving values. Filled values can be overridden. | P1 |
| FOOD-5 | Optional micronutrients (vitamins and minerals) as extra rows with amount, unit and % daily value. | P1 |
| FOOD-6 | Dietary labels (multi select): vegetarian, vegan, gluten-free, lactose-free, halal, kosher, organic, non-GMO. | P0 |
| FOOD-7 | Storage and shelf life: storage instructions, temperature range, shelf life (days), shelf life after opening (days). | P0 |
| FOOD-8 | Validation: a nutrient in a sub-group can't be more than its parent (e.g., saturated fat ≤ total fat, sugars ≤ carbohydrates); per-100 g macronutrients can't add up to more than 100 g. Violations are shown as errors. | P0 |
| FOOD-9 | The data is informational only; the UI shows a note that the business is responsible for label compliance. | P0 |

#### Products page & deals
| ID | Requirement | Priority |
|----|-------------|----------|
| PROD-1 | Products page: a table view (image, name, SKU, type, category, price, status) and a card/grid view, with a category tree in a side panel. | P0 |
| PROD-2 | Search by name, SKU, barcode and brand; filter by type, category, status, tag and price range; sort by any column. | P0 |
| PROD-3 | Product detail page with tabs: Overview, Details (type-specific fields), Weights & dimensions, Deals (the deals this product appears in). | P0 |
| PROD-4 | Duplicate a product (copies everything except SKU and barcode). | P1 |
| PROD-5 | Bulk actions: change category, change status, add tag, delete. | P1 |
| PROD-6 | CSV import/export per product type, with type-specific columns included (nested data such as ingredients and specs are exported as JSON columns). | P1 |
| PROD-7 | Deal line items: product, quantity, unit price (defaults to the product price, editable), discount (% or amount), line total. The deal value can be computed from line items or entered manually. | P0 |
| PROD-8 | Products that appear on deals can't be deleted, only archived. Archived products stay visible on existing deals but can't be added to new ones. | P0 |
| PROD-9 | Line items keep a snapshot of the product name, SKU and price at the time they were added, so later product edits don't change past deals. | P0 |
| PROD-10 | Report: revenue and quantity won by product and by category. | P1 |

### 6.7 Global
| ID | Requirement | Priority |
|----|-------------|----------|
| GLB-1 | Global search (Cmd/Ctrl+K) across contacts, companies and deals. | P0 |
| GLB-2 | Audit fields (created by/at, updated by/at) on all records. | P0 |
| GLB-3 | Soft delete with 30-day restore from a Trash view. | P1 |
| GLB-4 | Responsive layout usable on mobile browsers. | P0 |

## 7. Data Model (Conceptual)

```
Workspace 1─* User (via Membership: role)
Workspace 1─* Company 1─* Contact
Workspace 1─* Pipeline 1─* Stage
Workspace 1─* ProductType 1─* FieldDefinition
Workspace 1─* Category (self-referencing parent_id → tree)
Product *─1 ProductType, *─1 Category (primary), *─* Category (additional)
Product 1─* ProductImage
Product: common columns + weights/dimensions in base units
         + `attributes` JSONB validated against the type's FieldDefinitions
FoodDetails 1─1 Product: ingredients[], allergens, nutrition (per 100 g / per serving)
ElectronicsDetails 1─1 Product: spec rows (group, name, value, unit)
Deal 1─* DealLineItem *─1 Product (snapshot of name, SKU, price)
Deal  *─1 Stage, *─1 Company?, *─1 Contact (primary)?, *─1 User (owner)
Deal  1─* DealStageHistory
Task  *─1 User (assignee), polymorphic link → Contact | Company | Deal
Activity *─* {Contact, Company, Deal} (via ActivityLink), *─1 User (author)
Tag   *─* {Contact, Company, Deal}
CustomFieldDefinition 1─* CustomFieldValue (per record)
Notification *─1 User
```

Every table carries `workspace_id`, and every query is scoped by it.

**Why product details are modeled this way:** common fields that are filtered,
sorted and reported on (price, SKU, weight, dimensions) are real columns. Food
and electronics details have stable, well-known structure and validation rules,
so they get their own typed tables. Custom-type fields go in a JSONB
`attributes` column validated against the type's field definitions. This avoids
both a rigid table per type and an entity–attribute–value table that is slow
to query. JSONB can be indexed with GIN for filtering on custom fields.

## 8. Non-Functional Requirements

| Area | Requirement |
|------|-------------|
| Performance | p95 page load < 1.5 s and p95 API response < 300 ms for workspaces with up to 50k contacts and 10k deals. |
| Scalability | Support 10k workspaces in the MVP infrastructure; horizontal scaling of the stateless app tier. |
| Security | HTTPS only; passwords hashed with Argon2/bcrypt; tenant isolation enforced at the data-access layer (and ideally Postgres Row-Level Security); OWASP Top 10 mitigations; rate limiting on auth endpoints. |
| Privacy / Compliance | GDPR-ready: data export per workspace, account and workspace deletion, a record of data processing. Personal data is not used for anything beyond providing the service. |
| Availability | 99.5% monthly uptime target; daily backups with 30-day retention and point-in-time recovery. |
| Accessibility | WCAG 2.1 AA for core flows; full keyboard navigation of the pipeline board. |
| Browser support | Latest 2 versions of Chrome, Firefox, Safari and Edge. |
| Observability | Structured JSON logs with request/trace IDs; error tracking; basic product analytics. |
| i18n | English UI for the MVP; currency, date and timezone set per workspace; strings externalized for later translation. |

## 9. Recommended Technical Approach

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Language | TypeScript end to end | One language across the stack and shared types; easy to hire for. |
| Web framework | Next.js (App Router) with React | SSR/streaming, server actions and API routes in one deployable. |
| UI | Tailwind CSS + shadcn/ui; dnd-kit for the Kanban board; Recharts for charts | Fast to build and accessible by default. |
| Database | PostgreSQL | Relational data, full-text search (`tsvector`) and Row-Level Security. |
| ORM / migrations | Prisma (or Drizzle) | Type-safe queries and migrations. |
| Auth | Auth.js (NextAuth) with credentials + Google | Built-in session handling and OAuth. |
| Background jobs | pg-boss (Postgres-backed queue) | Reminders, digests and CSV imports with no extra infrastructure. |
| Email | Transactional provider (e.g., Resend / Postmark / SES) | Invites, password resets, reminders. |
| Validation | Zod | Shared schemas between client and server. |
| Testing | Vitest (unit), Playwright (E2E) | Fast, TypeScript-native. |
| Deployment | Docker image; Vercel or Fly.io/Render + managed Postgres | Simple operations for a small team. |
| CI | GitHub Actions: lint, typecheck, test, build | Standard and free for this scale. |

## 10. Success Metrics

| Metric | Target (3 months post-launch) |
|--------|-------------------------------|
| Time to first value (signup → first deal or import) | Median < 10 min |
| Activation (≥ 10 contacts and ≥ 1 deal within 7 days) | ≥ 40% of signups |
| Weekly active users / total users | ≥ 50% |
| Tasks completed on or before the due date | ≥ 60% |
| 30-day retention of workspaces | ≥ 35% |

## 11. Release Plan / Milestones

| Milestone | Scope | Est. |
|-----------|-------|------|
| M0 – Foundation | Repo setup, CI, auth, workspaces, invites, roles, app shell, design system | 2 wks |
| M1 – Contacts & Companies | CRUD, list/search/filter, detail + timeline, CSV import/export | 2 wks |
| M2 – Deals & Pipeline | Deal CRUD, Kanban board, stage config, stage history, list view | 2 wks |
| M3 – Tasks & Activities | Tasks, My Tasks/Today, activity logging, notifications, reminders | 2 wks |
| M3b – Products & Catalog | Categories, built-in product types, product CRUD, weights & dimensions, food and electronics details, Products page, deal line items | 2.5 wks |
| M4 – Reports & Dashboards | Home dashboard, pipeline + performance reports | 1.5 wks |
| M5 – Hardening & Beta | Global search, perf tuning, accessibility pass, E2E coverage, beta launch | 1.5 wks |

**Phase 2 candidates:** inventory/stock levels, product variants (size,
color), price lists, Gmail/Outlook two-way sync, calendar integration,
custom fields v2 and formulas, multiple pipelines, email templates, a public
REST API and webhooks, Zapier integration, a mobile app, and quotes/invoices.

## 12. Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| Scope creep toward "full" CRM | Hold to the non-goals; everything else goes to the Phase 2 backlog. |
| Tenant data leakage | Workspace scoping in the data-access layer, Postgres RLS, and automated cross-tenant tests. |
| Messy CSV imports | Column mapping, row-level validation report, dry-run preview, and undo of an import batch. |
| Product detail entry is slow (nutrition and spec tables have many fields) | Copy specs from a similar product, duplicate products, auto-calculated values (kJ, sodium, per serving), and CSV import. |
| Wrong nutrition or allergen data causes harm or liability | Validation rules, prominent allergen display, and a clear note that label compliance is the business's responsibility. |
| Low adoption because data entry is tedious | Quick-add forms, keyboard shortcuts, import, and (Phase 2) email sync. |

## 13. Open Questions

1. **Pricing model:** free tier plus per-seat pricing? Is billing (Stripe) in MVP scope?
2. **Hosting:** SaaS only, or also a self-hosted option?
3. **Data residency:** are any customers restricted to EU-only or a specific region?
4. **Custom fields:** keep them at P1, or promote to P0?
5. **Email digest and reminders:** which provider, and is SMS/WhatsApp ever needed?
6. **Branding and name** of the product.
7. **Products:** are variants (e.g., sizes or colors of one product) needed in
   the MVP? They are currently Phase 2.
8. **Products:** is stock/inventory tracking needed at all, or is the catalog
   only for quoting and deals?
9. **Products:** which nutrition format should be the default: EU (per 100 g,
   kJ + kcal, salt) or US FDA (per serving, calories, sodium, % daily value)?
   The draft stores both.
10. **Products:** besides Food and Electronics, what other built-in types should
    ship (e.g., clothing, cosmetics, services)?
