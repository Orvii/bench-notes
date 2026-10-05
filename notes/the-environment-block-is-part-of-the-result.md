# The environment block is part of the result

**Claim.** A benchmark number without its environment block — CPU model and count, OS and kernel, runtime and version, relevant flags, power state, container or bare metal — is not a result; it is an anecdote with digits. Print the block with every table, in the table's caption or header, never in a separate "setup" doc that readers skip.

**Why.** Every layer between the code and the silicon moves numbers: scheduler policy, kernel version, CPU microcode, runtime JIT generation, SIMD availability, transparent hugepages, container CPU quotas. Two "identical" machines differing in one of these can disagree by double digits — and the disagreement is invisible in the numbers themselves.

**Failure example.** A WASM-vs-TS comparison reproduced on a CI container showed half the speedup of the bare-metal original. Cause: the container's CPU quota throttled the multi-threaded path. Neither run was wrong; without the environment blocks, the two tables would have looked like a contradiction.

**Minimum block.** cpu model + cores/threads · os + kernel · runtime + version · simd/feature flags detected · power source + governor · container/quota or bare metal · date. bunaptic's snapshot caption ("AMD Ryzen 5 5600 (12 threads), Bun 1.4.3, BENCH_PROFILE=large") is the shape; add OS and power state and it is complete.

**Counter-note.** For *relative* conclusions measured minutes apart on one machine (A vs B, same session), the environment block still matters less than the pairing — but publish it anyway, because readers will want to know whether your relative result travels to their machine. The block is what makes a number portable.
