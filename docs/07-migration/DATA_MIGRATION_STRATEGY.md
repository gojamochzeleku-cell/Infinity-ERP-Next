# DATA MIGRATION STRATEGY

**Project:** Infinity ERP Next  
**Document:** Data Migration Strategy  
**Version:** 1.0  
**Status:** Proposed strategy — subject to business-owner and technical approval  
**Date:** 12 November 2026

---

# 1. PURPOSE

This document defines the strategy for migrating business data,
documents, records, and operational history from the existing
Infinity ERP into Infinity ERP Next.

The objective is to establish a controlled, auditable, secure,
reconciled migration that preserves business continuity and
historical integrity.

Migration must not begin against production data until the
replacement system, migration plan, acceptance criteria, and
cutover authorization have been approved.

# 2. MIGRATION OBJECTIVES

The migration must:

1. Preserve important business records.
2. Preserve company ownership and isolation.
3. Preserve user identity and company memberships.
4. Preserve historical tender and bid information.
5. Preserve procurement and import records.
6. Preserve financial balances and transaction history.
7. Preserve inventory quantities and valuation evidence.
8. Preserve supplier and customer relationships.
9. Preserve documents and attachments.
10. Preserve relevant workflow and approval history.
11. Identify duplicates and inconsistent records.
12. Reconcile migrated financial and operational totals.
13. Maintain auditability.
14. Protect production operations.
15. Support controlled rollback.
16. Avoid unauthorized changes to the existing ERP.

# 3. MIGRATION GOVERNANCE

## 3.1 Authority

Migration activities require defined ownership.

Suggested roles:

- Business Owner.
- Migration Lead.
- Technical Lead.
- Database Administrator.
- Finance Reconciliation Owner.
- Procurement Data Owner.
- Tender Data Owner.
- HR Data Owner.
- Security Reviewer.
- Acceptance Approver.

Responsibilities must be formally assigned before migration.

## 3.2 Approval gates

The migration must pass these gates:

1. Source-system inventory approved.
2. Target data model approved.
3. Data mapping approved.
4. Data classification approved.
5. Migration scripts reviewed.
6. Test migration completed.
7. Reconciliation accepted.
8. User acceptance completed.
9. Cutover plan approved.
10. Production cutover explicitly authorized.

No approval may be assumed from completion of a previous gate.

## 3.3 Production protection

Until explicit authorization:

- Existing production data remains authoritative.
- No production records are modified for migration.
- No production tables are dropped or altered.
- No production migrations are executed.
- No production files are deleted or moved.
- No existing workflows are disabled.
- No production users or permissions are changed.
- No live data is imported into the new system.

# 4. SOURCE SYSTEM SCOPE

The initial source system is the existing Infinity ERP.

The initial code inventory was based on read-only inspection
of the existing repository branch:

`feature/war-room-artifact-suite`

The inspected source includes:

- Company and employee records.
- Membership and role assignments.
- Tenders and tender reviews.
- Tender lots and lot items.
- Bid document versions.
- War Room artifacts.
- Suppliers.
- Shipments.
- Products.
- Inventory items.
- Stock transactions.
- Tasks and notifications.
- Audit logs.
- Memos and comments.
- Documents and employee documents.
- Correspondence and legal cases.
- Procurement-related records.
- HR and payroll records.
- Finance-related records.
- IT tickets.
- Company settings.
- Other operational and reporting records.

This is an initial code-level inventory, not a verified production
database inventory.

Actual source tables, row counts, data quality, file storage,
relationships, and historical completeness must be inspected
through an authorized read-only process before migration planning
is finalized.

# 5. MIGRATION SCOPE

## 5.1 Company and identity data

Potential migration scope:

- Companies.
- Users.
- Employees.
- Company memberships.
- Company role assignments.
- Membership role history.
- Account status.
- Relevant authentication metadata.

Password migration must follow an approved security strategy.
Plaintext passwords must never be extracted or stored.

## 5.2 Tender and bid data

Potential scope:

- Tender records.
- Tender notices.
- Tender lots.
- Lot items.
- Tender reviews.
- Bid submissions.
- Bid document versions.
- Tender deadlines.
- Clarifications.
- Evaluations.
- Awards.
- Related correspondence.
- Workflow history.
- Supporting documents.

## 5.3 Supplier and product data

Potential scope:

- Suppliers.
- Manufacturers.
- Supplier contacts.
- Supplier documents.
- Products.
- Product specifications.
- Product categories.
- Supplier-product relationships.
- Historical supplier quotations.

## 5.4 Procurement data

Potential scope:

- Purchase requests.
- Requisitions.
- Purchase orders.
- Purchase order lines.
- Approvals.
- Supplier quotations.
- Goods receipts.
- Procurement correspondence.
- Supporting documents.

The actual source inventory must determine which records exist
and which require reconstruction or manual migration.

## 5.5 Import and logistics data

Potential scope:

- Shipments.
- Shipment milestones.
- Shipping documents.
- Freight records.
- Customs records.
- Insurance records.
- Clearance records.
- Import permits.
- Logistics correspondence.
- Delivery records.
- Historical landed-cost calculations.

## 5.6 Inventory data

Potential scope:

- Products.
- Inventory items.
- Warehouses.
- Stock balances.
- Stock transactions.
- Receipts.
- Issues.
- Transfers.
- Adjustments.
- Reservations.
- Valuation records.

Historical balances must be reconciled before they become
operational opening balances.

## 5.7 Finance data

Potential scope:

- Chart of accounts.
- Accounting periods.
- Journal entries.
- Journal lines.
- Accounts payable.
- Accounts receivable.
- Supplier balances.
- Customer balances.
- Cash and bank records.
- Expenses.
- Budgets.
- Payroll-related financial postings.
- Tax records.
- Historical financial reports.

The initial source-code inventory did not establish the existence
of a complete double-entry ledger. The actual finance migration
scope must be based on a verified source-data and accounting review.

## 5.8 HR and payroll data

Potential scope:

- Employee records.
- Employment history.
- Departments.
- Positions.
- Leave records.
- Payroll records.
- Performance records.
- Employee documents.

Sensitive employee information must receive restricted handling.

## 5.9 Tasks and collaboration

Potential scope:

- Tasks.
- Assignments.
- Task comments.
- Task history.
- Notifications where relevant.
- Memos.
- Chat records where retention is required.
- Correspondence.
- Approval history.

## 5.10 Documents and records

Potential scope:

- Documents.
- Employee documents.
- Bid attachments.
- War Room artifacts.
- Legal records.
- Correspondence attachments.
- Supplier documents.
- Import documents.
- File metadata.
- Document versions.

Original files must be preserved unless a separate retention
and disposal policy explicitly authorizes otherwise.

# 6. MIGRATION PRINCIPLES

The migration must follow these principles:

- Read-only source extraction.
- Reproducible migration.
- Approved field mapping.
- Explicit company ownership.
- Stable source identifiers.
- Target identifier mapping.
- No silent record deletion.
- No silent duplicate removal.
- No unsupported financial assumptions.
- No unverified opening balances.
- No automatic approval of migrated records.
- Full reconciliation.
- Controlled exception handling.
- Traceable migration execution.
- Secure temporary storage.
- Tested rollback procedures.

# 7. SOURCE DATA DISCOVERY

Before implementation, conduct an authorized source inventory.

Collect:

- Database engine and version.
- Database schema.
- Table names.
- Column definitions.
- Foreign keys.
- Unique constraints.
- Indexes.
- Row counts.
- Null distributions.
- Company distribution.
- Date ranges.
- File references.
- Storage locations.
- Data volume.
- Encoding information.
- Existing migrations.
- Relevant application dependencies.

Discovery should use read-only database access.

Do not expose credentials in scripts, terminal output,
documentation, or Git history.

# 8. SOURCE-TO-TARGET MAPPING

## 8.1 Mapping requirements

Every migrated entity must have an approved mapping definition.

A mapping record should include:

- Source system.
- Source entity.
- Source field.
- Target entity.
- Target field.
- Transformation rule.
- Default rule where approved.
- Required or optional status.
- Validation rule.
- Data owner.
- Approval status.
- Exception handling.

## 8.2 Mapping categories

Use the following mapping classifications:

- Direct mapping.
- Renamed field.
- Type conversion.
- Normalization.
- Derived field.
- Reference mapping.
- Manual review.
- Excluded by approved decision.

No field should be discarded merely because the target model
does not yet contain a matching field.

Unmapped information must be documented and reviewed.

## 8.3 Source identifiers

Preserve source identifiers in migration reference records.

Suggested fields:

- Source system identifier.
- Source entity type.
- Source record identifier.
- Target entity type.
- Target record identifier.
- Migration batch identifier.
- Migration timestamp.

This mapping supports traceability and reconciliation.

# 9. COMPANY OWNERSHIP AND DATA ISOLATION

Infinity ERP supports multiple companies, initially including
YAH and CHI, with future companies possible.

Every company-owned record must be assigned to the correct
target company.

## 9.1 Company mapping

Company mapping must be explicit.

Do not infer company ownership from:

- Current user session.
- File name.
- Employee name alone.
- Tender title alone.
- Unverified business assumptions.

Ambiguous ownership must be placed in an exception queue.

## 9.2 Cross-company records

Some records may legitimately relate to more than one company.

Examples:

- Shared suppliers.
- Group-level reference data.
- Shared product catalogs.
- Intercompany transactions.
- Shared corporate documents.

These must be represented using explicit shared-data or
intercompany relationships.

Do not duplicate or expose company-owned records without
an approved data-sharing model.

## 9.3 Authorization preservation

Migrate user and company membership data carefully.

The target authorization model must remain membership-based.

Company ADMIN roles must remain company-scoped.

No unrestricted system-wide business administrator should be
introduced.

SUPERADMIN must not be created as part of migration.

The existing Django administrative privilege state must not be
changed during discovery or migration without explicit approval.

For the approved target authorization model, the existing admin
account must have Django `is_superuser=False`. Its active,
company-specific ADMIN memberships in YAH and CHI must be preserved.

Before any authorized privilege migration:

- Verify the exact source account identity using a stable account
  identifier.
- Verify and record its existing YAH and CHI ADMIN memberships.
- Change only the Django superuser privilege; do not remove or
  broaden either company membership.
- Record the before-and-after privilege state and membership evidence.
- Reconcile the resulting account and memberships after migration.

No unrestricted system-wide Django superuser account or SUPERADMIN
business role may remain in the target system. This requirement does
not authorize a production account change during discovery or
documentation work.

# 10. DATA QUALITY ASSESSMENT

Assess the source data before migration.

## 10.1 Quality dimensions

Evaluate:

- Completeness.
- Accuracy.
- Consistency.
- Uniqueness.
- Validity.
- Referential integrity.
- Timeliness.
- Company ownership.
- Historical continuity.

## 10.2 Common data quality issues

Identify:

- Missing required fields.
- Invalid dates.
- Invalid currency codes.
- Inconsistent units.
- Incorrect decimal precision.
- Broken relationships.
- Duplicate-looking suppliers.
- Duplicate-looking products.
- Missing attachments.
- Invalid file references.
- Orphaned records.
- Inconsistent status values.
- Unclear company ownership.
- Incomplete approval history.

## 10.3 Duplicate handling

Potential duplicates must be identified and reviewed.

The migration must not automatically merge or delete records
based only on matching names, amounts, dates, or descriptions.

Maintain:

- Original source record.
- Duplicate candidate group.
- Matching criteria.
- Review decision.
- Reviewer.
- Decision timestamp.
- Final target mapping.

When uncertain, preserve both records and flag them.

# 11. FINANCIAL DATA MIGRATION

Financial migration requires special controls.

## 11.1 Financial integrity

Preserve:

- Original transaction amounts.
- Original currencies.
- Exchange rates.
- Transaction dates.
- Posting dates.
- Reference numbers.
- Supplier/customer references.
- Tax details.
- Payment status.
- Supporting evidence.

Do not replace historical exchange rates with current rates.

## 11.2 Double-entry accounting

The target system is intended to support double-entry accounting.

Before migration, determine whether source records represent:

- Posted accounting entries.
- Operational expenses.
- Cash-flow records.
- Payment records.
- Payroll amounts.
- Imported financial summaries.
- Unposted estimates.

Do not convert incomplete operational records into posted
journal entries without accounting approval.

## 11.3 Opening balances

Opening balances require:

- Approved cutover date.
- Approved chart of accounts.
- Reconciled trial balance.
- Supporting schedules.
- Reconciliation sign-off.
- Approved adjustment entries.

Opening balances must not be generated from incomplete or
unverified reports.

## 11.4 Currency and exchange rates

Preserve transaction currency and base currency separately.

Preserve original exchange-rate evidence.

Where historical exchange-rate data is missing, flag the
record rather than inventing a rate.

## 11.5 Financial reconciliation

Reconcile at minimum:

- Trial balance.
- General ledger totals.
- Accounts payable.
- Accounts receivable.
- Cash and bank balances.
- Inventory valuation.
- Payroll liabilities.
- Tax balances.
- Retained earnings and opening equity.

Differences must be investigated and formally approved.

# 12. INVENTORY MIGRATION

Inventory must be migrated using controlled opening balances
and transaction history where available.

Preserve:

- Product identity.
- Warehouse.
- Bin or location.
- Unit of measure.
- Quantity.
- Batch or lot where available.
- Serial number where applicable.
- Valuation method.
- Cost evidence.
- Stock movement history.

## 12.1 Inventory reconciliation

Compare:

- Source quantity by product.
- Source quantity by warehouse.
- Target quantity by product.
- Target quantity by warehouse.
- Inventory valuation.
- Outstanding reservations.
- Pending receipts.
- Pending issues.

Differences must be documented.

## 12.2 Historical movement

Where reliable transaction history exists, migrate it with
original dates and references.

Where only an opening balance is available, document the
historical limitation.

Do not invent missing stock movements.

# 13. DOCUMENT AND FILE MIGRATION

## 13.1 File preservation

Preserve original files.

The migration should maintain:

- Original file name.
- File type.
- File size.
- Checksum.
- Source storage reference.
- Target storage reference.
- Company ownership.
- Document category.
- Upload timestamp where known.
- Uploader reference where available.
- Version metadata.

## 13.2 File integrity

Use checksums to verify file integrity before and after transfer.

A file should not be marked successfully migrated until
the target copy passes integrity verification.

## 13.3 Missing files

Missing or inaccessible source files must be recorded as
migration exceptions.

Do not silently replace missing originals with regenerated
documents.

## 13.4 Document access

Preserve approved document access restrictions.

A migrated file must not become visible to a broader group
because its target storage location has different default permissions.

# 14. WORKFLOW AND APPROVAL HISTORY

Historical workflow data should be migrated where reliable
and useful.

Preserve:

- Workflow identifier.
- Entity reference.
- Previous status.
- New status.
- Actor.
- Timestamp.
- Comment.
- Approval or rejection decision.
- Supporting evidence.

The existing workflow identifiers T02–T24 and I01–I16 are
important discovery inputs.

Their mapping to target workflows must be documented.

Historical records must not be replayed as new live approvals.

Migrated historical approvals must be clearly distinguishable
from approvals performed in the new system.

# 15. USER AND EMPLOYEE MIGRATION

Preserve stable identity relationships.

Review:

- User accounts.
- Employee records.
- Company memberships.
- Company roles.
- Account activation.
- Email addresses.
- Employment status.
- Historical assignments.

Password migration must use a secure, supported method.

If password hashes are incompatible, use a controlled password
reset or account activation process.

Do not expose existing password hashes or secrets.

Do not grant permissions merely because a user held a broad
legacy role.

All migrated permissions must be mapped to the approved
company-scoped authorization model.

# 16. DATA TRANSFORMATION

Transformations must be explicit and documented.

Examples:

- Date and time normalization.
- Currency code normalization.
- Decimal precision conversion.
- Unit-of-measure mapping.
- Status mapping.
- Reference-data mapping.
- Text encoding normalization.
- Company identifier mapping.

For every transformation, preserve the original value where
needed for auditability.

Do not silently round financial values.

Do not convert units without a verified conversion rule.

# 17. MIGRATION TOOLING

The migration tooling should support:

- Read-only extraction.
- Mapping configuration.
- Data validation.
- Transformation.
- Batch processing.
- Idempotent imports.
- Error capture.
- Exception reporting.
- Source-to-target mapping.
- Reconciliation.
- Audit logging.

Potential technologies may include:

- Python migration scripts.
- Django management commands.
- SQL extraction tools.
- PostgreSQL bulk loading where appropriate.
- Object storage transfer utilities.

Final tooling depends on the approved target architecture.

# 18. MIGRATION BATCHES

Migration should be divided into controlled batches.

Suggested sequence:

1. Reference data.
2. Companies and identity records.
3. Suppliers and products.
4. Documents and file metadata.
5. Tender and bid records.
6. Procurement records.
7. Shipment and import records.
8. Inventory records.
9. Finance records.
10. HR and payroll records.
11. Tasks and collaboration.
12. Historical audit and workflow records.

Dependencies may require adjustments to this sequence.

Each batch must have:

- Batch identifier.
- Source scope.
- Target scope.
- Record count.
- Start and completion timestamps.
- Execution status.
- Error count.
- Exception count.
- Reconciliation status.
- Approver.

# 19. IDEMPOTENCY AND RE-RUN SAFETY

Migration jobs should be safe to re-run where technically possible.

Use stable source identifiers and migration mapping records.

A repeated batch must not create uncontrolled duplicate target records.

The migration process must distinguish:

- New source records.
- Previously migrated records.
- Changed source records.
- Rejected records.
- Previously failed records.

Updates to already migrated target records require explicit
rules and audit history.

# 20. MIGRATION EXCEPTION MANAGEMENT

Every migration exception must be recorded.

Examples:

- Missing company ownership.
- Invalid reference.
- Duplicate candidate.
- Missing file.
- Invalid financial amount.
- Unsupported format.
- Missing currency.
- Unreconciled inventory.
- Incomplete approval history.
- Invalid employee relationship.

Exception records should contain:

- Source reference.
- Entity type.
- Company.
- Error category.
- Description.
- Severity.
- Owner.
- Resolution.
- Decision.
- Approval.
- Status.

Unresolved critical exceptions must block the relevant
migration batch or cutover gate.

# 21. MIGRATION REHEARSALS

Conduct rehearsals in a non-production environment.

Suggested rehearsals:

## Rehearsal 1 — Technical proof

- Validate extraction.
- Validate mapping.
- Validate target loading.
- Validate file transfer.
- Validate error handling.

## Rehearsal 2 — Business data validation

- Review sample tenders.
- Review supplier records.
- Review procurement records.
- Review inventory.
- Review financial data.
- Review company isolation.

## Rehearsal 3 — Full-volume rehearsal

- Execute full approved migration scope.
- Measure duration.
- Measure resource consumption.
- Reconcile record counts.
- Reconcile financial totals.
- Validate document integrity.
- Review unresolved exceptions.

## Rehearsal 4 — Cutover simulation

- Simulate final extraction.
- Simulate source freeze.
- Execute migration.
- Validate target.
- Simulate rollback.
- Measure recovery time.

Production cutover must not be attempted before required
rehearsals pass.

# 22. RECONCILIATION FRAMEWORK

Reconciliation is mandatory.

## 22.1 Record reconciliation

Compare source and target counts by:

- Entity.
- Company.
- Status.
- Date range.
- Migration batch.

## 22.2 Relationship reconciliation

Verify:

- Parent-child relationships.
- Foreign-key mappings.
- Company ownership.
- Document references.
- User and membership relationships.
- Workflow references.

## 22.3 Financial reconciliation

Verify approved financial control totals and balances.

## 22.4 Inventory reconciliation

Verify approved stock quantities and valuation.

## 22.5 File reconciliation

Verify file counts, sizes, and checksums.

## 22.6 Reconciliation sign-off

Each domain owner must review and approve relevant results.

A migration batch must not be declared reconciled merely because
the import command completed successfully.

# 23. SECURITY AND PRIVACY

Migration data must be protected throughout the process.

Controls include:

- Restricted access.
- Read-only source credentials.
- Encrypted transfer.
- Secure temporary storage.
- Secret management.
- Access logging.
- Company isolation.
- Data minimization.
- Approved retention.
- Secure deletion of temporary copies after approval.

Do not place production database credentials, API keys,
passwords, or personal secrets in Git.

Do not upload sensitive production data to public services.

# 24. MIGRATION ENVIRONMENTS

Use separate environments:

1. Development.
2. Migration testing.
3. User acceptance testing.
4. Production.

Production source data must not be copied into development
without an approved data-protection process.

Where realistic test data is needed, use masked or synthetic
data where practical.

# 25. CUTOVER STRATEGY

## 25.1 Preconditions

Cutover requires:

- Approved target system.
- Approved migration scope.
- Passed rehearsals.
- Reconciled critical data.
- User acceptance.
- Security approval.
- Backup verification.
- Rollback readiness.
- Business owner authorization.

## 25.2 Cutover sequence

Proposed sequence:

1. Announce approved maintenance window.
2. Confirm source-system backup.
3. Freeze approved source writes.
4. Capture final source extraction.
5. Execute final migration batches.
6. Transfer and verify files.
7. Reconcile critical data.
8. Validate company access.
9. Validate user access.
10. Validate critical business workflows.
11. Obtain cutover approval.
12. Enable approved target operations.
13. Monitor system health and business operations.

The existing production system must remain protected until
the cutover decision is formally made.

## 25.3 Parallel operation

If parallel operation is required, define:

- System of record.
- Write ownership.
- Synchronization rules.
- Conflict resolution.
- Reconciliation frequency.
- End date.

Uncontrolled dual writing must not be permitted.

# 26. ROLLBACK STRATEGY

Rollback must be planned before production cutover.

Potential rollback triggers:

- Critical data loss.
- Incorrect company isolation.
- Unreconciled financial balances.
- Missing critical documents.
- Failed authentication.
- Broken approval workflows.
- Critical operational failure.
- Security incident.

Rollback planning must identify:

- Decision authority.
- Rollback window.
- Target-system write restrictions.
- Source-system recovery process.
- Data created during target operation.
- Reconciliation of post-cutover transactions.
- Communication responsibilities.

Rollback must not rely on deleting or overwriting source data.

Any reversal of transactions must follow approved accounting
and operational controls.

# 27. POST-CUTOVER VALIDATION

After cutover, validate:

- User authentication.
- Company switching.
- Company data isolation.
- Tender operations.
- Bid document access.
- Supplier records.
- Procurement.
- Shipment tracking.
- Landed cost.
- Inventory.
- Accounting.
- HR and payroll.
- Documents.
- Tasks and approvals.
- Reporting.
- Audit logs.
- Background jobs.
- AI services where enabled.

Monitor errors, latency, queues, storage, and data integrity.

# 28. MIGRATION MONITORING AND REPORTING

Provide migration dashboards or reports showing:

- Total source records.
- Total imported records.
- Skipped records.
- Failed records.
- Duplicate candidates.
- Unresolved exceptions.
- Reconciled batches.
- File transfer status.
- Financial reconciliation status.
- Inventory reconciliation status.
- Processing duration.

Reports must distinguish actual counts from estimates.

# 29. MIGRATION ACCEPTANCE CRITERIA

Migration is acceptable when:

- Source inventory is approved.
- Target mappings are approved.
- Company ownership is verified.
- Required records are migrated.
- Critical relationships are intact.
- Documents pass integrity checks.
- Financial control totals reconcile.
- Inventory balances reconcile.
- User memberships are correctly mapped.
- Company-scoped permissions are preserved.
- Workflow history is traceable.
- Exceptions are resolved or formally accepted.
- Rehearsals pass.
- Rollback is demonstrated.
- Business owners sign off.
- Cutover is explicitly authorized.

# 30. MIGRATION RISKS

| Risk | Potential impact | Control |
|---|---|---|
| Incomplete source inventory | Missing records | Read-only discovery |
| Incorrect company mapping | Data exposure | Ownership reconciliation |
| Duplicate records | Operational confusion | Review and exception queue |
| Financial conversion errors | Incorrect accounts | Finance sign-off |
| Missing files | Loss of evidence | Checksums and file reconciliation |
| Invalid relationships | Broken records | Referential validation |
| Permission escalation | Security exposure | Membership-based role mapping |
| Incomplete workflow history | Loss of traceability | Historical mapping |
| Cutover failure | Business interruption | Rehearsal and rollback |
| Uncontrolled dual writing | Data divergence | Explicit system-of-record policy |

# 31. IMPLEMENTATION PHASING

## Phase 1 — Discovery

- Verify source schema.
- Verify source data volumes.
- Inventory document storage.
- Identify source relationships.
- Classify data.
- Identify sensitive records.

## Phase 2 — Mapping

- Approve source-to-target mapping.
- Define transformations.
- Define company mapping.
- Define exception categories.
- Define reconciliation controls.

## Phase 3 — Tooling

- Build extraction tooling.
- Build transformation tooling.
- Build import tooling.
- Build file transfer tooling.
- Build reconciliation reports.

## Phase 4 — Rehearsal

- Execute test batches.
- Review data quality.
- Reconcile financial and inventory records.
- Validate security.
- Conduct cutover simulation.

## Phase 5 — Acceptance and Cutover

- Obtain business approval.
- Obtain security approval.
- Verify backup and rollback.
- Execute authorized cutover.
- Monitor and reconcile.

# 32. OPEN MIGRATION DECISIONS

The following decisions require approval:

1. Exact production database inventory.
2. Exact production file storage inventory.
3. Historical data retention period.
4. Migration scope by module.
5. Archive-only versus active migration policy.
6. User password migration method.
7. Historical workflow retention.
8. Finance opening-balance date.
9. Inventory valuation cutover date.
10. Document version retention.
11. Treatment of inactive employees.
12. Treatment of obsolete suppliers and products.
13. Treatment of duplicate candidates.
14. Treatment of incomplete records.
15. Parallel operation policy.
16. Cutover maintenance window.
17. Rollback decision authority.

# 33. DOCUMENT STATUS AND GOVERNANCE

**Status:** Proposed migration strategy.

This document defines the migration approach. It does not
authorize production database access, production extraction,
data modification, import, cutover, or deletion.

All production migration actions require explicit authorization
and approved technical and business controls.

---

# 34. NEXT DOCUMENT

The next planned document is:

`docs/08-implementation/IMPLEMENTATION_BACKLOG.md`

It will translate the approved discovery, requirements,
architecture, database, security, UI, AI, and migration
documents into prioritized implementation epics, work packages,
dependencies, and acceptance criteria.
