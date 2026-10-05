# Property tests are half an oracle — pair them with a differential half

**Claim.** Property-based tests ("the output is sorted", "the sum is conserved") check *invariants*, not *identity*: a transformation can satisfy every property while computing a different function. For equivalence claims, properties are necessary and insufficient; the missing half is differential comparison against the original (see [differential-oracles](differential-oracles.md)). Use both, and know which failure each can catch.

**Why.** Properties are projections: they collapse the output space onto a few coordinates. Two programs agreeing on all projected coordinates can differ everywhere else. Conversely, differential comparison catches any observable difference but cannot tell you whether the difference *matters* — properties supply the meaning.

**Failure example.** A constant-folding pass must preserve "program output". Property suite checks: parses, type-checks, terminates, prints the same stdout on the scenario set. A bug makes the pass fold `x - x` to `0` for floats including NaN (where `NaN - NaN` is NaN, not 0). Stdout-equal properties pass on every scenario that never produces NaN; the differential oracle over a scenario inventory containing NaN catches it on the first run.

**Division of labor.**
- Differential: "nothing observable changed" — catches semantic drift, including cases no one thought to write a property for.
- Properties: "the things we care about hold" — catches cases where the differential oracle's boundary deliberately excludes an observable (timings, memory) that a property still governs.
- Known-answer vectors: the third leg for edges where both above share blind spots (shared bugs, excluded observables).

**Counter-note.** When the original program is unavailable (spec-from-scratch implementations, new formats), properties plus known-answer vectors *are* the whole oracle — accept that the equivalence claim then means "conforms to spec", not "preserves behavior", and say which one you proved.
