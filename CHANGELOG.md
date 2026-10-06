# Changelog

## [2026-10-06] - note 16: measure outflow, not inflow

### Added
- `notes/measure-outflow-not-inflow.md` — liveness and throughput are properties of the drain, not the queue: merged PRs, releases, completions over a window, plus the age of the oldest unprocessed item. Born from the dead-awesome-list retraction (retractions 008) and generalized to job queues and benchmark harnesses.
- README table row; hero.svg count fifteen → sixteen.

## [2026-10-05] - Note 15: where in the distribution

### Added
- `notes/where-in-the-distribution.md` — mean, median and tail can carry opposite signs for the same experiment; name the statistic that matches the decision and show the others.

### Modified
- `README.md` note index (15 rows), `hero.svg` count line.

## [2026-10-05] - Note 14: the benchmark code is the result

### Added
- `notes/the-benchmark-code-is-the-result.md` — an unauditable number is a vendor claim; the harness, input generator, environment block and raw rows ship in the same commit as the chart.

### Modified
- `README.md` note index (14 rows), `hero.svg` count line.

## [2026-10-05] - Initial release: thirteen notes

### Added
- Notes: median-over-mean, warmup-and-jit, checksum-anti-dce, ffi-boundary-crossover, publish-the-negative, ci-is-a-detector-not-a-ruler, repeats-and-confidence, pin-the-model-not-the-alias, thermal-state-is-a-variable, cache-aware-cost-accounting, agent-benchmarks-measure-the-stack, the-environment-block-is-part-of-the-result, paired-comparisons
- House shape enforced: claim / why / failure example / rule / counter-note
- `hero.svg` (mean-vs-median story), `CONTRIBUTING.md`, `LICENSE` (MIT)
- Sister footers across the research set
