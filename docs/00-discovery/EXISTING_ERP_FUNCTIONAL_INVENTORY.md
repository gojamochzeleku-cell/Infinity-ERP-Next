# EXISTING INFINITY ERP
## Functional Inventory and Technical Discovery

**Document:** 01 — Existing ERP Functional Inventory  
**Source repository:** gojamochzeleku-cell/Infinity-erp  
**Inspected branch:** feature/war-room-artifact-suite  
**Inspection type:** Read-only GitHub source inspection  
**Status:** Initial inventory; further business validation required

---

# 1. PURPOSE

This document records the functionality and technical structures identified in the existing Infinity ERP source code.

It is the baseline for rebuilding Infinity ERP Next.

It distinguishes:

- Functionality visible in source code.
- Existing database structures.
- Existing workflow and route structures.
- Preliminary architectural gaps.
- Items requiring further inspection or business confirmation.

This is not a claim that every production screen, workflow, permission, integration or business rule has been fully audited.

No production data or code was changed during this inspection.

# 2. SOURCE INSPECTION SUMMARY

The following source files were inspected:

| Source file | Purpose |
|---|---|
| core/models.py | Database models |
| core/urls.py | Application routes |
| core/middleware.py | Active company resolution |
| core/admin.py | Django admin configuration |
| core/chain.py | Business workflow engine |
| core/tender_views.py | Tender registration and lifecycle |
| core/war_room_views.py | AI War Room |
| core/war_room_artifact_views.py | War Room artifact review and transfer |
| core/war_room_documents.py | PDF, DOCX and XLSX generation |
| core/gemini.py | AI integration and analysis |
| core/proc_views.py | Suppliers and shipments |
| core/hr_fin_views.py | HR, payroll, leave and expenses |
| core/fin_views.py | Finance functions |
| core/inventory_views.py | Inventory management |
| core/it_views.py | IT and user administration |
| core/office_views.py | Office administration |
| core/saas_views.py | Company management |
| core/mgmt_views.py | Management dashboard and AI assistant |
| core/advanced_views.py | Reporting, calendar and audit trail |
| core/doc_views.py | Document management |
| core/resource_views.py | Company resource library |
| core/memo_views.py | Memos and task assignment |
| core/mail_views.py | Correspondence and email |
| core/control_views.py | Legal records and bid tracking |
| core/forecast_views.py | Cash-flow forecast |
| core/profit_views.py | Profitability dashboard |
| core/cost_views.py | Landed cost and AI pricing |
| core/pricing_views.py | Lot pricing |
| core/assembly_views.py | Lot assembly and bid operator workspace |
| core/storage_views.py | File storage and archiving |
| core/history_views.py | Task history |
| core/filing_views.py | Filing and physical records |
| core/recovery_views.py | Password recovery |
| core/report_views.py | Reports center |
| core/chat_views.py | Internal chat |
| core/global_views.py | Search and task reassignment |
| core/telegram_views.py | Telegram integration |
| core/deadline_views.py | Deadline center |
| core/tv_views.py | TV broadcast |
| core/qr_views.py | QR generation |
| core/supplier_views.py | Supplier upload portal |
| core/cover_sheet_views.py | Tender cover sheets |
| core/cron_views.py | Daily reminders |

## 2.1 Structural counts

| Item | Observed count |
|---|---:|
| URL declarations in core/urls.py | 124 |
| Model classes in core/models.py | 40 |
| Lines in core/models.py | 1,072 |
| Lines in core/chain.py | 1,416 |
| Lines in core/war_room_documents.py | 1,908 |
| Lines in core/gemini.py | 1,278 |
| Lines in core/tender_views.py | 749 |

These are source-code counts, not counts of unique business capabilities or production screens.

# 3. EXISTING FUNCTIONAL MODULE INVENTORY

## 3.1 Authentication and company management

Observed functionality:

- User login and logout.
- Company selection.
- Active company context.
- Employee profiles.
- Company membership records.
- Membership role assignments.
- Designated company workflow recipients.
- Company creation and deletion views.
- Employee management.
- Password recovery using reset codes.
- User activation and deactivation.
- User password reset.
- Group-level employee flag.

Relevant source:

- core/models.py
- core/middleware.py
- core/views.py
- core/saas_views.py
- core/it_views.py
- core/recovery_views.py

Important observation:

CompanyMembership and MembershipRole already provide a foundation for company-specific authorization.

However, Employee still contains legacy company and role fields. Both structures coexist.

CompanyRoleAssignment designates a workflow recipient for a company and role.

The actual authorization behavior must be mapped across all views before the new system is designed.

## 3.2 Tender management

Observed functionality:

- Tender listing.
- Tender registration.
- Draft saving.
- Tender editing.
- Tender detail.
- Tender submission.
- Tender deletion.
- Tender document upload.
- PDF-based AI data extraction.
- Tender review and decision records.
- Bid Manager assignment.
- CEO approval and rejection workflow.
- Tender lot management.
- Tender pricing.
- Bid document re-upload requests.
- Bid document version records.
- Bid submission status.
- Technical and financial result tracking.
- Competitor price recording.
- Award document upload.
- Agreement and contract document handling.
- CPO and bond expiry information.
- Tender cover sheet generation.
- Bid tracker assignment.

Relevant source:

- core/tender_views.py
- core/chain.py
- core/models.py
- core/assembly_views.py
- core/pricing_views.py
- core/cover_sheet_views.py

The Tender model contains a large number of commercial, technical, lifecycle and file fields.

TenderLot and LotItem provide additional lot-level structures.

## 3.3 Tender workflow and task chain

The existing workflow engine is implemented primarily in core/chain.py.

Observed task codes include:

| Workflow range | Observed business purpose |
|---|---|
| T02–T03 | Initial Bid Manager and CEO decisions |
| T04–T08 | Early tender preparation, cost and document activities |
| T09 | Main Bid Manager War Room task |
| T10–T17 | Supplier, technical, pricing, bank and bid-document preparation activities |
| T18–T20 | Physical submission, result review and award document handling |
| T21–T24 | Draft agreement, legal review, signature and final agreement |

The source also contains specialized task codes and paths, including:

- T10_LOT
- WR_REVIEW
- WR_ARTIFACT
- I06G

The logistics and execution workflow includes:

| Code | Observed purpose |
|---|---|
| I01 | Purchase order and supplier confirmation |
| I02 | Payment request |
| I03 | Higher-value payment approval |
| I04 | Letter of credit or bank transfer |
| I05 | Shipping documents |
| I06 | Clearing agent assignment |
| I06G | General Manager approval of agent fees |
| I07 | Customs duty and tax payment request |
| I08 | Duty and tax approval |
| I09 | Customs clearance |
| I10 | Inland transport to warehouse |
| I11 | Goods receiving and inspection |
| I12 | Delivery to customer |
| I13 | Customer acceptance and GRN |
| I14 | Receivable and collection |
| I15 | Project closure report |
| I16 | Final project approval |

Important:

The source contains multiple workflow advancement functions and specialized branches. The exact runtime transition map, exception behavior and historical task-code meaning must be verified before redesign.

Do not replace or discard these workflow identifiers without an approved migration and business mapping.

## 3.4 AI War Room

Observed functionality:

- Tender document analysis.
- AI analysis of purchased bid documents.
- Supplier context supplied to AI analysis.
- Technical compliance information.
- Tender summaries.
- Product brand and model comparison.
- Supplier intelligence.
- Commercial analysis.
- Eligibility and risk analysis.
- Clarification-related information.
- Source register.
- AI status and error tracking.
- Structured War Room data.
- PDF War Room report download.
- Versioned artifact generation.
- Artifact review and approval.
- Artifact return for revision.
- Transfer to Bid Operator.
- Working revisions linked to approved source artifacts.
- Artifact file download.

The WarRoomArtifact model identifies eight artifact types:

1. Tender Intelligence Report.
2. Technical Specification and Compliance Matrix.
3. Brand and Model Comparison Report.
4. Supplier Intelligence and Evaluation Report.
5. Commercial and Landed Cost Analysis.
6. Eligibility, Risk and Clarification Report.
7. BIDM Bid Strategy and Recommendation.
8. Evidence and Source Register.

Supported artifact formats:

- PDF.
- DOCX.
- XLSX.
- CSV.

Observed artifact states include:

- DRAFT.
- REVIEW.
- APPROVED.
- TRANSFERRED.
- WORKING.
- RETURNED.
- SUPERSEDED.

Relevant source:

- core/war_room_views.py
- core/war_room_artifact_views.py
- core/war_room_documents.py
- core/war_room_artifact_service.py
- core/gemini.py

The exact number of downloadable deliverables and all worksheet structures require a separate artifact-by-artifact inspection.

## 3.5 AI integration

Observed AI capabilities:

- Tender PDF extraction.
- Bid document analysis.
- PDF compression.
- File-byte processing.
- AI output parsing.
- Structured War Room output.
- AI assistant endpoint.
- Winning-price prediction function.
- AI-assisted pricing function.

The inspected AI implementation is centered on Gemini.

The code contains asynchronous background analysis using Python threading in the War Room path.

This is not evidence of a durable distributed job queue.

Further discovery is required for:

- API quota behavior.
- Provider failure handling.
- Model configuration.
- Prompt versions.
- Token and cost tracking.
- Research source verification.
- Document-size limits.
- Retry and timeout behavior.
- Data retention and privacy.

## 3.6 Supplier and procurement functions

Observed functionality:

- Supplier registration and listing.
- Supplier contact information.
- Supplier ratings.
- Supplier notes.
- Supplier upload link generation.
- Token-based supplier upload portal.
- Supplier quotation/proforma-related tender handling.
- Shipment listing.
- Shipment updates.
- Inventory checks associated with shipments.

Relevant source:

- core/proc_views.py
- core/supplier_views.py
- core/models.py
- core/chain.py

The inspected Supplier model is relatively simple.

A full supplier qualification, manufacturer registry, supplier-product catalog and supplier performance lifecycle have not been established by this inspection.

## 3.7 Import and logistics

Observed functionality:

- Purchase order document storage.
- Payment amount recording.
- SWIFT document storage.
- Shipping document storage.
- Clearing agent recording.
- Customs duty and tax amount recording.
- Customs document storage.
- Warehouse receipt.
- Inspection report.
- Delivery note.
- GRN/invoice document.
- Payment receipt.
- Closure report.
- Shipment status.
- Vessel name.
- Bill of lading.
- Estimated arrival date.
- Shipment inventory records.

Relevant source:

- core/models.py
- core/chain.py
- core/proc_views.py

The current Shipment model uses a OneToOne relationship with Tender.

This means the inspected model design allows one Shipment record per Tender, rather than a direct one-to-many shipment structure.

The actual operational need for split shipments and multiple containers must be confirmed.

## 3.8 Landed cost and pricing

Observed functionality:

- Lot-level landed cost calculation endpoint.
- AI price assistance endpoint.
- CEO lot pricing workspace.
- Lot item management.
- Quantity and unit pricing.
- Total item price calculation.
- Foreign exchange rate fields.
- Bank charge fields.
- Tax amount fields.
- Landed cost fields.
- Profit margin fields.
- Final bid price fields.

Relevant source:

- core/cost_views.py
- core/pricing_views.py
- core/assembly_views.py
- core/models.py

A complete independently modeled import-cost ledger and cost-allocation record structure was not identified in the inspected model inventory.

The exact allocation formulas, cost inclusion rules, rounding behavior and approval controls require further inspection.

## 3.9 Inventory and warehouse

Observed functionality:

- Inventory dashboard.
- Manual inventory adjustment.
- Product records.
- SKU.
- Product name and category.
- Current stock quantity.
- Minimum stock level.
- Location.
- Stock IN transactions.
- Stock OUT transactions.
- Manual stock adjustment transactions.
- Shipment-level expected and received quantities.
- Damaged quantity and condition tracking.

Relevant source:

- core/inventory_views.py
- core/proc_views.py
- core/models.py

The inspected Product model stores current_stock directly.

StockTransaction records movements but is relatively simple.

The inspected model inventory does not establish a full warehouse/bin ledger, reservation engine, batch tracking or complete inventory valuation system.

## 3.10 Finance and accounting

Observed functionality:

- Cash-flow records.
- Cash-flow dashboard.
- Cash-flow forecast.
- Profitability dashboard.
- Expense requests.
- Payroll records.
- Payment-related tender fields.
- Payment request workflow.
- Financial export.
- Guarantee tracker and finance settings endpoints.

Relevant source:

- core/fin_views.py
- core/forecast_views.py
- core/profit_views.py
- core/hr_fin_views.py
- core/advanced_views.py
- core/chain.py
- core/models.py

Important discovery:

The inspected 40 model classes include CashFlowEntry, ExpenseRequest and PayrollRecord.

They do not include a complete general-ledger model structure such as:

- Chart of accounts.
- Journal entry.
- Journal line.
- Accounts payable ledger.
- Accounts receivable ledger.
- Bank reconciliation.
- Accounting period.

This is a significant target-system gap to validate with the finance team.

It does not prove that no external accounting process or uninspected financial integration exists.

## 3.11 HR and payroll

Observed functionality:

- Staff directory.
- Employee registration.
- Employee profile.
- Employee documents.
- Leave requests.
- Expense requests.
- Payroll generation.
- Payroll history.
- Performance reviews.
- Employee salary fields.
- Contract expiry fields.

Relevant source:

- core/hr_fin_views.py
- core/models.py

The complete payroll calculation rules, statutory deductions, approval process and accounting integration require further discovery.

## 3.12 Tasks, memos and collaboration

Observed functionality:

- Personal tasks.
- Assigned tasks.
- Delegated tasks.
- Task detail.
- Task action handling.
- Task reassignment.
- Task comments.
- Task history.
- Notifications.
- Read/unread status.
- Memos.
- Memo creation and reading.
- Role-based memo recipients.
- Internal chat rooms.
- Chat participants.
- Text messages.
- Audio file attachment.
- Telegram notification fields.
- WhatsApp notification fields.
- Email notification fields.

Relevant source:

- core/models.py
- core/chain.py
- core/memo_views.py
- core/chat_views.py
- core/global_views.py
- core/history_views.py

Important observation:

Task.assigned_to and Task.assigned_by reference Employee.

This differs from the target design in which task assignment and authorization should be tied to an active company membership.

The existing task workflow must be mapped before migration.

## 3.13 Documents and records

Observed functionality:

- Document listing.
- Document upload.
- Document file access.
- Document scanner endpoint.
- Document checkout.
- Company resource library.
- Resource upload and deletion.
- Tender document versioning.
- Bid document hash and metadata fields.
- War Room artifact file storage.
- Tender file archive.
- File hash calculation.
- QR code generation.
- Filing portal.
- Spine labels.
- Cabinet labels.
- Visual filing map.

Relevant source:

- core/doc_views.py
- core/resource_views.py
- core/storage_views.py
- core/filing_views.py
- core/qr_views.py
- core/models.py

The existing system has several document-related models and storage paths.

A unified document ownership, classification, retention and versioning architecture should be designed for the new ERP.

## 3.14 Legal and correspondence

Observed functionality:

- Legal case listing.
- Correspondence records.
- Incoming and outgoing mail.
- Email composition.
- Email fetching action.
- Memos.
- Contract and agreement file fields.
- Legal approval workflow.
- Bid agreement tracking.

Relevant source:

- core/control_views.py
- core/mail_views.py
- core/memo_views.py
- core/models.py
- core/chain.py

## 3.15 IT service management

Observed functionality:

- IT dashboard.
- User management.
- User editing.
- User deletion.
- Password reset.
- User activation/deactivation.
- IT ticket submission.
- IT ticket resolution.
- Workflow repair endpoint.

Relevant source:

- core/it_views.py
- core/models.py
- core/repair_views.py

The inspected models include ITTicket.

A complete IT asset register and software-license lifecycle were not established by this inspection.

## 3.16 Office and corporate administration

Observed functionality:

- Office dashboard.
- Office manual.
- Supply requests.
- Visitor log records.
- Courier dispatch records.
- Document checkout.
- Corporate calendar.
- Deadline center.
- TV dashboard.
- TV broadcast.
- TV settings.
- QR code generation.
- Filing labels and filing maps.

Relevant source:

- core/office_views.py
- core/control_views.py
- core/tv_views.py
- core/deadline_views.py
- core/advanced_views.py
- core/filing_views.py
- core/models.py

## 3.17 Reporting and management

Observed functionality:

- Management dashboard.
- Reports center.
- Profitability dashboard.
- Cash-flow forecast.
- Cash-flow dashboard.
- Tender CSV export.
- Cash-flow CSV export.
- Audit trail.
- Audit log export.
- Global search.
- Corporate calendar.
- Deadline center.

Relevant source:

- core/mgmt_views.py
- core/report_views.py
- core/profit_views.py
- core/forecast_views.py
- core/advanced_views.py
- core/global_views.py

The complete list of report templates, formulas, filters and management KPIs requires further inspection.

# 4. EXISTING DATABASE MODEL INVENTORY

The inspected core/models.py contains 40 model classes.

## 4.1 Identity and organization

1. Company
2. Employee
3. CompanyMembership
4. MembershipRole
5. CompanyRoleAssignment

## 4.2 Workflow and collaboration

6. Task
7. Notification
8. AuditLog
9. Memo
10. TaskComment
11. TaskHistory
12. ChatRoom
13. ChatMessage

## 4.3 Tender and War Room

14. Tender
15. TenderReview
16. TenderLot
17. LotItem
18. BidDocumentVersion
19. WarRoomArtifact

## 4.4 Documents and corporate records

20. Document
21. CompanyResource
22. EmployeeDocument
23. Correspondence
24. LegalCase
25. CompanySetting
26. CourierDispatch
27. SupplyRequest
28. VisitorLog

## 4.5 HR and finance

29. LeaveRequest
30. ExpenseRequest
31. CashFlowEntry
32. PayrollRecord
33. PerformanceReview

## 4.6 Procurement, logistics and inventory

34. Supplier
35. Shipment
36. InventoryItem
37. Product
38. StockTransaction

## 4.7 IT and authentication support

39. ITTicket
40. PasswordResetCode

This inventory is limited to core/models.py. Other applications, external services or database structures may exist outside this file.

# 5. PRELIMINARY ARCHITECTURAL OBSERVATIONS

## 5.1 Large central models file

The inspected models.py contains 40 model classes and 1,072 lines.

The Tender model combines many different concerns:

- Tender identity.
- Tender lifecycle.
- AI analysis.
- Technical proposal files.
- Commercial proposal files.
- Pricing.
- Guarantees.
- Import documents.
- Payment information.
- Shipment and delivery records.
- Contract and closure documents.

Target direction:

Separate business domains while preserving traceable relationships and migration compatibility.

## 5.2 Large workflow engine

The chain.py file contains 1,416 lines.

It includes multiple workflow advancement functions and task-specific transition rules.

Target direction:

Document the existing workflow transition map before designing a configurable workflow engine.

## 5.3 Company authorization

Positive existing foundation:

- CompanyMembership exists.
- MembershipRole exists.
- CompanyRoleAssignment validates company and membership consistency.
- CurrentCompanyMiddleware resolves a company only through an active employee and active company membership.
- War Room views explicitly validate company membership and role.

Items requiring deeper review:

- Every view's authorization behavior.
- Queryset company scoping.
- File download authorization.
- Background task authorization and company context.
- Cross-company search.
- Group-level reporting.
- Employee legacy role usage.
- Django user flags and system-level privileges.

The admin.py inspected in this branch contains no model registrations. This alone does not establish the actual account privilege state.

## 5.4 Task assignment

Task assignment currently references Employee.

Target direction:

Use company membership as the authoritative assignment and authorization context while preserving employee identity and historical task records.

## 5.5 Shipment structure

Shipment currently uses a OneToOne relationship with Tender.

Target direction:

Evaluate a one-to-many tender-to-shipment relationship, including partial shipments, split deliveries and shipment consolidation.

## 5.6 Accounting structure

The inspected models do not show a complete double-entry ledger.

Target direction:

Design a proper chart of accounts, journal entries, journal lines, posting rules, accounts payable, accounts receivable and reconciliation.

## 5.7 Inventory structure

The current inventory models include Product and StockTransaction.

Target direction:

Design an auditable stock movement ledger with warehouse locations, reservations, valuation and reconciliation.

## 5.8 AI architecture

The inspected AI implementation is centered on Gemini.

Target direction:

Build a provider-independent AI gateway with quota-aware fallback, local document extraction, structured output validation and evidence tracking.

## 5.9 Document architecture

Several document systems coexist.

Target direction:

Create a unified document service with company ownership, access control, versioning, metadata, retention and audit history.

# 6. TARGET MODULE MAPPING

| Existing functionality | Infinity ERP Next target |
|---|---|
| Company and membership | Identity and organization |
| Tender registration | Tender management |
| Tender workflow | Workflow and approvals |
| Tender AI analysis | AI War Room |
| Lot assembly | Tender and bid management |
| Supplier records | Supplier management |
| Product and stock | Product catalog and inventory |
| Shipment and import fields | Import and logistics |
| Landed cost and pricing | Landed Cost Engine |
| Cash flow and expenses | Accounting and finance |
| Employee and payroll | HR and payroll |
| Documents and resources | Document management |
| Memo and task system | Workflow and collaboration |
| Legal and correspondence | Legal and corporate administration |
| IT tickets and users | IT service management |
| Reports and dashboards | Business intelligence |

# 7. ITEMS REQUIRING FURTHER DISCOVERY

The following areas are not yet fully verified:

1. All templates and actual screen behavior.
2. Every role's permissions on every route.
3. All workflow transitions and exception paths.
4. All existing report types and spreadsheet formulas.
5. Exact War Room downloadable deliverables.
6. All file storage and retention rules.
7. Actual production database schema and data volumes.
8. Existing integrations and external credentials.
9. Current scheduled jobs and deployment configuration.
10. Complete finance and accounting business processes.
11. Full inventory reconciliation and valuation rules.
12. Supplier and manufacturer qualification requirements.
13. Existing customer and contract management practices.
14. Actual YAH and CHI user membership and authorization records.
15. Production backup and recovery procedures.
16. Business-specific approval limits and delegation rules.
17. Existing data migration constraints.

These items must be inspected or confirmed before finalizing the requirements and migration plans.

# 8. PRELIMINARY GAP REGISTER

| ID | Area | Existing observation | Target discovery requirement |
|---|---|---|---|
| GAP-001 | Accounting | No complete double-entry model found in inspected models | Design full general ledger |
| GAP-002 | Task assignment | Task references Employee | Membership-aware assignment |
| GAP-003 | Shipment | One shipment per tender in current model | Support multiple shipments |
| GAP-004 | Inventory | Basic product stock and transactions | Complete stock ledger |
| GAP-005 | Product catalog | Basic SKU, category and stock | Structured technical catalog |
| GAP-006 | Suppliers | Basic supplier profile | Full supplier lifecycle |
| GAP-007 | Tender model | Many unrelated fields in one model | Separate business domains |
| GAP-008 | Workflow | Large procedural chain module | Configurable workflow engine |
| GAP-009 | Documents | Multiple document models and file paths | Unified document service |
| GAP-010 | AI | Gemini-centered implementation | Provider-independent AI gateway |
| GAP-011 | Reporting | Multiple report endpoints | Unified reporting and KPI definitions |
| GAP-012 | Authorization | Legacy and membership role structures coexist | One authoritative authorization model |
| GAP-013 | Import costs | Cost fields exist in tender and lot | Detailed cost ledger and allocation |
| GAP-014 | HR/payroll | Basic HR and payroll records exist | Complete configurable HR/payroll |
| GAP-015 | IT assets | IT tickets and user administration exist | Full IT asset and service management |

These are preliminary architectural gaps, not approved implementation changes.

# 9. PRODUCTION PROTECTION RULES

The following rules apply throughout discovery and rebuild:

- Do not modify the existing production repository.
- Do not change the production database.
- Do not change existing tender workflow behavior.
- Do not change task assignments or approvals.
- Do not change company permissions.
- Do not delete or overwrite historical records.
- Do not change production user privilege settings.
- Do not introduce SUPERADMIN.
- Do not deploy replacement code to production.
- Preserve the existing application until the replacement is accepted.

All new implementation work belongs in Infinity-ERP-Next.

# 10. INSPECTION LIMITATIONS

This inventory is based on read-only source inspection of the listed branch and files.

It does not establish:

- Which features are actively used by employees.
- Whether every route is accessible in production.
- Whether every route works correctly.
- Whether every model contains production records.
- Whether external integrations are currently operational.
- Whether hidden or external business processes exist.
- Whether the inspected branch exactly matches the deployed production commit.

Production behavior must be confirmed through approved business walkthroughs and controlled read-only discovery.

# 11. NEXT DISCOVERY DOCUMENTS

The next documents are:

1. Business Requirements and Gap Register.
2. Target System Architecture.
3. Database Entity and Relationship Design.
4. Security and Company Authorization Design.
5. UI and Navigation Blueprint.
6. AI Provider and Document Processing Design.
7. Data Migration Strategy.
8. Implementation Backlog.
9. Acceptance and Cutover Plan.

**Current status:** Initial existing ERP functional inventory drafted from source inspection. Subject to business validation and further discovery.

