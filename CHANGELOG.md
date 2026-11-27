# Changelog

All changes to the standards in this repository, by standard.
Versioning rules are in the README: MAJOR changes a threshold, a
required field or a verdict rule; MINOR adds without changing
existing verdicts; PATCH is wording only.

## Proof Record

### v0.2.0 — 2026-11-26

MINOR (additive; no existing verdicts change).

- Added the optional `chain` object: `partition_id`, `seq_num` and
  `chain_hash` link a record to the previous record's hash in its
  ledger partition, with a deterministic genesis hash for a
  partition's first record.
- Added the optional `epoch_ref` field: the version-record
  identifier for the issuing system's state at write time.
- README: added the ledger rule — a state-changing operation
  without a confirmed record is incomplete; audit before advance;
  records store credential references, never values.

### v0.1.0 — 2026-11-26

- Initial publication: the Proof Record schema — subject, method,
  measurements, verdict, evidence, limitations, SHA-256 body seal
  and the supersedes chain for corrections.
