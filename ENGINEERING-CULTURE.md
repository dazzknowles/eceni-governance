# Engineering culture

This document describes how Eceni's humans and AI collaborators ("twins") work together. It is operational guidance, not a set of corporate values.

The working pattern is:

> Challenge freely. Bring reasons and evidence. Let the accountable authority decide. Record the rationale. Execute the decision.

## Challenge is expected

Challenge decisions, assumptions and proposed designs when there is a meaningful reason to do so. Authorship, seniority and prior approval do not make a decision immune from challenge.

Challenge the decision, not the person. State the concern plainly and respectfully, explain its consequence and offer a better-aligned alternative where possible. Disagreement is useful; personal criticism is not.

## Bring reasons, not preferences

A challenge should identify evidence, a requirement, a consequence or a trade-off. "I prefer this", "this is more idiomatic" or an appeal to a general maxim is not enough on its own.

Good reasons connect the choice to something that matters: correctness, an accepted requirement, operational risk, maintainability, cost, security, or a known next stage of the system. The strength of the evidence should match the consequence of the decision.

## Keep authority accountable

Twins may propose, challenge, implement and review. They should expose consequential ambiguity instead of silently resolving product or architectural questions that belong to the relevant human or designated design authority.

Agreement between several twins is evidence, not authority. Consensus does not make an AI collaborator accountable for a design decision, and it must not allow twins to become the effective design authority by accumulation of unreviewed choices.

## Decide, then execute

Once the accountable authority has made a decision, it is authoritative. Implement and review against it rather than repeatedly relitigating it or quietly working around it.

Reopen a decision when material new evidence appears, a significant consequence was missed, or the governing requirements change. Make the new challenge explicit. Changing a decision in response to better evidence is a successful correction, not a failure or loss of face.

## Optimise for the known system

Do not optimise only for the current ticket when a locally convenient choice would make a known requirement or planned stage materially harder. Inexpensive seams are justified where the future need is understood.

Do not build for imaginary futures. Hypothetical products, vague extensibility and speculative flexibility do not justify complexity. Prefer the smallest design that serves the current work and the system we actually know we are building.

## Prefer boring engineering

Choose established, understandable and maintainable approaches unless a less conventional solution provides a concrete, material benefit. Cleverness carries a cost in explanation, review, operation and future change; it must earn that cost.

## Leave evidence behind

Preserve consequential decisions and their rationale in the appropriate durable place: the governing document, design record, issue, review or code where future contributors will look for it. Record enough context to explain what was decided and why, including rejected alternatives when that knowledge is likely to prevent the same debate or mistake.

The record is not bureaucracy for its own sake. Its purpose is to let the next human or twin act consistently without having to reconstruct the decision from conversation or guesswork.
