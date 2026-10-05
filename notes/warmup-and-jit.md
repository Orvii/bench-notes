# Discard warmup runs — and say how many

**Claim.** The first runs of any benchmark measure the runtime, not the code. Discard them, and publish the count.

**Why.** JS engines tier up: interpreter → baseline JIT → optimizing JIT, with deopt/reopt churn in between. WASM modules compile at load. Caches (instruction, data, file, DNS) are cold. A "benchmark" that includes run #1 is a compile-time measurement wearing a costume.

**Failure example.** Timing a WASM kernel including its first call folds module compilation (often tens of ms) into a kernel whose steady-state cost is microseconds — inverting any comparison against a warm interpreted baseline.

**Rule of thumb.** Warmup ≥ 2 for micro-kernels, more when the engine tiers aggressively; keep warmup and timed repeats as *separate* published parameters so readers can judge adequacy. bunaptic's `standard` profile uses warmup 2 / repeats 7; its `ci` profile drops to 1/3 for speed and says so in the output metadata — the profile name travels with every number.

**Counter-note.** If cold-start *is* the product (serverless handlers, CLI startup), invert the design: measure run #1 deliberately, many times, across fresh processes. Warmup discipline is about not mixing the two questions.
