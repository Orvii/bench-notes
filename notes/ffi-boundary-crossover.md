# The FFI boundary has a price: find the crossover, publish it

**Claim.** "Native/WASM is faster" is not a property of the kernel, it's a property of the *workload size*. Every call across a language boundary costs; below some size that cost exceeds the kernel's savings. Measure the crossover instead of asserting a winner.

**Why.** A JS→WASM call marshals arguments, switches stacks, and returns through the same door. Per-element calls pay that toll per element. Batch calls pay it once. The same kernel can lose at N=1k and win 5× at N=1M.

**Failure example (observed, published as-is).** In bunaptic's recorded snapshot (Ryzen 5 5600, Bun 1.4.3, large profile), the per-element `WASM loop` median is **6.54 ms** while the plain `TS loop` is **3.21 ms** — WASM loses at that size, purely on boundary cost. Meanwhile the SIMD dataset kernels win decisively (`0.0608 ms` dense dataset SIMD vs `0.2884 ms` scalar graph path). One table, both directions, no spin.

**Rule.** When comparing across a boundary, benchmark at ≥3 sizes spanning two orders of magnitude, and report the size at which the ranking flips. A single-size verdict is a claim about your test, not about the technology.

**Counter-note.** If your API can only be called per-element, the crossover is academic — the boundary cost *is* your architecture's cost, and the honest fix is batching at the API level, which is exactly what the negative result pointed at.
