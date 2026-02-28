# 🏗️ Component Impact Analysis: Purchase Channel Governance — Proposal Center / Seller Experience

**Spec:** [Purchase_Channel_Governance_Seller_Experience_PRD.md](./Purchase_Channel_Governance_Seller_Experience_PRD.md)
**Analyzed against:** 119 Commerce Platform components across 22 domains, 28 interaction patterns
**Analysis Date:** 2026-02-27
**Prepared by:** GitHub Copilot (Commerce Component Impact Analyzer)

---

## Domain Relevance Gate

| Gate | Result |
|------|--------|
| DG1 — Commerce Domain | ✅ Pass — subscription lifecycle, proposal/quote creation, catalog offer visibility, sovereign cloud compliance |
| DG2 — System Interaction | ✅ Pass — Proposal Center, Catalog Hydration, Assets, PubSec Segment Framework all named |

---

## Feature Domain Detection

| # | Feature Domain | Confidence | Why |
|---|---------------|-----------|-----|
| 1 | **Quote / Proposal** | High | Primary delivery surface is Proposal Center / Quote Center; all FRs describe proposal creation, availability selection, and renewal defaults |
| 2 | **Catalog / Offers** | High | EST-linked availability (`SKU Category = ExtendedServiceTerm`), hidden-offer NCOE surfacing, catalog hydration context-awareness are load-bearing dependencies |
| 3 | **Subscription Lifecycle** | Medium | EST default renewal, renewal proposal execution, EST-to-base transition all affect how subscriptions are created and renewed |

Secondary: **Security / Authorization (Commerce)** — seller identity recognized by catalog for NCOE hidden-offer access.

---

## Impact Summary

| Level | Count | Components |
|:-----:|:-----:|-----------|
| 🔴 Direct | 6 | Proposal Center / Quote Center, Quote Service, BigCat / Pricing Engine, Assets Service, PMC, Telemetry & Logging |
| 🟠 Indirect | 8 | Quote Transactor, QuoteServices-PAP, GSM, Subscription RP, Recurrence Service, CLP, PAv2, Constraints Service |
| 🔵 Informational | 4 | Approvals Service, CLM Platform, Software RP, ELM |
| 🟡 Monitoring | 3 | PubSec Segment Framework, MEO, CPAS |
| ⚪ None | 98 | (all others) |

**Interaction Patterns Triggered:** IP-4, IP-5, IP-3, IP-24, IP-8, IP-26
**Total Components Impacted:** 21 / 119

---

## Detailed Component Impact

| # | Component | ID | Domain | Impact | Evidence |
|---|-----------|----|--------|:------:|---------|
| 1 | **Proposal Center / Quote Center** | QP-3 | Quote & Proposal | 🔴 | Named in every FR (FR-PC-01–15), all user scenarios, and the Capability Impact table as the primary delivery surface. Requirements describe new default behaviors, new blocking logic, new UI indicators, and hidden-offer surfacing. |
| 2 | **Quote Service (QS)** | QP-1 | Quote & Proposal | 🔴 | Quote Service backs Proposal Center. FR-PC-03 (block self-renewing SKU), FR-PC-06 (effective date locking), FR-PC-08 (cloud context identification), and FR-PC-15 (fail-closed) all require new validation logic in the availability picker and proposal creation APIs. Strong signal across all FRs. |
| 3 | **BigCat / Pricing Engine** | CP-1 | Catalog & Pricing | 🔴 | Named explicitly in Capability Impact table ("Catalog Hydration API — Modify (dependency)"). FR-PC-07 requires catalog to return hidden-offer license-based products for seller/proposal identity. FR-PC-08 requires EST configuration (`SKU Category = ExtendedServiceTerm`) to be returned per product. FR-PC-15 (fail-closed) is contingent on catalog hydration succeeding. An open item explicitly flags a dependency on the catalog team confirming correct caller-identity recognition. |
| 4 | **Assets Service** | CM-10 | Charge Management | 🔴 | Named explicitly in Capability Impact table: "Assets — Modify (dependency) — Validate and prevent creation of license-based assets with auto-renew configuration where the base product renews into itself." This is the defence-in-depth layer below Proposal Center's enforcement. Also E2E FR13 (asset-level validation) is listed as a dependency. |
| 5 | **PMC (Proposal Management Center)** | QP-4 | Quote & Proposal | 🔴 | PMC manages proposal lifecycle, validation, and execution. All seller-facing proposal workflows (Scenarios 1–6) flow through PMC. The availability picker, EST default selection, effective date enforcement, and proposal submission are PMC functions sitting above the Quote Service API layer. |
| 6 | **Telemetry & Logging** | — | Infrastructure | 🔴 | Named directly in Capability Impact table: "Telemetry & Logging — Modify." FR-PC-13 mandates logging of all EST enforcement decisions (cloud context, customer segment, proposal ID, product, outcome). FR-PC-14 requires 7-year immutable retention. NFR-PC-03 and NFR-PC-04 reinforce this. Specific storage and audit infrastructure must be implemented. |
| 7 | **Quote Transactor (QT)** | QP-2 | Quote & Proposal | 🟠 | When a proposal is accepted and executed, it flows through the Transactor's 28-publisher pipeline. New EST configuration fields on the quote must be carried through to the downstream publishers (particularly the MCAPI, GSM, and Office publishers that provision subscriptions with renewal instructions). Indirect via **IP-4** and **IP-24**. |
| 8 | **QuoteServices-PAP** | QP-9 | Quote & Proposal | 🟠 | Post-transaction events (status changes, document generation, notifications) flow through PAP. NCOE proposals and EST-enforced proposals will generate additional event types. Indirect via **IP-25** (PAP event routing triggered by IP-24). |
| 9 | **GSM (Global Subscription Manager)** | AS-2 | Account & Subscription | 🟠 | Subscription creation with EST renewal instructions (scheduledActions / renewal term configuration) requires GSM to correctly register the renewal intent. NCOE subscriptions must be created under the correct hidden-offer availability. Indirect via **IP-3** and **IP-4** cascade from Quote Transactor. |
| 10 | **Subscription RP** | AS-3 | Account & Subscription | 🟠 | Provisions Azure subscriptions as resources; EST renewal configuration must be represented at the subscription resource level. Indirect via **IP-3** cascade from GSM. |
| 11 | **Recurrence Service** | CM-13 | Charge Management | 🟠 | Manages the recurring execution schedule that fires at term end and converts EST subscriptions back to base product (or into the next EST term). Pattern **IP-8** (Scheduled Mid-Term Updates): Assets → Recurrence → CLP → PAv2 → Rating. The EST renewal execution path runs through Recurrence at term end. |
| 12 | **CLP (Charge Line Processing)** | CM-12 | Charge Management | 🟠 | Processes charge lines during the recurring EST renewal cycle. Indirect via **IP-8** cascade from Recurrence. |
| 13 | **PAv2** | CM-1 | Charge Management | 🟠 | Charge events from EST renewals flow through PAv2 to Rating/Orders/Purchase. Indirect via **IP-1** cascade from CLP. |
| 14 | **Constraints Service** | PO-1 | Constraints & Policies | 🟠 | Offer Discovery & Eligibility pattern (**IP-5**) is triggered by hidden-offer surfacing: BigCat → SaaS Hub RP → MCAPI Group → Constraints. Constraint enforcement gates what sellers can add to NCOE proposals; the existing channel restrictions must be consistent with the new hidden-offer surfacing behavior. |
| 15 | **Approvals Service** | AG-2 | Agreement Lifecycle | 🔵 | NCOE has a sovereign approval pattern (Microsoft + NCOE review) in Approvals Service. However, the spec explicitly puts exception/override workflows **out of scope**: "No exception request or approval workflow is required or permitted." NCOE proposals follow standard quote approval flows — no changes needed. Informational context only. |
| 16 | **CLM Platform** | AG-1 | Agreement Lifecycle | 🔵 | MCA Product Terms are cited as the legal basis for EST requirements. CLM manages MCA agreement lifecycle but no changes to CLM are required — the agreement terms already exist. Informational. |
| 17 | **Software RP** | FL-5 | Fulfillment | 🔵 | Out of Scope section explicitly excludes Azure non-license-based products. Software RP (L+SA, ESU) is not a target for this release. Informational. |
| 18 | **ELM** | AA-1 | Access & Authorization | 🔵 | ELM controls seller access scoping and managed proposal entitlements — relevant to NCOE seller access. However, the spec frames hidden-offer surfacing via catalog hydration context (caller app ID), not ELM access packages. No direct FR references ELM. Informational unless catalog context approach is confirmed insufficient. |
| 19 | **PubSec Segment Framework** | — | (external) | 🟡 | Named in Capability Impact table as a dependency for government customer segment determination (FR-PC-11). The spec does not change PubSec — it consumes it. Proposal Center Engineering should coordinate with the PubSec team to audit accuracy of the government segment signal. Awareness required, no code change expected. |
| 20 | **MEO (Microsoft Email Orchestrator)** | CC-1 | Customer Communications | 🟡 | New proposal workflows for EST enforcement and NCOE proposals may generate new customer/seller notification events. No direct FR targets MEO, but NFR-PC-05 (consistency across surfaces) implies communications should be consistent. Monitor — confirm whether new email templates are needed. |
| 21 | **CPAS** | AA-2 | Access & Authorization | 🟡 | Seller identity for NCOE hidden-offer catalog access is a trust boundary concern. If the catalog caller-identity approach relies on CPAS authorization scope, CPAS may need configuration updates for NCOE proposal contexts. Monitor pending catalog team confirmation on caller-identity mechanism. |

---

## Triggered Interaction Patterns

### IP-4: Quote-to-Transaction *(Primary)*

```
Proposal Center (🔴) → Quote Service (🔴) → Quote Transactor (🟠) → PMC (🔴)
→ Publishers (QT-28 publishers) → Assets Service (🔴) → PAv2 (🟠)
```

Every proposal acceptance triggers this pipeline. EST default and hidden-offer configurations must flow cleanly end-to-end through each component.

---

### IP-5: Offer Discovery & Eligibility

```
BigCat (🔴) → SaaS Hub RP → MCAPI Group → Constraints (🟠)
```

Triggered by NCOE hidden-offer surfacing (FR-PC-07). Catalog must return hidden products for seller context — all components in this pattern need to honor the new visibility rule.

---

### IP-3: Subscription Lifecycle

```
GSM (🟠) → Subscription RP (🟠) → ARM → Entra
```

Triggered when proposed subscriptions are created with EST renewal configuration attached.

---

### IP-24: Transactor Publisher Pipeline

```
Quote Service (🔴) → Transactor (🟠) → [28 publishers: Office, Azure Plan, M365, AGC, GSM…]
→ QuoteServices-PAP (🟠)
```

EST configuration and NCOE hidden-offer data must propagate through the publisher fan-out to correctly instruct GSM and M365 RP on renewal instructions.

---

### IP-8: Scheduled Mid-Term Updates *(downstream, at term end)*

```
Assets (🔴) → Recurrence (🟠) → CLP (🟠) → PAv2 (🟠) → Rating
```

EST renewal execution at term end runs through this pattern. Proposal Center's job is to set the configuration correctly at creation time; this pattern executes it later.

---

### IP-26: Teleport Cross-Cloud Quote Migration *(monitoring)*

```
Quote Service → QuoteServices-PAP TeleportOutgoing → Blob Storage
→ QuoteServices-PAP TeleportIncoming → Quote Service
```

NCOE clouds (DE-SOV, FR-SOV) are sovereign deployments. Proposal creation in a sovereign cloud context may involve cross-cloud quote routing — confirm whether Teleport is in the NCOE proposal path.

---

## ⚠️ Risk & Coverage Gaps

| # | Finding | Severity | Recommendation |
|---|---------|:--------:|---------------|
| 1 | **Catalog caller-identity for NCOE hidden offers is an open item** — FR-PC-07 requires hidden offers to appear for seller/proposal context, but an open question explicitly asks the catalog team to confirm that Proposal Center's app ID is correctly recognized. If it isn't, NCOE sellers cannot add products. | 🔴 High | Resolve open item with Catalog Team before Phase 2 engineering begins. Get confirmation in writing. |
| 2 | **Partner Center and CST are not in scope** — NFR-PC-05 requires consistent enforcement across Proposal Center, Partner Center, M365 Admin Center, and CST. This spec only covers Proposal Center. Without consistency, sellers may bypass Proposal Center restrictions by using Partner Center. | 🔴 High | Notify Partner Center PM and CST PM immediately. Separate PRDs may be needed. |
| 3 | **Telemetry / 7-year immutable log storage has no named infrastructure** — NFR-PC-04 requires tamper-evident, immutable storage with 7-year retention, but no specific storage infrastructure component is identified in the spec. | 🟠 Medium | Add an NFR or design note specifying the storage mechanism (e.g., Azure Immutable Blob Storage, Legal Hold policies). Assign to Platform/Telemetry team. |
| 4 | **Assets Service change scope is underspecified** — The Capability Impact table says Assets is "Modify (dependency)" but no FR in this spec explicitly states what Assets must change. The only reference is E2E FR13 which lives in the E2E spec. | 🟠 Medium | Add a Proposal Center-scoped FR for the Assets validation requirement, or explicitly note that Assets changes are owned by the E2E spec and tracked separately under ADO 362560. |
| 5 | **Monthly-term license-based products** — An open item asks whether EST applies to monthly-term products. If CELA confirms it does, FR-PC-01/02/03 scope may need to expand and additional catalog configuration will be required. | 🟠 Medium | Block this with a CELA decision (owner: John Mueller) before Phase 2 engineering closure. |
| 6 | **Concurrent renewal + transition proposals** — FR-PC-05 (renewal proposals default to EST) and FR-PC-06 (EST-to-base transition effective date lock) create an edge case when both proposal types exist simultaneously for the same subscription. No error handling case covers this. | 🟡 Low | Add an edge case to the Error Handling table. Confirm with Quote Center engineering whether concurrent proposals for the same subscription are blocked or handled sequentially. |
| 7 | **IP-26 Teleport for NCOE proposals** — Sovereign cloud proposals may require Teleport (cross-cloud quote migration). The spec doesn't mention Teleport. If Proposal Center in the NCOE cloud context routes through Teleport, its behavior with hidden-offer products needs validation. | 🟡 Low | Confirm with Quote Service architecture whether NCOE proposals traverse the Teleport path. If yes, add to integration test plan. |

---

## 📋 Team Notification Matrix

| Component | Impact | Owning Team / Contact | Action Required |
|-----------|:------:|----------------------|----------------|
| **Proposal Center / Quote Center** | 🔴 | CPX / Enablers / Quote Center — Sapna Keshari, Sangram Keshari Maharana (PM); Rama Kiran Katta (Eng) | Primary delivery. All FR-PC-01–15 must be implemented. UX changes required (badges, blocked-picker messaging, cloud-context indicators). |
| **Quote Service (backend)** | 🔴 | CPX / Enablers / Quote Center Engineering — Rama Kiran Katta | New validation rules for EST default, self-renewing SKU block, effective date lock, fail-closed behavior (FR-PC-03, FR-PC-06, FR-PC-08, FR-PC-15). |
| **BigCat / Catalog Team** | 🔴 | Catalog / CP-1 team | Must confirm: (1) EST configuration (`SKU Category = ExtendedServiceTerm`) published for all in-scope products before Phase 2, (2) Seller/proposal caller-identity is recognized for NCOE hidden-offer visibility. Resolve open item before engineering kickoff. |
| **Assets Service** | 🔴 | CPX / Assets / Fulfillment | Validate and reject asset creation with auto-renew config where base product renews into itself (E2E FR13). Confirm scoping with E2E release owner (ADO 362560). |
| **Constraints Service** | 🟠 | CPX / Constraints — Vamsi Krishna Rallabhandi | Confirm channel constraint rules are consistent with new NCOE hidden-offer surfacing. No code change expected but validation required. |
| **Quote Transactor + Transactor Publishers** | 🟠 | Quote Center Engineering / MCAPI team | EST configuration and NCOE hidden-offer data must flow correctly through the 28-publisher pipeline. Coordinate with GSM and Office publishers for correct renewal instruction at subscription creation. |
| **PubSec Segment Framework** | 🟡 | CPX / PubSec Segment team | Audit accuracy of government segment signal for public cloud + USGov proposals. Confirm Proposal Center can reliably call the segment API. No spec change expected. |
| **Partner Center** | ⚠️ | Partner Center PM (unnamed in spec) | NFR-PC-05 requires consistency. Partner Center must also enforce EST defaults and self-renewing SKU block for the same customer segments. Separate PRD or explicit out-of-scope required. |
| **CST (Commerce Support Tool)** | ⚠️ | CST PM (unnamed in spec) | Same as Partner Center — NFR-PC-05 consistency requirement. Support agents using CST to create proposals must see the same EST enforcement. |
| **M365 Admin Center** | ⚠️ | M365 Admin Center team | Phase 1 changes (Purchase Services blade visibility) are live. For Phase 2, confirm M365 Admin Center also enforces EST defaults and hidden-offer restrictions for government/NCOE customers (consistent with NFR-PC-05). |
| **Telemetry / Platform Engineering** | 🔴 | Platform / Telemetry team | Implement 7-year immutable, tamper-evident log storage for EST enforcement decisions (NFR-PC-04). Define storage infrastructure now — this has a long procurement/setup lead time. |
| **CPX / Sovereign Cloud (GC)** | — | John Mueller | Owner of three open items: (1) Monthly-term EST applicability, (2) PCD representation of EST default for government pricing audience, (3) Business planner guidance for catalog configuration. All block Phase 2 design closure. |

---

## Summary Assessment

This spec is well-structured and compliance-driven. The two critical risks requiring immediate action before engineering begins are:

1. **Catalog team confirmation on NCOE hidden-offer caller-identity** — without this, the entire NCOE seller catalog browse feature (FR-PC-07) is blocked.
2. **Partner Center / CST scope alignment** — NFR-PC-05 is a cross-surface consistency requirement that this spec doesn't own, creating a delivery gap if those surfaces aren't notified and scoped separately.

The core Proposal Center implementation (FR-PC-01–06, FR-PC-08–12) is well-specified and can proceed in parallel with dependency resolution. FR-PC-07 (NCOE hidden offers) and FR-PC-13/14 (telemetry/retention) should be tracked as Phase 2 gate items given their dependency on catalog and infrastructure decisions.
