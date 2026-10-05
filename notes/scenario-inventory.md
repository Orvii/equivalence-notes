# The scenario inventory is the spec

**Claim.** For equivalence testing, the scenario list *is* the specification. Write it before the transformation's test harness, derive it from the input grammar and the failure modes you fear, and keep it as a runnable artifact — not as test-function names scattered in a file.

**Why.** "We tested the optimizer" carries zero information without the list. The list is also the only thing that lets a stranger audit coverage: happy paths are easy to enumerate; the inventory's value is the columns nobody volunteers — empty input, maximal input, malformed input, unicode, concurrency, offline, permission-denied.

**Failure example.** A dead-code-elimination pass tested only on well-formed modules will pass while deleting an export that a malformed-but-accepted module re-exports; the bug lives exactly in the column the inventory lacked.

**Construction rule.** Derive rows from three sources, in order: (1) the input grammar (every production gets a case), (2) the transformation's own decision points (every branch that can drop or rewrite code gets a case), (3) historical bugs (every past failure becomes a permanent row). Source 3 is why inventories only grow.

**Counter-note.** Inventories rot into ritual when rows stop mapping to decisions. Prune a row only when you can name the decision it no longer touches — and record the pruning in the changelog, because a deleted row is a removed claim.
