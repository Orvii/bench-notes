# Compare in pairs, not in averages

**Claim.** When asking "is A faster than B", run A and B **interleaved, on the same machine, in the same time window**, and compare within-pair differences. Two separate batches — all of A, then all of B — compare A-while-the-machine-was-in-one-state against B-while-it-was-in-another, and the machine's drift becomes your "result".

**Why.** Slow drift (thermal, neighbor noise, frequency scaling, background jobs) is usually larger than the effect you chase. Interleaving converts drift from a between-group confound into within-pair noise that pairing removes: each pair sees (nearly) the same machine state, so the difference isolates A-vs-B.

**Failure example.** Batch A runs minutes 0-5 of a laptop session (cool), batch B runs minutes 5-10 (warm, throttled). B "loses" by 9%. Re-run interleaved: the median within-pair difference is 0.4% with both signs represented. The batch design measured the cooling curve.

**Method.** Alternate A,B,A,B,... (or randomized order with a fixed seed); keep pairs adjacent in time; report the paired differences' median and a spread (or a sign test / Wilcoxon if you want a p-value — name the test). Report batch medians too, labeled as such, so readers see how much the design moved the answer.

**Counter-note.** Pairing assumes the two runs do not interfere. If A and B share state (cache warming, JIT tiering that benefits the second runner, disk prefetch), adjacency *creates* the difference: alternate direction (B,A,B,A) in a second pass and compare the two pairings — a systematic order effect shows up as a sign flip between passes.
