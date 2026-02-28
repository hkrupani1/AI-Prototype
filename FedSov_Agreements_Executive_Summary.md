# FedSov / Agreements — Executive Summary

**Reporting Period:** December 29, 2025 – May 28, 2026 (60 days back · 90 days forward)  
**Area Path:** `Commerce and Ecosystems Planning\Divisional\FedSov\Agreements`  
**Project:** Commerce and Ecosystems Planning  
**Generated:** February 27, 2026

---

## 📊 Executive Summary

### Overview

A total of **38 active work items** are currently tracked within the FedSov\Agreements area path (Scenarios, Releases, Risks, and Bugs only). The portfolio spans multiple strategic releases focused on MCA-E software true-up enforcement, seller-led FromSA purchasing, agreement implicit acceptance, and cross-cloud MACC enablement for USGov customers. The most significant near-term activity is 3 committed scenarios under the MCA-E Software True-up release and elevated bug volume (28 active bugs) concentrated in PMW/ECIF configuration and FromSA transact flows.

### Key Metrics

| Metric | Count |
|--------|-------|
| 🎯 Highlights (Completed) | 2 Scenarios |
| 🔦 Headlights (Committed) | 3 Scenarios |
| 🔻 Lowlights (Overdue) | 0 Scenarios |
| ⚠️ Risks Formally Tracked | 0 |
| 🐛 Active Bugs | 28 |
| 🔍 Active Development (Backlog/In Progress/In Scoping/Proposed) | 7 Scenarios |
| 📋 Historical Completed (outside look-back, for context) | 3 Scenarios |
| **Total Scenarios in Area** | **15** |

> ⚠️ **Data Quality Note:** Most scenarios do not have target dates set in ADO. This limits Lowlight detection and timeline tracking. Recommend enforcing target date hygiene as a mandatory field.

---

### Bug Status Summary

| Status | Count | Overdue (Past Target Date) |
|--------|-------|---------------------------|
| 🔴 Active + New | 24 | 0 |
| 🔄 In Progress / In Review | 4 | 0 |
| 🟡 Resolved | 0 | 0 |
| **Total** | **28** | **0** |

> ℹ️ Only 2 bugs have target dates set (#464999: Feb 27, 2026; #466489: Mar 2, 2026). Neither is currently overdue. The majority of bugs (26 of 28) have no target date assigned.

---

### Strategic Release Focus Areas

1. **[MCA-E Software] True-up amendment & co-term enforcement** (#443457) — 3 Committed scenarios driving Quote Center, Commerce Insights, and PMC enforcement of true-up for LSA, SA, and 3-year SW subscriptions
2. **Deals Continuous Improvement KTLO/Repair Item** (#214860) — 3 historically completed scenarios (Sep 2025); ongoing cadence for deal repair and CI items
3. **Seller led FromSA purchasing** (#1837) — 1 In-Progress scenario; active transact failures in this area represent the highest-urgency bug cluster
4. **Agreement Implicit Acceptance Policy** (#269561) — 1 Backlog capability documentation scenario; 2 active bugs with imminent target dates (Feb–Mar 2026)
5. **Cross Cloud MACC USGov** (#221130) — 1 In Scoping scenario for enabling MACC for qualified commercial customers in USGov cloud
6. **Deals KTLO/Repair Item/S360 Work - FY26** (#201902) — 1 Backlog scenario tracking NX Terms regression and repair items

---

### Critical Observations

- **MCA-E Software True-up is the #1 priority:** Three committed scenarios in Quote Center, Commerce Insights, and PMC are the clearest near-term delivery commitments for this area.
- **FromSA transact failures are actively blocking deals:** Four bugs (#440326, #440330, #447790, #447815) represent transact failures due to missing AvailabilityToken and DualUseRights UPN issues — these require urgent engineering attention.
- **Implicit Acceptance feature has time-sensitive bugs:** Two bugs (#464999, #466489) under Agreement Center/Implicit Acceptance have target resolution dates of Feb 27 and Mar 2, 2026 — immediate follow-up needed.
- **Zero formal risks tracked:** No Risk-type work items are active for this area path. Given the 28 active bugs and the complexity of MCA-E true-up changes, formal risk tracking is recommended.
- **Target date coverage gap:** Only 2 of 15 scenarios and 2 of 28 bugs have target dates, making portfolio health difficult to measure objectively.

---

## 🎯 Highlights — Completed within 60 Days (Dec 29, 2025 – Feb 27, 2026)

### Release: No Release Grouping — Ad-hoc In-Market Fixes

| Scenario ID | Title | Status | Completed Date | Key Achievements |
|-------------|-------|--------|----------------|-----------------|
| [#362772](https://dev.azure.com/CEPlanning/_workitems/edit/362772) | IN MARKET ISSUES 6277 - Custom language Numbering bug | ✅ Completed | Jan 23, 2026 | Resolved custom language numbering defect impacting in-market proposals; mitigated seller-facing agreement formatting errors |
| [#362777](https://dev.azure.com/CEPlanning/_workitems/edit/362777) | IN MARKET ISSUES 10300 - Lock proposal management for completed deals | ✅ Completed | Jan 23, 2026 | Addressed proposal management lock issue for completed deals, preventing inadvertent modification of closed agreements |

---

## 🔦 Headlights — Committed for Next 90 Days (by May 28, 2026)

### Release: [MCA-E Software] True-up amendment & co-term enforcement for LSA, SA & 3-yr SW Subs | In Design | [#443457](https://dev.azure.com/CEPlanning/_workitems/edit/443457)

| Scenario ID | Title | Status | Target Date | Key Objective |
|-------------|-------|--------|-------------|---------------|
| [#448470](https://dev.azure.com/CEPlanning/_workitems/edit/448470) | [MCA-E Software] True-up amendment & co-term enforcement - Quote Center enforcement (NX Terms) | 🚀 Committed | TBD | Enforce true-up amendment and co-term rules in Quote Center for NX Terms across LSA, SA, and 3-yr SW subscription agreements |
| [#450877](https://dev.azure.com/CEPlanning/_workitems/edit/450877) | [MCA-E Software] True-up amendment & co-term enforcement - Commerce Insights | 🚀 Committed | TBD | Surface true-up compliance and co-term enforcement signals in Commerce Insights for seller and partner visibility |
| [#450921](https://dev.azure.com/CEPlanning/_workitems/edit/450921) | [MCA-E Software] True-up amendment & co-term enforcement - PMC | 🚀 Committed | TBD | Implement true-up amendment & co-term enforcement logic within PMC to complete end-to-end coverage |

> ⚠️ **Note:** No target dates are set for these committed scenarios. Timeline risk is elevated — date commitment required from engineering leads.

---

## 🔻 Lowlights — Overdue Scenarios

**No overdue scenarios identified.**

> The absence of lowlights is primarily attributable to missing target dates across the portfolio (13 of 15 scenarios have no target date). This may mask overdue items. Target date population is strongly recommended for the next review cycle.

---

## ⚠️ Risks & Issues

**No formal Risk work items are tracked** for the `Commerce and Ecosystems Planning\Divisional\FedSov\Agreements` area path. However, the following scenario-level risks are observable from work item data:

| Risk Description | Related Work Items | Recommended Action |
|-----------------|-------------------|-------------------|
| FromSA transact failures blocking deals (AvailabilityToken & DualUseRights) | [#440326](https://dev.azure.com/CEPlanning/_workitems/edit/440326), [#440330](https://dev.azure.com/CEPlanning/_workitems/edit/440330), [#447790](https://dev.azure.com/CEPlanning/_workitems/edit/447790), [#447815](https://dev.azure.com/CEPlanning/_workitems/edit/447815) | Elevate to L2 risk; assign engineering owner for resolution sprint |
| MCA-E committed scenarios missing target dates | [#448470](https://dev.azure.com/CEPlanning/_workitems/edit/448470), [#450877](https://dev.azure.com/CEPlanning/_workitems/edit/450877), [#450921](https://dev.azure.com/CEPlanning/_workitems/edit/450921) | Require Eng + PM date commitment in next sprint review |
| Implicit Acceptance bugs due within days | [#464999](https://dev.azure.com/CEPlanning/_workitems/edit/464999) (Feb 27), [#466489](https://dev.azure.com/CEPlanning/_workitems/edit/466489) (Mar 2) | Immediate follow-up; escalate if not resolved by target |
| Zero formal risk tracking in this area | No Risk work items | Create Risk items in ADO for the 3 risk areas above |

---

## 🔍 Active Development

### Release: Seller led FromSA purchasing | In Progress | [#1837](https://dev.azure.com/CEPlanning/_workitems/edit/1837)

| Scenario ID | Title | Status | Target Date | Key Objective |
|-------------|-------|--------|-------------|---------------|
| [#376748](https://dev.azure.com/CEPlanning/_workitems/edit/376748) | [NX-Terms] Seller led FromSA purchasing | 🚀 In Progress | TBD | Enable seller-led purchasing path within FromSA flow with NX Terms compliance, including agreement creation and signing |

---

### Release: [Capability] Agreement Implicit Acceptance Policy | In Progress | [#269561](https://dev.azure.com/CEPlanning/_workitems/edit/269561)

| Scenario ID | Title | Status | Target Date | Key Objective |
|-------------|-------|--------|-------------|---------------|
| [#374454](https://dev.azure.com/CEPlanning/_workitems/edit/374454) | Capability Doc: [Capability] [Agreement Center and Template Service] Agreement Implicit Acceptance Policy | 📋 Backlog | TBD | Author capability documentation for Agreement Implicit Acceptance Policy to support engineering and partner readiness |

---

### Release: Cross Cloud MACC (USGov with MACC in Global) | In Scoping | [#221130](https://dev.azure.com/CEPlanning/_workitems/edit/221130)

| Scenario ID | Title | Status | Target Date | Key Objective |
|-------------|-------|--------|-------------|---------------|
| [#448674](https://dev.azure.com/CEPlanning/_workitems/edit/448674) | As a seller I can create a proposal in USGov cloud and add/end MACC contribution for a customer | 📋 In Scoping | TBD | Enable proposal creation in USGov cloud for qualified commercial customers with MACC; allow add/end of MACC contributions cross-cloud |

---

### Release: Deals KTLO/Repair Item/S360 Work - FY26 | In Progress | [#201902](https://dev.azure.com/CEPlanning/_workitems/edit/201902)

| Scenario ID | Title | Status | Target Date | Key Objective |
|-------------|-------|--------|-------------|---------------|
| [#296431](https://dev.azure.com/CEPlanning/_workitems/edit/296431) | [NX Terms] Regression bugs and repair items | 📋 Backlog | TBD | Track and resolve NX Terms regression bugs and repair items to maintain production stability |

---

### Other / Removed Parent Release Scenarios

| Scenario ID | Title | Status | Former Release | Key Objective |
|-------------|-------|--------|---------------|---------------|
| [#98049](https://dev.azure.com/CEPlanning/_workitems/edit/98049) | NX Agreements Local Work | 📋 Backlog | MCE Non-Divisional Work: NX (Removed) | Backlog of NX Agreements local work items pending scoping and assignment |
| [#148197](https://dev.azure.com/CEPlanning/_workitems/edit/148197) | Enhance Agreement Center | 📋 Backlog | Enhance Agreement Center (Removed) | Capability backlog for Agreement Center enhancements supporting enterprise contracting scale |
| [#450700](https://dev.azure.com/CEPlanning/_workitems/edit/450700) | Research: Seller Experience on Quote Center - NX Terms (MCA-E Agreement) | 📋 Proposed | No Parent | Research initiative on seller experience for NX Terms in Quote Center in context of MCA-E agreements |

> ℹ️ Scenarios #98049 and #148197 are parented under **Removed** releases. Recommend re-parenting to active releases or archiving these backlog items.

---

## 🚨 Bug Analysis — Active Bugs Requiring Attention

**28 active bugs** are currently open in the FedSov\Agreements area path. Key clusters identified below.

---

### High Priority Bugs — FromSA Transact Failures

| Bug ID | Title | Status | Description |
|--------|-------|--------|-------------|
| [#440326](https://dev.azure.com/CEPlanning/_workitems/edit/440326) | [FromSA] Transact fails due to missing AvailabilityToken for Dual User Rights SKU | 🔴 Active | Transact flow failure when AvailabilityToken missing for DualUseRights SKUs; blocking deal closure |
| [#440330](https://dev.azure.com/CEPlanning/_workitems/edit/440330) | [FromSA] Transact fails due to DualUseRights UPN populated instead of SKU UPNs | 🔴 Active | DualUseRights UPN mismatch causing transact failure; incorrect UPN propagation instead of SKU UPNs |
| [#447790](https://dev.azure.com/CEPlanning/_workitems/edit/447790) | 3PP: [FromSA] Transact fails due to missing AvailabilityToken for Dual User Rights | 🔄 In Review | Third-party partner transact failure variant; in review for fix |
| [#447815](https://dev.azure.com/CEPlanning/_workitems/edit/447815) | 3PP: [FromSA] Transact fails due to DualUseRights UPN populated instead of SKU UPNs | 🔄 In Review | Third-party partner UPN mismatch variant; in review for fix |

**Impact Assessment:** These 4 bugs represent a systemic issue in the FromSA transact flow for Dual User Rights SKUs. All 4 are variations of the same root cause (AvailabilityToken missing + DualUseRights UPN mismatch). Resolution of the root cause would likely close all 4. **Recommend treating as a single escalation with a unified fix.**

---

### High Priority Bugs — PMW / ECIF Term Configuration

| Bug ID | Title | Status | Description |
|--------|-------|--------|-------------|
| [#370970](https://dev.azure.com/CEPlanning/_workitems/edit/370970) | [PMW]: Direct Government Contract Proposals with ECIF term not able to transact | 🔴 Active | Direct Gov proposals with ECIF term blocked from transacting; deal-blocking severity |
| [#397370](https://dev.azure.com/CEPlanning/_workitems/edit/397370) | [PMW]: Description field in disabled state when configuring ECIF term SKU | 🔴 New | ECIF term SKU configuration UX broken; description field disabled incorrectly |
| [#431142](https://dev.azure.com/CEPlanning/_workitems/edit/431142) | ECIF - invalid purchaseTermUnits values and cannot transact | 🔴 New | Invalid purchaseTermUnits value set during ECIF configuration causing transact failure |
| [#367254](https://dev.azure.com/CEPlanning/_workitems/edit/367254) | ECIF Modification - Custom Term | 🔴 Active | Custom term issues affecting ECIF modification flow |
| [#398107](https://dev.azure.com/CEPlanning/_workitems/edit/398107) | [PMW]: Both is displayed when more than two types are selected for ECIF term | 🔴 Active | Display defect in PMW ECIF term type selection |
| [#435543](https://dev.azure.com/CEPlanning/_workitems/edit/435543) | [PMW]: Proposals with "ECIF terms Modify and Cancel" options are not present | 🔴 New | Modify and Cancel options missing for ECIF term proposals in PMW |
| [#386396](https://dev.azure.com/CEPlanning/_workitems/edit/386396) | [PMW]: while configuring applicable law the application becomes slow | 🔴 Active | Performance degradation in PMW when configuring applicable law for terms |

**Impact Assessment:** ECIF-related bugs form the largest cluster (7 bugs). Multiple are deal-blocking for Direct Gov proposals. Root cause analysis across this cluster is recommended.

---

### High Priority Bugs — Implicit Acceptance (Time-Sensitive)

| Bug ID | Title | Status | Target Date | Description |
|--------|-------|--------|-------------|-------------|
| [#464999](https://dev.azure.com/CEPlanning/_workitems/edit/464999) | [Implicit Acceptance][Agreement Center] Content Refresh Date and Agreement Effective Date mismatch | 🔴 New | **Feb 27, 2026** | Content Refresh Date and Agreement Effective Date out of sync in Agreement Center for Implicit Acceptance |
| [#466489](https://dev.azure.com/CEPlanning/_workitems/edit/466489) | [Implicit Acceptance][Agreement Center] Already executing Policy - Still able to execute again | 🔴 New | **Mar 2, 2026** | Policy execution idempotency issue — can execute an already-running policy again, creating duplicate execution risk |

**Impact Assessment:** Both bugs have imminent target dates. #464999 is due **today** (Feb 27). Immediate owner verification and status update required.

---

### Other Active Bugs

| Bug ID | Title | Status | Description |
|--------|-------|--------|-------------|
| [#168098](https://dev.azure.com/CEPlanning/_workitems/edit/168098) | [Modern Quotes]: "End Date is in past" error not displayed on line item on configured past end date | 🔴 Active | UX validation error not surfacing correctly for expired end dates in Modern Quotes |
| [#212595](https://dev.azure.com/CEPlanning/_workitems/edit/212595) | [NX Workspace]: Inform seller that No signature is needed when there is signed MCA | 🔴 Active | Seller not informed when MCA signature is not required; UX gap in NX Workspace |
| [#222208](https://dev.azure.com/CEPlanning/_workitems/edit/222208) | [CI-Repair][NX Terms - ECIF] Display meaningful error when ECIF case not found | 🔴 New | Missing meaningful error message for ECIF case not found scenario |
| [#292440](https://dev.azure.com/CEPlanning/_workitems/edit/292440) | [PMW] Savings plan drop down for ACD Product displays wrong data in view Agreement | 🔴 Active | Data display error in agreement view for ACD product savings plan |
| [#293614](https://dev.azure.com/CEPlanning/_workitems/edit/293614) | [QC - Terms] Unable to see deal desk approval error when CACO flight enabled | 🔴 New | Deal desk approval error not visible when CACO flight is on |
| [#295071](https://dev.azure.com/CEPlanning/_workitems/edit/295071) | StartOnFirstOfTheMonth flag not set — start date computed wrong | 🔴 New | Start date computation error due to missing SOFOM flag |
| [#328856](https://dev.azure.com/CEPlanning/_workitems/edit/328856) | [PMW]: Proposal behavior after test term expiry | 🔄 In Review | Unexpected proposal behavior post-term expiry; in review |
| [#379309](https://dev.azure.com/CEPlanning/_workitems/edit/379309) | [PMC][EA to MCA-E late renewal]: proposal not completing | 🔴 New | Proposal stuck and not turning to completed state for EA-to-MCA-E late renewals |
| [#435503](https://dev.azure.com/CEPlanning/_workitems/edit/435503) | Currency mismatch for Milestone Amount in MACC | 🔴 New | Currency mismatch causing incorrect milestone amounts in MACC agreements |
| [#451606](https://dev.azure.com/CEPlanning/_workitems/edit/451606) | MACC Modify - Old start date scenario | 🔴 New | MACC modification improperly setting old start dates |
| [#453293](https://dev.azure.com/CEPlanning/_workitems/edit/453293) | Change from Invoice Language to Preferred Communication during Agreement Creation | 🔴 New | Invoice language not switching to preferred communication language during agreement creation |
| [#453874](https://dev.azure.com/CEPlanning/_workitems/edit/453874) | Validation Service: Async validation stuck as "InProgress" when Rule SDK throws | 🔴 Active | Async validation flow hangs in InProgress when Rule SDK throws exception; process integrity risk |
| [#465528](https://dev.azure.com/CEPlanning/_workitems/edit/465528) | [PMW] - Error at download/view agreement for Poland Country | 🔴 Active | Agreement download/view fails for Poland country — potential geo-specific issue |
| [#367661](https://dev.azure.com/CEPlanning/_workitems/edit/367661) | When selecting "Start Date" all dates are previous 1 day for France | 🔴 Committed | Off-by-one date issue for France locale in start date picker |

---

## 📋 Historical Completed Scenarios (Sep 2025 — Outside Look-Back Period, Provided for Context)

### Release: Deals Continuous Improvement KTLO/Repair Item | In Progress | [#214860](https://dev.azure.com/CEPlanning/_workitems/edit/214860)

| Scenario ID | Title | Completed Date |
|-------------|-------|----------------|
| [#267539](https://dev.azure.com/CEPlanning/_workitems/edit/267539) | [NX Terms - ECIF] Service classification of ECIF in PMW causes sellers to find wrong ECIF | Sep 24, 2025 |
| [#296417](https://dev.azure.com/CEPlanning/_workitems/edit/296417) | [CI MIM] Remove blank from Azure credit/ACD/SPD terms | Sep 24, 2025 |
| [#304732](https://dev.azure.com/CEPlanning/_workitems/edit/304732) | [CI- Feedback] Agreement id number to be visible even if no new Terms are added | Sep 24, 2025 |

---

## 🔗 Key Links

- [Release: MCA-E Software True-up enforcement](https://dev.azure.com/CEPlanning/_workitems/edit/443457)
- [Release: Seller led FromSA purchasing](https://dev.azure.com/CEPlanning/_workitems/edit/1837)
- [Release: Agreement Implicit Acceptance Policy](https://dev.azure.com/CEPlanning/_workitems/edit/269561)
- [Release: Cross Cloud MACC USGov](https://dev.azure.com/CEPlanning/_workitems/edit/221130)
- [Release: Deals KTLO/S360 FY26](https://dev.azure.com/CEPlanning/_workitems/edit/201902)
- [Release: Deals CI KTLO/Repair](https://dev.azure.com/CEPlanning/_workitems/edit/214860)
- [Area Path Query — FedSov/Agreements](https://dev.azure.com/CEPlanning/Commerce%20and%20Ecosystems%20Planning/_workitems?_a=edit&path=Commerce%20and%20Ecosystems%20Planning%5CDivisional%5CFedSov%5CAgreements)

---

*Report generated by Azure DevOps Executive Summary Generator (ado-executive-summary.prompt.md) | Area: FedSov / Agreements | Generated: February 27, 2026*
