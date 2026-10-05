# Environment equivalence is a precondition, not a courtesy

**Claim.** A differential equivalence result is only as strong as the identity of the two environments. Locale, timezone, filesystem case-sensitivity, line endings, dependency versions, and env vars are inputs to most real programs; if the original and transformed runs differ in any of them, the oracle compares two different programs and every verdict — pass or fail — is about the pair, not the transformation.

**Why.** These variables are invisible in source and loud in behavior: date formatting under a different locale, path joins under different separators, sort order under a different collation, float parsing under a different libc. Transformation bugs and environment differences produce identical symptoms, and the differential design cannot tell them apart.

**Failure example.** A pass renames a temp-file creation to use the OS temp dir. On the CI image (case-insensitive FS, `/tmp`) original and transformed agree; on a developer's case-sensitive volume with `TMPDIR` pointing elsewhere, the transformed run collides with an existing directory. The equivalence suite passed in the only environment it ran in.

**Method.** Freeze the environment as code: container image digest (or OS + package versions), locale/timezone set explicitly, dependency lockfile identical on both sides, env vars whitelisted and injected. Run both sides of every differential pair in the *same* frozen environment, sequentially or in identical twins. Record the image digest in the result row — environment identity is metadata of the verdict.

**Counter-note.** If the transformation's contract *includes* environment adaptation (a portability pass, a cross-platform shim), then environment variation is the scenario axis, not a frozen precondition: vary it deliberately per the scenario inventory and compare within each environment cell. Freezing everything there would test nothing.
