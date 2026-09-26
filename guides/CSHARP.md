# C# Implementation Guide

**Guide version:** 1.1.0

**Introduced in Governance baseline:** 1.1.0

**Revised in Governance baseline:** 1.3.0

**Governing Laws:** [QUA-001](../LAWS.md#qua-001--follow-the-applicable-implementation-guide) and [QUA-003](../LAWS.md#qua-003--source-is-human-usable-and-intent-is-discoverable)

## Scope

This guide applies to hand-authored and Eceni-maintained C# source and tests. New files comply completely. New and materially changed declarations in existing files comply from the project's adopted source baseline; untouched inherited source is not thereby represented as compliant.

Generated, vendored and externally imposed source is outside ordinary enforcement when its origin is identifiable and it is not hand-maintained. Its generator, templates, maintained inputs and Eceni-authored partial files remain governed.

## Types are explicit

Declare the type of every local variable explicitly. Do not use `var` where C# provides a viable explicit type.

Explicit types make data shape and numeric or nullable semantics visible at the point of use and reduce the work required to understand code during review.

Target-typed construction is compliant because the declared type remains visible:

```csharp
Product product = new();
List<Product> products = [];
```

Use `var` only where the language requires type inference, such as for an anonymous type. Intentional dynamic binding is declared as `dynamic`; `var` is not a synonym for `dynamic`. A repeated need for another permitted case should become an explicit guide rule rather than an informal local convention.

## Naming

- Use `PascalCase` for namespaces, types, methods, properties, events and public constants.
- Prefix interfaces with `I`.
- Use `camelCase` for parameters and local variables.
- Use `_camelCase` for private instance fields.
- Suffix asynchronous methods with `Async`.
- Choose names that describe domain meaning rather than implementation mechanics.
- Avoid abbreviations unless they are established domain or technical terminology.
- Preserve the conventional written form of established acronyms within identifiers, including `ID`, `UTC`, `HTTP`, `PV` and `VAT`.
- Combine acronym forms with normal identifier casing: `ProductID`, `productID`, `_productID` and `VATRate`, not `ProductId`, `productId`, `_productId` or `VatRate`.
- Framework-owned, generated and externally imposed names remain unchanged where renaming would break or obscure their governing contract.
- Include units or time basis where omission could mislead, such as `timeoutSeconds`, `sizeBytes` or `createdAtUTC`.

## XML documentation

Public and protected types and members are contracts and must use C# XML documentation. Internal members that form contracts across projects or significant component boundaries follow the same rule.

Inherited or obvious standard contracts, such as an ordinary override, may use `<inheritdoc/>` or an equivalent tool-supported reference rather than duplicate the same explanation.

Documentation explains the contract information a consumer or maintainer needs. Explain purpose, expectations, units, nullability, results, material side effects, failure behaviour, security boundaries and complex or conditional parameters where they are not already unambiguous.

Use `<param>`, `<typeparam>`, `<returns>`, `<exception>`, `<remarks>` and `<example>` when they communicate useful contract information. Do not add boilerplate that merely repeats a name, type or declaration. Keep references and claims current when behaviour changes.

## Source comments and design intent

Meaningful names, types and structure are the first means of making implementation understandable. Add a focused source comment where a competent maintainer would otherwise have to infer a non-obvious invariant, constraint, workaround, trade-off, evidence limitation, compatibility obligation, failure behaviour or consequential design decision.

Comments normally explain why. Particularly complex code may also need a concise explanation of what it does. Put cross-cutting reasoning in its appropriate authoritative artefact and reference it from the affected source rather than copying a long decision history into a comment.

## Readability and structure

- State access modifiers explicitly.
- Prefer small, cohesive types and methods with one clear responsibility.
- Prefer straightforward control flow over compressed or clever expressions when the latter make intent harder to verify.
- Preserve established formatting within a project and use automated formatting where available.
- Treat compiler and analyser warnings as work to resolve. A suppression must be as narrow as possible and state why the warning does not apply.

## Checks

Uses of `var`, naming and acronym rules, formatting, unjustified suppressions, documentation presence and broken XML references are suitable for compiler or analyser enforcement. Existing findings may be baselined so that enforcement prevents new debt without demanding unrelated bulk cleanup.

Documentation usefulness, naming clarity and whether the right intent is discoverable remain review judgements. Comment or documentation volume is not a quality measure.
