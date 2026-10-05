# Cost accounting without cache hits is fiction

**Claim.** When a runtime serves part of a request from a prompt cache, the billed cost and the served latency both change — often by an order of magnitude on the cached prefix. Any cost or speed figure that counts tokens without separating **cache writes, cache reads, and uncached tokens** describes a billing model that no longer exists. Report the three counters separately, plus the derived hit rate.

**Why.** Providers price cache reads at a steep discount (commonly ~10% of base input price) and serve them faster. A workload that re-sends a large stable prefix (system prompt, repo context) may pay a fraction of its naive token cost once the cache is warm — and pay full price on every cache miss. The same workload can therefore cost 10× differently depending on cache state, which is a property of *request ordering and timing*, not of the workload.

**Failure example.** A benchmark reports "$0.42 per task" averaged over 100 runs executed back-to-back: run 1 pays the cache write, runs 2-100 ride cache reads. A user running the task once per day with an expired cache pays the run-1 price every time. The published number is true for the benchmark and false for the user — because cache state was never reported.

**Rule.** Per run, record: input tokens uncached, cache-write tokens, cache-read tokens, output tokens; compute cost from the provider's published per-class prices with the price table version dated. Report hit rate alongside any aggregate cost. If the API hides the counters, say so and mark the cost figure as an estimate with its assumption (cold or warm).

**Counter-note.** Cache behavior can be adversarial to measure: TTL expiry, eviction under load, and providers that silently change cache policy. A hit-rate figure is a statement about a window, not a constant — date it like a version pin, and re-measure when costs matter.
