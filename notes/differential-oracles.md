# When you cannot write the expected output: differential oracles

**Claim.** Most transformations have no hand-writable expected output. The workable oracle is **differential**: run the original and the transformed program on the same inputs and compare observables. The original program is your test oracle — imperfect, but available and exact.

**Why.** Writing expected outputs for a compiler pass means re-implementing the semantics you are testing. Differential testing outsources correctness to "the thing everyone already trusts in production", and converts semantic questions into comparison questions.

**Failure example (shared failure).** If original and transformed share a bug, differential testing is blind to it — both sides agree. This is not a flaw to fix but a boundary to state: differential oracles prove *preservation*, not *correctness*. Pair them with a few absolute oracles (property tests, known-answer vectors) at the edges where shared failure is likely.

**Practical notes.**
- Compare **structured observables**, not stdout strings: exit code, returned value, thrown error identity/order, and for async code, the interleaving of observable events.
- Nondeterminism (time, randomness, hash order) must be injected and seeded on both sides, or the oracle reports phantom inequivalence.
- When the transformation changes performance-relevant behavior intentionally, exclude timings from the comparison explicitly — silently including them turns an optimizer into a failing test suite.

**Counter-note.** Differential oracles degrade when the original is slow: running both sides on a 10⁶-case inventory doubles an already expensive suite. Sample the inventory for the differential pass and run the full inventory only on release candidates — and say which you ran.
