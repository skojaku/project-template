# Criteria for a runnable experiment plan

An experiment Issue gets the label `ready` only when every item below is filled in
concretely. This file is the single definition: the Issue template, the planning
skill, and the dispatcher's check all follow it.

| # | Item | What counts as concrete |
|---|---|---|
| 1 | Question | One sentence that a result can answer yes/no or with a number. |
| 2 | Hypothesis | What we expect, and what result would contradict it. |
| 3 | Data | Where each dataset is (path or URL), its size, and any preprocessing. |
| 4 | Method | Models, algorithms, and parameter values or ranges to run. |
| 5 | Metrics | Exact definitions of what is measured and how it is computed. |
| 6 | Success criteria | Numeric thresholds or comparisons, written before seeing results. |
| 7 | Randomness | Random seeds and the number of repetitions. |
| 8 | Compute | Rough runtime, GPU needed or not, memory, number of parallel jobs. |
| 9 | Outputs | Which files and figures must exist when the run finishes. |
| 10 | If it fails | What to report if the run fails or the hypothesis is rejected. |

Anything unknown must be written as an explicit open question, not left blank.
