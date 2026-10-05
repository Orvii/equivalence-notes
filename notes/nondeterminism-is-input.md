# Treat nondeterminism as an input, not as noise

**Claim.** For equivalence testing of programs with nondeterministic behavior (time, randomness, hash iteration order, concurrency scheduling), the correct move is to **inject and seed** every nondeterministic source on both sides of the comparison. Untamed nondeterminism does not make equivalence tests flaky; it makes them meaningless in both directions — phantom failures and silent passes.

**Why.** A differential oracle compares observables. If run A draws `Math.random()` freely and run B draws differently, the outputs differ with no transformation bug anywhere (phantom failure). Worse inverse: a transformation that *introduces* a randomness-dependent branch can pass a comparison that happened to draw lucky (silent pass). Seeding converts both failure modes into reproducible specimens.

**Method.** Enumerate the sources: clocks (inject a fake clock), RNG (seed at process start, same seed both sides), hash order (fixed-seed hash or sorted iteration), scheduler (single-threaded execution, or a deterministic scheduler where available). Then run the comparison across **multiple seeds**, because one seed proves equivalence on one timeline; a seed sweep probes the behavior space.

**Failure example.** A pass reorders two independent async side effects. Under free scheduling the differential test passes or fails at random depending on interleaving; under a deterministic scheduler with an event-order observable, the reordering becomes a stable, minimizable specimen.

**Counter-note.** Some transformations legitimately change scheduling (parallelization passes). There, event-order equivalence is the wrong observable — compare the *set* of events plus per-event causality, and state that relaxation explicitly in the observability boundary (see [observability-boundary](observability-boundary.md)). Seeding everything and then ignoring the boundary is rigor pointed at the wrong target.
