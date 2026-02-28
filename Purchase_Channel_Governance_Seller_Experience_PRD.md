# Product Specification: Purchase Channel Governance — Proposal Center / Quote Center Seller Experience

**Last updated:** 2026-02-24

**Authored by:** Hiren Rupani

**Status:** Draft

**Links:**

- E2E Release Spec: [Purchase_Channel_Governance_spec.md](./commerce-docs/internalDocs/product_management/documents/Sovereign%20Cloud/Purchase_Channel_Governance/Purchase_Channel_Governance_spec.md)
- E2E One-Pager: [Purchase_Channel_Governance.md](./commerce-docs/internalDocs/product_management/documents/Sovereign%20Cloud/Purchase_Channel_Governance/Purchase_Channel_Governance.md)
- ADO Release: [362560](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems/edit/362560)
- ADO Scenario (EST / Proposal Center): [450791](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems/edit/450791)

## Key Roles

| Team | Role | Name |
|------|------|------|
| CPX / Enablers / Quote Center | PM | Sapna Keshari |
| CPX / Enablers / Quote Center | PM | Sangram Keshari Maharana |
| CPX / Enablers / Quote Center | Engineering | Rama Kiran Katta |
| CPX / Sovereign Cloud | GC (PM) | John Mueller |
| CPX / Constraints | GC (Eng) | Vamsi Krishna Rallabhandi |

## Change Log

| Date | Author | Changes | Reviewed / Approved By |
|------|--------|---------|------------------------|
| 2026-02-24 | Hiren Rupani | Initial draft — Proposal Center / Seller Experience scoped spec derived from E2E release spec | |

---

## Overview

This specification defines Proposal Center / Quote Center requirements for the Purchase Channel Governance release. The release introduces compliance controls for sovereign clouds that directly change how sellers create and manage proposals for license-based products. Proposal Center is the **exclusive** transaction surface for customers in NCOE clouds (DE-SOV, FR-SOV) and a critical enforcement surface for EST default renewal across all clouds.

The two primary Proposal Center obligations from the E2E release are:

1. **EST Default Renewal Enforcement (all clouds):** Proposal Center must default to Extended Service Term (EST)-linked availability for all government license-based proposals (public cloud, USGov, USSec, USNat) and for all license-based proposals in NCOE (all customers). Sellers must be blocked from selecting an availability where the base product renews into itself.

2. **NCOE Proposal-Only Model:** In NCOE clouds (DE-SOV, FR-SOV), all license-based products are published as hidden offers. Sellers can browse and add these hidden products to proposals; customers have no self-serve purchase or management path and must transact via proposals.

---

## Summary

The Purchase Channel Governance release addresses active compliance escalations and contract obligations in sovereign clouds. Proposal Center changes are scoped to two delivery phases:

- **Phase 1 (January 29, 2026):** Policy controls — no Proposal Center changes required.
- **Phase 2 (April 17, 2026):** Catalog-driven persona controls + EST default renewal enforcement in Proposal Center.

Proposal Center must be updated to:
- Default to EST-linked availability at proposal creation and renewal for government customers (all clouds) and all customers (NCOE).
- Block seller selection of any availability where the base product renews into itself.
- Surface hidden-offer license-based products in seller catalog browse for NCOE proposals, while those same products remain invisible to customers.
- Enforce correct effective dating for EST-to-base-product transition proposals (1st of the following month).
- Display clear cloud-context indicators and EST-default indicators in the seller UI.

---

## Problem Statement

### Compliance and Legal Risk

Microsoft Customer Agreement (MCA) Product Terms explicitly state:

> *"Online services subscriptions for government and academic customers will not be automatically renewed unless Customer chooses the auto-renewal option."*

Government entities cannot legally pay for services they have not explicitly committed to purchasing. Without Proposal Center enforcement:

- Sellers can today select auto-renewing SKUs when creating government proposals, violating MCA terms.
- Renewal proposals created before term-end can inadvertently set subscriptions to renew into themselves, creating compliance gaps.
- NCOE cloud operators (Delos for DE-SOV, Bleu for FR-SOV) have a formal requirement that all license-based purchases and changes flow through seller proposals — a requirement the current Proposal Center does not enforce.

### Current State Gaps in Proposal Center

| Gap | Impact |
|-----|--------|
| No EST default renewal at proposal creation for government customers | MCA non-compliance; government customers may be auto-billed |
| Seller can select auto-renewing SKU for government proposals | Compliance violation; must be blocked |
| NCOE hidden-offer products not surfaced for sellers | Sellers cannot create proposals for NCOE license-based products |
| Renewal proposals do not default to EST-linked availability | Subscriptions renew into base product, violating NCOE operator requirements |
| EST-to-base transition proposals have no enforced effective date defaulting | Customers may be transitioned before completing the EST month |

---

## Solution Summary

Proposal Center implements a cloud-aware, catalog-driven approach:

1. **EST Default Renewal:** At proposal creation and renewal, Proposal Center reads the catalog EST configuration (`SKU Category = ExtendedServiceTerm`) and automatically selects the EST-linked availability as the default. The seller sees a clear indicator that EST is the default renewal behavior.

2. **Self-Renew Blocking:** The availability picker hides or disables any option where the base product renews into itself—for government customers in public cloud/USGov/USSec/USNat, and for all customers in NCOE.

3. **NCOE Seller Catalog Access:** Proposal Center's catalog browse calls use the seller/proposal context identity, which causes the catalog to return hidden-offer products for NCOE clouds. These products are surfaced to sellers but remain invisible to customers browsing M365 Admin Center.

4. **EST-to-Base Transition Date Enforcement:** When a seller creates a proposal to move a customer from an EST subscription back to a base product, Proposal Center defaults the effective date to the 1st of the following month and prevents selection of an earlier date.

### Cloud Requirements Matrix — Proposal Center

| Requirement | USSec / USNat | USGov / Public Cloud (government customers) | NCOE (DE-SOV, FR-SOV) |
|-------------|---------------|----------------------------------------------|------------------------|
| EST default availability at proposal creation | ✅ Required (government customers) | ✅ Required (government customers) | ✅ Required (all customers) |
| Seller blocked from selecting self-renewing SKU | ✅ Required | ✅ Required | ✅ Required |
| Cancellation at expiration available (not default) | ✅ Required | ✅ Required | ✅ Required |
| EST-to-base transition defaults to 1st of following month | ✅ Required | ✅ Required | ✅ Required |
| Renewal proposals also default to EST-linked availability | ✅ Required | ✅ Required | ✅ Required |
| Seller can browse hidden-offer license-based products | Not applicable | Not applicable | ✅ Required |
| Proposal is the exclusive purchase/management channel | Not applicable | Not applicable | ✅ Required |
| Persona-based self-serve restrictions (customer self-serve blocked) | Via CEA (customer-facing surfaces; not Proposal Center) | Not required | Via CEA (customer-facing surfaces; not Proposal Center) |

**Key distinction:** USGov customers retain full self-serve capability for non-license-based products. Proposal Center applies only EST default restrictions for USGov government customers — no other persona-based proposal restrictions are required.

---

## Design Principles

| Principle | Description |
|-----------|-------------|
| **Compliance First** | MCA contractual obligations and NCOE operator requirements drive all design decisions |
| **Catalog as Source of Truth** | EST default behavior and action intent are expressed through catalog configuration (CEAs, SKU Category); Proposal Center consumes catalog data and does not implement independent eligibility logic |
| **Partner / Seller Enablement** | All governance restrictions apply to customer self-serve actions; partner-assisted actions and proposals are fully enabled |
| **Cloud-Specific Behavior** | Restrictions are differentiated by cloud cohort; USGov customers are not subject to persona-based proposal restrictions |
| **Service Continuity** | EST default ensures no break in service at term end while explicit renewal decisions are made |
| **Consistent Enforcement** | EST default behavior must be enforced identically across Proposal Center, Partner Center, M365 Admin Center purchase experience, and Commerce Support Tool (CST) |

---

## Success Criteria & Metrics

| ID | Metric Type | Description | Target |
|----|-------------|-------------|--------|
| M1 | Compliance | Unauthorized auto-renew into base product for government proposals | 0 post-release |
| M2 | Compliance | NCOE proposals created without EST-linked default | 0 post-release |
| M3 | Adoption | Proposals for NCOE license-based products using EST-linked availability | 100% |
| M4 | Quality | Seller-reported errors due to EST/availability enforcement | Baseline ± 5% |
| M5 | Delivery | Phase 2 Proposal Center changes complete | April 17, 2026 |
| M6 | User Success | Proposal creation workflow completion time (no regression) | Baseline ± 5% |

---

## Scope

### In Scope

**Phase 2 (April 17, 2026) — Scenario 450791**

- Proposal Center defaults to EST-linked availability for all government license-based proposals across all clouds (public, USGov, USSec, USNat)
- Proposal Center defaults to EST-linked availability for all license-based proposals in NCOE (DE-SOV, FR-SOV) for all customers
- Seller is blocked from selecting availability where the base product renews into itself
- Cancellation at expiration is available as an option but is not the default selection
- Renewal proposals created prior to commitment end also default to EST-linked availability
- Transition proposals from EST back to base product default to effective date of 1st of the following month
- Seller catalog browse in Proposal Center surfaces hidden-offer license-based products for NCOE cloud context
- Proposal Center displays clear cloud-context and EST-default indicators in the seller UI

### Out of Scope

- **Exception / override workflow for governance rules:** Governance restrictions are compliance-mandatory (contractual and legal obligations under MCA). No exception request or approval workflow is required or permitted for this release.
- **CSP channel governance controls in Proposal Center:** CSP program is not currently in use in US Federal government or NCOE clouds. Customer self-serve restrictions for CSP are handled via existing catalog action intent, not via Proposal Center.
- **USGov persona-based self-serve restrictions:** USGov customers retain full self-serve capability. No persona-based proposal creation restrictions apply to USGov proposals beyond EST default renewal.
- **Azure (non-license-based) offer governance:** Existing GSM validation checks are sufficient; no new Proposal Center work is required.
- **RI and Savings Plan auto-renew controls:** Removed from scope (Scenario 389109 descoped).
- **Discovery API catalog filtering:** Deferred to future work.
- **Governance rule administration UI within Proposal Center:** Governance rules are managed via catalog ingestion (CEAs), not via a Proposal Center admin experience.
- **Phase 1 (January 29, 2026) — MCAPI Policy:** Policy-based experience controls (Purchase Services blade visibility) are enforced in M365 Admin Center, not in Proposal Center.

---

## Functional Requirements

### Priority Guide

**P0:** Must have — critical for compliance and contract obligations
**P1:** Should have — important for operational effectiveness
**P2:** Nice to have — enhances seller experience and auditability

### Functional Requirements Table

| ID | Description | Priority | Cloud Scope | Related E2E FR |
|----|-------------|----------|-------------|----------------|
| FR-PC-01 | Proposal Center MUST default to the availability that renews into the linked EST offer at term end when a seller creates a new proposal for a government license-based product | P0 | Public, USGov, USSec, USNat | FR12 |
| FR-PC-02 | Proposal Center MUST default to EST-linked availability for all license-based proposals, regardless of customer segment | P0 | NCOE (DE-SOV, FR-SOV) | FR12 |
| FR-PC-03 | Proposal Center MUST block the seller from selecting any availability where the base product renews into itself (i.e., same product/SKU as the current subscription at term end) | P0 | All clouds | FR12 |
| FR-PC-04 | Proposal Center MUST offer "cancel at expiration" (auto-renew: false) as an available option but MUST NOT present it as the default selection | P0 | All clouds | FR12 |
| FR-PC-05 | When a seller creates a renewal proposal prior to the end of the customer's existing commitment, the EST-linked availability MUST also be the default selection | P0 | All clouds | FR12 |
| FR-PC-06 | When a seller creates a proposal to transition a customer from an EST subscription back to a base product, the effective date MUST default to the 1st day of the following month; the seller MUST NOT be able to select an earlier effective date | P0 | All clouds | FR12 |
| FR-PC-07 | Proposal Center MUST surface all license-based products (including hidden offers) in seller catalog browse and search for NCOE cloud proposals; these products are not visible to customers | P0 | NCOE only | FR3, FR4 |
| FR-PC-08 | Proposal Center MUST identify the customer's cloud context (public, USGov, USSec, USNat, DE-SOV, FR-SOV) at proposal creation time and apply the appropriate EST and availability rules for that cloud | P0 | All clouds | FR4 |
| FR-PC-09 | Proposal Center MUST display a clear visual indicator (badge or banner) identifying the cloud context and EST default behavior when EST is enforced for the proposal | P1 | All clouds | FR12 |
| FR-PC-10 | Proposal Center MUST display a clear UX message when an availability is unavailable because it renews the base product into itself, explaining why the option is blocked | P1 | All clouds | FR12 |
| FR-PC-11 | Proposal Center MUST identify whether a customer qualifies as a government customer (via existing PubSec segment framework) at proposal creation time to correctly apply EST defaults on public cloud and USGov proposals | P0 | Public, USGov | FR11, FR12 |
| FR-PC-12 | Proposal Center MUST NOT apply persona-based self-serve restrictions or additional proposal creation constraints for USGov proposals beyond EST default renewal; USGov customers retain full self-serve capability | P0 | USGov only | Cloud Req Matrix |
| FR-PC-13 | Proposal Center MUST log all EST enforcement decisions (EST selected, self-renew blocked, effective date defaulted) including the cloud context, customer segment, proposal ID, product, and outcome | P0 | All clouds | NFR4 |
| FR-PC-14 | All governance enforcement logs from Proposal Center MUST be retained for a minimum of 7 years | P0 | All clouds | NFR9 |
| FR-PC-15 | If catalog hydration fails to return EST configuration for a proposal, Proposal Center MUST fail closed — defaulting to EST-linked availability and blocking self-renewing SKUs — until catalog data is available | P0 | All clouds | FR12 |

---

## User Experience

### Target Users & Personas

| Persona | Cloud Context | Key Goals | Proposal Center Impact |
|---------|---------------|-----------|------------------------|
| **Field Seller (NCOE)** | DE-SOV, FR-SOV | Create proposals for license-based products on behalf of customers | Must use Proposal Center for all license-based transactions; can browse hidden offers; EST is the default renewal |
| **Field Seller (Government)** | Public, USGov, USSec, USNat | Create proposals for government license-based products | EST default availability at proposal creation; cannot select self-renewing SKU |
| **Field Seller (USGov)** | USGov | Create proposals; customer also has self-serve access | EST default renewal only; no persona-based restrictions beyond EST |
| **Seller / Renewal Manager** | All clouds | Create renewal proposals before commitment end | Renewal proposals also default to EST; cannot select self-renewing SKU |
| **Seller / EST Transition Manager** | All clouds | Transition customer from EST back to base product | Effective date forced to 1st of following month |

### User Scenarios & Flows

#### Scenario 1: Seller Creates New Proposal for Government Customer (EST Default — All Clouds)

**Applies to:** Public cloud, USGov, USSec, USNat (government customers)

1. Seller opens Proposal Center and creates a new proposal.
2. Seller selects a government customer tenant; Proposal Center identifies customer as government via PubSec segment framework.
3. Seller adds a license-based product (e.g., Microsoft 365 E5) to the proposal.
4. Proposal Center reads catalog EST configuration (`SKU Category = ExtendedServiceTerm`) for the product.
5. Proposal Center defaults to the availability that renews into the linked EST offer at term end. Seller sees an EST indicator badge on the selected availability.
6. The availability where the base product renews into itself is hidden or disabled in the picker; a tooltip explains: *"This availability is not available — government subscriptions cannot renew into the same product."*
7. Seller can optionally select "Cancel at expiration" but EST renewal is the pre-selected default.
8. Seller finalizes and sends the proposal. Customer accepts; subscription is created with renewal instructions to convert to EST linked offer at term end.

#### Scenario 2: Seller Creates Renewal Proposal Before Commitment End (EST Default)

**Applies to:** All clouds (government customers on public/USGov/USSec/USNat; all customers on NCOE)

1. Customer has an active Microsoft 365 E5 subscription with 2 months remaining on commitment.
2. Seller proactively opens Proposal Center to create a renewal proposal.
3. Proposal Center identifies the renewal context and defaults to the EST-linked availability (consistent with new purchase behavior).
4. Seller completes the renewal quote; customer accepts prior to term end.
5. Subscription renews at term end with instructions to convert to EST linked offer at the next term end.

#### Scenario 3: EST Subscription Expires; Seller Transitions Customer Back to Base Product

**Applies to:** All clouds

1. Customer's subscription reaches term end; it automatically converts to the EST linked offer (monthly, 3% uplift, no break in service).
2. Customer and seller agree to transition back to the base product commitment.
3. Seller opens Proposal Center, selects the customer's EST subscription, and creates a transition proposal.
4. Proposal Center defaults the effective date to the **1st day of the following month**. The seller cannot select an earlier date.
5. Customer accepts proposal; subscription transitions from EST to base product on the 1st of the following month.
6. New annual commitment begins; renewal instructions are set to renew into EST linked offer at the next term end.

#### Scenario 4: Seller Creates Proposal for NCOE Customer (Proposal-Only Model)

**Applies to:** NCOE clouds (DE-SOV, FR-SOV)

1. Customer in DE-SOV or FR-SOV cannot self-serve purchase license-based products (hidden offers; no Purchase Services blade in M365 Admin Center).
2. Customer contacts seller to request a license-based product.
3. Seller opens Proposal Center and creates a new proposal for the NCOE customer.
4. Seller searches for the license-based product. Proposal Center surfaces the product (even though it is a hidden offer), because catalog hydration recognizes the seller/proposal context.
5. Proposal Center defaults to EST-linked availability for all NCOE license-based proposals.
6. Seller completes the proposal; customer accepts. Subscription is created under the customer tenant.
7. All subsequent management actions (license increases, upgrades, cancellations) for this subscription must also be requested by the customer through a new seller proposal.

#### Scenario 5: Seller Attempts to Create Renewal Proposal for NCOE Customer (No Self-Renew)

**Applies to:** NCOE clouds (DE-SOV, FR-SOV)

1. Customer has an active Microsoft 365 E3 subscription approaching term end.
2. Seller opens Proposal Center and adds the renewal for the NCOE customer.
3. Availability where base product renews into itself is blocked; seller sees: *"Subscriptions in this cloud cannot renew into the same product. Select the EST-linked availability or cancel at expiration."*
4. Proposal Center defaults to EST-linked availability.
5. Seller optionally selects "Cancel at expiration" if customer preference is to end the subscription, but this is not the default.

#### Scenario 6: Seller Creates Proposal for USGov Customer (EST + Full Self-Serve Retained)

**Applies to:** USGov only

1. Seller opens Proposal Center for a USGov government customer.
2. Proposal Center applies EST default renewal for license-based products (same as other government clouds).
3. Seller is blocked from selecting self-renewing SKU; cancellation at expiration is available.
4. **No additional persona-based restrictions apply.** USGov customers retain full self-serve capability via M365 Admin Center for products outside this EST enforcement. Proposal Center does not impose additional quote restrictions for USGov.

---

## Error Handling & Edge Cases

| Scenario | Proposal Center Behavior | Seller Guidance |
|----------|--------------------------|-----------------|
| Catalog hydration fails for EST configuration | Fail closed — default to EST-linked availability; block self-renewing SKU | Display: *"Unable to load renewal configuration. EST default is applied. Contact support if issue persists."* |
| EST-linked offer not yet in catalog for a product | Block proposal submission for that product | Display: *"EST-linked offer is not available for this product. Contact the business planner to configure EST."* |
| Seller attempts to select effective date before 1st of following month for EST-to-base transition | Proposal Center prevents date selection; resets to 1st of following month | Display: *"Transition from EST to base product must take effect on the 1st of the following month per [cloud] operator requirements."* |
| Government segment qualification cannot be determined for customer | Fail safe — apply EST default as if customer is government | Log incident for investigation; do not block proposal creation |
| NCOE hidden-offer product not returned in seller catalog | Escalate to catalog team; seller cannot add product | Display: *"This product is not available for proposals in this cloud. Contact your catalog administrator."* |
| Seller creates proposal in NCOE without EST-linked offer available | Block proposal for that line item | Display: *"All [cloud] license-based products require EST-linked renewal. EST offer is not configured for this product."* |

---

## Non-Functional Requirements

| ID | Description | Priority | Related E2E NFR |
|----|-------------|----------|-----------------|
| NFR-PC-01 | Proposal Center catalog hydration for EST configuration and hidden-offer visibility must not degrade proposal creation page load beyond 5% of current baseline | P0 | NFR1 |
| NFR-PC-02 | EST enforcement decisions must be evaluated within the existing proposal creation response time SLA; no additional latency budget | P0 | NFR1 |
| NFR-PC-03 | All EST enforcement and hidden-offer catalog decisions must be logged with caller identity, cloud, product, proposal ID, action, and outcome | P0 | NFR4 |
| NFR-PC-04 | Compliance-critical enforcement logs must support audit log retention for 7 years in immutable, tamper-evident storage | P0 | NFR9 |
| NFR-PC-05 | Governance enforcement in Proposal Center must be consistent with enforcement in Partner Center, M365 Admin Center, and CST for the same products and customer segments | P0 | NFR4 |
| NFR-PC-06 | Proposal Center changes must support zero-downtime deployment | P0 | NFR10 |
| NFR-PC-07 | Catalog EST configuration used by Proposal Center must be cacheable and refreshable without a Proposal Center redeployment | P1 | NFR11 |

---

## Commerce Platform Capability Impact

| Capability | Type | Description | Related FRs |
|------------|------|-------------|-------------|
| **Proposal Center / Quote Center** | Modify | Default to EST-linked availability for all government license-based proposals (all clouds) and all license-based proposals (NCOE); block self-renewing SKU selection; enforce 1st-of-month effective date for EST-to-base transitions; surface hidden-offer products for NCOE seller context | FR-PC-01 through FR-PC-15 |
| **Catalog Hydration API** | Modify (dependency) | Return EST configuration flag and hidden-offer visibility based on caller context (seller/proposal identity for NCOE) | FR-PC-07, FR-PC-08 |
| **Assets** | Modify (dependency) | Validate and prevent creation of license-based assets with auto-renew configuration where base product renews into itself; NCOE: for all customers; public/USGov/USSec/USNat: for government customers | E2E FR13 |
| **PubSec Segment Framework** | Dependency | Provide government customer segment determination at proposal creation time for public cloud and USGov proposals | FR-PC-11 |
| **Telemetry & Logging** | Modify | Log all EST enforcement decisions from Proposal Center; ensure 7-year retention | FR-PC-13, FR-PC-14 |

---

## Product Dependencies & Risks

### Dependencies

| Dependency | Description | Impact if Unavailable |
|------------|-------------|----------------------|
| **Catalog EST Configuration (SKU Category = ExtendedServiceTerm)** | Catalog must be configured with EST-linked offer relationships for all government license-based products (all clouds) and all NCOE license-based products | Cannot implement EST default renewal; proposals may create subscriptions with incorrect renewal behavior |
| **Extended Service Terms (EST) Linked Offers in Catalog** | EST-linked offers must exist and be published in catalog ([Release 107803](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems/edit/107803) / [Release 199697](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems/edit/199699)) | Cannot default to EST; subscriptions renew into base product; MCA non-compliance |
| **Catalog Hydration Context-Aware Response (FR4)** | Catalog must return EST configuration and hidden-offer visibility based on seller/proposal identity for NCOE | Seller cannot browse NCOE hidden offers; cannot create NCOE proposals |
| **PubSec Segment Framework (ADO 70760)** | Government customer segment determination for public cloud and USGov proposals | Cannot distinguish government customers; EST defaults may be applied to non-government customers or missed for government customers |
| **Assets Team EST Validation (E2E FR13)** | Assets team must validate auto-renew configuration at asset creation to reject invalid configurations | Defense-in-depth gap; proposals may be accepted but assets created with incorrect renewal |

### Risks

| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| EST-linked offers not fully configured in catalog by Phase 2 deadline | High — Proposal Center cannot enforce EST default for products without linked offers | Medium | Assets team and business planners to audit EST offer configuration early; daily catalog reporting to flag missing configurations (E2E NFR7) |
| PubSec segment determination incorrect for USGov customers | Medium — EST defaults applied incorrectly | Low | Fail safe: if segment cannot be determined, apply EST default as if customer is government |
| Seller UX friction from EST enforcement causing proposal abandonment | Medium — seller productivity regression | Low | Invest in clear UI messaging explaining EST default rationale; track proposal completion rate (M6) |
| Regression in partner purchase workflows for NCOE proposals | High — NCOE customers cannot transact | Low | Extensive integration testing for NCOE proposal creation; validate seller catalog browse with hidden offers |
| Catalog hydration performance degradation for EST config queries | Medium — increased proposal creation latency | Low | Implement caching for EST configuration; establish performance SLOs; conduct load testing before Phase 2 deployment |

---

## Implementation Plan

### Release Strategy

**Phase 2 — April 17, 2026** (Proposal Center changes are all Phase 2)

- Implement EST-linked availability as default at proposal creation for government customers (public, USGov, USSec, USNat) and all customers (NCOE).
- Block availability picker from showing self-renewing SKUs.
- Enforce 1st-of-month effective date for EST-to-base transition proposals.
- Surface NCOE hidden-offer products in seller catalog browse.
- Deploy with feature flag to enable staged rollout.

**Rollback:** EST delivery defaults can be reverted via feature flag without catalog or deployment changes.

### Deployment Sequence

1. Catalog hydration EST configuration validation (dependency — must be live before Proposal Center changes).
2. Proposal Center seller catalog browse update for NCOE hidden offers.
3. Proposal Center EST default availability enforcement.
4. Proposal Center self-renewing SKU block.
5. Proposal Center EST-to-base effective date enforcement.
6. Telemetry and logging for EST enforcement decisions.

### GtM Strategy

| Audience | Communication Type | Timeline | Message |
|----------|--------------------|----------|---------|
| Field Sellers | Seller portal announcement + training | 2 weeks before Phase 2 | EST is now the default renewal for government and NCOE proposals; self-renewing SKUs are blocked; explanation of NCOE proposal-only model |
| NCOE Sellers | Dedicated training session | 2 weeks before Phase 2 | Proposal Center is the exclusive channel for all NCOE license-based transactions; hidden offers are now visible in proposal creation |
| Internal Support Teams | Training + troubleshooting guide | 1 week before Phase 2 | EST enforcement logic; escalation procedures; how to handle edge cases |

---

## Open Items

| Open Question | Owner | ETA |
|---------------|-------|-----|
| Does EST requirement apply to monthly-term license-based products (limited benefit vs annual terms)? CELA opinion required. | John Mueller | TBD |
| How does the PCD represent EST default for a government pricing audience within a commercial product (audience-specific renewal behavior)? | John Mueller | TBD |
| What guidance is provided to business planners to ensure EST-linked offers are configured for all applicable products before Phase 2 deadline? | John Mueller | TBD |
| Confirm Proposal Center caller identity / app ID is correctly recognized by catalog hydration as seller/proposal context for NCOE hidden-offer visibility | Proposal Center Engineering / Catalog Team | TBD |

---

## Appendix

### Key Terminology

| Term | Description |
|------|-------------|
| **EST (Extended Service Term)** | A monthly rolling term that activates at subscription expiration, ensuring no break in service. Priced at 3% monthly uplift over base monthly price. Can be cancelled at any time with prorated refund. See [EST Functional Spec](./commerce-docs/internalDocs/designs/product%20life%20cycle/extended-service-term/extended-service-term-functional-spec.md) |
| **EST-linked availability** | The catalog availability configured to renew a subscription into the linked EST offer at term end (via scheduledActions / renewal term config) |
| **Self-renewing availability** | An availability where the base product renews into itself at term end (same product/SKU for next commitment period). Blocked for government customers (public/USGov/USSec/USNat) and all NCOE customers |
| **Hidden offer** | A product published to the catalog but not visible to customers browsing M365 Admin Center. Visible only to sellers via Proposal Center and partner context. Used for all license-based products in NCOE clouds |
| **NCOE Clouds** | DE-SOV (Germany Sovereign Cloud, operated by Delos) and FR-SOV (France Sovereign Cloud, operated by Bleu) |
| **US Federal Government Clouds** | USGov, USSec, and USNat — sovereign clouds with restricted network connectivity and stringent purchase controls |
| **Government Customer** | A customer holding a government pricing audience qualification under the PubSec segment framework. For MCA EST purposes: applies to all government customers in public cloud, USGov, USSec, USNat |
| **CEA (Catalog Extensibility Artifact)** | A catalog configuration object that specifies action intent (allowed/blocked) per persona, cloud, and channel |
| **Proposal Center / Quote Center** | The seller-facing tooling used by Microsoft field sellers to create, manage, and submit pricing proposals for customers |

### References

- **E2E Spec:** [Purchase_Channel_Governance_spec.md](./commerce-docs/internalDocs/product_management/documents/Sovereign%20Cloud/Purchase_Channel_Governance/Purchase_Channel_Governance_spec.md)
- **Scenario 450791:** [Proposal Center EST Default Renewal](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems/edit/450791)
- **Scenario 371568:** [License-based Products Published as Hidden Offers (NCOE)](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems/edit/371568)
- **EST Release 107803:** [Extended Term for CSP](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems/edit/107803)
- **EST Release 199697:** [Extended Term for MCA-E and Buy Online](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems/edit/199697)
- **EST Functional Spec:** [extended-service-term-functional-spec.md](./commerce-docs/internalDocs/designs/product%20life%20cycle/extended-service-term/extended-service-term-functional-spec.md)
- **PubSec Framework:** ADO [70760](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems/edit/70760)
- **ADO Release:** [362560](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems/edit/362560)
