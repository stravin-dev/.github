<p align="center">
  <a href="https://stravin.dev>
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="./assets/stravin-lockup-dark.svg">
      <source media="(prefers-color-scheme: light)" srcset="./assets/stravin-lockup-light.svg">
      <img alt="Stravin" src="./assets/stravin-lockup-light.svg" width="320">
    </picture>
  </a>
</p>

<h3 align="center">Stateless, multi-region hosted Git built for human teams and agent-scale engineering.</h3>

---

### Introducing Stravin

Modern software engineering has outgrown stateful Git servers.

Traditional Git hosting platforms were designed for an era of human-paced pushes landing on disk-bound primary replicas. That architecture breaks down under today's workloads: massive monorepos, globally distributed teams, and fleets of autonomous coding agents pushing thousands of branches in parallel. When storage, reference locking, packfile compaction, and server-side hooks all fight for the same host disk, teams hit familiar walls—`git push` stalls during background repacks, cross-region write latency penalties, noisy-neighbor contention, and brittle replication topologies.

**Stravin** rethinks hosted Git from the storage engine up.

Built in Go on managed cloud primitives, Stravin separates durable object storage from reference linearization so repositories scale to thousands of concurrent pushes per second without trading away home-region write speed or multi-region high availability.

---

### What Stravin Solves

- **Agent-Scale Write Concurrency** — By storing immutable, content-addressed packfiles in sharded object storage and coordinating references via atomic per-ref compare-and-swap (Ref-CAS), Stravin eliminates single-manifest bottlenecks and filesystem ref-lock contention. Thousands of parallel branch pushes succeed without blocking each other.
- **Fast Writes Locally, Fast Reads Everywhere** — Writes pin to a repository's home region with zero cross-region round trips on the push path. Asynchronous global replication and transparent origin fallback keep clones and fetches fast for developers and runners in any region.
- **Disposable Compute, Zero Repack Storms** — Stateless Git nodes treat local NVMe strictly as a warm, rebuildable cache. Tiered, LSM-style packfile compaction and index generation run completely out-of-band on isolated workers, so heavy repository maintenance never steals CPU or I/O from live reads and writes.
- **Zero-Latency Safety Guardrails** — Synchronous pre-receive checks run inside hermetic WebAssembly sandboxes concurrently with packfile uploads—enforcing secret scanning, commit hygiene, and policy rules with effectively zero added push latency. Heavy downstream workflows run asynchronously through a transactional outbox.
- **Defense-in-Depth Multi-Tenancy** — Standard Git wire protocol compatibility (SSH and Smart HTTP) meets strict process, namespace, and resource isolation so untrusted packs and noisy workloads stay safely contained.

---

### Built for the Next Decade of Software Delivery

Whether you are shipping from a single laptop or orchestrating thousands of autonomous agents against a shared codebase, Git should never be the bottleneck. Stravin brings cloud-native durability, predictable low latency, and clean modular architecture to the foundation of every engineering workflow.
