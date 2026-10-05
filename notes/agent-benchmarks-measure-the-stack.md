# Agent benchmarks measure the stack, not the model

**Claim.** A score on an agentic benchmark (SWE-style tasks, terminal tasks, tool-use suites) is a property of the **whole stack**: model + harness/scaffold + toolset + environment image + retry policy. Quoting such a score as a model property — "model X is 72%" — without pinning the rest is quoting a number the model never produced alone.

**Why.** The harness decides what the model may see and do: which tools exist, how errors are fed back, whether the agent can retry, how long the context lives. Two scaffolds around one model differ by double digits on the same task set; one environment image with a flaky network turns passes into infra errors. The variance sources are multiplicative, and only one of them is the thing being advertised.

**Failure example.** A leaderboard row says 72%. The fine print: scaffold v3, toolset A, 3 retries on infra errors, environment image from March. Reproducing with scaffold v4 and no retries yields 61%. Neither number is wrong; the *attribution* was wrong both times it was quoted as "the model's score".

**Rules.**
- Pin and publish: scaffold name+version, tool list, environment image digest, retry policy, sampling temperature, and the task-set version.
- Report pass@k with k stated, and split failures into `agent` vs `environment` classes (retry-on-infra-error with a declared cap, then classify what remains).
- Compare stacks to stacks: changing the model measures the model only if everything else is frozen; changing the scaffold measures the scaffold only under the same freeze. Varying both measures nothing.

**Counter-note.** For *product* questions ("what will my users experience?") the stack is exactly what you want to measure — publish stack scores as stack scores. The error is not measuring stacks; it is laundering stack scores into model scores.
