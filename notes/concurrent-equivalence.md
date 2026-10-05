# Concurrent programs need weaker equivalence — chosen on purpose

**Claim.** For concurrent or parallelized code, sequential-equivalence oracles are unworkable: interleavings differ run to run even without any transformation. The workable move is to pick a **weaker, named consistency condition** as the equivalence relation — quiescent consistency, linearizability of published operations, or final-state equality plus invariant checks — and state which one, because each admits different implementations and catches different bugs.

**Why.** A parallelizing transformation legitimately reorders operations that commute. An oracle demanding identical event order rejects every correct parallelization (phantom). An oracle demanding only final-state equality accepts a parallelization that loses updates (silent pass). The named condition in between is the contract: "after quiescence, the observable state equals the sequential result" admits reordering while catching lost work.

**The ladder, strongest to weakest.**
1. **Sequential equivalence** — identical event order; only for single-threaded code.
2. **Linearizability** — each operation appears atomic at some point between invoke and response; right for published concurrent APIs.
3. **Quiescent consistency** — results match sequential after quiet periods; right for bulk/parallel kernels where mid-flight order is irrelevant.
4. **Final-state + invariants** — equality at the end plus structural invariants (sums conserved, no duplicates); the floor, and weaker than most teams think.

**Failure example.** A pass parallelizes a map over independent items. Final-state equality passes; but the pass also reorders *logged* side events that a downstream consumer treats as a commit log. Under linearizability-of-log the transformation fails; under final-state it passes. The boundary — is the log part of the contract? — decides, and only naming it makes the test meaningful (see [observability-boundary](observability-boundary.md)).

**Counter-note.** Weaker conditions need more runs to catch violations: a lost update may need thousands of schedules to surface. Pair the named condition with stress scheduling (many seeds, thread counts, and a deterministic scheduler where available — see [nondeterminism-is-input](nondeterminism-is-input.md)), and publish the run count alongside the verdict.
