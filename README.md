<picture>
  <source media="(prefers-color-scheme: dark)" srcset="hero.svg">
  <img alt="equivalence-notes — proving a transformation changed nothing observable" src="hero.svg">
</picture>

# equivalence-notes

Methodology notes for **behavioral-equivalence testing**: proving that a program transformation — an optimizer pass, a refactor, a transpiler, a minifier — changed nothing observable.

The question every transformation project eventually faces: *fast is easy to measure; same is hard.* These notes are the hard half.

## The notes

| Note | The problem it attacks |
|---|---|
| [scenario-inventory](notes/scenario-inventory.md) | "we tested it" with no list of what *it* includes |
| [differential-oracles](notes/differential-oracles.md) | needing an expected output you cannot write by hand |
| [observability-boundary](notes/observability-boundary.md) | deciding what counts as "the same behavior" before the argument starts |
| [combinatorial-explosion](notes/combinatorial-explosion.md) | the pairwise matrix that quietly became 10⁶ cells |

## House rules

- An equivalence claim names its **observability boundary** first: outputs, exit codes, throw paths, observable ordering, timings excluded or included. Unnamed boundaries are where "equivalent" goes to die.
- The scenario inventory is an artifact, not a vibe: a list a stranger can run, with the empty/long/malformed cases present by construction.
- A failing equivalence test is a **specimen**: minimize it before fixing anything. The minimized counterexample is the deliverable; the fix is the cleanup.

---

Orvii — Open, Research, Vision, Innovation & Ideas. Born as the public half of a private optimizer's test gate; the gate stays private, the method does not.

---

Part of the Orvii research set: [bench-notes](https://github.com/Orvii/bench-notes) (measurement methodology) · [retractions](https://github.com/Orvii/retractions) (corrections ledger) · [harness-atlas](https://github.com/Orvii/harness-atlas) (capability evidence).
