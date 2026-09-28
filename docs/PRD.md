# Product Requirements Document: Lightweight CRM for Small Businesses & Freelancers

| Field        | Value                         |
|--------------|-------------------------------|
| Status       | Draft v0.1                    |
| Last updated | 2026-09-28                    |
| Owner        | sennuramamoorthy              |
| Scope        | MVP (Release 1)               |

---

## 1. Summary

A simple, fast CRM for freelancers and small businesses (1–10 users). It keeps
contacts and companies, deals in a visual pipeline, tasks and activities, and a
few dashboards in one place. Salesforce and HubSpot are built for large sales
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
5. **G5: Fast onboarding.** A new user can import contacts from CSV and create
   a first deal within 10 minutes.

### 3.2 Non-Goals (MVP)
- Marketing automation (email campaigns, drip sequences, landing pages).
- Customer support ticketing.
- Invoicing, payments and accounting (possible later integration).
- Two-way email/calendar sync (Phase 2).
- Native mobile apps (the MVP is a responsive web app).
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

### 6.6 Global
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
Deal  *─1 Stage, *─1 Company?, *─1 Contact (primary)?, *─1 User (owner)
Deal  1─* DealStageHistory
Task  *─1 User (assignee), polymorphic link → Contact | Company | Deal
Activity *─* {Contact, Company, Deal} (via ActivityLink), *─1 User (author)
Tag   *─* {Contact, Company, Deal}
CustomFieldDefinition 1─* CustomFieldValue (per record)
Notification *─1 User
```

Every table carries `workspace_id`, and every query is scoped by it.

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
| M4 – Reports & Dashboards | Home dashboard, pipeline + performance reports | 1.5 wks |
| M5 – Hardening & Beta | Global search, perf tuning, accessibility pass, E2E coverage, beta launch | 1.5 wks |

**Phase 2 candidates:** Gmail/Outlook two-way sync, calendar integration,
custom fields v2 and formulas, multiple pipelines, email templates, a public
REST API and webhooks, Zapier integration, a mobile app, and quotes/invoices.

## 12. Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| Scope creep toward "full" CRM | Hold to the non-goals; everything else goes to the Phase 2 backlog. |
| Tenant data leakage | Workspace scoping in the data-access layer, Postgres RLS, and automated cross-tenant tests. |
| Messy CSV imports | Column mapping, row-level validation report, dry-run preview, and undo of an import batch. |
| Low adoption because data entry is tedious | Quick-add forms, keyboard shortcuts, import, and (Phase 2) email sync. |

## 13. Open Questions

1. **Pricing model:** free tier plus per-seat pricing? Is billing (Stripe) in MVP scope?
2. **Hosting:** SaaS only, or also a self-hosted option?
3. **Data residency:** are any customers restricted to EU-only or a specific region?
4. **Custom fields:** keep them at P1, or promote to P0?
5. **Email digest and reminders:** which provider, and is SMS/WhatsApp ever needed?
6. **Branding and name** of the product.
