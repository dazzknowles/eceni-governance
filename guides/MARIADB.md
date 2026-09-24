# MariaDB Implementation Guide

**Guide version:** 1.0.0

**Introduced in Governance baseline:** 1.1.0

**Governing Law:** [QUA-001](../LAWS.md#qua-001--follow-the-applicable-implementation-guide)

## Scope

This guide applies to Eceni-authored MariaDB schemas, routines, views, migrations and queries.

## Routine and view security is explicit

Stored routines and views must declare `SQL SECURITY INVOKER` explicitly.

`SQL SECURITY DEFINER` is permitted only when the object deliberately implements a reviewed privilege boundary that cannot be achieved safely with invoker permissions. The design must identify the definer identity, granted operations, callers, risk, tests and operational ownership. Relying on MariaDB's implicit [`DEFINER` default](https://mariadb.com/docs/server/server-usage/stored-routines/stored-functions/stored-routine-privileges) is not permitted.

Invoker security does not remove the need for least privilege: application and migration identities receive only the permissions necessary for their declared purpose under [SEC-001](../LAWS.md#sec-001--capability-is-minimized).

## Join intent is explicit

- Spell join type fully: `INNER JOIN`, `LEFT OUTER JOIN` or `RIGHT OUTER JOIN`.
- Do not use comma-separated table lists as implicit joins.
- State every join predicate in its corresponding `ON` clause unless a deliberate cross join is required.
- Use `CROSS JOIN` explicitly when a Cartesian product is intended.

The purpose is to make cardinality and null-preservation decisions visible during review, not to prefer one join type over another.

## Database definitions are source-controlled

Schema objects, including tables, routines, views, triggers and events, must have a canonical, reviewable representation in the project repository.

A change made through DbForge, another database tool or directly against a database is not complete until the normalized definition and any required deployment change are preserved in source control. The deployed database is runtime state and evidence; it is not the sole source of truth.

Exclude environment-specific or sensitive material from the canonical representation:

- application and customer data;
- secrets and credentials;
- environment-specific accounts and grants;
- incidental definer identities;
- tool metadata and formatting noise.

Automation or an agent should export, normalize and reconcile definitions as part of the same work item rather than relying on a human to remember a separate copying step. Removed objects must be represented deliberately; an exporter must not leave obsolete files looking authoritative.

This practice continues the intent of the earlier private [MySQL2SCM](https://github.com/dazzknowles/mysql2scm) experiment, which enumerated database objects, captured their `SHOW CREATE` definitions and wrote one file per object to a version-controlled working copy. The historical implementation is provenance, not a dependency or current standard.

## Required system data is reconstructible

System and reference data governed by [DATA-002](../LAWS.md#data-002--required-system-data-is-reconstructible) must be explicitly allow-listed for export or acquired reproducibly from its canonical source. Never infer that every row in a small table is safe or appropriate for source control.

Versioned exports must:

- declare the selected table and columns;
- use stable keys and deterministic row ordering;
- use a reviewable, deterministic representation;
- preserve required relationships without relying on environment-specific surrogate values;
- define deletion, retirement and update semantics;
- carry provenance, classification and source-version metadata.

Projects must provide a clean bootstrap profile. They may additionally reference approved representative seeds, such as a sanitised UAT snapshot, for tasks that require realistic state or scale. Seed artefacts containing non-public data remain outside ordinary source control and are accessed only under explicit task authority.

## Work belongs at the least expensive appropriate layer

The database is typically the most expensive shared component. Do not ask it to perform presentation-only ordering of an already bounded result set when the application can sort that data more economically.

Keep ordering in the database when it:

- affects row selection, pagination or `LIMIT`;
- is required by windowing, grouping or aggregation;
- defines stable query or streaming semantics;
- can use an index to avoid greater work;
- materially reduces the rows or data transferred;
- is necessary for correctness or concurrency consistency.

Apply the same whole-system reasoning to other work. Push selective filtering and set operations into the database when that avoids transferring or processing unnecessary data. Do not move a large unsorted result into an application merely to reduce visible database work.

For material or disputed paths, use representative query plans, volumes and timings rather than assuming which layer is cheaper. Reassess under [GOV-002](../LAWS.md#gov-002--decisions-remain-valid-only-while-their-basis-holds) when volume, topology or service characteristics materially change.

## SQL is deterministic and reviewable

- Specify ordering whenever callers depend on order; do not rely on incidental storage order.
- Use stable tie-breakers for pagination and limiting.
- Select named columns rather than `SELECT *` in application-facing code.
- Qualify columns where more than one source is present.
- Keep parameter direction and purpose visible through consistent naming.
- Avoid dynamic SQL unless the requirement cannot be met safely with static SQL; any use requires explicit security review and parameterisation.
- Comment consequential intent, assumptions and non-obvious performance choices rather than narrating syntax.

## Checks

Static checks can detect missing `SQL SECURITY`, use of `DEFINER`, shorthand or implicit joins, `SELECT *`, unstable limiting and common unsafe dynamic-SQL patterns. [CHK-DB-001](../CHECKS.md#chk-db-001--database-definitions-match-source) specifies source/deployment drift detection; [CHK-DATA-001](../CHECKS.md#chk-data-001--database-bootstrap-is-reproducible) covers schema and system-data reconstruction. Placement of work between the database and application remains evidence-led engineering judgement.
