# Pin the model, not the alias

**Claim.** When benchmarking or comparing LLM providers, identify the model by its immutable ID **and the date**, never by a marketing alias (`-latest`, `-preview`, a provider's friendly name). An alias is a pointer that moves; a benchmark against a pointer is a benchmark against whatever the pointer meant that morning.

**Why.** Providers retarget aliases silently: `-latest` rolls forward, preview names graduate, and the same alias can serve different quantizations or routing policies per region. Two runs "on the same model" a week apart can be different models, and a cross-provider comparison using each vendor's alias compares naming schemes, not systems.

**Failure example.** A comparison concludes "provider A's flagship beats provider B's" using `flagship-latest` on both sides. A month later the conclusion inverts and neither team changed code — A's alias rolled to a new checkpoint while B's did not. The original table is now uninterpretable: it records a date, not a model.

**Rule.** Record, per run: resolved model ID (from the API response where available, not the request), snapshot/checkpoint tag if exposed, provider, date, and the alias as *sent*. When the resolved ID is unavailable, say so in the caption — an acknowledged unknown beats a confident alias.

**Counter-note.** If the question is precisely "what does the alias serve today" (fleet-routing reliability, aliasing behavior studies), then the alias *is* the subject — measure it repeatedly over time and report the drift. The rule forbids using aliases as model identity, not studying them as behavior.
