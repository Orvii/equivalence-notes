# The minimized counterexample is the deliverable

**Claim.** When an equivalence test fails, the first product is not a fix — it is a **minimized specimen**: the smallest input that still shows the inequivalence. Minimize before diagnosing; commit the specimen with the bug report or the fix; treat an unminimized failure as an unfinished investigation.

**Why.** A 400-line module that misbehaves after transformation contains, usually, a 6-line core that misbehaves for one reason. Debugging the 400-line version means re-deriving that reason through noise, and the fix you write will be shaped by the noise. The minimized case also *is* the regression test — it goes straight into the scenario inventory (see [scenario-inventory](scenario-inventory.md), source 3).

**Method.** Delta-debugging by hand or tool: halve the input, keep whichever half still fails, repeat; then shrink tokens within the surviving half (drop statements, shrink literals, rename to single identifiers). Stop when removing anything makes the test pass. Two invariants make this safe: the failure must reproduce deterministically (seed everything), and the comparison must be the same observables as the original test (see [observability-boundary](observability-boundary.md)).

**Failure example.** An optimizer pass reordered two observable side effects; the original failing module was 300 lines. The minimized specimen: two function calls whose order the pass swapped because it treated a pure-looking helper as side-effect-free. The fix was one purity-check line; the specimen is four.

**Counter-note.** Minimization can over-fit: the smallest failing case may exercise a *different* bug than the one users hit (same symptom, other cause). Keep the original failing input alongside the specimen; if the fix passes the specimen but not the original, you minimized yourself into a neighboring bug.
