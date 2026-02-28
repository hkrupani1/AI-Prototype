# NX Terms Continuous Improvement – Product Specification

**Status:** Draft
**Version:** 0.1
**Last Updated:** February 25, 2026
**Authored by:** [Author Name]

**Links:**
- Link to BRD – [To be provided]
- Link to One Pager – [To be provided]
- Link to ADO – [To be provided]
- Link to Finance Requirements – [To be provided]

---

## Key Roles

| Team | Role | Name |
|------|------|------|
| Enterprise Commerce Studio | PM Owner / Author | [Name] |
| PMW Engineering | Engineering Lead | [Name] |
| Deal Desk / Finance | Approver / Stakeholder | [Name] |
| Legal / Compliance | Stakeholder | [Name] |
| UX Design | Designer | [Name] |
| Sales Operations | Stakeholder | [Name] |
| e-Signature Integration | Engineering Stakeholder | [Name] |

---

## Change Log

| Date | Author | Changes | Reviewed / Approved By |
|------|--------|---------|------------------------|
| 2026-02-25 | [Author] | Initial draft from seller research study (Jan–Feb 2026) | |
| | | | |

---

## Overview

NX Terms is the contract terms management module within the Proposal Management Workspace (PMW), used by Commercial Executives to configure and manage MCA-E (Microsoft Customer Agreement – Enterprise) deal terms. A design research study conducted January–February 2026 across ~10 sellers in APAC, EMEA, and Americas identified significant friction across the end-to-end NX Terms workflow — from term search and configuration through internal approvals and customer signing. This specification defines the product enhancements targeting FY27 delivery to address those findings, improve seller productivity, accelerate deal closure, and increase customer confidence in the contracting experience.

## Summary

This specification defines continuous improvement enhancements for NX Terms within the Proposal Management Workspace (PMW), driven by a January–February 2026 seller research study across APAC, EMEA, and Americas. Eight capability areas are targeted: smarter keyword-based term search with suggestions, in-tool term previews, bulk configuration with smart defaults, streamlined approval workflows, real-time signature tracking with flexible signing order, a contract pricing summary for customers, improved special-term date handling, and updated in-product guidance. These improvements are expected to reduce contract processing time by >30%, eliminate redundant approval cycles for non-material changes, and significantly reduce deals stalled at the signing or customer acceptance stage. Delivery is planned across FY27 with success tracked via seller NPS, deal cycle time, approval accuracy, and customer signing turnaround metrics.

---

## Executive Summary

**Background:** NX Terms is an essential module within the Proposal Management Workspace (PMW) where sellers configure and manage contract terms (standard clauses, negotiated amendments, and custom addenda) for Microsoft Customer Agreement – Enterprise (MCA-E) deals. A design research study (January–February 2026) involving approximately 10 Commercial Executives across multiple regions (APAC, EMEA, Americas) was conducted to identify continuous improvement opportunities for FY27 planning. This research uncovered critical pain points in the NX Terms workflow that impede deal velocity and diminish user (seller and customer) satisfaction.

**Purpose of Improvements:** Based on these findings, this document outlines a set of feature enhancements and process changes aimed at solving the identified issues. By addressing core problems in term search, configuration, approvals, and signature processes, the NX Terms tool will better enable sellers to close deals faster and with greater confidence, while improving the customer's contract experience. These improvements align with business goals of accelerating deal cycles, improving seller productivity, and increasing customer trust in the contracting process.

**Key Proposed Features:**

- **Smarter Term Search:** Implement robust keyword-based search (with synonyms, partial matches, and filters) and term suggestions to help sellers quickly find the correct terms and related required clauses.
- **In-Platform Term Previews:** Allow sellers to preview the text of any contract term within the tool (without generating a full agreement) to verify language and share it with customers early.
- **Bulk Configuration & Defaults:** Enable one-time input of common data (e.g. term dates) to propagate across all relevant terms/SKUs, reducing repetitive entries and errors.
- **Streamlined Approval Workflow:** Optimise the approval logic so that non-financial changes don't trigger full re-approvals, improve the approver selection UI, and automatically log approval evidence for compliance.
- **Transparent Signature Tracking:** Provide visibility into the e-signature process (internal signer status, customer signing status) and allow flexible signing order (customer-first or Microsoft-first). Introduce alerts for incomplete customer acceptance (checkout) to prevent missed steps.
- **Contract Pricing Summary:** Include a summary of product-level prices and discounts in the contract documentation, addressing customer concerns about "blind" signing without seeing financial terms.
- **Flexible Term Handling:** Improve how special terms are handled – ensure term expirations default appropriately (prevent inadvertent short expiries) and allow multi-entity Azure Commitment (MACC) amendments to have sensible date ranges for each new entity (no implied retroactive coverage).
- **Policy & Guidance Updates:** Update in-app guidance and sales training to clarify new commerce processes (e.g. differences between EA and MCA-E, empowerment rules) and set correct expectations for customers (e.g. on pricing, signature steps).

**Benefits:** These enhancements will directly tackle the most frequent pain points – making term management faster, easier, and more transparent. We expect to reduce the time sellers spend on administrative tasks (like searching for terms and duplicating data entry), eliminate common causes of deal delays (approval and signature bottlenecks), and improve overall satisfaction. This will lead to quicker deal closures (boosting revenue recognition), higher seller productivity, and a smoother customer onboarding experience. Success will be measured via metrics such as reduced contract processing time, improved seller satisfaction scores, fewer deal-support escalations, and positive customer feedback post-implementation (see [Goals & Success Metrics](#goals--success-metrics) for details).

---

## Problem Statement

**Current State & Challenges:** The NX Terms experience has multiple friction points that hinder both internal users (sellers, deal support) and customers:

- **Inefficient Term Search:** Sellers report that finding the correct term or amendment can be frustrating and time-consuming. The search function only matches exact titles and often fails for common keywords or abbreviations, making it "hit-and-miss". For example, a seller trying to add a security provision noted that searching "Sentinel" or its acronym "SEIM" returned nothing, because the relevant clause was titled differently – buried under an unrelated name. This misalignment between search and the seller's mental model forces sellers to manually scan long lists or use external references, wasting valuable time (sometimes 5+ minutes per term search as observed during interviews).

- **Repetitive & Error-Prone Configuration:** The tool requires manual re-entry of identical information for each term or product line item. Sellers must input the same dates, numbers, or descriptions multiple times, leading to frustration and occasional inconsistencies. In large deals (with dozens of SKUs or amendments), this repetitiveness significantly slows down the process and increases the risk of errors (e.g. one term accidentally set to a different end date than others).

- **No Term Preview or Context:** Currently, sellers cannot view the full text of a term clause without adding it to a draft and generating the entire contract PDF. This means they often add all possible terms and then download a 50+ page document just to verify each clause's language. Not only is this inefficient, but it also hinders collaboration: sellers cannot easily share a single clause with a customer's legal team for review. One participant described this as a major pain point, wishing for the "ability to preview individual amendments without downloading the entire MCA".

- **Approval Workflow Frictions:** The internal approval process for non-standard terms and discounts is overly sensitive and lacking transparency. Minor, non-financial changes (e.g. adjusting a date or formatting) trigger a full re-approval by all parties (including Finance), causing ~24-hour delays even when revenue impact is zero. Selecting the correct approver is also error-prone: the dropdown list often shows multiple similar names without clear roles, leading to trial-and-error submissions. Moreover, once approvals are obtained, the system doesn't store any evidence of them – unlike legacy systems (EA/VLC) where sellers attached approval emails, NX Terms only records a button click. This lack of an audit trail means sellers have to retain emails externally to prove approvals for compliance, which is risky and inconvenient.

- **Opaque Signature & Acceptance Process:** The digital signing stage leaves both sellers and customers in the dark. By default, Microsoft's internal signatory must sign first, but sellers have no visibility into when that happens, resulting in a "black hole" of indeterminate length. Sellers often resort to manually chasing the internal signatory (e.g. an executive) to expedite their signature, since the customer is left waiting without notification until Microsoft signs. Additionally, once the customer signs, they must perform a final "acceptance/checkout" step to activate the agreement – a nuance that many customers overlook, as they assume signing the document completes the process. The tool does not notify the seller if a customer fails to complete this step, so deals have sat incomplete until sellers manually followed up days later. This two-step process and lack of alerts is causing confusion and delays in deal activation.

- **Contract Content Gaps:** The generated contract documents sometimes omit key information that customers expect to see. Notably, pricing and discount details are not visible in the MCA-E contract at signing. Customers must trust that the subsequent order form or invoice will correctly reflect agreed discounts. In the study, one sales rep highlighted that this is counterintuitive – *"if you were making the same agreement in your personal life, would you expect the contract to only show half of the benefits you were expecting?"*. As a workaround, sellers find themselves sending separate emails or unofficial quote documents to confirm pricing, which is not ideal. Another content issue arises with customers who had heavily customised Enterprise Agreements: they find the new MCA-E contracts confusing or lacking comparable terms in some cases, which requires additional explanation and assurance from the seller.

- **Rigid Term Handling:** A couple of specific system behaviours create edge-case headaches:
  - Certain regulatory terms (e.g. financial services compliance or DORA addenda) used to default to a 30-day expiration in the tool. In one instance, a seller failed to notice this short default, and the clause expired before the deal closed, forcing the customer to re-sign an amendment later. (Recent updates have since forced explicit date entry for these terms, mitigating the issue, but ensuring appropriate defaults remains important.)
  - In multi-entity Azure Commitment (MACC) deals, if a new entity is added to an existing commitment, the tool ties the new entity's term retroactively to the original commitment's start date, even if that was a year or more in the past. This creates legal confusion – the customer perceives it as being asked to back-date an agreement or wondering if they missed out on benefits. Sellers currently have no easy way to adjust this within NX Terms, and such cases require awkward workarounds (or manual contract edits) to satisfy customer and legal expectations.

**Impact:** Collectively, these issues lead to longer deal cycles, higher workload for sellers, and reduced trust in the tool:

- Sellers waste time on low-value tasks (searching, re-entering data, chasing approvals) instead of engaging customers. One participant described the NX Terms process as having *"significant friction… high time waste"* in critical parts of the journey.
- Deals may be delayed or jeopardised, especially in time-sensitive periods (e.g. end of quarter) when an approval resets or a signature stalls unexpectedly. These delays can directly impact revenue recognition and customer satisfaction.
- Customers may feel less confident in the contracting process. Lack of pricing transparency and confusing signing steps can erode trust, requiring extra reassurance from sellers and potentially risking the deal if concerns aren't addressed.

Without intervention, these pain points will only grow as more customers and deals transition to MCA-E (New Commerce platform). Therefore, it's critical to enhance NX Terms to eliminate these bottlenecks and deliver a frictionless experience for all parties.

---

## Research Findings Summary

> **Note:** This section is synthesised from the January–February 2026 design research study involving ~10 Commercial Executives across APAC, EMEA, and Americas. Direct access to emails, Teams messages, and SharePoint interview recordings was not available during drafting — update this section once reviewed against those sources.

### Theme 1: Customer Pain Points

| Pain Point | Finding | Severity |
|---|---|---|
| **Inefficient Term Search** | Search only matches exact titles; keywords like "Sentinel" or "SEIM" return no results even when a matching clause exists under a different name. Sellers spend 5+ minutes per term search. | High |
| **Repetitive Data Entry** | Sellers manually re-enter identical dates, numbers, and descriptions for each term and SKU in large deals (10–50+ entries per deal). Error risk increases significantly. | High |
| **No In-Tool Term Preview** | Sellers must add terms to a draft and generate a full 50+ page PDF just to verify a single clause's language. Cannot share individual clauses with customer legal teams. | High |
| **Opaque Approval Process** | Approver dropdown shows ambiguous names with no role context, leading to wrong submissions. Any edit (even non-financial) triggers full re-approval, causing ~24-hour delays. No audit trail stored. | High |
| **Invisible Signing Process** | Sellers have no visibility into internal signatory status — a "black hole." Customers left waiting without notification until Microsoft signs. Separate checkout/acceptance step frequently missed. | High |
| **Missing Pricing in Contract** | Final MCA-E contract omits pricing and discount details. Customers sign without seeing agreed financials, which erodes trust and creates confusion. *"Would you expect the contract to only show half of the benefits?"* | Medium–High |
| **Regulatory Term Expiry Bugs** | Regulatory terms (e.g. DORA addendum) previously defaulted to 30-day expiry. At least one clause expired before deal close, requiring customer re-signature. | Medium |
| **MACC Multi-Entity Date Issue** | Adding a new entity to an existing MACC forces the new entity's term start date to the original contract start date, implying back-dated obligations and creating legal confusion. | Medium |
| **UI Performance Under Load** | With 5+ amendments in a proposal, the date-picker control and form inputs become sluggish, degrading the configuration experience for complex deals. | Low–Medium |

### Theme 2: Business Goals

| Goal | Rationale |
|---|---|
| **Accelerate deal closure & revenue recognition** | Approval and signature bottlenecks push deals across quarter boundaries, delaying revenue recognition and risking deal loss. |
| **Improve seller efficiency & morale** | Sellers invest significant time on administrative workarounds. Reducing friction frees sellers to focus on customer engagement, directly supporting FY27 seller experience goals. |
| **Enhance customer trust at signing** | The contracting stage is the customer's final impression before MCA-E commitment. Transparency in pricing and a smooth signing process build trust and aid New Commerce adoption. |
| **Reduce operational & compliance risk** | Absence of approval audit trails creates compliance exposure. Automating records and alerts reduces manual oversight burden and risk of missed contract activation. |
| **Scale New Commerce without linear headcount growth** | Pain points will compound as MCA-E volume grows. Improvements must deliver efficiency gains that scale without proportional support increases. |

### Theme 3: Key Decisions & Observations from Research

| Decision / Observation | Status | Notes |
|---|---|---|
| Regulatory term explicit date entry is now mandatory | ✅ Implemented (late FY26) | Addresses accidental short expiry defaults. Build on this with auto-alignment. |
| Microsoft-first signing is the current default | In Review | Sellers need flexibility. Customer-first option proposed; Legal sign-off required. |
| No approval audit trail is stored in NX Terms | ❌ Gap | Unlike legacy EA/VLC systems. Must be addressed for compliance. |
| Checkout/acceptance is a separate step post-signing | ❌ User confusion | Customers routinely miss this. Automated reminders + long-term elimination proposed. |
| Pricing omitted from MCA-E contract | ❌ Gap | Must be addressed via Pricing Summary addendum; Legal format approval required. |
| DocuSign migration underway (from Adobe Sign) | ✅ In Progress | Signature status API integration must support both during transition. |

### Recommendations for Improvement (by Theme)

**Seller Productivity:**
- Implement fuzzy/keyword search with synonym metadata enrichment — prioritise most-searched failed queries as the initial synonym corpus.
- Add "Apply to All" bulk date/field actions to eliminate the #1 source of repetitive entry.
- Introduce in-tool term previews as a quick win; requires only an API exposure of existing term content.

**Approval Workflow:**
- Define material vs. non-material change rules in collaboration with Finance/Policy before engineering begins — this is the key governance dependency.
- Implement approval logging immediately (low engineering effort, high compliance value).
- Improve approver selection with role context and region-based pre-filtering.

**Signing & Activation:**
- Surface DocuSign/Adobe Sign real-time webhook status in the PMW Signature tab.
- Introduce automated 24-hour reminder for outstanding customer acceptance (checkout) step — this is a high-impact, relatively low-effort improvement.
- Define customer-first signing eligibility criteria with Legal before enabling the UI toggle.

**Contract Transparency:**
- Engage Legal early on the Pricing Summary format; this is the primary dependency before engineering begins.
- Review and suppress enterprise-irrelevant boilerplate (e.g. consumer payment terms) in MCA-E templates.

**Special Terms:**
- Validate current DORA/regulatory term fix in production before building auto-alignment on top.
- Create a distinct amendment template for multi-entity MACC additions with independent date logic.

---

## User Personas

The proposed improvements will primarily benefit the following user groups:

- **Commercial Executive (Seller):** Front-line salespeople (account executives, deal managers) who use NX Terms to assemble and close enterprise deals. Typically managing large, complex contracts during customer renewals or migrations from Enterprise Agreements. They need the tool to be fast and reliable so they can focus on customer negotiations. This persona experienced the bulk of the identified pain points (difficult search, repetitive input, waiting on approvals, lack of contract transparency, etc.).

- **Deal Desk Analyst / Finance Approver:** Internal specialists who review and approve non-standard deal components (e.g. extra discounts, non-standard terms). They interface with NX Terms via approval requests. Their interests are in ensuring compliance and financial viability without unnecessary process overhead. Pain points include redundant approval cycles (reviewing the same proposal multiple times due to minor edits) and lack of context on what changed in a resubmitted approval.

- **Legal/Compliance Officer:** While not direct users of the UI, these stakeholders define many of the terms and policies that NX Terms must enforce (e.g. required clauses for regulated industries, signatory rules). They may also get involved via offline processes for truly custom terms. Their priority is that contracts include all necessary protections and that any deviations go through proper approvals. They are concerned with auditability (record-keeping of approvals) and correct term usage. When NX Terms fails to capture an approved exception or if a required clause is omitted, it creates legal risk and re-work.

- **Enterprise Customer (Procurement & Signatory):** The end customer's representatives who review and sign the contract. They often have to interact with the outputs of NX Terms (the contract documents and the signing portal). They expect clear contract documentation that reflects the negotiated deal, and a straightforward signing process. When information is missing (like pricing) or the signing process is confusing (multiple steps, unclear email notifications), it undermines their confidence and can delay their internal approval of the deal. Although not direct users, their experience is heavily influenced by how well NX Terms facilitates a transparent and accurate contracting process.

These personas, especially the sellers, were the focus of the research and are the primary drivers for the requirements in this specification. Improving NX Terms will help sellers and support teams (Deal Desk, Legal) do their jobs more efficiently, and will result in a better experience for customers as well.

---

## Business Need

Transforming the NX Terms experience addresses several critical business needs:

- **Accelerate Deal Closure & Revenue Recognition:** The current inefficiencies in NX Terms often lead to delays at the final stages of sales (e.g. waiting on re-approvals or signatures). Every day a deal is delayed can push revenue into the next quarter or risk losing the sale entirely. By removing bottlenecks and automating non-value-add tasks, we can shorten the contract processing time, enabling deals to close within the desired fiscal period and improving sales productivity.

- **Improve Seller Efficiency & Morale:** Sellers are a precious and costly resource – their time should be spent on customer engagement and strategy, not wrestling with internal tools. Currently, however, sellers spend significant time finding workarounds for NX Terms limitations (as evidenced by multiple pain points). These frustrations can negatively impact seller morale and confidence in the new sales process. By delivering a smoother workflow (fewer clicks, intuitive search, clear statuses), we empower our sales team to be more effective and reduce burnout. This directly aligns with the FY27 goal of improving seller experience in high-value sales journeys.

- **Enhance Customer Trust and Satisfaction:** The contract phase is often the customer's last impression before signing a major deal. Issues like missing pricing details in the contract or confusion during signing can sow doubt and require extra explanation. By making contracts more transparent (including critical info like discounts) and ensuring the signing process is predictable and communicative, we build trust with customers at a crucial moment. Smoother contracting will also make it easier for customers to transition from legacy agreements to MCA-E, supporting the broader New Commerce adoption strategy.

- **Reduce Operational Risk and Support Load:** The lack of audit trails for approvals and the need for manual interventions (e.g. tracking signatures, reminding customers to complete acceptance) present compliance risks and generate additional work for support teams. Automating these and maintaining proper records will reduce the chances of errors (like missed approvals or unsigned contracts going unnoticed) and diminish the need for post-deal clean-up by operations. It also ensures we meet internal audit and compliance requirements by having a clear history of who approved what and when.

- **Increase Process Scalability for New Commerce:** As volume grows, the identified pain points will scale poorly. For instance, if search is currently slow for a single seller, consider hundreds of sellers experiencing the same – the aggregate productivity loss is significant. The business needs a terms management process that can handle more deals and users without linear increases in support or cycle time. The proposed improvements (like better search and suggestions, data automation, and elimination of manual steps) are aimed at making NX Terms robust and scalable for the expected growth in MCA-E transactions.

In summary, fixing NX Terms is not just a UX nicety; it is a business imperative to ensure that our sales processes don't become the bottleneck to closing deals. By investing in these improvements now, we prepare the field for larger volumes and more complex deals in FY27 and beyond, while also de-risking the final stages of the sales cycle.

---

## Goals & Success Metrics

The following are the key objectives of the NX Terms Continuous Improvement initiative, along with how we will measure success:

- **Reduce Contract Processing Time:** Goal: Streamline the NX Terms workflow so that sellers can configure and finalize contracts significantly faster. Success Metrics: Decrease the average time taken from starting term configuration to obtaining all approvals and signatures by a substantial margin (target example: >30% reduction, measured in minutes/hours per deal). Specifically track improvements in sub-tasks like term search time (e.g. from minutes to seconds per term) and time waiting for approvals/signatures at quarter-end (via internal SLAs).

- **Improve Seller Satisfaction & Adoption:** Goal: Boost the confidence and satisfaction of sellers using NX Terms, so they rely on the tool (rather than workarounds) and provide positive feedback. Success Metrics: Increase seller satisfaction scores in periodic surveys – e.g. an increase in the PMW/NX Terms user NPS or a rise in the "tool trust" rating measured in the post-study baseline survey. Look for a reduction in negative comments or complaints about NX Terms in sales forums and fewer escalations to support. Additionally, monitor usage analytics for any uptick in tool adoption (for instance, fewer manual contract adjustments or off-system deals as NX Terms becomes easier to use).

- **Higher Deal Accuracy & Compliance:** Goal: Ensure contracts are configured correctly the first time and all approvals are properly captured, thereby avoiding rework and audit issues. Success Metrics: Track the percentage of deals that require re-approval or re-signing due to tool-related errors – the goal is to minimize these occurrences (target near 0% for standard deal scenarios). Conduct periodic audits of closed deals to verify approval records are present for 100% of deals requiring exceptions. Also monitor legal/finance escalations: a decline in the number of deals flagged for missing clauses or compliance misses will indicate success.

- **Faster Customer Signing & Activation:** Goal: Shorten the time from final seller submission to customer signature, and ensure customers have clarity during signing. Success Metrics: Measure the average duration between sending a contract for signature and final customer acceptance. The aim is to reduce delays attributed to internal signatory holdups or customers failing to complete the acceptance. A successful outcome would be, for example, a reduction in the average signature turnaround time by a set target (e.g. 20%) and a significant decrease in deals stalled due to customers not performing the checkout step (monitored via system logs and support records).

- **Positive Customer Feedback:** Goal: Increase customer confidence in the contracting process by addressing pain points like missing information and confusing steps. Success Metrics: Qualitative feedback from customers (via account team surveys or anecdotal reports) indicating fewer concerns about contract clarity. Look for faster customer turnaround on signing (as a proxy for reduced confusion) and perhaps an increase in customers willing to serve as references for the streamlined contracting process. We can also monitor if fewer customers insist on redlining our contracts offline due to greater trust in the standard documents.

Each of these metrics will be baselined (using data from late FY26 where available, e.g. the research's baseline trust/satisfaction survey and system analytics on processing times) and tracked over the course of FY27 as the improvements are rolled out. Our overall goal is that by mid-FY27, the contracting stage is no longer perceived as a major hurdle by the field or customers, as reflected in faster deal closures and improved sentiment.

### Success Criteria & Metrics Table

| ID | Metric Type | Description | Target | Data Collection Status |
|----|-------------|-------------|--------|------------------------|
| M1 | User Success | Average time from term configuration start to final approved contract | >30% reduction vs FY26 baseline | Needs Implementation |
| M2 | User Success | Average term search time per term | <30 seconds (from ~5 min) | Needs Implementation |
| M3 | Business Impact | % deals requiring re-approval due to tool-related errors | <1% | Needs Implementation |
| M4 | Business Impact | Average signature turnaround time (contract sent → customer acceptance) | >20% reduction vs FY26 baseline | Needs Implementation |
| M5 | Adoption | Seller satisfaction / NPS score for NX Terms | Measurable improvement vs baseline survey | Exists (survey mechanism) |
| M6 | Adoption | # of escalations to deal support related to NX Terms friction | >25% reduction YoY | Needs Implementation |
| M7 | Tech KPI | % of deals with 5+ amendments experiencing UI performance issues | <2% | Needs Implementation |
| M8 | Business Impact | % of closed deals with complete approval audit records on file | 100% | Needs Implementation |

---

## High-Level Solution Intent

To achieve the above goals, we propose the following major enhancements to NX Terms:

### 1. Smarter Search & Term Suggestions

Revise the term search feature to use keyword-based matching, not just exact string matches. Sellers should be able to find terms by commonly used keywords or abbreviations (e.g. searching "Sentinel" should retrieve the relevant security amendment even if it's officially titled differently). We will implement a synonyms and fuzzy matching system so that partial matches and alternate terminology (like product codenames or colloquial term names) are recognised. Additionally, introduce search filters (e.g. filter by product category, regulation type, region) to narrow results in long lists. Finally, an auto-suggestion capability will be added: if a seller adds one term that typically is paired with others (say, an industry-specific clause), the system will suggest related terms they might want to add next. This will not auto-add clauses without consent, but will save the user from separately searching for each companion clause.

### 2. In-Tool Term Preview

Provide a "Preview" action for each term in the library. When a seller clicks a term (either from search results or within the proposal), they should see the full legal text and any relevant details (e.g. applicability notes, effective period, etc.) in a readable format within the app. This pop-up or side panel allows the seller (and their customer, if needed) to review the exact wording of a clause prior to adding it to the contract. The preview will be read-only, ensuring sellers cannot inadvertently modify standard legal language.

### 3. Bulk Configuration & Smart Defaults

Reduce repetitive data entry by introducing bulk actions and intelligent defaults during term configuration:

- Sellers will be able to set common attributes once and apply them across multiple items. For example, a new "Apply to All" option could propagate a chosen start and end date to all selected terms or SKUs in a proposal.
- The system will leverage context to pre-fill certain fields. If the overall deal has a known commitment term (e.g. a 3-year Azure commitment), any newly added term or discount will default to that timeframe (with the option to adjust if needed).
- Where applicable, use template configurations: for instance, if a seller selects a "standard multi-year discount" package, the tool could automatically add and link the required annual terms with appropriate decreasing percentages.

### 4. Streamlined Approval Workflow

Overhaul aspects of the internal approval process to minimise unnecessary delays:

- **Selective Approval Triggers:** Update the logic so that changes to a proposal that do not affect the financials or risk profile do not reset existing approvals.
- **Improved Approver Selection UI:** Redesign the approval request interface to reduce confusion – display approvers by role or department and auto-filter the list to the likely required approver.
- **Automated Approval Logging:** Implement an audit trail for approvals within the tool, recording who approved, when, and what was approved.

### 5. Transparent Signature & Acceptance Tracking

Make the electronic signing process visible and flexible for sellers and customers:

- **Real-Time Status Visibility:** Display the live status of each required signature within the proposal's Signature tab.
- **Configurable Signing Order:** Provide an option for the seller to choose the signing sequence (Microsoft-first or Customer-first) when initiating the signature process.
- **Acceptance Step Notifications & Streamlining:** Introduce an automated reminder and notification system for the post-signature "checkout" step.
- **Internal Copy as PDF:** Ensure that once fully signed, the final PDF is easily accessible to both the seller and the customer.

### 6. Contract Pricing & Terms Visibility

Ensure that key commercial details are visible to customers in the contract they sign. We will include a new "Pricing Summary" section in the contract PDF or as an attachment, listing the products, quantities, prices, and any discounts or credits that have been agreed (mirroring the final quote). Additionally, we will review the standard contract templates for any extraneous or confusing clauses, ensuring that enterprise customers aren't distracted or alarmed by irrelevant text.

### 7. Flexible Term Handling

Introduce functionality and safeguards for special term scenarios:

- **Auto-Align Term Expiries:** The system will by default align any added term's end date to the overall agreement end date unless specified otherwise.
- **Improved Multi-Entity Support:** Modify the logic for adding entities to an existing MACC so that the new entity's term addendum can have its own valid date range instead of being forced to the original commitment's start date.
- **Grouping and Performance:** Ensure the system handles multiple amendments (4–5 or more) without performance issues.

### 8. Improved Guidance & Training

Alongside technical changes, update user guidance both in-product and via field readiness materials:

- **In-Product Tips:** Add context-sensitive help text or tooltips for features that frequently confuse users.
- **Process Documentation:** Work with Sales Operations and Readiness teams to update playbooks and FAQs for MCA-E.
- **Policy Alignment:** Coordinate with legal and commercial policy teams to ensure that the tool's defaults and options remain aligned with policy.

---

## Design Principles

These principles guide design and trade-off decisions across all NX Terms improvements:

| Principle | Description |
|---|---|
| **Seller-first simplicity** | Every UI change must reduce clicks and cognitive load for the seller. Complexity should be absorbed by the system, not the user. |
| **Non-destructive defaults** | Auto-filled values and bulk operations must never silently overwrite intentional user input. Defaults are hints, not mandates — always overridable. |
| **Audit-by-design** | All approvals, status changes, and key decisions must be logged automatically. Compliance evidence should not depend on manual steps or external email trails. |
| **Progressive disclosure** | Surface the most common actions prominently; advanced options (e.g. custom signing order, multi-entity date overrides) appear contextually when needed, not by default. |
| **Resilient to e-sign vendor change** | Signature tracking and notification logic must be built as an abstraction layer, not tightly coupled to Adobe Sign or DocuSign specifically, given the active migration. |
| **Policy-enforced, not policy-hidden** | Where policy restricts options (e.g. customer-first signing eligibility), the UI should explain the constraint clearly rather than silently hiding the option. |

---

## Scope

### In Scope

- Keyword-based term search with synonym/fuzzy matching and filter support
- In-tool term preview (read-only modal/side panel)
- Bulk field configuration and smart date defaults for terms and SKUs
- Material vs. non-material change classification for approval logic
- Approver selection UI improvement with role context and region pre-filtering
- Approval audit logging stored within the proposal record
- Real-time signature status display (per signer, with timestamps)
- Configurable signing order (Microsoft-first / Customer-first, subject to policy)
- Automated customer acceptance (checkout) reminders and seller notifications
- Pricing Summary section in contract package
- Contract template review to remove irrelevant enterprise boilerplate
- Auto-alignment of regulatory term end dates to agreement end date
- Multi-entity MACC amendment date logic fix (independent date ranges per entity)
- UI performance improvements for proposals with 5+ amendments
- In-product tooltips, help text, and updated field guidance
- Sales readiness documentation and playbook updates for MCA-E

### Out of Scope

- Full elimination of the customer checkout/acceptance step (longer-term platform dependency; noted as ideal state but not in this PRD)
- AI-driven term recommendation or automatic clause generation
- Custom clause authoring by sellers within the tool (remains an offline/Legal process)
- Changes to pricing or discount policies themselves (this spec addresses display, not policy)
- Changes to the underlying MCA or standard contract legal language
- Dynamic pricing or consumption-based billing visibility beyond what is settled at deal time
- Full e-signature vendor migration (DocuSign transition tracked separately; this spec builds on top of whatever provider is active)

---

## Functional Requirements

This section details the functional requirements for each proposed feature/improvement, including representative user stories, acceptance criteria, and any dependencies or notes.

### Functional Requirements Summary

| No | Description | Priority | Related Metrics |
|----|-------------|----------|-----------------|
| FR1 | Enhanced term search with keyword/fuzzy matching, synonyms, and filters | P0 | M1, M2, M5 |
| FR2 | In-tool read-only term preview (modal/side panel) | P0 | M1, M2, M5 |
| FR3 | Bulk field configuration and smart date defaults across terms/SKUs | P0 | M1, M5, M6 |
| FR4 | Material vs. non-material change classification; approval audit logging; approver UI improvement | P0 | M3, M6, M8 |
| FR5 | Real-time signature status tracker; configurable signing order; acceptance reminders | P0 | M4, M5, M6 |
| FR6 | Pricing Summary section in contract package; template boilerplate review | P1 | M5, M6 |
| FR7 | Regulatory term date alignment; multi-entity MACC date logic; UI performance for 5+ amendments | P1 | M1, M7 |
| FR8 | In-product guidance (tooltips, help text); updated sales readiness documentation | P2 | M5, M6 |

---

### FR1: Enhanced Term Search & Suggestions

**User Story:** As a Commercial Executive, I want to quickly find the correct contract terms by typing keywords or related phrases, so that I don't waste time searching with exact titles or scrolling through long lists. I also want the system to help me identify other related terms I might need, so I don't accidentally miss required clauses for my deal.

**Acceptance Criteria:**

- When the user enters a partial term name or keyword, the system returns relevant results even if the exact term name is not entered (e.g. searching "Sentinel" returns the clause "Microsoft Sentinel Security Addendum").
- The search results should include matches from term titles, common aliases (synonyms), and short descriptions. (E.g. a search for "GDPR" should match the "Data Protection Addendum" even if that phrase isn't in the title.)
- The user can apply filters (such as Product = "Azure", Industry = "Financial Services", Region = "EMEA") to narrow down relevant terms if the initial keyword is too broad.
- After the user selects a term to add, the system checks if there are known related terms and prompts the user: *"You have added [Term X]. You may also need [Term Y] and [Term Z]."* The user can then one-click add those suggested terms or dismiss the suggestions.
- The suggestions mechanism should be non-intrusive (no automatic additions without user consent) and should only suggest terms when contextually appropriate.

**Dependencies & Notes:**

- This feature will require enhancing the term metadata with synonyms/keywords for each term, in collaboration with the content management team.
- Search filters may depend on term attributes not currently exposed (like industry tagging or region applicability), requiring new metadata fields.
- Related-term suggestion rules will be developed with the Legal/Policy team to ensure relevance and accuracy.
- Search infrastructure may need an update (e.g. indexing titles and synonyms). Performance testing is required.

---

### FR2: Term Preview Functionality

**User Story:** As a seller, I want to preview the full text and details of a term or amendment within the app before I add it, so that I can verify it's the correct one and discuss the language with my customer if needed.

**Acceptance Criteria:**

- Each term in the NX Terms library shall have a "Preview" action (e.g. a clickable icon or link).
- Clicking "Preview" opens a pop-up or side panel showing:
  - The full legal text of the term (formatted readably).
  - Any important metadata or conditions (e.g. if the term is only valid in certain countries).
  - (Optional) A reference ID or link to internal guidance for this term.
- The preview must be read-only; the user cannot edit the term text here.
- The preview should load in under 2 seconds under normal network conditions.
- If a term is updated or versioned, the preview should reflect the latest text.
- The user should be able to open previews for multiple terms in succession without losing their place in the workflow.

**Dependencies & Notes:**

- We will need an API or method to retrieve the content of a single term from the backend repository.
- Dynamic placeholders in term text (if those exist) must be handled – either replaced with sample values or highlighted clearly in the preview.
- Close collaboration with UX design is needed to determine how the preview is presented (modal vs. side panel).
- Term previews could be cached per session for performance.
- Security/permissions: Only authorised users should be able to view the preview content.

---

### FR3: Bulk Field Configuration & Defaults

**User Story:** As a seller, I want to set common contract details (like term dates or customer info) once and have them apply to all relevant parts of the contract, so I don't have to re-type the same information over and over for each product or amendment.

**Acceptance Criteria:**

- The user can select multiple line items or terms and update a field (e.g. an end date) for all of them in one action.
- The system auto-populates fields when possible:
  - When a new term or product discount is added, default its end date to the overall agreement end date.
  - If a term or product requires a start date, default it to the contract's start date (or today's date for an amendment added mid-term) as appropriate.
  - If multiple similar items are added together, present an option to "link" their configurations.
- The UI should provide clear feedback after bulk operations – e.g. affected fields could be highlighted.
- Any required fields that the system auto-fills should be visibly marked (e.g. a notation like "(defaulted to contract end date)").
- The solution should cover all high-frequency repetitive inputs, including: effective dates for terms and discounts, customer information appearing in multiple places, and deal identifiers used in multiple documents.
- Bulk application of values should be transactional and support a single "Undo" action.

**Dependencies & Notes:**

- Requires frontend changes for multi-select and batch actions, and backend changes to handle bulk updates in a single request.
- Default value hierarchy must be clearly defined and coded with thorough testing for edge cases.
- UI changes for multi-select will need user validation to ensure they are intuitive.

---

### FR4: Optimised Approval Workflow

**User Story:** As a Deal Desk approver (and as a seller who triggers approvals), I want the system to only request my approval when absolutely necessary and to make it obvious and easy to approve, so that I can turn around deal approvals quickly without impeding the sales cycle.

**Acceptance Criteria:**

- The system classifies proposal edits as "material" or "non-material" with respect to approvals:
  - **Material edits** (e.g. increasing a discount, adding a risk-increasing term) invalidate prior approvals and require re-review.
  - **Non-material edits** (e.g. correcting a typo, adjusting term dates within approved boundaries) do not reset the approval state.
  - Clear rules and examples of each category will be documented and aligned with finance and policy teams.
- The approver selection interface is improved:
  - Default to the most likely approver based on deal parameters where possible.
  - Display each approver option with additional context (e.g. "Jane Doe – Finance (UK/EU)").
  - If multiple approvals are needed, clearly indicate all required approvers and automatically route sequentially.
- Approval records must be stored and viewable:
  - Once an approver clicks "Approve", the system logs the approval with a timestamp and identifier.
  - Sellers can view a summary of approvals on an "Approvals" tab of the proposal.
  - If an approved proposal is materially modified, previous approvals show as "Invalidated" with a reason.
  - Data logged: approver's name, role, decision (approved/rejected), timestamp, and optional comments.
- The UI should warn sellers when a modification will trigger re-approval (e.g. "Changing this field will require re-approval from Finance").
- The system prevents common mistakes like sending an approval to an unauthorised approver.

**Dependencies & Notes:**

- Logic for differentiating material vs. non-material changes requires input from Finance and Operations policy – a rule engine or config file is recommended.
- Upstream dependency on Identity/Org data for approvers to provide contextual info (titles/roles).
- Storing approval data will involve changes to the database schema (with appropriate data retention policies).
- Training will be needed to inform approvers of the new experience.

---

### FR5: Signature Process Visibility & Control

**User Story:** As a seller, I want to track the status of internal and customer signatures in real-time, and have the flexibility to change the signing order when needed, so that I can manage customer expectations and not be caught off-guard by signing delays.

**Acceptance Criteria:**

- Once a contract is sent for signing, the seller can view a status tracker showing each required signer and their status (e.g. "Pending", "Completed on [date/time]", "Declined/Cancelled"), covering:
  - Each Microsoft internal signer.
  - The external customer signer(s).
- The system supports configurable signing order:
  - Default remains Microsoft-first, but sellers have an option to choose "Send to Customer first".
  - Certain high-risk deals may disable customer-first (policy-controlled); the UI handles this by disabling the option where not allowed.
- The system sends a notification/reminder if a contract is signed by one party but awaiting the other for more than 24 hours.
- If the customer's acceptance (checkout) remains incomplete for a certain threshold (e.g. 48 hours), an automated email is sent to the customer explaining how to complete the acceptance.
- After all parties sign and the customer accepts, both seller and customer automatically receive a confirmation with a link to the final documents.
- If an e-signature process is cancelled or fails, the status tracker shows this and guides the seller on next steps.

**Dependencies & Notes:**

- Integration with E-Signature Service (Adobe Sign / DocuSign): Requires coordination with the e-signature integration team to fetch real-time status updates via APIs.
- Policy for Signing Order: Allowing customer-first signing requires legal team approval and confirmation of any jurisdictional constraints.
- Notification infrastructure must be configurable to avoid spamming, with appropriate email deliverability and messaging.
- Thorough testing required across a variety of scenarios (multiple signers, different signing orders, proxy signers, different email clients, etc.).
- Changes must not affect the legal validity of signatures.

---

### FR6: Contract Pricing & Info Summary

**User Story:** As a customer, I want the contract documents I sign to clearly reflect the main commercial terms (like the products, prices, discounts) of our agreement, so that I have complete confidence in what I'm signing and don't need to refer to external documents or emails for critical information.

**Acceptance Criteria:**

- The generated contract package will include a Pricing Summary page (or section) whenever there are product-specific prices or discounts in the deal. This summary should list, at minimum:
  - Each product or SKU covered by the proposal.
  - The quantity and term (e.g. 1000 units, 3-year term).
  - List price and the agreed discounted price (or discount percentage).
  - Any lump-sum monetary commitments (e.g. Azure consumption commitments) and applicable discount or incentive.
- The summary should be clearly formatted and referenced from the contract (e.g. "See Schedule 1 for Pricing Summary").
- The information in the summary must be consistent with what the customer sees online and what ultimately will be billed.
- For consumption-based services, the summary should explicitly state the arrangement (e.g. "Azure services will be billed as consumed at rates reflecting a 15% discount from retail, per the attached schedule.").
- Contract templates will be reviewed to remove or contextualise any irrelevant standard terms that have caused customer confusion.
- A preamble will be included (as advised by Legal): "This summary is for convenience and the binding terms are as per the MCA and attached term documents."

**Dependencies & Notes:**

- Will require pulling data from the CPQ system or proposal details already stored in PMW to populate the pricing summary.
- Coordination with the Legal department is necessary to approve the format and contents.
- The solution should be toggle-able or adjustable per market to account for regional legal constraints.
- Contract validation tests will need to be updated to account for these changes.

---

### FR7: Special Terms Handling & Validation

**User Story:** As a seller, I want the system to intelligently handle special-case terms (like regulatory addenda and multi-entity commitments) by setting appropriate defaults and providing flexibility, so that I don't inadvertently make mistakes that could complicate the deal.

**Acceptance Criteria:**

- **Default Expiry for Regulatory Terms:** For terms like the financial services addendum or DORA clause, the system must not impose an arbitrary short default expiry. These clauses should default to the main agreement's end date or require explicit input for the date. A seller should never be able to accidentally add a regulatory term that expires before the main contract.

- **Multi-Entity MACC Date Logic:** When adding an additional customer entity to an existing MACC contract, the system should allow the new entity's commitment to start from the current date (or a date of their choosing) instead of forcing it to mirror the original commitment's past start date. The resulting amendment for the new entity should reflect the actual dates of that entity's participation in the contract.

- **Graceful Co-termination Handling:** If synchronising dates in a multi-entity scenario is required by business policy, the system should handle it gracefully (e.g. by explicitly stating that the new entity's commitment is for a shorter duration to align with the primary term) rather than showing an erroneous start date.

- **Load/Performance:** The system must continue to function smoothly when many terms are present (5 or more amendments). Date picker and form inputs should remain responsive – addressing the reported "sluggish calendar UI" issue.

**Dependencies & Notes:**

- The default behaviours for regulatory terms may be partially addressed by a recent hotfix (requiring explicit end dates). We will verify the current state and build upon it.
- Changes in date handling for multi-entity scenarios may require adjustments to the contract generation logic and potentially a new template for multi-entity MACC addendums.
- Thorough testing is needed for scenarios with multiple overlapping special terms.
- Coordination with the platform team may be needed to handle date validation rules.

---

## UI Screen Narratives

### 1. Term Library & Search Panel

**Purpose:**
Enable sellers to search, filter, and select appropriate contract terms efficiently.

**Key UI Elements:**
- Search bar with auto-suggest and fuzzy matching
- Filter panel (Region, Industry, Product, Term Type)
- Search results list:
  - Term title
  - Short description/snippet
  - "Preview" button
  - "Add to Proposal" button

**User Actions:**
- Type keyword or partial term name
- Apply filters
- Click "Preview" or "Add to Proposal"

**System Response:**
- Dynamically displays matching terms
- Filters results
- Opens Term Preview Modal or adds term to proposal

---

### 2. Term Preview Modal

**Purpose:**
Allow sellers to view full legal text and metadata of a term before adding it to a proposal.

**Key UI Elements:**
- Term title and version
- Full legal text (scrollable)
- Metadata (applicability, expiry rules)
- "Add to Proposal" button
- "Close" button

**User Actions:**
- Click "Preview" from Term Library
- Review term content
- Click "Add to Proposal" or "Close"

**System Response:**
- Loads and displays term content
- Adds term to proposal or closes modal

---

### 3. Proposal Builder – Configuration Tab

**Purpose:**
Configure terms, discounts, and product details efficiently.

**Key UI Elements:**
- List of added terms and products
- Editable fields (start/end dates, discount %, quantities)
- "Apply to All" bulk action buttons
- "Link Fields" toggle
- Default indicators

**User Actions:**
- Edit fields
- Select items and apply bulk actions
- Toggle field linking

**System Response:**
- Applies changes to selected items
- Highlights updated fields
- Validates inputs

---

### 4. Proposal Approvals Panel

**Purpose:**
Manage and track internal approvals for non-standard terms or discounts.

**Key UI Elements:**
- Approval status tracker
- Approver selection dropdown with role labels
- Approval history log
- "Send for Approval" button

**User Actions:**
- Select approvers
- Click "Send for Approval"
- View approval history

**System Response:**
- Validates approver eligibility
- Sends approval request
- Logs decisions and updates status

---

### 5. Signature Status Dashboard

**Purpose:**
Provide real-time visibility into the signing and acceptance process.

**Key UI Elements:**
- Timeline of signature steps
- Status indicators (Pending, Signed, Accepted)
- Timestamps and signer names
- "Resend Reminder" button
- "Download Signed Agreement" link

**User Actions:**
- View signature status
- Send reminders
- Download final documents

**System Response:**
- Updates status in real-time
- Sends reminders
- Notifies seller of incomplete acceptance

---

### 6. Pricing Summary Preview

**Purpose:**
Display a summary of commercial terms included in the contract.

**Key UI Elements:**
- Table of SKUs, quantities, prices, discounts
- Commitment amounts
- Notes or disclaimers

**User Actions:**
- Review pricing summary
- Download or share with customer

**System Response:**
- Pulls data from proposal and CPQ systems
- Renders summary in contract preview and final PDF
- Flags missing pricing data

---

## Non-Functional Requirements

| No | Description | Priority | Related Metrics |
|----|-------------|----------|-----------------| 
| NFR1 | Term preview must load full clause text in <2 seconds under normal network conditions | P0 | M2 |
| NFR2 | Bulk field updates must apply to all selected items atomically (all succeed or all fail); support single Undo action | P0 | M1 |
| NFR3 | Approval logging must persist records for the lifetime of the contract plus a minimum of 7 years for audit compliance | P0 | M8 |
| NFR4 | Signature status updates must reflect the underlying e-sign provider status within 5 minutes of an event (e.g. signer opens document, signs) | P0 | M4 |
| NFR5 | The system must remain responsive (date-picker, form inputs) with 10+ amendments in a proposal — no UI lag >1s on field interaction | P1 | M7 |
| NFR6 | Signature tracking and notification logic must be implemented as a provider-agnostic abstraction layer supporting both Adobe Sign and DocuSign | P1 | M4 |
| NFR7 | All new APIs must return responses in <500ms at p95 under expected load | P1 | M1, M2 |
| NFR8 | Pricing Summary content must dynamically reflect the latest proposal data at the time of contract generation; must not be stale if deal is modified post-draft | P0 | M3 |
| NFR9 | Search indexing must support synonym metadata without requiring a code deploy to update (config-driven) | P2 | M2 |

---

## Product Dependencies & Risks

### Dependencies

| Dependency | Description | Impact if Unavailable |
|---|---|---|
| E-Signature API (Adobe Sign / DocuSign) | Required to pull real-time signature status events into PMW | Signature status tracker cannot function; sellers remain blind to signing progress |
| CPQ / Proposal Data Service | Required to populate Pricing Summary in contract package | Pricing Summary section cannot be generated; feature must be deactivated |
| Term Content Repository / API | Required to serve full clause text for in-tool previews | Term preview unavailable; sellers revert to downloading full contract PDFs |
| Finance / Policy — Material Change Rules | Required to define which edits trigger re-approval | Approval optimisation cannot be safely implemented without agreed rules |
| Legal Team — Pricing Summary Format Sign-off | Required before engineering can build the Pricing Summary contract section | Feature blocked until Legal approves format and wording |
| Org / Directory Service | Required to show approver role and region context in the selection UI | Approver UI improvement partially degraded; falls back to name-only display |
| Commerce Platform Team | May be required for multi-entity MACC date rule changes in contract assembly | MACC date fix may be delayed if platform dependency is not scoped early |

### Risks

| Risk | Impact | Likelihood | Mitigation |
|---|---|---|---|
| Legal approval of Pricing Summary format delayed, blocking FR6 | High | Medium | Engage Legal in discovery phase with a draft format before engineering begins; define interim scope (tooltips only) if Legal review extends past Sprint 2 |
| Material vs. non-material change rules not agreed with Finance before dev begins, causing re-work | High | Medium | Run a policy workshop in FY27 Q1; document agreed rules formally before FR4 engineering starts |
| DocuSign migration timeline changes break signature status integration | Medium | Medium | Build to a provider-agnostic abstraction layer (NFR6); test against both providers in staging |
| Bulk configuration "Apply to All" creates unintended overwrites on complex proposals | Medium | Low | Gate behind user confirmation dialog; require explicit Undo support; QA with scenarios of 20+ mixed items |
| Customer-first signing order not approved by Legal for standard deals | Medium | Medium | Scope as an opt-in with clear policy controls; prepare a gated rollout (pilot with select deals only) |
| Search synonym corpus insufficient at launch, limiting search improvements | Low–Medium | High | Staff content metadata enrichment sprint before feature launch; prioritise top-failure-mode terms from historical search logs |
| UI performance regressions introduced by new bulk action controls on complex proposals | Low | Low | Mandatory performance testing with 10+ amendment proposals before release; regression benchmarks in CI pipeline |

---

## Implementation Plan

### Release Strategy

Phased rollout aligned to FY27 quarters:

- **Phase 1 (FY27 Q1):** Internal dogfooding with select sellers in one region (EMEA or APAC). Focus on FR1 (search), FR2 (preview), and FR3 (bulk defaults) as highest-impact, lower-risk changes.
- **Phase 2 (FY27 Q2):** Expand to all regions. Add FR4 (approval optimisation + logging) and FR5 (signature tracking). Policy alignment with Finance/Legal required before this phase.
- **Phase 3 (FY27 Q3):** GA for all features including FR6 (Pricing Summary) — pending Legal sign-off — and FR7 (special term date handling). Rollback via feature flags if issues found.
- **Phase 4 (FY27 Q4):** FR8 (in-product guidance), field readiness materials, retrospective on metrics, and backlog refinement based on seller feedback.

Rollback approach: All features deployable behind feature flags, enabling targeted deactivation without full rollbacks.

### Preview Strategy

| Preview Element | Description |
|---|---|
| Target Audience | 5–10 Commercial Executives across EMEA and APAC who participated in the Jan–Feb 2026 research study (continuity feedback) |
| Duration | 4–6 weeks per phase |
| Success Criteria | Seller reports measurable reduction in time for term search and configuration; no critical data accuracy issues |
| Exit Criteria | <5% error rate on bulk operations; all P0 bugs resolved; seller NPS neutral or positive |
| Feedback Mechanism | Weekly check-in calls + in-tool feedback widget; tracked in ADO |

### Timing Estimates

> *Note: These are initial projections during scoping phase and subject to change once engineering is engaged.*

| Phase | Estimated Duration | Key Deliverables |
|---|---|---|
| Discovery & Policy Alignment | ~4 weeks | Material change rules agreed; Legal Pricing Summary draft approved; synonym corpus initial build |
| Design & Engineering Planning | ~4 weeks | UX mockups finalised; engineering estimates confirmed; ADO backlog populated |
| Phase 1 Development (FR1, FR2, FR3) | ~8 weeks | Search, preview, bulk defaults in staging |
| Phase 1 Testing & Dogfood | ~4 weeks | Internal seller testing; P0/P1 bug resolution |
| Phase 2 Development (FR4, FR5) | ~8 weeks | Approval logging, signature tracking in staging |
| Phase 2 Testing & Regional Rollout | ~4 weeks | All-region rollout of Phase 1+2 |
| Phase 3 Development (FR6, FR7) | ~6 weeks | Pricing Summary, MACC date fix, performance pass |
| Phase 3 GA | ~2 weeks | Full GA launch; communications to field |
| Phase 4 Guidance & Retrospective | ~4 weeks | In-product tooltips, sales playbook updates, metrics review |

---

## Open Items

| Open Question | Owner | ETA for Resolution |
|---|---|---|
| What constitutes a "material vs. non-material" change for approval re-triggering? | PM + Finance / Policy Lead | FY27 Q1 — before FR4 engineering begins |
| Has Legal agreed to the Pricing Summary format and wording? | PM + Legal | FY27 Q1 — before FR6 engineering begins |
| Is customer-first signing permitted for standard MCA-E deals? Under what conditions? | Legal | FY27 Q1 |
| Which e-sign provider will be active at Phase 2 launch — Adobe Sign or DocuSign? | e-Signature Integration Team | FY27 Q1 |
| Is the DORA / regulatory term explicit date fix confirmed in production, or still pending? | Engineering | Immediate |
| What is the data retention policy for approval audit logs? (Legal / Compliance guidance) | Legal / Compliance | FY27 Q1 |
| Does the Commerce Platform team own the MACC date assembly logic, or does it live in PMW? | Engineering | FY27 Q1 |
| Who owns synonym metadata enrichment for the term search corpus, and what is the initial seed? | PM + Content Management | FY27 Q1 |

---

## Dependency Analysis

> *Generated: February 25, 2026. Based on spec review across all functional requirements, non-functional requirements, open items, and risk sections.*

### Internal Dependencies

| # | Team / System | What They Need to Provide | Likely Blocking Date |
|---|---|---|---|
| 1 | **Finance / Deal Desk (Policy Lead)** | Formal definition of "material vs. non-material" change rules that determine when edits trigger a re-approval. Without agreed rules, FR4 (approval optimisation) cannot be safely engineered. | **FY27 Q1** — must be resolved in a policy workshop before Phase 2 development starts |
| 2 | **Legal / Compliance** | (a) Sign-off on the Pricing Summary format, wording, and disclaimer; (b) ruling on whether customer-first signing is permitted and under what conditions; (c) data retention policy for approval audit logs (minimum 7 years required by NFR3). All three block separate FR deliverables. | **FY27 Q1** — all three must be resolved before FR5/FR6 engineering begins in Phase 2/3 |
| 3 | **PMW Engineering / Platform Team** | Confirmation of whether MACC multi-entity date assembly logic lives in PMW or the Commerce Platform, affecting which team owns the FR7 fix. Also needed: confirmation that the DORA/regulatory term explicit-date hotfix is live in production. | **Immediately** (DORA fix confirmation); **FY27 Q1** (MACC ownership scoping) |
| 4 | **Commerce Platform Team** | If MACC date assembly lives on the platform side, they must expose a mechanism to set independent date ranges per entity for multi-entity MACC addenda. | **FY27 Q1** — must be scoped early to avoid delaying FR7 in Phase 3 |
| 5 | **Content Management Team** | Build and maintain the synonym/keyword metadata corpus for the term search index (FR1). Initial seed must prioritise terms with the highest historical search-failure rate. Also owns ongoing config-driven updates (NFR9 requires no code deploy for synonym updates). | **FY27 Q1** — must complete initial metadata sprint before Phase 1 FR1 launches |
| 6 | **Org / Directory Service (Identity)** | Expose approver role, title, and region context via API so the approver selection UI can display contextual labels (e.g. "Jane Doe – Finance (UK/EU)") rather than name only (FR4). | **FY27 Q2** — needed before Phase 2 launches; degraded fallback (name-only) is possible if delayed |
| 7 | **UX Design** | Finalised mockups for all FR1–FR8 UI changes, especially the term preview panel (modal vs. side-panel decision), the bulk-action controls, and the signature status dashboard. | **End of Discovery + Design phase (~8 weeks from start)** — before Phase 1 development begins |
| 8 | **Sales Operations / Field Readiness** | Updated seller playbooks, MCA-E training materials, and in-field FAQs for Phase 4 guidance improvements (FR8). | **FY27 Q4** — needed for final phase; not on critical path for earlier phases |

### External / System Dependencies

| # | Team / System | What They Need to Provide | Likely Blocking Date |
|---|---|---|---|
| 9 | **E-Signature Integration Team (Adobe Sign + DocuSign)** | Real-time webhook/API integration exposing per-signer status events (signed, pending, declined) into PMW's Signature tab (FR5, NFR4). Must support both providers simultaneously during the active migration. Also must confirm which provider will be live at Phase 2 launch. | **FY27 Q1** (provider confirmation); **FY27 Q2** (integration ready for Phase 2) |
| 10 | **CPQ / Proposal Data Service** | Expose a stable API or data feed of deal-level pricing details (SKUs, quantities, list price, agreed price/discount, MACC commitment amounts) to populate the FR6 Pricing Summary dynamically at contract generation time. Must reflect latest proposal data (NFR8 — no stale data). | **FY27 Q2–Q3** — must be available before Phase 3 FR6 development; early scoping needed in Discovery phase |
| 11 | **Term Content Repository (Backend)** | Expose an API to serve the full legal text of a single term by ID, with version awareness, for the FR2 in-tool preview feature. Must handle dynamic placeholders gracefully. Latency target: <2 seconds (NFR1). | **FY27 Q1** — needed before Phase 1 FR2 development; likely a quick win if the API exposure is straightforward |

### Critical Path Blockers Summary

| Priority | Dependency | Blocking Feature | Blocks Phase |
|---|---|---|---|
| 🔴 Critical | Finance/Policy — material change rules | FR4 (approval workflow) | Phase 2 |
| 🔴 Critical | Legal — Pricing Summary format sign-off | FR6 (contract pricing) | Phase 3 |
| 🔴 Critical | Legal — customer-first signing ruling | FR5 (configurable signing order) | Phase 2 |
| 🔴 Critical | E-Signature API (dual-provider support) | FR5 (signature tracking) | Phase 2 |
| 🟡 High | CPQ / Proposal Data Service API | FR6 (pricing summary content) | Phase 3 |
| 🟡 High | Term Content Repository API | FR2 (term preview) | Phase 1 |
| 🟡 High | Content Management (synonym corpus) | FR1 (smarter search) | Phase 1 |
| 🟡 High | Commerce Platform — MACC date logic ownership | FR7 (multi-entity date fix) | Phase 3 |
| 🟢 Medium | Org/Directory Service (approver roles) | FR4 (approver UI enrichment) | Phase 2 |
| 🟢 Medium | Engineering — DORA hotfix production confirmation | FR7 (term date alignment) | Immediate |

> **Key watch item:** Three of the four Phase 2 features (FR4, FR5) are blocked on Legal and Finance policy decisions that must be resolved in FY27 Q1 via a dedicated policy workshop. If those rulings slip, Phase 2 and everything downstream shifts accordingly.

---

## Appendix

### Key Terminology

| Term | Description |
|---|---|
| **NX Terms** | The contract terms management module within PMW used to configure MCA-E deal terms (clauses, amendments, addenda) for enterprise deals |
| **PMW** | Proposal Management Workspace — the internal seller tool used to manage Microsoft enterprise sales proposals end-to-end |
| **MCA-E** | Microsoft Customer Agreement – Enterprise. The new standard enterprise agreement replacing the EA/VLC for New Commerce transactions |
| **EA / VLC** | Enterprise Agreement / Volume Licensing Contract — the legacy Microsoft enterprise agreement model |
| **MACC** | Multi-entity Azure Commitment — a commercial commitment structure where multiple customer entities participate under a single Azure consumption commitment |
| **MCA** | Microsoft Customer Agreement — the underlying legal framework for MCA-E |
| **Deal Desk** | Internal Microsoft team (Finance / Operations) that reviews and approves non-standard deal terms, discounts, and exceptions |
| **Commercial Executive (CE)** | Front-line Microsoft seller (account executive or deal manager) responsible for managing enterprise sales proposals and customer relationships |
| **DORA** | Digital Operational Resilience Act — an EU regulatory framework for financial services; a DORA addendum clause may be required for qualifying customers |
| **Checkout / Acceptance** | The post-signature step in New Commerce where the customer must actively confirm their agreement in the commerce portal to activate the deal |
| **DocuSign / Adobe Sign** | E-signature services used to manage digital signing of MCA-E contracts; a migration from Adobe Sign to DocuSign was underway as of late 2025 |
| **CPQ** | Configure-Price-Quote system — upstream system that holds deal pricing and discount details used to generate proposals |
| **Feature Flag** | A configurable software switch that enables/disables a feature at runtime without a code deployment; used for phased rollouts and rollbacks |
| **P0 / P1 / P2** | Priority tiers: P0 = Must have (launch blocker), P1 = Important (not a launch blocker), P2 = Nice to have (can be deferred) |

### References

| Reference | Link |
|---|---|
| Product Spec Template | `commerce-docs/.github/prompts/snippets/templates/product-spec-template.md` |
| Vision Document Template | `commerce-docs/internalDocs/product_management/vision-document-template.md` |
| NX Terms Research Interview Media | *(SharePoint — access required: Enterprise Commerce Studio > General > Knowledge tank > 2026_NX terms)* |
| NX Terms Research Data | *(SharePoint — access required: Enterprise Commerce Studio > Shared Documents)* |
| Commerce Substrate Capability Taxonomy | https://eng.ms/docs/office-of-coo/commerce-ecosystems/commerce-platform-experiences/commerce-platform-documentation/resources/taxonomy |
