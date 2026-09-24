# C# Implementation Guide

**Guide version:** 1.0.0

**Introduced in Governance baseline:** 1.1.0

**Governing Law:** [QUA-001](../LAWS.md#qua-001--follow-the-applicable-implementation-guide)

## Scope

This guide applies to hand-authored C# source and tests. Generated code and externally imposed source formats are outside its scope when their origin is identifiable.

## Types are explicit

Declare the type of every local variable explicitly. Do not use `var`.

Explicit types make data shape and numeric or nullable semantics visible at the point of use and reduce the work required to understand code during review.

## Naming

- Use `PascalCase` for namespaces, types, methods, properties, events and public constants.
- Prefix interfaces with `I`.
- Use `camelCase` for parameters and local variables.
- Use `_camelCase` for private instance fields.
- Suffix asynchronous methods with `Async`.
- Choose names that describe domain meaning rather than implementation mechanics.
- Avoid abbreviations unless they are established domain or technical terminology.
- Use one spelling consistently for an established abbreviation within a public model; do not create parallel forms such as `Id` and `ID` for the same concept without a governed compatibility reason.
- Include units or time basis where omission could mislead, such as `timeoutSeconds`, `sizeBytes` or `createdAtUtc`.

## XML documentation

Use XML documentation for:

- public types and contracts whose purpose, constraints or consequences are not obvious from their signature;
- public members whose behaviour, units, nullability, side effects, failure modes or security boundary require explanation;
- interfaces and extension points consumed across component boundaries;
- implementation decisions where the reason is important to safe maintenance.

Document internal or private members when they carry a non-obvious invariant, workaround, evidence limitation or consequential design decision.

Documentation explains intent and constraints; it must not merely restate syntax. Add `<param>`, `<returns>`, `<exception>`, `<remarks>` and `<example>` only when they convey useful information. Keep references and claims current when behaviour changes.

## Readability and structure

- State access modifiers explicitly.
- Prefer small, cohesive types and methods with one clear responsibility.
- Prefer straightforward control flow over compressed or clever expressions when the latter make intent harder to verify.
- Preserve established formatting within a project and use automated formatting where available.
- Treat compiler and analyser warnings as work to resolve. A suppression must be as narrow as possible and state why the warning does not apply.

## Checks

The absence of `var`, naming rules, formatting and unjustified suppressions are suitable for automated analysis. Documentation usefulness and clarity remain review judgements.
