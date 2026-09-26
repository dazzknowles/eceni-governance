# MariaDB Implementation Guide

**Guide version:** 1.1.0

**Introduced in Governance baseline:** 1.1.0

**Revised in Governance baseline:** 1.3.0

**Governing Laws:** [QUA-001](../LAWS.md#qua-001--follow-the-applicable-implementation-guide) and [QUA-003](../LAWS.md#qua-003--source-is-human-usable-and-intent-is-discoverable)

## Scope

This guide applies to Eceni-authored and Eceni-maintained MariaDB schemas, routines, views, migrations and queries. New objects comply completely. New and materially changed definitions in an existing database comply from the project's adopted source baseline; untouched inherited definitions are not thereby represented as compliant.

## Naming and layout

- Use plural `PascalCase` table names, such as `CollectionAttempts`.
- Use `PascalCase` column names.
- Preserve the conventional written form of established acronyms, including `ID`, `UTC`, `HTTP`, `PV` and `VAT`: use `DeviceID`, `ObservedAtUTC` and `HTTPStatus`, not `DeviceId`, `ObservedAtUtc` or `HttpStatus`.
- Name a table's ordinary surrogate primary key `ID`. Name a referencing column for the referenced entity, such as `SiteID` or `CollectionRunID`.
- Use `esp<Entity><Action>` for Eceni stored procedures, such as `espDeviceGetByID` and `espTelemetryObservationInsert`.
- Prefix parameters by direction and use `camelCase` after the prefix: `in_deviceID`, `out_collectionRunID` and `inout_attemptCount`.
- Prefix routine-local variables with `local_` and use `camelCase` after the prefix.
- Use short but meaningful table aliases. Avoid aliases whose meaning cannot be understood locally.
- Name keys and constraints using `PK_<Table>`, `FK_<Child>_<ParentOrPurpose>`, `UQ_<Table>_<Purpose>` and `IX_<Table>_<Purpose>`.
- Match a source-controlled object's filename to its database object name.
- Write SQL keywords in uppercase and use consistent indentation within the project.
- Include units or time basis in identifiers where omission could mislead. The standard `CreateDate` and `LastActionDate` names defined below are UTC by contract.

Names describe domain meaning rather than incidental implementation. Avoid abbreviations unless they are established domain or technical terminology.

## Common row metadata

An ordinary user-maintained business table is expected to include these columns unless their purpose genuinely does not apply:

- `Deleted` — a non-null logical deletion flag, ordinarily `TINYINT(1) NOT NULL DEFAULT 0`;
- `CreateUserID` — the actor responsible for creation;
- `CreateDate` — the UTC creation time;
- `LastActionUserID` — the actor responsible for the latest material mutation;
- `LastActionDate` — the UTC time of the latest material mutation.

Creation metadata is immutable after insertion. Last-action metadata changes only with a material mutation, including logical deletion; reads do not update it. Normal reads exclude logically deleted rows unless the contract explicitly requests them. Physical deletion, retention and uniqueness behaviour for deleted rows must be decided for the affected data rather than inferred from the flag.

Actor columns may identify a human, service or system actor according to the project's identity model. Use an explicit system identity where the model provides one. Null is permitted only where the contract deliberately represents an unknown or unavailable actor.

These columns provide current attribution, not a complete audit history. A requirement to reconstruct changes needs a separately designed audit mechanism that defines actions, actors, timestamps, correlation, retained state, access and sensitive-data treatment.

## Referential integrity distinguishes business data from attribution

Use database-enforced foreign keys by default for genuine business relationships. A business relationship is not left unenforced merely for convenience or because application code currently supplies a valid value.

The standard `CreateUserID` and `LastActionUserID` attribution columns are soft references by default and do not carry foreign keys to the shared user table. Foreign keys from many child tables into that common identity table have previously created disproportionate locking and timeout behaviour. A project may add such a foreign key where its topology and workload show that the integrity benefit outweighs the contention and maintenance cost. The metadata default is intentional, not an accidental omission or a precedent for business relationships.

A soft reference still has a defined target and validation boundary. The application or routine must supply and validate it appropriately, and deletion or retirement of the referenced identity must preserve required attribution. Do not add indexes to every metadata reference mechanically; index them when an evidenced access, integrity or operational need justifies the write and storage cost.

Name foreign keys and their supporting indexes consistently. Assess high-fan-in or high-write relationships using representative concurrency and workload evidence when their locking behaviour may be material.

## Types and nullability are deliberate

- Choose data types, lengths, signedness and numeric precision for the domain and credible range rather than copying an arbitrary default.
- Use exact numeric types where exact values matter; do not use floating-point storage for money or another exact decimal contract.
- Use UTC for stored instants unless a requirement explicitly needs another representation. Preserve an original offset or lexical value separately where evidence or user meaning requires it.
- Make nullability express a defined domain state. Do not use null merely to avoid choosing a default or modelling a state.
- Select character set and collation deliberately where comparison, ordering, case or international text behaviour can affect correctness.

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
- Treat external values as data and bind them through parameters. Externally influenced table, column, direction or expression choices must come through a closed, validated allow-list rather than becoming executable structure directly.
- Avoid dynamic SQL unless the requirement cannot be met safely with static SQL; any use requires explicit security review, value parameterisation and controlled structural composition.
- Comment consequential intent, assumptions and non-obvious performance choices rather than narrating syntax.

## Routine contracts are visible

Routine definitions and their neighbouring documentation must make input and output meaning, result-set shape, no-result behaviour, material side effects, expected failure behaviour and transaction ownership discoverable. Result-set column names and meanings are contracts with their consumers and must not change casually.

Stored procedures should remain independently understandable. Do not create hidden or difficult-to-follow procedure-to-procedure call graphs. A procedure may call another only where the reuse, transaction and failure semantics are clearer than keeping the operation explicit, and the dependency is visible in the source-controlled definitions and review.

## Concurrency and audit mechanisms remain evidence-led

Keep transactions as short as correctness permits, acquire locks in a consistent order where practical and do not hold database locks across user interaction or avoidable external calls. Use locking reads deliberately and make deadlock or concurrency-conflict handling bounded and visible.

Eceni has not yet selected one portfolio-wide row-locking, optimistic-concurrency or audit-history mechanism. Choose the mechanism from an actual consistency and history requirement, record the decision, and promote a reusable pattern only after a real workload such as Solar has exercised it.

## Checks

Static checks can detect many naming and acronym violations, missing `SQL SECURITY`, use of `DEFINER`, shorthand or implicit joins, `SELECT *`, unstable limiting, unbound values and common unsafe dynamic-SQL patterns. They can also identify missing expected row metadata and unnamed constraints while allowing an explicit non-applicability decision.

[CHK-DB-001](../CHECKS.md#chk-db-001--database-definitions-match-source) specifies source/deployment drift detection; [CHK-DATA-001](../CHECKS.md#chk-data-001--database-bootstrap-is-reproducible) covers schema and system-data reconstruction. Whether a relationship is business data or attribution, whether documentation is useful, and where work should run remain evidence-led engineering judgements.
