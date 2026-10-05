# Where equivalence testing explodes — and the cheapest sound approximation

**Claim.** Full pairwise coverage over (scenario × transformation-pass × input-shape × environment) grows multiplicatively and dies quietly: suites get sampled without anyone deciding what the sampling means. The workable move is to name the explosion, then choose an approximation with a stated soundness argument — not to let runtime choose for you.

**Why.** Four passes, 200 scenarios, 5 input shapes, 3 environments = 12 000 differential runs. Each run executes two programs. The suite crosses the hour mark and someone adds `--grep` — coverage becomes folklore.

**The approximations, cheapest first.**
1. **Pass isolation:** test each pass against the untransformed original (n passes × scenarios), not every pass *composition*. Catches per-pass bugs; misses interaction bugs.
2. **Composition chains:** add a small set of full-pipeline runs over the scenarios most likely to expose interactions (those touching shared state: symbol tables, caches).
3. **Pairwise over the pass set:** all 2-pass combinations instead of 2^n; sound for bugs that need exactly two passes to appear — which is where most interaction bugs live.
4. **Randomized composition (fuzz the pass order):** no coverage guarantee, but finds the 3-pass monster pairwise cannot; keep the seed and the minimized specimen when it does.

**Evidence in the wild.** Compiler test suites converge on exactly this shape: exhaustive per-pass, sampled composition, plus a fuzzer for the tail. The honest report states which layer caught what.

**Counter-note.** If the transformation is *shipped as the composition* (a single "optimize" button), pass-isolation results are evidence about components, not about the product. Then layer 2 or 4 is not optional — it is the only test of what users actually run.
