# Adding a note

A note is one problem, attacked in a fixed shape. Notes that break the shape get sent back.

## Template

```markdown
# <imperative title naming the problem>

**Claim.** One sentence: what to do.

**Why.** The mechanism — why the failure happens, not that it happens.

**Failure example.** A concrete case: numbers, inputs, observed wrong outcome. Real artifacts linked where public.

**Rule / method.** The actionable procedure, with its parts named.

**Counter-note.** The condition under which this advice inverts or stops applying. Every note has one; a note without a counter-note is a slogan.
```

## Rules

- One failure mode per note. Two problems = two notes.
- The failure example must be reproducible in the reader's head from the text alone; link the public artifact when one exists.
- No note may depend on private project internals. If the lesson came from a private gate, restate it until it stands alone (this repo exists precisely as the public half of such a gate).
- Cross-link siblings (`scenario-inventory`, `differential-oracles`, `observability-boundary`, `combinatorial-explosion`, `minimize-the-specimen`) where the argument touches them.
