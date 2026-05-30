<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://writprotocol.dev/writ-W-paper.svg">
    <img alt="Writ Protocol" src="https://writprotocol.dev/writ-W-ink.svg" width="120">
  </picture>
</p>

# Writ Protocol

**An open delegation-and-evidence format for AI agents.**

When an AI agent acts on someone's behalf — fills a form, sends an email,
calls an API — there's no structured way today to express *what it was
allowed to do*, prove *it stayed in bounds*, or recover when it didn't.
Writ Protocol is the layer that fills that gap. It sits above capability
primitives, below governance. Every authorized agent action travels with
a signed *writ*; every action emits a signed *receipt*. Anyone can
follow the chain.

## Where things live

- **[writ-protocol](https://github.com/writprotocol/writ-protocol)** —
  v0.1 specification, concept paper, and the TypeScript reference
  implementation (core, engine, MCP harness). MIT-licensed.
- **[writprotocol.dev](https://writprotocol.dev)** — public landing page.
- **[registry.writprotocol.dev](https://registry.writprotocol.dev)** —
  append-only static registry. Signed writs and receipts published as
  JSON, addressed by ID, no directory listings. Sourced from a private
  GitHub repo, served via Cloudflare Pages.

## v0.1 status

- Wire format (`protocol: "writ/v0"`) stable for the v0 cycle. Will
  promote to `writ/v1` at protocol stabilization.
- Reference engine: signs writs and receipts with Ed25519 over RFC 8785
  canonical JSON, gates an agent's actions against the writ's declared
  scope and constraints, publishes signed artifacts to the registry. 75
  tests green.
- Five `core.*` actions implemented end-to-end as the starter set
  (`file.read`, `browser.navigate`, `form.fill`, `form.submit`,
  `browser.screenshot`); the full vocabulary will grow with usage.
- What's deferred to later revisions is named in the spec (tokens as a
  wire artifact, full amendment schema, validator dispatch for non-core
  namespaces). Nothing masquerades as shipped that isn't.

## Verifiable

The project dogfoods its own protocol. A signed writ + receipt pair from
integration testing lives at:

- [`writ_s9cgwkeb2o`](https://registry.writprotocol.dev/writ/writ_s9cgwkeb2o.json) — the writ that authorized the run.
- [`receipt_4y3jxubjfa`](https://registry.writprotocol.dev/receipt/receipt_4y3jxubjfa.json) — the evidence of what happened.

Both are `mode: "dryrun"` (produced during testing against a real form
without sending the submission). Signatures verify against
`issued_by.key` and `produced_by.key` respectively, using vanilla
Ed25519 over RFC 8785 canonical JSON — no protocol-specific verification
machinery required. See the [reference README][rr] for a four-line
verification snippet.

[rr]: https://github.com/writprotocol/writ-protocol#verify-locally

## License

MIT, across all repos.
