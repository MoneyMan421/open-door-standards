# Open Door Standards

The shared standards for checkable AI work.

AI systems increasingly do real work — writing, coding, buying,
publishing, operating tools. The work is only trustworthy when it can
be checked: what was used, what was allowed, what happened, what was
measured, and what changed. These standards define the common formats
that make that checking possible across tools, vendors and time.

They are published openly, on purpose. This is the **Open Door
Protocol**: transparency for AI — the door is left open so users can
see the test, the record and the reasoning, and decide for themselves
what deserves trust.

## The stack these standards serve

The standards support one working stack, in five layers:

1. **Know** — skills, instructions, context and evidence an AI can
   rely on.
2. **Govern** — identity, permissions, boundaries and human approval.
3. **Run** — efficient execution that does not waste compute, money
   or time.
4. **Prove** — tests, measurements, audit records and drift
   detection.
5. **Reuse** — hardware, tools and prior work whose condition is
   known well enough to trust again.

## The standards

| Standard | What it defines | Status |
|---|---|---|
| Proof Record | The common record emitted by every checker, gate, scan and grade: subject, method, measurements, verdict, evidence and limits. | **v0.2 — in this repo** (`schemas/proof-record.schema.json`) |
| Task Signature | The contract for one task: requester, goal, allowed tools, data scope, limits, expiry and success test. | Planned |
| Gate Policy | How tool actions are allowed, denied or escalated to a human, and how removals are recorded. | Planned |
| Drift Suite | How a baseline is pinned for a model, tool, skill or workflow, and how a re-run reports exactly what moved. | Planned |
| Skill Scan | The criteria for grading a third-party skill or tool before installation: provenance, permission surface, hidden-instruction risk and measured quality. | Planned |
| GPU Grade | The published battery and grade rules for certifying the health of used datacenter GPUs. | v1.0 written; to be published here |

Every product that implements one of these standards references this
repository and the standard's version. Formats live here so they can
never quietly drift apart between products.

## The Proof Record (v0.2)

The Proof Record is the seed standard: the one record shape every
tool in the stack emits.

- A record is **serial-bound to its subject** — a specific skill
  version, tool version, task, output or hardware serial number.
- It states the **method and its version**, the **measured values**,
  the **targets they were measured against**, and the **verdict**.
- It carries its **evidence** and its **limits** with it. A record
  that hides its limits is not a proof.
- It is **hash-sealed**: the SHA-256 of the canonical record body
  travels with the record, so later edits are visible.
- Records are **append-only in spirit**: a correction is a new record
  that names the record it supersedes, never a silent edit.
- When records are kept in a ledger, they **chain**: each record
  names the previous record's hash in its partition, and the first
  record uses a deterministic genesis hash — removing or altering
  any record breaks the chain for everything after it.
- Every record carries its **version context** (`epoch_ref`): the
  identifier of the version record for the issuing system's state at
  write time. Version records are records like any other, so the
  exact state in force at any moment can be reconstructed.
- A record is **a measurement record, not a warranty.** It states
  what was measured, by what method, on what date — nothing about
  the future.

The machine-readable schema is
[`schemas/proof-record.schema.json`](schemas/proof-record.schema.json).

## The ledger rule

Where a product keeps its records in a ledger, one rule governs:

**A state-changing operation without a confirmed record is
incomplete — in the ledger's terms, it did not happen.**

A success reported without a record is a defect, not a shortcut.
Records are the gate, not an afterthought. Two supporting rules:

- **Audit before advance:** work that passes through a gate (a phase
  advance, a certification, a release) confirms its record before
  the advance, never after.
- **References, never values:** a permanent record may name the
  credential, approval or token that authorised an action by its
  reference — it never stores the credential's value.

## Versioning

Standards here are versioned semantically:

- **MAJOR** — a change to a threshold, a required field, or a verdict
  rule. Records issued under different major versions are not
  directly comparable.
- **MINOR** — an added test, field or record type that does not
  change existing verdicts.
- **PATCH** — wording, examples or clarification only.

Every version stays public, with its changelog. A record always
names the exact standard version it was issued under.

## Status

Seed published November 26, 2026; the Proof Record is at v0.2 (see
CHANGELOG.md). The Proof Record schema is
the first standard in the repo; the remaining standards land here as
their products reach the point of needing a shared format — the
standard is written when it is earned, not before.

Created by Collin.
