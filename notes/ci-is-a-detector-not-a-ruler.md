# CI is a detector, not a ruler

**Claim.** Benchmark numbers produced on shared CI runners are fine for catching *regressions* and useless for stating *performance*. Use wide-threshold CI checks for the first question; a named, quiet machine for the second. Never mix the two in one table.

**Why.** CI runners are multi-tenant: CPU steal, noisy neighbors, throttled bursts, differing host generations week to week. A 5% regression signal drowns in ±30% environment noise, and an absolute number published from CI is a number about a machine you cannot name.

**Failure example.** A PR "optimizes" a kernel by 8%; CI bench goes green both before and after because the runner's variance is ±25%. Worse inverse: a harmless PR "regresses" 15% on a cold host and gets reverted for no reason. Both outcomes teach the team to ignore the bench.

**Evidence in the wild.** bunaptic ships a `ci` profile (warmup 1, repeats 3, 0.25× scale) explicitly for fast, coarse CI signal, while its *published* snapshot comes from a named machine with the `large` profile — the profile name travels with every number so nobody mistakes a detector reading for a ruler reading.

**Counter-note.** If your artifact only ever runs on ephemeral infra (serverless, containers), CI-like variance *is* the production condition — then measure the distribution over many CI runs and publish percentiles of the environment itself. The rule is not "CI numbers are bad"; it is "know which question each number answers".
