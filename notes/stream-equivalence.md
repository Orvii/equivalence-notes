# Equivalence for streaming outputs: compare the contract, not the chunking

**Claim.** When the program under transformation produces a stream (tokens, events, SSE frames), byte-for-byte stream comparison is the wrong oracle: chunk boundaries are implementation detail. The right observables are the **reassembled output** plus, where the contract includes it, the **event sequence semantics** — and the boundary must state which of the two the transformation is allowed to change.

**Why.** Two runs of the *same* untransformed streaming program can chunk differently under different load or buffer sizes. A chunk-exact oracle therefore fails on identical behavior (phantom), while a reassemble-only oracle misses a transformation that reorders or drops *events* whose order is part of the contract (silent pass). The boundary decides; the oracle implements the decision.

**The two contracts.**
- **Content contract:** the concatenation of all chunks must match (modulo declared normalization). Chunking free. Use for text/token streams where only the final text matters.
- **Event contract:** the sequence of semantic events (tool-call start/args/end, status transitions) must match as a sequence; payloads compared per event. Use when consumers parse the stream incrementally — which is what every agent loop does.

**Method.** Reassemble both sides; compare under the content contract. Then parse both sides into event sequences; compare under the event contract with per-event payload equality. Report which contract failed — a content-only failure and an event-order failure are different bugs with different fixes.

**Failure example.** An optimizer inlines a helper that yielded two stream events into one yield. Final text identical (content contract passes); an incremental consumer that commits state at each event boundary sees one commit instead of two and corrupts its state (event contract fails). Chunk-exact comparison would have flagged both runs randomly and taught the team to ignore the suite.

**Counter-note.** If the transformation's *purpose* is changing stream shape (batching, compression, replay determinism), the event contract is the product spec — invert: compare chunk-level properties (batch sizes, replay determinism) as first-class observables, and demote content equality to a sanity check.
