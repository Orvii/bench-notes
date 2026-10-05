# Thermal state is a variable — measure it or control it

**Claim.** CPU frequency is not constant: sustained load throttles, laptops derate on battery, and a cold machine runs the first minute faster than the tenth. A benchmark that ignores thermal state measures the cooling solution as much as the code. Either control it (same power mode, plugged in, idle-cooled between runs) or record it (clock frequency, power source, ambient) alongside every number.

**Why.** Modern CPUs trade frequency for temperature continuously. Two identical suites run back-to-back can differ by 10-20% purely because the second started hot. Battery power adds a second derate layer below the OS scheduler. Neither effect appears in your code, and neither appears in a median — it appears as an unexplained gap between "the same" experiment on two days.

**Failure example.** A kernel "regresses" 12% in an afternoon re-run. Nothing changed in the repo. The morning run started from a cold soak; the afternoon run followed a full test suite. The diff was heat, and the commit that "fixed" it fixed nothing.

**Rule.** Fixed power mode and plugged-in for all published numbers; a cool-down idle between timed batches; record `power source` and, where readable, clock frequency or a thermal sensor in the run metadata. If you cannot control it (field measurements), publish the distribution across states instead of one number per configuration.

**Counter-note.** If the product runs hot by nature (long training jobs, sustained servers), cold-soaked microbenchmarks misrepresent it: throttle *is* the steady state. Then benchmark through the throttle — long runs, report the degraded plateau, and say the first minute is not representative of the tenth.
