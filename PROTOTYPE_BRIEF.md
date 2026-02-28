# Proposal Center – UX Prototype Brief

> Generated following the **PRD Prototype Playbook** methodology

---

## 1. Product Identity

| Field | Value |
|---|---|
| **Product Name** | Proposal Center (Quote Center) |
| **Codename** | SC.L2O.Mepla.Simple |
| **Platform** | Web (Dynamics 365 / MSX Shell) |
| **Design System** | Fluent UI / Dynamics 365 Shell |
| **Version** | Prototype v1.0 |

---

## 2. Target Users

| Persona | Description |
|---|---|
| **Primary** | Microsoft Field Sellers / Account Executives |
| **Secondary** | Deal Approvers / Pricing Managers |
| **Tertiary** | Partner Center Operators (CSP indirect) |

---

## 3. Design Style

- **Shell**: Dynamics 365 dark navy top nav (#1b1a27) with waffle grid, logo, search, avatar
- **Typography**: Segoe UI, 13–14px body, 18–20px headings
- **Primary Color**: #0078d4 (Microsoft Blue)
- **Border Radius**: 2px (Fluent UI standard)
- **Elevation**: 3-tier shadow system (sm, md, panel)
- **Components**: Fluent UI-inspired — data tables, command bars, status badges, slide-in panels, breadcrumbs, tab bars, wizard steps, finder panes, toggle switches

---

## 4. Screens in Scope

| # | Screen | File | Description |
|---|---|---|---|
| 1 | **Overview Dashboard** | `index.html` | Landing page with metrics, quick actions, recent proposals, favorite customers |
| 2 | **My Proposals** | `proposals.html` | Filterable/searchable list with tabs (My Proposals / Needs My Approval) |
| 3 | **New Proposal Wizard** | `new-proposal.html` | 5-step wizard: Channel → Market → Cloud → Details → Review |
| 4 | **Quote Editor – Products** | `quote-editor.html` | Dual-pane editor with Product Finder, line items table, details/config pane |
| 5 | **Quote Editor – Agreement** | `quote-terms.html` | Term Finder with amendment cards, clause previews, configuration panel |
| 6 | **Review & Publish** | `review-publish.html` | Summary sections, signatory forms, transaction options, approval history, publish action |
| 7 | **Customer 360** | `customer.html` | Full customer view with 7 tabs: Overview, Agreements, Concessions, Subscriptions, Billing, History, About |
| 8 | **Customer Search** | `customers.html` | Search with filters (segment, geography), result cards with stats & quick actions |

---

## 5. Primary User Flow

```
Overview Dashboard
    ├─→ "New Proposal" → New Proposal Wizard → Quote Editor (Products)
    ├─→ Recent Proposals → Quote Editor (Products)
    └─→ Favorite Customers → Customer 360

My Proposals
    └─→ Click proposal → Quote Editor (Products)
                              ├─→ Products tab (add/configure/price)
                              ├─→ Agreement tab (add terms/amendments)
                              └─→ Review & Publish (verify → publish)

Customers
    └─→ Search → Customer 360
                    ├─→ Overview (metrics, recent proposals, concessions)
                    ├─→ Agreements (MCA, EA details)
                    ├─→ Concessions (MACC/CACO progress)
                    ├─→ Subscriptions (active subs table)
                    ├─→ Billing Accounts
                    ├─→ History (activity timeline)
                    └─→ About (org details, contacts, account team)
```

---

## 6. Global Components

| Component | Description |
|---|---|
| **Top Nav** | Dark navy bar with Dynamics 365 logo, app name, global search, help/settings/notifications/avatar |
| **Sidebar Nav** | 220px left nav with Overview, Proposals, Customers, Analytics, Settings |
| **Status Badges** | Draft (gray), Active (blue), Pending (orange), Published (green), Expired (red) |
| **Command Bar** | Action buttons for save, submit, approve, share, etc. |
| **Data Tables** | Sortable, hoverable rows with link-cells and badges |
| **Slide-in Panels** | Right-side panels for details/config (320–500px) |
| **Prototype Watermark** | Fixed bottom-right "PROTOTYPE — Not Production" label |

---

## 7. Dummy Data

| Entity | Examples |
|---|---|
| **Customer** | Contoso Corporation, Contoso Ltd (UK), Contoso GmbH, Contoso Pharmaceuticals |
| **Proposals** | Enterprise Azure Migration FY26, M365 E5 Renewal, Azure DevOps Expansion |
| **Products** | Microsoft 365 E5, Azure Plan, Azure Reserved VM Instances, Dynamics 365 Sales |
| **User** | Alex Johnson (Account Executive) |
| **Approver** | Maria Lopez |
| **Signatory** | Jane Doe, Robert Smith (Contoso) |

---

## 8. Key Interactions

- **Product Finder**: Search products, expand categories, click + to add to line items
- **Term Finder**: Search terms, add amendments, configure clause parameters
- **Line Item Config**: Select row → details pane shows pricing, quantity, discount, term controls
- **Tab Navigation**: Products ↔ Agreement tabs in quote editor
- **Wizard Flow**: 5-step sequential with back/next, step indicator, skip-to-step
- **Customer Tabs**: 7 tabs with content switching (Overview through About)
- **Filter & Search**: Proposals list filtering by status, search by name/customer
- **Publish Confirmation**: Dialog confirmation before publishing to customer

---

## 9. Source Codebase Reference

Built from analysis of:
- `SC.L2O.Mepla.Simple` (Frontend) — React 17, TypeScript, Redux, Apollo Client, Fluent UI
- `SC.L2O.Mepla.Backend` (Backend) — Azure Functions, GraphQL (Apollo Server), TypeScript
- Key source files: `App.tsx`, `routes.ts`, `Quote.tsx`, `Editor.tsx`, `ProductFinder`, `TermFinder`, `ReviewAndPublish.tsx`, `Customer.tsx`
- Automated test locators: `QuoteCenterDriverPage.ts` for comprehensive UI element mapping

---

*This prototype is for demonstration and stakeholder review purposes only. It contains no real customer data or business logic.*
