# Eceni Commandments

**Introduced in Governance baseline:** 1.0.0

**Adopted:** 23 September 2026

**Scope:** All Eceni product and engineering work, whether performed by people, agents or automation

## Purpose and authority

The Eceni Commandments are concise, portfolio-level principles governing product and engineering judgement. They turn the essential boundaries of Eceni's broader [Engineering Culture](ENGINEERING-CULTURE.md) into binding obligations.

The layers have distinct purposes:

- **Culture** describes the broader aspirations and working behaviours Eceni wants to cultivate.
- **Commandments** establish binding boundaries for product and engineering judgement.
- **Laws** translate those boundaries into concrete rules, defaults and explicitly governed exceptions.
- **Checks** enforce Laws only where assessment can be objective, reliable and proportionate.

The Harness consumes the applicable Governance baseline and captures evidence of its application. It does not define, reinterpret, amend or waive Governance.

## Applying the Commandments

> Act within explicit authority and represent evidence faithfully. Satisfy applicable primary obligations and explicit constraints before optimising quality and value. When applicable obligations cannot coexist, return the conflict to Eceni's design authority.

Correctness, security and privacy are primary obligations. A project, work order, agent or automation may not trade them away for performance, economy, convenience or delivery speed.

Required user outcomes, service levels, recovery decisions, budgets and other accepted commitments are explicit constraints. Within those boundaries, improve total quality and value across usability, maintainability, observability, resilience, performance and economy. A quality attribute becomes a hard constraint when Governance or an approved specification requires it.

### Applicability is explicit

A Commandment may be genuinely inapplicable to particular work, but it must not be silently ignored. Non-applicability must be explicit, justified and recorded by the appropriate authority. It is not a device for escaping an inconvenient obligation.

### Commandments are not waivable by delivery

Applicable Commandments cannot be waived, reinterpreted or overridden through ordinary project, work-order or agent authority. If work cannot satisfy an applicable Commandment, it is blocked pending a decision by Eceni's design authority.

Eceni's design authority may amend the Commandments through an explicit, reasoned and versioned Governance decision. An amendment creates a new immutable Governance baseline; it does not rewrite the historical record.

### Projects retain their Governance lineage

Every project must identify its current Eceni Governance baseline and retain its Governance lineage. [GOV-003](LAWS.md#gov-003--projects-retain-their-governance-lineage) defines the concrete record required for each transition.

## 1. Bounded Autonomy

> **Make authority explicit. Within it, act autonomously; beyond it, return to accountable authority.**

Autonomy is the normal operating mode inside an accepted authority boundary. Uncertainty alone does not require interruption, but consequential ambiguity that would exceed the boundary does. Challenge supported by evidence is expected; after accountable authority decides, execute that decision unless material new evidence emerges.

This protects against both needless permission-seeking and the quiet accumulation of consequential decisions by people or agents that do not hold the relevant authority.

**Provenance:** [Engineering Culture](ENGINEERING-CULTURE.md); [authority envelopes and grants](https://github.com/dazzknowles/saas-product-lab/issues/15#issuecomment-5573769602); [bounded context](https://github.com/dazzknowles/saas-product-lab/issues/15#issuecomment-5573890948); [estimation and budget authority](https://github.com/dazzknowles/saas-product-lab/issues/15#issuecomment-5573967574). The Commandment consolidates those statements into an Eceni portfolio-level formulation.

## 2. Data Is Entrusted

> **Treat data as entrusted to us. Respect the people and things it represents. Design for security, privacy and deliberate recovery from the start.**

Data is not merely a technical asset. Its collection, use, access, retention, movement, recovery and deletion can affect people, organisations and the real-world things it describes. Those consequences must be considered as part of the design rather than added after implementation.

Recovery is a mandatory design decision, not an instruction to retain everything. Data may appropriately be transient, reproducible, expired or deliberately deleted. A decision that data or service state need not be recoverable must be explicit, justified and recorded.

**Provenance:** [Eceni security, privacy and recoverability invariants](https://github.com/dazzknowles/saas-product-lab/issues/5#issuecomment-5499990917); [Design for Failure](https://github.com/dazzknowles/saas-product-lab/issues/5#issuecomment-5576064462). The Commandment consolidates detailed historical defaults beneath one portfolio-level obligation.

## 3. Faithful Evidence

> **Represent evidence and uncertainty faithfully. Seek independent challenge in proportion to the consequences.**

Distinguish what is known, assumed, inferred, unknown and not checked. Do not report failure as success, absence of evidence as evidence of absence, or confidence as certainty.

Consequential claims should not depend solely on their author or implementer. Independence and depth of challenge should be proportionate to the possible consequence; routine work does not require ceremonial review.

**Provenance:** [Engineering Culture](ENGINEERING-CULTURE.md); [independent verification](https://github.com/dazzknowles/saas-product-lab/issues/5#issuecomment-5463878582); [digital four-eyes review](https://github.com/dazzknowles/saas-product-lab/issues/7#issuecomment-5463877655); [Governance conflict classification](https://github.com/dazzknowles/saas-product-lab/issues/15#issuecomment-5625204604). The wording consolidates evidence, uncertainty and independent challenge; it was not previously agreed in this exact form.

## 4. Value Over Waste

> **Use resources in proportion to value. Eliminate waste; never confuse activity with productivity.**

Resources include money, included capacity, compute, tokens and human time. Economy does not mean choosing the lowest immediate cost or compromising required quality, security or privacy. It means considering the whole lifecycle and spending deliberately where doing so creates value.

> We don't mind spending money. We abhor wasting it.

**Provenance:** [commercial and resource sanity](https://github.com/dazzknowles/saas-product-lab/issues/5#issuecomment-5500542836); [efficiency and waste](https://github.com/dazzknowles/saas-product-lab/issues/5#issuecomment-5501470328). Both were explicitly proposed as Eceni-level operating principles; this Commandment consolidates them.

## 5. Pay for a Lesson Once

> **Pay for a lesson once. Preserve the knowledge; reuse it until the evidence changes.**

Consequential decisions, their rationale and known-good patterns should be recorded where future work can find and assess them. Preserve the evidence, context, applicability and supersession history, not only the final conclusion.

The purpose is reusable knowledge, not documentation volume. Prior learning accelerates later products without becoming unquestionable precedent: reuse it while the context remains applicable and revisit it when contrary evidence appears.

**Provenance:** [preserve and reuse learning](https://github.com/dazzknowles/saas-product-lab/issues/5#issuecomment-5501354985); [the canonical company bible and knowledge lifecycle](https://github.com/dazzknowles/saas-product-lab/issues/5#issuecomment-5576128829); [Engineering Culture](ENGINEERING-CULTURE.md). The Commandment retains the historical formulation with minor editing.

## 6. Build Quality In

> **Build quality in. Solve real problems with systems that are correct, secure, usable, understandable, maintainable, observable, resilient and appropriately performant.**

Quality is designed into the whole user and operational outcome rather than inspected into a finished implementation. Prefer the smallest understandable design that serves the real problem and leaves sensible seams for known next stages. Assume components, dependencies, networks, processes and people will fail; make recovery safe and proportionate.

Performance is one measure of quality. Measure it by the useful outcome delivered, including end-to-end waiting time, interaction effort and avoidable cognitive load rather than only component benchmarks. At each decision point, put the necessary information, context and actions in front of the user; minimise avoidable steps, recall and context-switching.

Improve performance within correctness, security, privacy, maintainability and explicit commercial constraints. Do not buy speculative architecture for imaginary futures.

**Provenance:** [raw engineering and product principles](https://github.com/dazzknowles/saas-product-lab/issues/5); [pragmatic engineering](https://github.com/dazzknowles/saas-product-lab/issues/5#issuecomment-5532004721); [Design for Failure](https://github.com/dazzknowles/saas-product-lab/issues/5#issuecomment-5576064462); [Engineering Culture](ENGINEERING-CULTURE.md). This Commandment consolidates several historical quality themes. The original sequence “Correct. Secure. Maintainable. Performant. Observable. Economical.” remains provenance rather than a canonical ordering.

## Provenance and independent Eceni adoption

Some source discussions began as Rio or SaaS Product Lab working material. They are evidence of the founder's engineering reasoning, not inherited Rio governance. Eceni has assessed, consolidated and adopted the Commandments independently for its own product and engineering portfolio, consistent with the later [Eceni provenance correction](https://github.com/dazzknowles/saas-product-lab/issues/16).
