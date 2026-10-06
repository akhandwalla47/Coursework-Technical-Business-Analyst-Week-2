# Phase 1 Scope Template

Use this to define a disciplined Smart-Recovery first release.

OP-01: Self-Service Balance Lookup Portal
OP-02: Automated Payment Plan Selection
OP-03: Promise-to-Pay Confirmation & Alerts
OP-04: Automated Queue Triage & Allocation
OP-05: Shift Handoff & Audit Trail Logging

## In scope

List the capabilities you believe should be built in Phase 1.


- Authentication & Access - Lightweight, 2-factor customer identity verification (date of birth + OTP sent to registered mobile/email).
- Account Summary & Visibility - Real-time balance lookup, overdue payment status display, and clear breakdown of outstanding charges.
- Self-Service Payment Plan Engine - Interactive selection of pre-approved 3–6 month payment plans for early-stage delinquency (1–29 DPD).
- Promise-to-Pay Capture & Reminders - Single-click promise date selection with automated instant SMS/email receipts and calendar reminders.
- Automated Queue Triage Engine - Routing logic that intercepts 38% straightforward case volume (BM-02) and diverts them to self-service.
- Real-time Operational Dashboards - Basic operational reporting for team leaders showing portal conversion rates, routed case reasons, and freed capacity.

Justification for Inclusions:
1. Maximises Hard Efficiency and Volume Reduction (OP-01 & OP-04):
    OP-01 directly eliminates the largest administrative bottleneck in the activity log—2,468 view_status and 1,894 spreadsheet_reconcile tasks (BM-16). Combining this with OP-04 intercepts 38,000 straightforward accounts (BM-02) before they reach representative queues, saving 60,800 operational hours annually (£1,337,600 in hard labor savings). 
2. High Customer Impact & Revenue Uplift (OP-02 & OP-03):
    OP-02 and OP-03 target the 40% of customers who prefer self-resolution (SN-099). They eliminate 'awaiting callback' queue stagnation (SN-007, SN-053) and unlock £6.24M in potential annual recovery uplift.
3. Low Implementation Friction & High Feasibility (Priya & Daniel):
    Bundling OP-01, OP-03, and OP-04 leverages low-complexity technical patterns (£45k each). Total Phase 1 capital expenditure is capped at £260,000, which is fully paid back by hard labor savings alone in under 2.5 months.   
4. Mitigates Key ADKAR Risks:
    Including context-rich hand-off attachments ensures representatives do not reject portal-routed cases (SN-108). Framing the portal as an "admin shield" addresses job security fears (SN-097).   

## Out of scope

- Automated Shift Handoff & Audit Trail Logging (OP-05) - Lower Direct Customer Value: While valuable for internal compliance (SN-008, SN-040), OP-05 does not directly reduce incoming customer call volumes or enable online payments. Deferring it avoids over-engineering Phase 1.
- Hardship & Vulnerability Auto-Decisions - Regulatory Risk & Lack of Human Oversight: Cases involving financial hardship, mental health vulnerability, or regulatory forbearance require human empathy and complex judgment (SN-041, SN-054). Automating these decisions creates severe regulatory exposure.
- Late-Stage / Legal Watch Cases (>60 DPD) - High Financial & Legal Risk: Late-stage debts require bespoke legal negotiation and specialist intervention (SN-055). Pushing high-risk accounts to self-service violates the bank risk rules/ policies.   

## Deliverable planning

| Deliverable Name | Targeted Completion Date | Estimated Time Required | Potential Blockers & Dependencies |Justification & Risk Strategy |
|---|---|---|---|---|

Deliverable 1: ADKAR & Scope Definition | Monday, 5 Oct | 3.5 hours | Delay in setting clear scope boundaries; stakeholder misalignment on exclusions. | Setting strict Phase 1 scope early prevents scope creep and ensures all downstream workflow, backlog, and prototype design remain focused and buildable.

Deliverable 2: To-Be Process Map (Camunda) | Tuesday, 6 Oct | 3.5 hours | Over-complicating exception paths or missing key human hand-off steps. | Mapping the complete To-Be process requires dedicated concentration. Completing it on Tuesday creates the visual blueprint needed for Wednesday's backlog writing.

Deliverable 3: Prioritised Jira Backlog | Wednesday, 7 Oct | 2.0 hours | Tight 2-hour window due to PHP workshop & interview power hour; ambiguous story acceptance criteria. | Drafting stories directly from Tuesday's Camunda diagram speeds up writing. Using Given/When/Then acceptance criteria ensures stories are testable for Priya.

Deliverable 4: Clickable Prototype & Briefing Deck | Thursday, 8 Oct | 3.5 hours | Getting bogged down in CSS styling; formatting slides instead of refining narrative logic. | Combining the Copilot prototype build and Pyramid Principle slide deck on Thursday brings all evidence together into a single, cohesive approval package for leadership.

## Assumptions

Record what must be true for this scope to work.

- Legacy database records required for basic account summary and balance checks are accessible enough to support real-time lookup during Phase 1.
- Eligibility rules for 3–6 month self-service payment plans can be agreed with Finance and Operations without requiring a full credit policy redesign.
- Phased Rollout Support: Operations leadership will support a phased rollout, starting with a limited pilot on straightforward, early-stage delinquent accounts (1–29 days past due).
- Messaging Triggers: Outbound communication channels (SMS and email) can be triggered automatically to send customers secure portal access links and instant receipts.  

## Dependencies and constraints

Note the most important delivery and operating constraints.

- Real-time balance checks depend on reliable API data retrieval from the bank's core legacy database without introducing system latency.
- All customer-facing portal text, payment plan terms, and automated confirmation messages require formal compliance sign-off prior to launch (SN-019).
- Routed cases must automatically attach full portal session logs so representatives do not make customers repeat information (SN-036, SN-108).
- The delivery schedule is restricted to a tight Phase 1 development window with capped starter capital (£260,000 total investment). 

## Why this scope is credible

Write 1-2 paragraphs linking the chosen scope to:
- Week 1 top-ranked opportunities
- measurable value
- delivery feasibility
- change and adoption risk

This Phase 1 scope is directly grounded in our top-ranked discovery opportunities: Self-Service Balance Lookup (OP-01), Automated Payment Plan Selection (OP-02), and Promise-to-Pay Confirmation (OP-03), underpinned by Automated Queue Triage (OP-04). By focusing strictly on early-stage, low-risk delinquent accounts (representing 38% of the total portfolio), the solution removes the single largest administrative drain on the bank - over 4,300 monthly status checks and spreadsheet reconciliations (BM-16). This delivers 60,800 annual hours saved (£1,337,600 in hard labor savings), ensuring the project achieves full payback in under 2.5 months on labor efficiency alone.

From a delivery and change perspective, the plan is highly feasible and carries low adoption risk. By keeping initial setup simple (£45k to £85k per tool) and excluding complex edge cases like financial hardship and balance disputes, we avoid over-complex technical engineering and scope creep. Framing the portal as an "admin shield" for representatives, while enforcing context-rich hand-offs when cases require human support, directly resolves staff insecurity (SN-097) and ensures operational buy-in from day one (SN-108). 
