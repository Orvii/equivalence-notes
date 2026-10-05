# Golden files are equivalence oracles with a maintenance tax

**Claim.** Golden-file testing (snapshot the original program's output, compare the transformed program against it) is the most common equivalence oracle and the easiest to abuse: every intentional behavior change turns every affected golden file into a failure that a tired reviewer approves with "update snapshots". The tax is real; pay it consciously or the oracle silently stops meaning anything.

**Why.** Golden files freeze *behavior as of the day they were recorded*, including bugs and incidental formatting. They answer "did anything change?" — not "is it right?". Over time the approval gesture (`--update-goldens`) becomes reflexive, and the suite's verdict degrades from "equivalent" to "whoever updated last thought this looked fine".

**Failure example.** A formatter change reflows whitespace; 400 golden files differ. Reviewers cannot read 400 diffs, approve the bulk update, and in the same wave a genuine one-line semantic change rides through unread. The oracle did its job; the process overruled it.

**Method.**
- Keep goldens **minimal and generated**: derive them from the scenario inventory, one per scenario, not one per incidental output surface.
- On bulk update, require the update commit to contain **only** golden changes plus a linked explanation — mixing code and goldens in one commit is how semantic changes hide.
- Diff-review the goldens themselves periodically: a golden file nobody can explain is a liability, not an asset.
- Prefer structured goldens (parsed values) over byte-exact text where the boundary allows; byte-exactness couples the oracle to formatting decisions outside the transformation's contract (see [observability-boundary](observability-boundary.md)).

**Counter-note.** For outputs with no stable structure (rendered UI, prose, error text under active redesign), byte-exact goldens are the only practical oracle — accept the tax, but shrink the surface: golden the smallest fragment that captures the contract, not the whole document.
