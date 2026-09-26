# Eceni Laws

**Introduced in Governance baseline:** 1.1.0

**Adopted:** 24 September 2026

**Scope:** Eceni product and engineering work to which each Law applies

## How Laws apply

Laws translate the [Eceni Commandments](COMMANDMENTS.md) into concrete engineering rules, defaults and explicitly governed exceptions.

Every Law states its applicability, exception policy, required evidence and suitable Checks. Genuine non-applicability is distinct from an exception: it must be explicit, justified and recorded under the applicable Governance baseline.

An exception exists only where the Law defines one. If a Law permits no exception, ordinary project, work-order or agent authority cannot depart from it; changing the rule requires a new Governance baseline. A permitted exception follows [GOV-001](#gov-001--departures-follow-a-governed-lifecycle).

Checks enforce only the objective portions of Laws. Passing a Check does not prove compliance with judgement-based obligations, and a missing Check does not make a Law optional.

## EVI-001 — Claim Strength Must Not Exceed Evidence

> Every consequential claim of compliance, completion, success or capability must identify its supporting evidence and use a result classification that faithfully represents that evidence.

Unverified, partially verified, not observed, not run, failed, blocked and not applicable outcomes must not be represented as Pass. Silence, absence of evidence and timeout are not consent or proof.

### Applicability

Specifications, acceptance decisions, reviews, tests, operational evidence and Harness outcomes.

### Exceptions

None. A specification may define more precise evidence states but may not redefine an unsupported result as Pass.

### Required evidence

- the criterion assessed;
- the result classification;
- the supporting evidence, or an explicit reason evidence is unavailable;
- the responsible assessment.

### Checks

Structured results may enforce required fields, permitted states and valid state transitions. Whether evidence substantively supports the claim still requires proportionate review.

### Basis

Implements [**Faithful Evidence**](COMMANDMENTS.md#3-faithful-evidence). [Solar r04](https://github.com/dazzknowles/solar-optimiser/blob/main/docs/requirements/foxess/read-only-capability/r04/candidate-foxess-read-only-capability-integration-spec-r04-20260910T220245611Z.md) distinguished documented claims, candidate interpretations and tenant-zero verification; its later addenda demonstrated why deferred evidence must not silently become completion evidence.

## EVI-002 — Evidence Timing Must Be Proportionate

> Evidence need not precede implementation. Where building or running the system is the quickest and most reliable way to obtain required evidence, accountable authority may defer evidence completion rather than require a separate proving exercise.

A deferral must:

- record why separate pre-build verification would be disproportionate;
- preserve the outstanding evidence obligation;
- identify its owner and an objective trigger or review point;
- distinguish implementation completion from verified acceptance;
- record what may and may not proceed while evidence remains outstanding;
- return contrary findings to specification or design authority.

### Applicability

Work where implementation or operation is itself the proportionate evidence-producing mechanism.

### Exceptions

Deferral is not permitted where prior evidence is necessary to protect correctness, security, privacy or another explicit hard constraint before release or exposure.

### Required evidence

The recorded deferral decision and the durable obligation created under GOV-001, followed by evidence classified under EVI-001.

### Checks

Automation may require ownership, triggers and separation between implementation completion and verified acceptance. It cannot determine whether deferral is substantively proportionate.

### Basis

Implements [**Faithful Evidence**](COMMANDMENTS.md#3-faithful-evidence), [**Value Over Waste**](COMMANDMENTS.md#4-value-over-waste) and [**Build Quality In**](COMMANDMENTS.md#6-build-quality-in). Solar [r04a](https://github.com/dazzknowles/solar-optimiser/blob/main/docs/requirements/foxess/read-only-capability/r04/r04a-phase1-vertical-slice-sequencing-and-pv-mapping-addendum-20260918T214259000Z.md) and [r04b](https://github.com/dazzknowles/solar-optimiser/blob/main/docs/requirements/foxess/read-only-capability/r04/r04b-phase1-evidence-completion-decoupling-addendum-20260918T234214000Z.md) established that the real vertical slice could be the sensible evidence-producing mechanism without pretending that tenant-zero verification had already passed.

## GOV-001 — Departures Follow a Governed Lifecycle

> An accepted specification, Governance baseline or recorded decision must not be silently reinterpreted. Every proposed departure, deferral, exception or non-applicability decision must follow a repeatable, traceable process from discovery through resolution.

The process must:

1. Identify the affected baseline, rule, requirement or decision.
2. Classify the proposal accurately as a departure, deferral, permitted exception or non-applicability.
3. Record evidence, rationale, scope, consequences and obligations that remain.
4. Confirm that the decision-maker holds the required authority.
5. Record approval, rejection or return for more evidence.
6. State what becomes authoritative instead while preserving the original source.
7. Create owned, trackable obligations for anything left outstanding.
8. Preserve material state changes and evidence.
9. Close only through demonstrated satisfaction or an explicit superseding decision.

Every case requires a stable identity and durable history. Outstanding obligations must record their acceptance conditions, owner, current state and objective trigger or next review point. Silence, age or completion of related implementation does not close them.

### Applicability

Baselined Governance, approved specifications, consequential design decisions and acceptance criteria.

### Exceptions

None to the requirement to record and govern a departure. This Law does not create permission to waive a Commandment or an exceptionless Law.

### Required evidence

The durable decision record, authority, affected source identities, rationale, consequences, compensating controls, residual obligations, state history and closure evidence.

### Checks

Automation may enforce identity, ownership, required fields, valid state transitions and closure evidence. [CHK-GOV-001](CHECKS.md#chk-gov-001--parent-issues-with-open-sub-issues-remain-open) is the first specified Check. Human authority judges the adequacy of rationale and controls.

### Basis

Implements [**Bounded Autonomy**](COMMANDMENTS.md#1-bounded-autonomy), [**Faithful Evidence**](COMMANDMENTS.md#3-faithful-evidence) and [**Pay for a Lesson Once**](COMMANDMENTS.md#5-pay-for-a-lesson-once). Solar r04a and r04b preserved their source baseline and recorded scoped changes rather than allowing implementation to reinterpret it silently.

## GOV-002 — Decisions Remain Valid Only While Their Basis Holds

> An accepted decision remains authoritative until material evidence, assumptions or governing constraints change. When they change, the decision must be reassessed rather than treated as permanent precedent.

Where a decision depends materially on variable conditions, record:

- the assumptions on which it relies;
- relevant price, volume, capability, risk or service-level thresholds;
- observable events that trigger reassessment;
- a review point when change cannot be detected reliably;
- the authority responsible for reconsideration.

Material triggers include pricing or licensing changes, service-level changes, significant usage changes, new provider capabilities or restrictions, changed security or privacy risk, better technical options and changed product requirements.

Reassessment does not presume reversal. It determines whether the decision remains correct under current evidence. Prefer event-driven review over arbitrary recurring review where practical.

### Applicability

Consequential decisions whose correctness depends on changeable external or operational conditions.

### Exceptions

None when a material recorded assumption or constraint has changed. Trivial decisions need not manufacture review triggers.

### Required evidence

The decision basis, reassessment triggers, detected material change, reassessment result and accountable authority.

### Checks

Automation may monitor objective triggers such as renewal dates, cost thresholds, usage growth and service-level breaches.

### Basis

Implements [**Faithful Evidence**](COMMANDMENTS.md#3-faithful-evidence), [**Value Over Waste**](COMMANDMENTS.md#4-value-over-waste) and [**Pay for a Lesson Once**](COMMANDMENTS.md#5-pay-for-a-lesson-once): reuse a sound decision until the evidence changes, then reconsider it honestly.

## GOV-003 — Projects Retain Their Governance Lineage

> Every project must identify its current Eceni Governance baseline and retain the complete lineage of Governance baselines under which it has operated.

The lineage must identify:

- the baseline under which the project was created;
- its current applicable baseline;
- every subsequently adopted baseline;
- the decision by which each transition was made;
- material applicability decisions, permitted exceptions and migration work associated with the transition.

Changing a version number alone is not adoption. A project must not represent itself as compliant with a baseline until required migration work and applicability decisions have been completed or explicitly governed as outstanding obligations.

### Applicability

All Eceni product and engineering projects.

### Exceptions

None.

### Required evidence

A durable project record linking each adopted baseline to its adoption decision and material migration evidence.

### Checks

Automation may verify that a project declares a known baseline, preserves an ordered lineage and has no ungoverned migration obligations.

### Basis

Implements [**Bounded Autonomy**](COMMANDMENTS.md#1-bounded-autonomy), [**Faithful Evidence**](COMMANDMENTS.md#3-faithful-evidence) and [**Pay for a Lesson Once**](COMMANDMENTS.md#5-pay-for-a-lesson-once), and makes Governance evolution auditable without rewriting project history.

## VER-001 — Conformance Evidence Is Independently Derived

> Where the consequences justify it, evidence used to establish conformance must be designed from the governing requirement independently of the implementation being assessed.

The verifier begins with the specification, Law or acceptance criterion and determines what evidence would prove it. Tests that merely reproduce the implementation's structure or assumptions do not provide independent conformance evidence.

Independence can come from another human, agent or deliberately isolated verification context. It is independence of reasoning and evidence, not a ritual requirement for a particular job title.

### Applicability

Apply particularly to:

- correctness, security and privacy obligations;
- destructive or difficult-to-reverse behaviour;
- recovery and data-integrity claims;
- material customer, contractual or financial behaviour;
- core calculations and consequential external integrations;
- criteria explicitly designated for independent verification by a specification.

For low-consequence work, ordinary implementation tests and review may be sufficient.

### Exceptions

Where independent verification would be disproportionate or genuinely impractical, record that conclusion and the alternative evidence under GOV-001. It must not be assumed silently.

### Required evidence

- the requirement or criterion assessed;
- the independently derived test, review or observation;
- provenance identifying who or what produced it and from which inputs;
- the result classified under EVI-001.

### Checks

Automation may verify traceability, separation of artefacts or agents, and presence of results. It cannot reliably determine whether reasoning was genuinely independent.

### Basis

Implements [**Faithful Evidence**](COMMANDMENTS.md#3-faithful-evidence) and [**Build Quality In**](COMMANDMENTS.md#6-build-quality-in). Solar's [independently derived test suite](https://github.com/dazzknowles/solar-optimiser/commit/751bae5) found defects missed by implementation-led tests, while five rounds of adversarial design review demonstrated the value of proportional independent challenge.

## SEC-001 — Capability Is Minimized

> Every component, credential, integration, agent and automation must receive only the capability necessary for its declared purpose.

Where a provider supports granular permissions, use the narrowest sufficient scope. Where it does not:

- expose only explicitly permitted operations;
- allow-list endpoints and methods;
- omit generic or arbitrary execution paths;
- isolate credentials and limit their reach;
- record the provider limitation and residual risk;
- require fresh review before expanding capability.

A claim such as “read-only” must describe an enforceable boundary, not merely intended behaviour.

### Applicability

External integrations, service identities, credentials, administrative tooling, agents, automation and security boundaries.

### Exceptions

Broader capability is permitted only when technically unavoidable and explicitly justified under GOV-001, with proportionate compensating controls and accountable acceptance of residual risk.

### Required evidence

The declared purpose, required operations, granted and reachable capability, any mismatch, compensating controls, verification and authority for later expansion.

### Checks

Static allow-lists, permission inspection, tests proving forbidden operations are unreachable and alerts on capability expansion may be automated.

### Basis

Implements [**Data Is Entrusted**](COMMANDMENTS.md#2-data-is-entrusted) and [**Bounded Autonomy**](COMMANDMENTS.md#1-bounded-autonomy). FoxESS supplied a broadly capable private key without a provider-enforced read-only scope, so Solar created a smaller enforceable capability through its adapter boundary.

## DATA-001 — Data Use Is Purpose-Bound

> Collect, access, retain, transmit and expose only the data necessary for a declared product or engineering purpose.

Data must not be retained, logged, copied into evidence, sent to a third party or supplied to an AI system merely because it is available or potentially useful.

For each material data flow, establish proportionately:

- what data is involved and what it represents;
- the purpose requiring it;
- who or what can access it;
- where it is stored or transmitted;
- relevant retention, deletion, export and recovery behaviour;
- any external processor, provider or AI recipient;
- what sensitive detail must be redacted or excluded from diagnostics and evidence.

When the purpose ends or changes, continued possession or use requires fresh justification. Recovery requirements must respect deliberate deletion and retention limits.

### Applicability

All data handled by Eceni product and engineering systems, including telemetry, metadata, diagnostics, evidence, prompts and operational records.

### Exceptions

Additional collection or retention requires a specific evidenced need and appropriate authority under GOV-001. “We may want it later” is insufficient.

### Required evidence

The purpose, material flow, access boundary, storage or recipient, retention/deletion/recovery decision, and authority for exceptional use.

### Checks

Secret scanning, log-content tests, schema and egress inspection, retention checks and prohibited-field detection may enforce objective parts.

### Basis

Implements [**Data Is Entrusted**](COMMANDMENTS.md#2-data-is-entrusted) and [**Value Over Waste**](COMMANDMENTS.md#4-value-over-waste). Moving and retaining only necessary data also reduces latency, bandwidth, storage, processing, inference cost and operational exposure.

## DATA-002 — Required System Data Is Reconstructible

> Data required for a system to operate correctly must have a canonical, versioned source or a reproducible acquisition process.

This includes dropdown and enumeration values represented as data, geographic and industry reference datasets, system roles, templates, defaults, mappings and rules deliberately maintained outside code.

Each material dataset must declare:

- its purpose and classification;
- whether source control, an immutable artefact or an upstream provider is canonical;
- provenance, licence and source version where applicable;
- stable keys and deterministic ordering;
- import and update behaviour;
- whether removed rows are deleted, retired or retained;
- whether runtime editing is permitted and how conflicts with the canonical source are resolved.

A clean environment must be reconstructible without copying an arbitrary production database. Large, licensed or externally maintained datasets need not live directly in Git when the repository retains an immutable version or checksum and a reproducible acquisition and import process. Derived data may retain its recipe, inputs and version rather than every generated row.

### Environment bootstrap modes

Projects may provide more than one explicit bootstrap profile:

- **Clean:** build the schema and required system/reference data from canonical sources. This is the default.
- **Representative seed:** restore an approved, immutable snapshot from an environment such as UAT when a task genuinely requires representative state, scale or edge cases.

A representative seed must record its source, capture time, schema/Governance compatibility, checksum, data classification, sanitisation status, access authority and disposal requirements. An agent may use it only when the work order authorises that data and environment profile. Production data is not an ordinary development seed.

Where safer synthetic data can provide the necessary evidence, prefer it. A restored snapshot must be migrated deliberately to the required source baseline rather than silently treated as current.

### Applicability

System and reference data required to build, run, test or meaningfully exercise an Eceni product.

### Exceptions

None to reconstructibility. The canonical material may live outside Git where size, licensing, sensitivity or authoritative upstream ownership justifies that choice and the acquisition path remains reproducible.

### Required evidence

Dataset manifests, provenance, version or checksum, classification, import procedure and a successful reconstruction result. Representative seeds additionally require authority and sanitisation/disposal evidence.

### Checks

[CHK-DATA-001](CHECKS.md#chk-data-001--database-bootstrap-is-reproducible) specifies reconstruction and seed-profile validation.

### Basis

Implements [**Data Is Entrusted**](COMMANDMENTS.md#2-data-is-entrusted), [**Pay for a Lesson Once**](COMMANDMENTS.md#5-pay-for-a-lesson-once) and [**Build Quality In**](COMMANDMENTS.md#6-build-quality-in). It distinguishes canonical operating data from customer/operational backups while allowing agents to choose the authorised environment their task needs.

## ECO-001 — Prefer Bounded Cost to Recurring Waste

> Prefer bounded upfront engineering effort or cost over recurring operational expenditure when evidence shows a clear whole-life benefit and the change does not compromise required correctness, security, privacy or quality.

Apply particularly when:

- deterministic software can satisfactorily replace recurring AI inference;
- avoiding unnecessary data movement reduces processing, storage or network cost;
- a small implementation change removes repeated manual work;
- included or already-paid capacity can satisfy the need appropriately;
- modest engineering work prevents a recurring third-party or infrastructure charge.

The assessment must include expected volume and useful lifetime, implementation and maintenance cost, recurring unit and operational costs, a reasonable payback horizon, opportunity cost, delivery impact and quality/security/privacy consequences.

### Applicability

Material recurring infrastructure, service, inference, data-transfer and operational costs.

### Exceptions

A recurring cost may be preferred for speed, reversibility or risk reduction when its whole-life trade-off is explicit and within commercial authority. Uncertain volume or lifetime may justify the simpler recurring option until evidence changes. GOV-002 requires reassessment when the basis changes.

### Required evidence

The material assumptions, whole-life comparison, constraints, decision authority and reassessment triggers.

### Checks

Automation may surface cost thresholds, usage trends and repeated inference or transfer patterns. An agent may analyse spending but may not authorise commercial expenditure.

### Basis

Implements [**Value Over Waste**](COMMANDMENTS.md#4-value-over-waste) without confusing economy with the lowest immediate cost or speculative optimisation.

## QUA-001 — Follow the Applicable Implementation Guide

> Implementation must conform to every applicable, versioned Eceni language or platform implementation guide.

Where no Eceni guide exists:

1. Follow the project's established conventions where they remain sound.
2. Follow authoritative language, platform and vendor guidance.
3. Prefer conventional, understandable implementation over novelty.
4. Record a decision when a consequential choice remains ambiguous or could become reusable portfolio guidance.

“Industry best practice” alone is not an adequate justification: it is ambiguous and can conceal contradictory preferences.

### Applicability

Eceni-authored source code, database code, configuration, tests and other implementation artefacts. Generated code and externally imposed formats may be declared out of scope with evidence of their origin.

The initial applicable guides are:

- [C# implementation guide](guides/CSHARP.md)
- [MariaDB implementation guide](guides/MARIADB.md)

### Exceptions

A material departure requires a concrete benefit, recorded rationale and proportionate review under GOV-001. Project-specific guidance may strengthen or specialise an Eceni guide but may not silently weaken it.

### Required evidence

The applicable guide version, automated results where available, review of judgement-based requirements and any governed departure.

### Checks

Formatters, analysers, linters and structural tests should enforce objective rules. Judgement-based guidance remains subject to review rather than false automation.

### Basis

Implements [**Build Quality In**](COMMANDMENTS.md#6-build-quality-in), [**Pay for a Lesson Once**](COMMANDMENTS.md#5-pay-for-a-lesson-once) and [**Value Over Waste**](COMMANDMENTS.md#4-value-over-waste) by making known-good implementation decisions reusable while allowing evidence-backed evolution.

## QUA-002 — Technology Foundations Require Explicit Authority

**Introduced in Governance baseline:** 1.2.0

> Where the applicable specification or project record does not define a technology choice, an agent must not establish a durable technology dependency by assumption. It must use an already-authorised project or portfolio default or obtain a decision from the design authority before implementation.

A technology is not authorised merely because it is familiar, conventional, quick to implement or technically suitable. Apply the following order:

1. Use the technology required by the authoritative specification or work item.
2. Otherwise use an applicable, explicitly adopted project or portfolio default.
3. Where neither exists, ask the design authority to decide before creating a durable dependency.

The decision request should be proportionate. It should normally identify the recommended choice, material alternatives and the consequences that distinguish them, such as build and runtime requirements, deployment and operations, security, privacy, licensing, cost, maintainability, available skills, portability and interoperability.

Once a technology baseline has been authorised, agents retain autonomy over ordinary implementation choices within it, subject to the other applicable Laws and guides. Projects should record reusable defaults so the same settled question is not repeatedly raised.

### Applicability

Choices that create or materially change a maintained dependency on a programming language, runtime, application framework, database technology, deployment platform, external service or similarly consequential component. It applies particularly to the first executable implementation in a repository and to prototypes intended to be merged, deployed or maintained.

An incidental implementation detail within an authorised stack does not require a separate decision merely because alternatives exist.

### Exceptions

Design authority may authorise a time-bounded exploratory spike before selecting a technology. The spike must be identified as disposable, state what it is intended to learn and must not silently become the maintained implementation, merge baseline or production dependency.

Where an external constraint leaves no genuine technology choice, record the constraint and its authoritative source rather than manufacturing an approval question. Emergency departures follow GOV-001 and do not create an enduring default without subsequent review.

### Required evidence

The authoritative specification, adopted default or design-authority decision; the scope of the choice; material rationale and consequences; and any reassessment trigger required by GOV-002.

### Checks

Automation may detect the introduction of new language, runtime, framework, database, service or deployment manifests and require a reference to the applicable authority. Because repository artefacts do not reliably reveal whether a choice is consequential or already imposed, ambiguous cases require review rather than automatic rejection.

### Basis

Implements [**Bounded Autonomy**](COMMANDMENTS.md#1-bounded-autonomy), [**Pay for a Lesson Once**](COMMANDMENTS.md#5-pay-for-a-lesson-once) and [**Build Quality In**](COMMANDMENTS.md#6-build-quality-in). The [first Eceni Harness slice](https://github.com/dazzknowles/eceni-harness/commit/3e9ea51) demonstrated the gap by establishing Python as a maintained runtime without a Harness technology baseline or an explicit design-authority decision. The implementation may be useful, but suitability after the choice is not authority to make it.

## QUA-003 — Source Is Human-Usable and Intent Is Discoverable

**Introduced in Governance baseline:** 1.3.0

> Maintained source must support efficient, safe work by a competent human using the technology's standard tooling. Its contracts must be discoverable, and material non-obvious intent and constraints must be preserved in the most appropriate durable form.

Use names, types, interfaces and structure to communicate ordinary intent directly. Preserve additional explanation where a competent maintainer could not otherwise understand, change, verify or operate the work safely. The appropriate authoritative form may be:

- idiomatic contract documentation exposed through normal tooling;
- a focused source or configuration comment;
- an accepted specification or requirement;
- a decision record for a cross-cutting choice or rejected alternative;
- a meaningfully named and traceable test;
- a runbook or another versioned operational artefact.

Do not duplicate the same explanation mechanically across several places. Retain one authoritative home and stable references where other artefacts depend on it. Commit history, transient chat and private recollection are not sufficient homes for intent that remains necessary to maintain the current system.

Contract documentation and comments must explain useful purpose, behaviour, constraints, consequences or reasoning. They must not merely restate a declaration or narrate obvious syntax. Particularly complex implementation may need a concise explanation of what it does as well as why it exists.

### Applicability

Eceni-authored and Eceni-maintained source code, database definitions, configuration, infrastructure definitions, scripts, tests and code-facing contracts.

New source, newly exposed contracts and materially changed areas must comply. Untouched inherited source may remain outside the assessed scope, but the project must not represent that unassessed source as compliant. Where Eceni assumes maintenance responsibility for generated, vendored or inherited work, it must identify the authoritative source and the boundary of its responsibility.

Generated or externally controlled source need not be rewritten when its origin is identifiable, its authoritative input or generator remains maintainable and its contracts remain discoverable through an appropriate mechanism.

### Exceptions

A bounded exception is permitted where an externally controlled format, framework or tool makes the ordinary mechanism unavailable or would produce a materially worse result. Record the exact scope, constraint, alternative means of discoverability and maintenance consequence under GOV-001.

Urgent diagnosis, containment or restoration work may defer missing documentation only where documenting first would materially worsen the immediate outcome. The obligation remains owned and trackable, is not Pass under EVI-001, and must be completed when the change is stable before the work is accepted as ordinarily complete.

### Required evidence

The exact source and applicable guide revisions; compiler, analyser or structural results where available; the authoritative intent artefact or self-explanatory contract; and proportionate review of whether a future competent maintainer can find and use the necessary information without private knowledge or mandatory access to an AI system.

### Checks

Automation may verify required documentation presence, valid references, identifier form, generated-source classification and other objective guide rules. It cannot determine whether names, comments or documentation communicate sufficient and accurate intent; that remains a review judgement. Comment counts and documentation word counts are not evidence of compliance.

### Basis

Implements [**Pay for a Lesson Once**](COMMANDMENTS.md#5-pay-for-a-lesson-once) and [**Build Quality In**](COMMANDMENTS.md#6-build-quality-in). It consolidates the useful outcomes identified by Rio's draft [Human-Usable Source](https://github.com/riosystems/rioit-governance/wiki/RIO-LAW-ENG-003-Human-Usable-Source) and [Discoverable Design Intent](https://github.com/riosystems/rioit-governance/wiki/RIO-LAW-ENG-002-Discoverable-Design-Intent) work without importing Rio's governance structure or treating its drafts as Eceni authority.
