# Phase 1 Scope & Delivery Readiness Plan

**Project:** Smart-Recovery Portal  
**Target Portfolio:** Early-Stage Delinquency (1–29 Days Past Due)  
**Author:** Business Analysis Lead  
**Target Audience (Stakeholders):** Senior Leadership (Daniel Okoye, Priya Nair, Gareth Evans)  

---

## 1. Opportunities & Strategic Priorities

The following high-value Opportunities (**OPs**) were identified and ranked during Week 1 Discovery:

* **OP-01: Self-Service Balance Lookup Portal** — Allows customers to authenticate and view real-time balance details online without calling a representative.
* **OP-02: Automated Payment Plan Selection** — Enables self-service selection of pre-approved 3–6 month instalment arrangements.
* **OP-03: Promise-to-Pay Confirmation & Alerts** — Captures future payment commitments with automated SMS/email reminders.
* **OP-04: Automated Queue Triage & Allocation** — Background routing logic that diverts straightforward accounts away from manual phone queues.
* **OP-05: Shift Handoff & Audit Trail Logging** — Internal compliance tool for representative logging across shift changes.


## 2. Phase 1 In-Scope System Capabilities & Justifications

The capabilities selected for Phase 1 combine **OP-01, OP-02, OP-03, and OP-04** into a single, cohesive user journey. The table below outlines each specific feature alongside its business and operational justification.

| System Capability | Target Opportunity | Specific Technical & Functional Scope | Unified Business & ROI Justification |
| :--- | :--- | :--- | :--- |
| **Authentication & Access** | **OP-01 (Rank 1)** | • 2-Factor Identity Verification (Account Ref + DOB + 6-digit SMS/Email OTP)<br>• Hard lockout after 3 failed verification attempts with automated queue escalation (`VER-01`). | **Compliance & Security:** Replaces manual representative security checks while ensuring strict FCA data privacy compliance (`VER-01`). |
| **Account Summary & Visibility** | **OP-01 (Rank 1)** | • Real-time display of Total Outstanding Balance, Overdue Amount, Days Past Due (1–29 DPD), and account status (`VIS-01`) retrieved directly from the legacy database. | **High Volume Elimination:** Directly removes 2,468 `view_status` and 1,894 `spreadsheet_reconcile` manual rep tasks monthly (`BM-16`), saving £1.34M in annual labor overhead. |
| **Self-Service Payment Plan Engine** | **OP-02 (Rank 2)** | • Interactive selection of pre-approved 3, 4, 5, or 6-month instalment options for early-stage accounts (`PAY-01`) with automatic write-back to the legacy database. | **High Revenue Impact:** Addresses 40% of customers preferring self-resolution (`SN-099`), unlocking up to £3.84M in annual recovery uplift (`FA-07`). |
| **Promise-to-Pay Capture & Reminders** | **OP-03 (Rank 3)** | • Calendar date selection for future payment promises up to 28 days out (`PAY-02`) with automated instant SMS/email confirmation receipts (`REP-01`). | **Queue Stagnation Fix:** Eliminates 'awaiting callback' queue stagnation (`SN-007`, `SN-053`) and unlocks £3.07M in annual recovery uplift. |
| **Automated Queue Triage Engine** | **OP-04 (Rank 4)** | • **Placement:** API microservice layer sitting between the DB and rep worklists.<br>• **Specific Triage Logic:** Intercepts 38% of total accounts (`BM-02` = 38,000 out of 100,000 accounts flagged as 1–29 DPD with `risk_flag = N` and no hardship history) and steers them to SMS/portal self-service instead of rep worklists. | **Operational Efficiency:** Prevents 38% of simple cases from entering manual phone queues, freeing 60,800 representative hours annually. |
| **Context-Rich Representative Hand-Off** | **ADKAR Mitigation (CR-02)** | • Mandatory data payload bundler (`RTE-02`) attached to all escalated or abandoned portal sessions, containing: Session ID, DOB Auth Status, Pages Viewed, and Exit Reason Code. | **ADKAR Adoption Shield:** Eliminates representative rejection of portal-routed tickets (`SN-108`) and prevents customers repeating details (`SN-036`). |
| **Operational Management Dashboard** | **Priya Metric Alignment** | • Real-time manager dashboard (`REP-02`) tracking exactly **3 management metrics**:<br>1. *Self-Service Conversion Rate* (% 1–29 DPD resolved online)<br>2. *AHT & Hours Saved* (Reduction in manual status calls)<br>3. *Context Attachment Rate* (% routed cases with complete logs). | **Observability:** Satisfies Gareth's need for real-time pipeline visibility without scope creep. |

---

## 3. Explicit Exclusions & Scope Boundaries

To protect the delivery schedule and prevent technical over-engineering, the following items are strictly **Out of Scope**:

* **OP-05: Shift Handoff & Audit Trail Logging:**  
  * *Justification:* Internal operational tool (`SN-008`, `SN-040`). While valuable for compliance, it does not directly reduce incoming customer call volumes or generate recovery revenue. Deferred to **Phase 2**.
* **Automated Hardship & Vulnerability Decisions:**  
  * *Justification:* Cases involving financial hardship, mental health vulnerability, or regulatory forbearance (`SN-041`, `SN-054`) require human empathy and flexible judgment. Automating these decisions creates severe FCA regulatory risk. These remain **100% human-led**.
* **Disputed Balance Resolutions:**  
  * *Justification:* Customers contesting fees or balance calculations (`SN-120`) cannot be settled via automated 3–6 month rules. Excluded to prevent customer friction.
* **Late-Stage / High-Risk Accounts (>60 DPD or `risk_flag = Y`):**  
  * *Justification:* Requires specialist negotiation and legal oversight (`SN-055`). Kept strictly with specialist human representatives.

---

## 4. Deliverable Planning Schedule

| Deliverable Name | Targeted Completion Date | Estimated Time Required | Potential Blockers & Dependencies | Justification & Risk Strategy |
| :--- | :--- | :---: | :--- | :--- |
| **Deliverable 1: ADKAR & Scope Definition** | Monday, 5 Oct | 3.5 hours | Delay in setting clear scope boundaries; stakeholder misalignment on exclusions. | Setting strict Phase 1 scope early prevents scope creep and ensures all downstream workflow, backlog, and prototype design remain buildable. |
| **Deliverable 2: To-Be Process Map (Camunda)** | Tuesday, 6 Oct | 3.5 hours | Over-complicating exception paths or missing key human hand-off steps. | Mapping the complete To-Be process creates the visual blueprint needed for Wednesday's backlog writing. |
| **Deliverable 3: Prioritised Jira Backlog** | Wednesday, 7 Oct | 2.0 hours | Tight 2-hour window due to PHP workshop & interview power hour; ambiguous acceptance criteria. | Drafting stories directly from Tuesday's Camunda diagram speeds up writing and ensures stories are testable for Priya. |
| **Deliverable 4: Clickable Prototype & Briefing Deck** | Thursday, 8 Oct | 3.5 hours | Getting bogged down in CSS styling; formatting slides instead of refining narrative logic. | Combining the Copilot prototype build and Pyramid Principle slide deck brings all evidence together into a single approval package. |

---

## 5. Assumptions, Dependencies & Constraints

### Key Assumptions
* **Legacy DB Read Accessibility:** Legacy database records required for basic account summary and balance checks are accessible via simple read-APIs during Phase 1.
* **Policy Rule Agreement:** Eligibility rules for pre-approved 3–6 month payment plans can be agreed with Compliance without requiring a full credit policy overhaul.
* **Phased Pilot Support:** Operations leadership will support a phased rollout starting with a 10% pilot on early-stage delinquent accounts (1–29 DPD).

### Dependencies & Constraints
* **Legacy System Data Retrieval:** Real-time balance checks depend on API response times from the core 20-year-old legacy database without causing system latency.
* **Compliance Approval:** All customer-facing portal text, payment plan terms, and automated confirmation messages require formal compliance sign-off prior to launch (`SN-019`).
* **Outbound Messaging Channel:** Automated SMS and email confirmation receipts rely on integration with the bank's existing outbound messaging gateway.
* **Fixed Budget Constraint:** Phase 1 capital expenditure is capped at **£260,000**.

---

## 6. Why This Scope Is Credible (Base Case vs. Risk-Adjusted Return)

This Phase 1 scope is directly grounded in our top-ranked discovery opportunities: **Self-Service Balance Lookup (OP-01)**, **Automated Payment Plan Selection (OP-02)**, and **Promise-to-Pay Confirmation (OP-03)**, underpinned by **Automated Queue Triage (OP-04)**. By focusing strictly on early-stage, low-risk delinquent accounts (representing **38% of total portfolio volume** / 38,000 accounts), the solution directly removes over 4,300 monthly manual status checks and spreadsheet reconciliations (`BM-16`). 

### Financial Payback Realism:
* **Base Case (Happy Path):** Assuming 100% target digital adoption across the 38% eligible population, the system saves **60,800 operational hours annually** (£1,337,600 in hard labor efficiency), delivering full capital payback on the £260k investment in **2.33 months**.
* **Risk-Adjusted Case (Factoring ADKAR Adoption Drag):** Factoring in realistic change adoption risks—such as initial customer unawareness (`CR-03`) and representative friction during ramp-up (`CR-01`)—a conservative **50% adoption rate** in Year 1 still saves 30,400 operational hours (£668,800 in hard labor savings). This achieves full capital payback in **4.6 months**, proving that the business case remains exceptionally strong even under pessimistic operational conditions.

From a delivery and risk perspective, this scope avoids technical over-engineering by excluding complex edge cases like financial hardship and balance disputes. Framing the portal as an "admin shield" for representatives—while enforcing context-rich hand-offs when cases require human support—directly resolves staff insecurity (`SN-097`) and ensures operational buy-in from day one (`SN-108`).