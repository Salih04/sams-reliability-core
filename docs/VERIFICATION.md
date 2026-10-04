# Verification and provenance

The following tests ran against the original implementation snapshot before the public surface was reduced. They are **not runnable from this evidence package**, which omits the private implementation and its test harness. Counts and outcomes come from the completed GitHub Actions run documented in [the CI record](../results/CI_2026-10-04.md).

| Scenario | Service used | Observed check |
| --- | --- | --- |
| Stream deletion, restart without persistence, and trimmed history | Redis 7 | Resume reports an explicit gap when history cannot be proved complete. |
| Concurrent event writes during replay | Redis 7 | Handoff test found no missing or duplicated event at the replay/live boundary. |
| Concurrent approve/reject and decision/deadline races | PostgreSQL 16 | Exactly one durable outcome was accepted. |
| Concurrent refresh claims | PostgreSQL 16 | Single-use claim and reuse behavior held under the tested race. |
| Decision recorded without its workflow signal | Temporal development server | Workflow recovered the stored decision. |
| Worker stopped and replaced during approval wait | Temporal development server | Waiting workflow resumed after replacement. |
| Unknown or conflicting tenant attribution | Redis/PostgreSQL and unit tests | Delivery failed closed in the tested cases. |

## Negative controls

The original test campaign deliberately introduced regressions and observed failures: read-then-write approval, trusting signal payload rather than durable state, missing deadline predicate, missing stream-generation check, late live capture, and read-then-write refresh. These controls were run on the original implementation and restored. They are historical test observations, not experiments reproduced by this package.

## How to assess the evidence

Review the failure contracts, the test scenarios, the CI job outcome, and the explicit limitations. For a deeper technical interview, ask about the race setup, why the negative control fails, and which state is authoritative. This package intentionally does not provide a reusable production solution.
