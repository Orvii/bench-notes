# Report the median, and the p95

**Claim.** For timing benchmarks, the mean is the wrong headline number. Report the median of repeated runs, plus p95 to show the tail.

**Why.** Timing distributions are not symmetric. Scheduling interrupts, GC pauses, page faults and thermal throttling all push individual runs *up*; nothing pushes them meaningfully below the physical floor. A single 40 ms hiccup in ten 2 ms runs moves the mean by ~4 ms and the median by ~0. The mean reports your worst moment; the median reports your typical one.

**Failure example.** Seven runs: `[2.1, 2.2, 2.0, 2.3, 2.1, 2.2, 41.0]` ms. Mean ≈ 7.7 ms — a number no run actually produced. Median 2.2 ms, p95 ≈ 41 ms: typical and tail, both true.

**Evidence in the wild.** [bunaptic's bench harness](https://github.com/nixaut-codelabs/bunaptic) sorts samples and reports `median` and `p95` columns for every kernel; its recorded snapshot publishes both, not the mean.

**Counter-note.** The mean is still the right number when you measure *throughput over a fixed window* (total work / total time), because there the outliers are the workload. Know which question you are asking: latency → median; throughput → mean of totals.
