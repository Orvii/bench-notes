# Publish the negative result

**Claim.** A benchmark report that contains only wins is advertising. The rows where your optimization lost are the most informative rows you have — publish them in the same table, same font.

**Why.** Three reasons, in ascending order of importance. One: readers calibrate trust — a table with a loss in it is believable, a table of pure wins is not. Two: the negative localizes the problem (boundary cost, allocation pattern, cache behavior) better than any win does. Three: file-drawer bias is how whole fields end up unreproducible; small engineering blogs can choose not to join.

**Failure example (our own).** bunaptic exists to make neural-network kernels fast with Rust-WASM. Its first recorded snapshot's headline row is a loss: per-element WASM slower than TypeScript. Keeping it in turned the README's honesty section from prose into evidence, and pointed the next engineering step at batching across the boundary rather than at writing more kernels.

**How to do it without spin.** Same table, same units, machine + runtime + profile in the caption, and one sentence of interpretation that names the mechanism ("boundary cost dominates at this size") instead of an excuse ("results may vary").

**Counter-note.** Do not publish negatives *selectively* either — dropping the win that embarrasses a competitor is the same bias with the sign flipped. The rule is the whole table or no table.
