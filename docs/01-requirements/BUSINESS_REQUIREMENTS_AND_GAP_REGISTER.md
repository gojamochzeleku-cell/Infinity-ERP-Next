# INFINITY ERP NEXT
## Business Requirements and Gap Register

**Document:** 02 — Business Requirements and Gap Register  
**Version:** 1.0  
**Status:** Initial requirements baseline — subject to business validation  
**Organization:** Infinity Investment Group  
**Companies in initial scope:** YAH and CHI  
**Source baseline:** Existing ERP functional inventory and Master Blueprint

---

# 1. PURPOSE

This document defines the business capabilities, controls and expected outcomes required from Infinity ERP Next.

It has five purposes:

1. Establish what the new ERP must accomplish.
2. Identify gaps between the inspected existing ERP and the target system.
3. Prioritize requirements according to business importance.
4. Define measurable acceptance criteria.
5. Provide a traceable foundation for architecture, database design and implementation.

This is a requirements baseline, not an authorization to modify the existing production ERP.

# 2. REQUIREMENT CLASSIFICATION

## 2.1 Priority levels

| Priority | Meaning |
|---|---|
| P0 — Critical | Mandatory for platform safety, financial integrity or core business operation |
| P1 — High | Essential business capability for the relevant implementation phase |
| P2 — Medium | Important improvement or supporting capability |
| P3 — Future | Advanced capability that can follow stable core implementation |

## 2.2 Requirement status

| Status | Meaning |
|---|---|
| Confirmed | Explicitly established by the project scope or user decision |
| Observed | Identified in inspected existing source code |
| Proposed | Recommended target capability awaiting business approval |
| To validate | Requires business walkthrough, source inspection or evidence |
| Approved | Formally accepted by the project owner |
| Implemented | Built in the new ERP |
| Accepted | Verified against its acceptance criteria |

An observed feature is not automatically considered complete, reliable or accepted.

## 2.3 Requirement types

- BR: Business requirement.
- SEC: Security requirement.
- FIN: Financial control requirement.
- DAT: Data and records requirement.
- AI: Artificial intelligence requirement.
- INT: Integration requirement.
- OPS: Operational requirement.
- UX: User experience requirement.
- MIG: Migration requirement.
- REP: Reporting requirement.

# 3. BUSINESS REQUIREMENTS

## 3.1 Organization and multi-company operations

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-ORG-001 | The system shall support multiple companies under Infinity Investment Group. | P0 | Confirmed |
| BR-ORG-002 | YAH and CHI shall operate within the same platform with independent company data scopes. | P0 | Confirmed |
| BR-ORG-003 | The system shall support adding future companies without redesigning the platform. | P1 | Proposed |
| BR-ORG-004 | Users shall have explicit memberships in the companies they are authorized to access. | P0 | Confirmed |
| BR-ORG-005 | A user's role in one company shall not automatically grant authority in another company. | P0 | Confirmed |
| BR-ORG-006 | Authorized group reporting shall consolidate data without bypassing company access controls. | P0 | Proposed |
| BR-ORG-007 | Company-specific settings, numbering and approval rules shall be configurable. | P1 | Proposed |
| BR-ORG-008 | Intercompany transactions shall be separately identifiable and auditable. | P1 | Proposed |

Acceptance criteria:

- A user without membership in a company cannot read or modify that company's records.
- Company switching changes the server-validated authorization context.
- Company-specific records remain isolated in lists, details, exports, search and downloads.
- Authorized consolidated reporting includes only companies the user is permitted to view.
- Intercompany transactions retain both company references and appropriate accounting treatment.

## 3.2 Identity, roles and authorization

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-IAM-001 | One user identity shall support memberships in multiple companies. | P0 | Confirmed |
| BR-IAM-002 | Company roles and permissions shall be membership-scoped. | P0 | Confirmed |
| BR-IAM-003 | Company ADMIN shall only administer its authorized company. | P0 | Confirmed |
| BR-IAM-004 | The system shall not introduce SUPERADMIN as a business role. | P0 | Confirmed |
| BR-IAM-005 | The platform shall not depend on unrestricted Django superuser access for normal administration. | P0 | Confirmed |
| BR-IAM-006 | Access to sensitive actions shall be checked on the server. | P0 | Proposed |
| BR-IAM-007 | Role changes, membership changes and privilege changes shall be audited. | P0 | Proposed |
| BR-IAM-008 | Approval authority shall support limits and separation of duties. | P0 | Proposed |
| BR-IAM-009 | User activation, suspension and membership termination shall be controlled. | P1 | Proposed |
| BR-IAM-010 | Authentication shall support stronger security controls, including optional MFA. | P1 | Proposed |

Acceptance criteria:

- Company ADMIN cannot administer another company without a separate authorized membership.
- A disabled membership cannot be used to access company data.
- Permission checks apply to API requests, page actions, file downloads and background operations.
- Privilege changes identify the actor, target, company, previous value, new value and timestamp.
- No ordinary business workflow requires unrestricted system-wide administrator privileges.

## 3.3 Tender discovery and management

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-TND-001 | Users shall register and track tender opportunities. | P0 | Observed |
| BR-TND-002 | Tender documents shall be securely stored and linked to the tender. | P0 | Observed |
| BR-TND-003 | The system shall track deadlines and submission requirements. | P0 | Observed |
| BR-TND-004 | Technical and commercial compliance shall be separately reviewable. | P0 | Proposed |
| BR-TND-005 | Tender preparation shall support multiple assigned participants. | P1 | Proposed |
| BR-TND-006 | Bid decisions and approvals shall retain their evidence and history. | P0 | Proposed |
| BR-TND-007 | Submission evidence and submission timestamps shall be recorded. | P0 | Observed |
| BR-TND-008 | Award, rejection and cancellation outcomes shall be recorded. | P1 | Observed |
| BR-TND-009 | Tender amendments and addenda shall be versioned. | P1 | Proposed |
| BR-TND-010 | Tender and bid records shall connect to procurement and execution records. | P0 | Proposed |

Acceptance criteria:

- Each tender has a unique company-scoped reference.
- Mandatory documents and requirements can be checked before submission.
- Submission evidence is retained and linked to the correct tender.
- Changes to critical tender information are traceable.
- Awarded tenders can be handed over without losing bid history or approval records.

## 3.4 Tender workflow and approvals

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-WF-001 | Business workflows shall support defined stages and authorized transitions. | P0 | Observed |
| BR-WF-002 | Existing T02–T24 workflow identifiers shall be preserved or explicitly mapped. | P0 | Confirmed |
| BR-WF-003 | Existing I01–I16 workflow identifiers shall be preserved or explicitly mapped. | P0 | Confirmed |
| BR-WF-004 | Workflow actions shall verify company membership and authority. | P0 | Proposed |
| BR-WF-005 | Approval requests shall record decisions, comments and timestamps. | P0 | Proposed |
| BR-WF-006 | Workflows shall support return, rejection, cancellation and revision paths. | P1 | Proposed |
| BR-WF-007 | Delegation shall be limited, time-bound and auditable. | P1 | Proposed |
| BR-WF-008 | Approval limits shall support financial and operational thresholds. | P1 | Proposed |
| BR-WF-009 | Workflow delays shall support reminders and escalation. | P1 | Proposed |

Acceptance criteria:

- Unauthorized users cannot advance, approve or bypass a workflow.
- Each transition records the actor, time, previous stage and new stage.
- Rejected and returned work retains its previous evidence and comments.
- Existing workflow identifiers have documented migration mappings.
- Approval limits are enforced server-side.

## 3.5 AI War Room and bid intelligence

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-AI-001 | AI shall assist with tender document analysis. | P1 | Observed |
| BR-AI-002 | AI shall extract technical and commercial requirements. | P1 | Observed |
| BR-AI-003 | AI shall identify missing, unclear and conflicting information. | P1 | Proposed |
| BR-AI-004 | AI conclusions shall link to supporting source evidence where available. | P0 | Proposed |
| BR-AI-005 | AI shall distinguish verified, user-input, calculated, estimated and pending information. | P0 | Confirmed |
| BR-AI-006 | AI-generated commercial calculations shall expose their assumptions and formulas. | P0 | Proposed |
| BR-AI-007 | AI shall assist with product and supplier comparisons. | P1 | Observed |
| BR-AI-008 | AI shall support structured reports and downloadable work products. | P1 | Observed |
| BR-AI-009 | AI shall not approve tenders or commit expenditure independently. | P0 | Confirmed |
| BR-AI-010 | Human review and approval shall be available for consequential AI outputs. | P0 | Confirmed |
| BR-AI-011 | AI provider failures shall not block ordinary ERP operations. | P0 | Proposed |
| BR-AI-012 | AI usage, provider, model and relevant errors shall be traceable. | P1 | Proposed |

Acceptance criteria:

- Every material AI finding identifies its source or is marked unsupported/pending.
- Missing input is not silently replaced with invented values.
- AI-generated calculations expose inputs, formulas and currency.
- Users can review and correct AI output before business use.
- Provider failure does not prevent users from accessing existing tender records.
- AI cannot independently approve a bid, purchase order or financial posting.

## 3.6 Supplier, manufacturer and product management

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-SUP-001 | The system shall maintain supplier profiles. | P1 | Observed |
| BR-SUP-002 | Manufacturer and supplier identities shall be distinguishable. | P1 | Proposed |
| BR-SUP-003 | Supplier qualification and verification evidence shall be retained. | P1 | Proposed |
| BR-SUP-004 | Supplier quotations and price history shall be traceable. | P1 | Proposed |
| BR-SUP-005 | Supplier performance shall be measurable. | P2 | Proposed |
| BR-PRD-001 | The system shall maintain a structured product catalog. | P1 | Observed |
| BR-PRD-002 | Products shall support manufacturer, model and part number. | P1 | Proposed |
| BR-PRD-003 | Technical specifications shall support structured comparison. | P1 | Proposed |
| BR-PRD-004 | Product alternatives and equivalent models shall be documented. | P2 | Proposed |
| BR-PRD-005 | Product revisions and supporting technical documents shall be retained. | P2 | Proposed |

Acceptance criteria:

- A supplier can be linked to multiple products and quotations.
- A manufacturer can be linked to multiple suppliers.
- Technical comparisons use normalized attributes and units where possible.
- Supplier qualification status has evidence and review history.
- Product substitutions retain the original requested specification and approval.

## 3.7 Procurement and purchasing

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-PUR-001 | Purchase requisitions shall be traceable to a company and requesting user. | P1 | Proposed |
| BR-PUR-002 | Purchase requisitions shall support budget and approval checks. | P1 | Proposed |
| BR-PUR-003 | Supplier quotations shall be comparable. | P1 | Observed |
| BR-PUR-004 | Purchase orders shall be controlled and versioned. | P1 | Proposed |
| BR-PUR-005 | Purchase orders shall link to tender, contract or other authorized demand. | P1 | Proposed |
| BR-PUR-006 | Goods receipt shall be matched against authorized orders. | P1 | Proposed |
| BR-PUR-007 | Invoice matching shall identify price and quantity differences. | P1 | Proposed |
| BR-PUR-008 | Purchase returns and order amendments shall be recorded. | P2 | Proposed |

Acceptance criteria:

- Purchase orders cannot be issued without required approval.
- Goods receipt records identify the relevant purchase order and line.
- Quantity and price variances are visible before invoice approval.
- Order amendments preserve prior versions and approvals.

## 3.8 Import, landed cost and logistics

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-IMP-001 | Import files shall group supplier and customs documents. | P1 | Observed |
| BR-IMP-002 | Import documents shall support status, expiry and verification. | P1 | Proposed |
| BR-IMP-003 | Exchange rates shall retain source and effective date. | P0 | Proposed |
| BR-LC-001 | Landed cost shall include configurable cost components. | P0 | Proposed |
| BR-LC-002 | Costs shall be allocated to shipment and item levels. | P0 | Proposed |
| BR-LC-003 | Allocation methods shall be recorded and reproducible. | P0 | Proposed |
| BR-LC-004 | Estimated and actual costs shall be distinguishable. | P0 | Proposed |
| BR-LC-005 | Uncertain and duplicate-looking costs shall be flagged for review, not silently removed. | P0 | Confirmed |
| BR-LC-006 | Landed cost variance shall be reported. | P1 | Proposed |
| BR-LOG-001 | A tender or purchase order shall support multiple shipments where required. | P1 | Proposed |
| BR-LOG-002 | Partial shipments and partial deliveries shall be supported. | P1 | Proposed |
| BR-LOG-003 | Shipment milestones and documents shall be traceable. | P1 | Observed |
| BR-LOG-004 | Customs clearance and inland delivery shall be tracked. | P1 | Observed |
| BR-LOG-005 | Damage, shortage and insurance claims shall be recorded. | P2 | Proposed |

Acceptance criteria:

- Every landed cost amount links to its source document or approved user input.
- Allocation totals reconcile to the amount being allocated, subject to documented rounding.
- The system shows allocation method, rate and calculation basis.
- Unknown cost inclusion is explicitly visible.
- Multiple shipment records can be linked to one tender or purchase order.
- Shipment quantities reconcile with received and delivered quantities.

## 3.9 Inventory and warehouse

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-INV-001 | The system shall maintain company-scoped warehouses. | P1 | Proposed |
| BR-INV-002 | Stock movements shall have source transactions. | P0 | Observed |
| BR-INV-003 | Goods receipt and goods issue shall be auditable. | P0 | Proposed |
| BR-INV-004 | Stock transfers shall preserve source and destination. | P1 | Proposed |
| BR-INV-005 | Stock reservations shall prevent uncontrolled allocation. | P1 | Proposed |
| BR-INV-006 | Inventory valuation shall use an approved accounting method. | P1 | Proposed |
| BR-INV-007 | Physical counts shall support reconciliation. | P1 | Proposed |
| BR-INV-008 | Damaged, quarantined and available stock shall be distinguishable. | P1 | Proposed |

Acceptance criteria:

- Stock balances can be reconstructed from posted movements.
- A movement cannot silently change another company's inventory.
- Transfers create linked issue and receipt records.
- Stock adjustments require authority and a reason.
- Inventory valuation reconciles to the approved valuation method.

## 3.10 Accounting and finance

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-FIN-001 | The system shall maintain a chart of accounts. | P0 | Proposed |
| BR-FIN-002 | The system shall support double-entry journal entries. | P0 | Proposed |
| BR-FIN-003 | Posted entries shall have equal debit and credit totals. | P0 | Proposed |
| BR-FIN-004 | Posted entries shall not be silently overwritten or deleted. | P0 | Proposed |
| BR-FIN-005 | The system shall support accounts payable. | P0 | Proposed |
| BR-FIN-006 | The system shall support accounts receivable. | P0 | Proposed |
| BR-FIN-007 | The system shall support bank and cash reconciliation. | P1 | Proposed |
| BR-FIN-008 | The system shall support accounting periods and period locks. | P0 | Proposed |
| BR-FIN-009 | Multi-currency transactions shall retain transaction and functional currency values. | P0 | Proposed |
| BR-FIN-010 | Exchange gains and losses shall be calculated and traceable. | P1 | Proposed |
| BR-FIN-011 | Financial reports shall reconcile to posted ledger entries. | P0 | Proposed |
| BR-FIN-012 | Budgets and cost centers shall support management controls. | P1 | Proposed |

Acceptance criteria:

- No unbalanced journal entry can be posted.
- Every posted entry identifies its source and company.
- Reversals retain references to the original entries.
- Trial balance debit and credit totals agree.
- Financial statements are generated from posted ledger records.
- Period locks prevent unauthorized backdated posting.
- Exchange rate and currency conversion basis are retained.

## 3.11 HR and payroll

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-HR-001 | Employee records shall be maintained by company and employment relationship. | P1 | Observed |
| BR-HR-002 | Employee contracts and supporting documents shall be retained. | P1 | Observed |
| BR-HR-003 | Leave and attendance shall be managed. | P1 | Observed |
| BR-HR-004 | Payroll shall support configurable salary components. | P1 | Proposed |
| BR-HR-005 | Payroll shall support authorized review and approval. | P0 | Proposed |
| BR-HR-006 | Payroll calculations shall be reproducible and auditable. | P0 | Proposed |
| BR-HR-007 | Applicable statutory rules shall be configurable and validated. | P0 | To validate |
| BR-HR-008 | Payroll shall integrate with finance through controlled posting. | P1 | Proposed |

Acceptance criteria:

- Payroll calculations retain the applicable rule and period.
- Changes to salary components are auditable.
- Only authorized users can approve and post payroll.
- Payroll totals reconcile to the resulting accounting entries.
- Statutory rules are reviewed before production use.

## 3.12 Documents and records

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-DOC-001 | Documents shall have company ownership and access rules. | P0 | Proposed |
| BR-DOC-002 | Documents shall support version history. | P1 | Observed |
| BR-DOC-003 | Documents shall link to business records. | P0 | Observed |
| BR-DOC-004 | File downloads shall enforce authorization. | P0 | To validate |
| BR-DOC-005 | Document metadata shall support classification and search. | P1 | Proposed |
| BR-DOC-006 | Retention and archive rules shall be configurable. | P2 | Proposed |
| BR-DOC-007 | Document access and changes shall be auditable. | P0 | Proposed |
| BR-DOC-008 | OCR and extraction shall preserve source references. | P1 | Proposed |

Acceptance criteria:

- Unauthorized users cannot retrieve a document by guessing its URL or identifier.
- Each version identifies its creator, time and source.
- Documents remain linked to the correct company and business record.
- Archived records remain retrievable according to retention rules.

## 3.13 Tasks, collaboration and communication

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-COL-001 | Tasks shall support company-scoped assignment. | P0 | Proposed |
| BR-COL-002 | Tasks shall support deadlines, priorities and status. | P1 | Observed |
| BR-COL-003 | Task comments and history shall be retained. | P1 | Observed |
| BR-COL-004 | Notifications shall respect company and user permissions. | P0 | Proposed |
| BR-COL-005 | Internal discussions shall link to relevant business records. | P2 | Proposed |
| BR-COL-006 | Delegation and reassignment shall be auditable. | P1 | Proposed |

Acceptance criteria:

- Users can only assign tasks to authorized company memberships.
- Task history remains available after reassignment.
- Notifications do not disclose unauthorized company information.
- Delegated tasks retain the original owner and delegation history.

## 3.14 Reporting and executive intelligence

| ID | Requirement | Priority | Status |
|---|---|---|---|
| BR-REP-001 | Management dashboards shall be company-scoped. | P0 | Proposed |
| BR-REP-002 | Authorized group dashboards shall consolidate approved company data. | P1 | Proposed |
| BR-REP-003 | Reports shall identify reporting period and currency. | P0 | Proposed |
| BR-REP-004 | Reports shall be traceable to source transactions. | P1 | Proposed |
| BR-REP-005 | Reports shall support PDF, DOCX and XLSX where appropriate. | P1 | Observed |
| BR-REP-006 | KPI definitions shall be documented and consistent. | P1 | Proposed |
| BR-REP-007 | Financial reports shall reconcile with the general ledger. | P0 | Proposed |

Acceptance criteria:

- A report identifies its company scope and reporting period.
- A report's totals can be traced to source records.
- Financial report totals reconcile with posted accounting data.
- Unauthorized users cannot export data outside their company scope.

# 4. CROSS-CUTTING NON-FUNCTIONAL REQUIREMENTS

| ID | Requirement | Priority | Acceptance direction |
|---|---|---|---|
| NFR-001 | Security by default | P0 | Unauthorized access is denied server-side |
| NFR-002 | Company data isolation | P0 | Cross-company access scenarios fail |
| NFR-003 | Auditability | P0 | Material actions retain actor and timestamp |
| NFR-004 | Financial accuracy | P0 | Controlled calculations and reconciliations |
| NFR-005 | Data integrity | P0 | Database constraints protect critical relationships |
| NFR-006 | Availability | P1 | Operational recovery objectives are documented |
| NFR-007 | Backup and recovery | P0 | Restore procedure is documented and demonstrated |
| NFR-008 | Performance | P1 | Response targets are measured under agreed workloads |
| NFR-009 | Mobile usability | P1 | Core workflows are usable on mobile and desktop |
| NFR-010 | Accessibility | P2 | Accessible navigation and controls |
| NFR-011 | Maintainability | P1 | Modular code and documented interfaces |
| NFR-012 | Observability | P1 | Errors and background job failures are traceable |
| NFR-013 | Interoperability | P2 | Documented APIs and controlled integrations |
| NFR-014 | Localization | P2 | Configurable date, number and currency presentation |
| NFR-015 | Resilience | P0 | AI and integration failures do not corrupt business records |
| NFR-016 | Scalability | P1 | Architecture supports growth in companies and records |
| NFR-017 | Data retention | P1 | Retention and archive policy is configurable |
| NFR-018 | Deployment safety | P0 | Development and production environments are isolated |

Performance targets, availability targets and recovery time objectives must be agreed after hosting and workload discovery. Do not invent targets before measurement.

# 5. CONSOLIDATED GAP REGISTER

The following gaps are based on the inspected source inventory. They are preliminary until verified against production behavior and business practice.

| Gap ID | Area | Existing baseline | Target capability | Priority |
|---|---|---|---|---|
| GAP-001 | General ledger | Complete double-entry model not identified | Full accounting ledger | P0 |
| GAP-002 | Task authorization | Task assignment references Employee | Membership-aware task assignment | P0 |
| GAP-003 | Company authorization | Legacy and membership structures coexist | Single authoritative authorization model | P0 |
| GAP-004 | Shipment | One-to-one Tender relationship | Multiple shipments and partial deliveries | P1 |
| GAP-005 | Inventory | Basic product stock and transactions | Auditable warehouse and valuation ledger | P1 |
| GAP-006 | Product catalog | Basic product structure | Structured technical catalog | P1 |
| GAP-007 | Supplier | Basic supplier profile | Supplier qualification and performance | P1 |
| GAP-008 | Tender domain | Large Tender model combines many concerns | Separated tender, bid, contract and execution domains | P1 |
| GAP-009 | Workflow | Large procedural workflow module | Documented and configurable workflow engine | P1 |
| GAP-010 | Documents | Multiple document models and storage paths | Unified document service | P1 |
| GAP-011 | AI | Gemini-centered integration | Provider-independent gateway | P1 |
| GAP-012 | AI evidence | Evidence capability exists but needs validation | Source-linked and confidence-aware AI outputs | P0 |
| GAP-013 | Landed cost | Cost fields and calculations exist | Detailed component ledger and allocation | P0 |
| GAP-014 | Finance controls | Basic cash-flow and expense structures | AP, AR, bank reconciliation and ledger controls | P0 |
| GAP-015 | HR/payroll | Basic employee and payroll records | Complete configurable HR/payroll | P1 |
| GAP-016 | Reporting | Multiple report endpoints | Governed KPI and reporting framework | P1 |
| GAP-017 | Audit | Audit log model and views exist | Consistent event coverage and tamper-resistant retention | P0 |
| GAP-018 | Background work | Thread-based AI work observed | Durable jobs, retries and monitoring | P1 |
| GAP-019 | IT assets | IT tickets and user administration observed | IT asset and license lifecycle | P2 |
| GAP-020 | Migration | No replacement migration plan yet | Reconciled and reversible migration | P0 |

# 6. REQUIREMENT DEPENDENCIES

Implementation dependencies must be respected.

| Capability | Depends on |
|---|---|
| Company-scoped modules | Identity, membership and authorization |
| Tender approvals | Workflow engine and audit framework |
| AI War Room | Document service, AI gateway and evidence model |
| Supplier procurement | Supplier and product catalog |
| Landed cost | Import records, currency and cost components |
| Inventory valuation | Stock ledger and accounting rules |
| Accounts payable | Supplier invoices and general ledger |
| Accounts receivable | Customer invoices and general ledger |
| Payroll posting | HR, payroll rules and general ledger |
| Executive reporting | Governed source data and KPI definitions |
| Migration | Target schema, source mapping and reconciliation |

# 7. BUSINESS DECISIONS REQUIRING OWNER CONFIRMATION

The following questions must be answered during discovery. They must not be silently assumed by developers.

## 7.1 Organization

- What is the approved legal and operational company hierarchy?
- Which users need access to both YAH and CHI?
- Which reports may be consolidated across companies?
- Are intercompany sales, purchases, loans or shared expenses required?

## 7.2 Accounting

- What chart of accounts is currently used by each company?
- Which accounting basis and financial reporting rules apply?
- Which currencies are functional and reporting currencies?
- Which inventory valuation method is approved?
- Which approval limits apply to payments and journals?
- Which Ethiopian tax and statutory rules must be configured?

## 7.3 Tender and procurement

- Which existing tender stages are mandatory?
- Which roles approve each stage?
- Which bid documents are mandatory for each tender category?
- Which quotation comparison rules are used?
- Which events require management approval?

## 7.4 Import and landed cost

- Which cost components are included in inventory cost?
- Which costs are expensed rather than capitalized?
- Which allocation method applies to freight, insurance, duties and local charges?
- How should shared costs be allocated across shipments and items?
- How should uncertain, duplicated or unsupported charges be reviewed?

## 7.5 Inventory and delivery

- How many warehouses and storage locations exist?
- Are serial numbers, batches or expiry dates required?
- Which goods receipt and inspection approvals are required?
- How are partial deliveries and customer acceptance handled?

## 7.6 HR and payroll

- What employment categories and salary structures exist?
- Which attendance and leave rules apply?
- Which payroll deductions and statutory requirements apply?
- Who approves payroll and salary changes?

## 7.7 Documents and retention

- Which document classes have mandatory retention periods?
- Which documents require restricted access?
- Which records must remain available after employee departure?
- Which documents require electronic approval or signature?

# 8. RISK REGISTER

| Risk ID | Risk | Impact | Required control |
|---|---|---|---|
| R-001 | Cross-company data exposure | Critical | Server-side company authorization and isolation review |
| R-002 | Incorrect accounting design | Critical | Finance-led design and reconciliation acceptance |
| R-003 | Loss of workflow history | High | Workflow mapping and migration reconciliation |
| R-004 | Incorrect landed cost | High | Source-linked calculations and independent reconciliation |
| R-005 | AI hallucination | High | Evidence references and human approval |
| R-006 | Missing document history | High | Versioned migration and document reconciliation |
| R-007 | Inventory mismatch | High | Stock ledger and physical reconciliation |
| R-008 | Provider quota exhaustion | Medium | Quota-aware fallback and local extraction |
| R-009 | Incomplete migration | Critical | Exception reports and rollback plan |
| R-010 | Unauthorized privilege escalation | Critical | Membership-scoped roles and audited administration |
| R-011 | Uncontrolled production changes | Critical | Separate repository and explicit release authorization |
| R-012 | Unverified statutory calculations | High | Local legal and finance validation |

# 9. PRIORITIZED DELIVERY REQUIREMENTS

## Foundation — P0

1. Identity and company membership.
2. Company-level data isolation.
3. Membership-scoped authorization.
4. Audit framework.
5. Secure document access.
6. Workflow authorization and history.
7. Double-entry accounting foundation.
8. Financial posting controls.
9. Evidence-based AI controls.
10. Landed cost traceability.
11. Migration and recovery controls.

## Core business — P1

1. Tender and bid lifecycle.
2. AI War Room.
3. Supplier and manufacturer management.
4. Product technical catalog.
5. Procurement.
6. Import management.
7. Shipment management.
8. Warehouse and inventory.
9. Accounts payable and receivable.
10. HR and payroll.
11. Management dashboards.
12. Reporting and exports.

## Advanced capability — P2 and P3

1. Advanced supplier intelligence.
2. Forecasting and predictive analytics.
3. IT asset lifecycle.
4. Advanced automation.
5. Advanced integrations.
6. Additional business intelligence.

Priority does not override dependencies. Foundation controls must be implemented before dependent modules are exposed to production users.

# 10. REQUIREMENTS TRACEABILITY

Each requirement must eventually link to:

- One or more architecture components.
- Database entities and constraints.
- User interface screens.
- API endpoints or services.
- Permission rules.
- Audit events.
- Implementation tasks.
- Acceptance scenarios.
- Migration mappings where applicable.

The requirements register should be updated when a requirement is approved, changed, implemented or accepted.

A requirement must not be marked accepted solely because a screen or endpoint exists.

# 11. ACCEPTANCE GOVERNANCE

A requirement is accepted only when:

1. The business owner confirms the expected behavior.
2. The implementation satisfies the defined acceptance criteria.
3. Company access and permission boundaries are respected.
4. Relevant audit records exist.
5. Financial and operational calculations are reconciled where applicable.
6. Required documents and evidence are retained.
7. Known exceptions and limitations are documented.

Critical security, company isolation and financial integrity requirements cannot be waived merely to accelerate delivery.

# 12. NEXT DISCOVERY DOCUMENTS

1. Target System Architecture.
2. Database Entity and Relationship Design.
3. Security and Company Authorization Design.
4. UI and Navigation Blueprint.
5. AI Provider and Document Processing Design.
6. Data Migration Strategy.
7. Implementation Backlog.
8. Acceptance and Cutover Plan.

**Current status:** Initial business requirements and gap register drafted. Subject to business-owner validation and approval.

