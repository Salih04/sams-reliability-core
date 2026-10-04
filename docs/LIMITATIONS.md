# Limits of the evidence

- No production traffic, deployment reliability, load test, reconnect-storm measurement, or throughput claim is established.
- Temporal was tested on a development server, not a production cluster or Temporal Cloud. Server restart and long-lived workflow versioning were not demonstrated.
- The integration tests stubbed LLM, Git, and Docker activities. They test workflow control flow and failure handling, not agent output quality.
- The private system's resumable event path was off by default at the verified snapshot, and retention was not scheduled.
- Tenant isolation in the verified snapshot relied on application query predicates rather than PostgreSQL row-level security; account-level roles were not per organization.
- The evidence package omits the production implementation, complete schema, auth routes, and full test harness. The historical CI outcome verifies the earlier implementation snapshot, not the contents of this reduced package.
- A public code snapshot existed before this package was proposed. Making a repository private or rewriting its history cannot retract copies that others may already hold.
