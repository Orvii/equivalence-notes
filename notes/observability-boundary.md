# Name the observability boundary before the argument

**Claim.** "Behaviorally equivalent" is undefined until you list what an observer may see. Write the boundary explicitly — outputs, exit codes, error types and throw order, observable event ordering, and (decided, not defaulted) timings and memory — before writing a single equivalence test. Most equivalence disputes are boundary disputes in disguise.

**Why.** Two engineers can both be right: one claims the transformation is equivalent because results match; the other claims inequivalence because stack traces differ. Neither stated whether error identity is inside the boundary. The argument was never about the code.

**Failure example.** A minifier that renames local variables preserves outputs but changes `error.name`/stack frames and debugger-visible identifiers. Under a boundary that includes stack text, it is inequivalent; under one that excludes it, equivalent. Shipping either claim without the boundary invites a production surprise when someone's error-reporting pipeline diffs stack strings.

**Boundary checklist.** Return values · stdout/stderr bytes · exit code · thrown error type/message/order · observable side-effect order (file writes, network calls) · timing (in/out, say which) · memory (in/out) · identifier visibility (debugger, stack frames, reflection).

**Counter-note.** A boundary that includes everything makes equivalence untestable (timings always differ); one that excludes everything makes it meaningless. The craft is excluding exactly what the transformation is *allowed* to change — and documenting that permission, because it is a contract with every downstream consumer.
