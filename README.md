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
| [minimize-the-specimen](notes/minimize-the-specimen.md) | fixing the 400-line failure instead of the 6-line cause |
| [nondeterminism-is-input](notes/nondeterminism-is-input.md) | phantom failures and silent passes from unseeded randomness |
| [golden-files-rot](notes/golden-files-rot.md) | the bulk snapshot update that approves everything |
| [stream-equivalence](notes/stream-equivalence.md) | chunk-exact oracles failing on identical behavior |
| [concurrent-equivalence](notes/concurrent-equivalence.md) | demanding sequential order from a parallelization |
| [property-tests-are-half-an-oracle](notes/property-tests-are-half-an-oracle.md) | invariants passing while the function changed |
| [environment-is-part-of-the-program](notes/environment-is-part-of-the-program.md) | a differential pair that passed because both sides ran in the same wrong environment |
| [the-power-bound-is-the-result](notes/the-power-bound-is-the-result.md) | a "no difference" reported without the effect size the study could have detected |

## House rules

- An equivalence claim names its **observability boundary** first: outputs, exit codes, throw paths, observable ordering, timings excluded or included. Unnamed boundaries are where "equivalent" goes to die.
- The scenario inventory is an artifact, not a vibe: a list a stranger can run, with the empty/long/malformed cases present by construction.
- A failing equivalence test is a **specimen**: minimize it before fixing anything. The minimized counterexample is the deliverable; the fix is the cleanup.

---

Orvii — Open, Research, Vision, Innovation & Ideas. Born as the public half of a private optimizer's test gate; the gate stays private, the method does not.

---

Part of the Orvii research set: [harness-atlas](https://github.com/Orvii/harness-atlas) · [convention-map](https://github.com/Orvii/convention-map) · [bench-notes](https://github.com/Orvii/bench-notes) · [provider-reliability](https://github.com/Orvii/provider-reliability) · [context-file-evidence](https://github.com/Orvii/context-file-evidence) · [retractions](https://github.com/Orvii/retractions) · [svg-instruments](https://github.com/Orvii/svg-instruments).
