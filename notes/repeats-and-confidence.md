# How many repeats is enough? Let the spread answer

**Claim.** "We ran it 7 times" is not a methodology. The right repeat count depends on the run-to-run spread, and the honest report shows the spread — min/median/p95 or a confidence interval — so readers can see whether a 5% difference between two implementations is signal or weather.

**Why.** With high variance, more repeats buy precision slowly (error shrinks with √n). Doubling repeats from 7 to 14 cuts the median's uncertainty by ~24%, not 50%. Knowing that stops both the 3-run brag and the 10 000-run waste.

**Failure example.** Implementation A median 2.2 ms, B median 2.3 ms, both with p95 ≈ 3.0 ms and n=7. The 4.5% gap sits far inside the observed spread; publishing "A is 4.5% faster" is publishing noise. The same two medians with n=200 and p95 ≈ 2.4 ms would be a real, if modest, win.

**Rule.** Report n, median, and a tail statistic together; if the difference you care about is smaller than the run-to-run spread, say the measurement cannot resolve it — that sentence is a result, not a failure.

**Evidence in the wild.** bunaptic's harness prints warmup, repeats, min, median, p95 and max per kernel, and its profiles make n explicit (`ci` 3, `quick` 5, `standard` 7, `large` ≥10), so every published table carries its own precision budget.

**Counter-note.** For bimodal workloads (cache hit/miss, JIT tier switches) no n fixes a median that straddles two populations — split the populations and report both, or instrument which mode each run hit.
