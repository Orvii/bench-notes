# Publish the benchmark code, or publish nothing

**Claim.** A benchmark result without its benchmark code is an advertisement with error bars. The code is part of the result: it encodes the warmup, the oracle, the input generation, the environment assumptions — every decision the number depends on. Numbers travel; code is what makes them checkable.

**Why.** Reviewers cannot audit a measurement they cannot read. The classic failure modes all live in code, not in tables: warmup inside the timed region, dead-code-eliminable workloads, input generators that produce trivially cacheable data, timers with insufficient resolution, comparisons across differently-configured runs. A table hides all of them; a diff exposes all of them.

**Failure example.** A widely-cited "X is 10× faster than Y" post shipped a chart. The code, extracted later by a third party, timed X on pre-warmed input and Y cold, with Y's allocation inside the loop and X's hoisted. The 10× was the measurement design.

**Rule.** Benchmark commits include: the harness, the input generator (with seeds), the environment block, and the raw result rows — the same commit, not a later "tooling" repo. If the harness is proprietary, the honest move is to say the numbers are unauditable and label them as vendor claims.

**Counter-note.** Some benchmark code embeds licensing or security constraints (proprietary workloads, internal endpoints). Then publish the *shape*: a reduced harness on synthetic inputs that reproduces the methodology, plus a statement of what the real workload differs in. Half-published method beats a chart; full method beats both.
