# Changelog

## [2026-10-06] - note 13: byte-identity is a perfect oracle

### Added
- `notes/byte-identity-is-a-perfect-oracle.md` — where the artifact is regenerable text, byte-for-byte diffing replaces scenario inventories: total, deterministic, self-diagnosing. Conditions for honesty (deterministic generator, committed inputs, independently verified identity before the gate goes live) and the cases where brittleness is the wrong tool.
- README table row.

## [2026-10-05] - Note 12: the power bound is the result

### Added
- `notes/the-power-bound-is-the-result.md` — a null without its minimum detectable effect is not a finding; report point estimate + bound + the n that would detect the effect you care about.

### Modified
- `README.md` note index (12 rows), `hero.svg` count line.

## [2026-10-05] - Note 11: environment is part of the program

### Added
- `notes/environment-is-part-of-the-program.md` — locale, timezone, case-sensitivity, line endings and env vars are inputs; a differential pair that differs in any of them compares two programs, not one transformation.

### Modified
- `README.md` note index (11 rows).

## [2026-10-05] - Initial release: ten notes

### Added
- Notes: scenario-inventory, differential-oracles, observability-boundary, combinatorial-explosion, minimize-the-specimen, nondeterminism-is-input, golden-files-rot, stream-equivalence, concurrent-equivalence, property-tests-are-half-an-oracle
- House rules: observability boundary first, inventory as artifact, specimen as deliverable
- `hero.svg` (two traces, compared observables), `CONTRIBUTING.md`, `LICENSE` (MIT)
