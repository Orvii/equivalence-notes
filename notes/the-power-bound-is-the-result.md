# A null without its power bound is not a finding

**Claim.** "We found no difference" is not a result until it carries the size of difference the experiment could have detected. The bound — the minimum detectable effect at the study's n, or the equivalence interval a test actually rules out — *is* the finding. A null published without it cannot be distinguished from an experiment that was never capable of seeing anything.

**Why.** Absence of evidence is the most over-claimed sentence in empirical work. Two studies can both report "no effect" while one rules out everything above 2 percentage points and the other could not have seen a 30-point effect. Cited side by side they look like replication; they are not even the same claim. The reader who wants to know "does X matter" gets nothing from a p-value alone when the p-value is large.

**Failure example.** An ablation reports that adding a configuration file changes pass rate by +2.3pp, p=0.66, and the coverage writes "the file makes no difference." The study's own power analysis says a 10pp effect was undetectable at its n and that even a 30pp effect would be caught barely half the time. The honest sentence is "any effect is smaller than ~10–15pp, and this experiment could not have seen smaller" — a materially different claim, and a useful one: it tells the next study how big to run.

**Method.** Report three numbers with every null: the observed point estimate, the equivalence or confidence bound the test supports, and the minimum detectable effect at the achieved sample size (with the n that *would* detect the effect size you care about). Where the bound is wide, say the study is power-limited in the abstract, not the limitations section — the abstract is where the headline gets written.

**Counter-note.** A bound is only as good as its variance model. Equivalence tests on clustered data (tasks, repos, users) must cluster the resampling; a per-observation bound on task-clustered runs overstates precision. And a tight bound on a narrow corpus ("no effect on these three Python repos") does not transfer — the bound travels with the population it was computed on.
