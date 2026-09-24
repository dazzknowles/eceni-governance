# Eceni Checks

**Introduced in Governance baseline:** 1.1.0

**Adopted:** 24 September 2026

Checks automate objective enforcement of [Eceni Laws](LAWS.md) where doing so is reliable and proportionate. A Check does not define Governance and cannot waive, reinterpret or replace the Law it supports.

## CHK-GOV-001 — Parent Issues with Open Sub-Issues Remain Open

**Implements:** [GOV-001](LAWS.md#gov-001--departures-follow-a-governed-lifecycle)

**Status:** Specified; not yet implemented

**Initial implementation target:** GitHub Actions

When a governed parent issue is closed, inspect all direct and nested sub-issues. If any remain open:

1. Reopen the parent issue.
2. Add a concise explanation identifying the outstanding obligations.
3. Preserve the original closure event as evidence of the rejected transition.

Apply the Check only to issues explicitly participating in the governed lifecycle, identified by an agreed issue type or label.

The Check must not automatically close sub-issues when their parent is closed. To supersede an obligation, the responsible authority closes that sub-issue explicitly with the superseding decision before closing the parent.

Reopening corrects an invalid lifecycle transition; it does not create a new Governance decision.

## CHK-DB-001 — Database Definitions Match Source

**Implements:** [QUA-001](LAWS.md#qua-001--follow-the-applicable-implementation-guide) and the [MariaDB implementation guide](guides/MARIADB.md#database-definitions-are-source-controlled)

**Status:** Specified; not yet implemented

**Initial implementation target:** Agent-assisted export plus automated ephemeral-database comparison

For a project governed by the MariaDB implementation guide:

1. Create a clean ephemeral database from the versioned definitions.
2. Export and normalize the resulting object definitions.
3. Compare the material definitions with the canonical source representation.
4. Report missing, unexpected or materially different objects as drift.

Where a database tool is used to author a change, an agent may export and normalize the changed definitions into the working tree for review. A live or development database must not be copied blindly into source control or treated as authoritative merely because it is deployed.

Normalization may remove environment-specific accounts, grants, incidental definer identities, tool metadata and formatting noise. It must not hide material security, behaviour, schema or data-type differences.

The Check must not export application data, secrets or credentials. It reports drift and prepares reviewable changes; it does not automatically accept live state or commit it as Governance-compliant source.

## CHK-DATA-001 — Database Bootstrap Is Reproducible

**Implements:** [DATA-002](LAWS.md#data-002--required-system-data-is-reconstructible)

**Status:** Specified; not yet implemented

**Initial implementation target:** MySQL2SCM plus an ephemeral MariaDB environment

For the clean bootstrap profile:

1. Create an empty ephemeral database.
2. Apply the versioned database definitions.
3. Acquire or load every required system/reference dataset from its declared canonical source.
4. Verify dataset versions or checksums, stable keys and required relationships.
5. Run the project's declared readiness evidence.

For a representative-seed profile, additionally verify that the selected immutable artefact matches its manifest and that the task records its access authority, classification, sanitisation status, schema compatibility and disposal requirement.

The Check must not make an unavailable or unauthorised seed look like successful evidence. If the required database or artefact cannot be accessed, report the result as unavailable or blocked under [EVI-001](LAWS.md#evi-001--claim-strength-must-not-exceed-evidence), not Pass.

Production data must not be selected automatically as a development or test seed. Prefer a clean or synthetic profile unless representative environment data is necessary for the task's evidence.
