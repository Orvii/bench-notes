# Make the work un-eliminable: checksum your output

**Claim.** A benchmark whose result is unused can be optimized away. Consume the output — a checksum is the cheapest consumer — and print it.

**Why.** Compilers and JITs delete dead computation. If your timed loop's result never escapes, an optimizing engine may hoist it, constant-fold it, or drop it entirely; you then measure an empty loop and report a spectacular number.

**Failure example.** Timing `sum = Σ f(x)` where `sum` is dead after the loop: V8's escape analysis can reduce the body to nothing. The printed checksum column is also a *correctness* guard: two implementations claiming the same speedup must agree on it, or one of them is not computing the same function.

**Evidence in the wild.** bunaptic's harness threads a checksum through every timed run and prints it beside median/p95; its WASM-vs-TS table shows identical checksums (`4554.1409`) across implementations — same math, different speed. Where results are floats, compare checksums with tolerance and say so.

**Counter-note.** The checksum itself must be cheap relative to the work (a running XOR/add, not a hash of a megabyte buffer per iteration), and must depend on *every* iteration, or the engine can compute it once and skip the middle.
