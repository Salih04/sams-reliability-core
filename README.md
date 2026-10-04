# SAMS — reliability evidence

This repository is a curated public evidence package derived from the private SAMS project. It documents selected reliability mechanisms and their verification while intentionally omitting production implementation, product surface, and security-sensitive internals.

Public examples, if added, may be simplified reference implementations. The private application contains the full production system. This package does not grant access to that source code.

SAMS is a private, multi-tenant system for durable LLM agent workflows. The engineering evidence here covers resumable event delivery, concurrent human decisions, fail-closed tenant boundaries, single-use refresh tokens, and workflow recovery. The [architecture](docs/ARCHITECTURE.md) explains the trust and durability boundaries; [verification](docs/VERIFICATION.md) lists the failure scenarios and observed results; [limitations](docs/LIMITATIONS.md) defines what those results do not prove.

## Evidence at a glance

| Concern | Publicly stated guarantee | Evidence boundary |
| --- | --- | --- |
| Event resume | A client receives a complete missed interval or an explicit gap | Private implementation; recorded Redis integration tests |
| Replay to live | A reconnecting client does not silently skip or duplicate events at handoff | Private implementation; recorded real-Redis race test and negative control |
| Approval race | A human decision and a deadline settle to one durable outcome | Private implementation; recorded PostgreSQL race tests |
| Lost workflow signal | The durable decision can be recovered without a delivered wake-up signal | Private implementation; recorded Temporal dev-server test |
| Refresh reuse | A refresh token is single-use and reuse revokes its session family | Private implementation; recorded PostgreSQL and unit tests |
| Tenant boundary | Ownership comes from trusted stored state; unresolved ownership fails closed | Private implementation; recorded Redis/PostgreSQL and unit tests |

The original full-code extract passed 543 unit tests (3 tests requiring the complete application were deselected) and 25 integration checks in GitHub Actions on 4 October 2026. The integration job used Redis 7, PostgreSQL 16, and a Temporal development server. These are **historical results for the prior private implementation snapshot**, not a test run of this reduced evidence package. See [the provenance record](results/CI_2026-10-04.md).

This project has not served production traffic and has not been load-tested. Temporal was tested on a development server. See all [limitations](docs/LIMITATIONS.md).

The private system was built with AI coding agents in a specification, review, and validation workflow. I own the architecture, engineering decisions, acceptance criteria, and technical validation.

All rights reserved. No licence is granted.
