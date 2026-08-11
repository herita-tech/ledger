# Herita ledger

Primary designated publication channel for the Herita promissory-note ledger.

Herita issues electronic promissory notes. This repository publishes the evidence that lets anyone —
a holder, a counterparty, a court, an auditor — check the integrity of that record without asking
Herita for anything, and without trusting Herita.

## Status — nothing is published yet

Read this section before relying on anything below it.

| | |
| --- | --- |
| Checkpoints published | **None.** Anchoring is not live. |
| Archive mirroring | **Not yet in place.** |
| Escrow deposit | **Not yet in place.** |

This repository exists so the publication channel is established and citable before the genesis
checkpoint. Everything under "What will be published here" describes the intended contents, not the
current contents. When the first checkpoint lands this section will say so.

## What will be published here

Each anchor cycle will publish:

- **Checkpoint cores** — `{ headHash, seq, prevCoreHash, exportDigest }`. A core is immutable once
  published. It is signed by a dedicated ledger-attestation key held separately from the credential
  that writes to this repository, so write access to this repository alone cannot mint an accepted
  checkpoint.
- **Attestations** — timestamp proofs over a core, as separate append-only records keyed by the
  core's hash. These accrue over time (an initial submission, later upgrades), which is why they are
  kept apart from the immutable core.
- **The public export** — event envelopes and public payloads.
- **The attestation public key**, so verification outlives Herita.
- **The offline verifier and instructions for running it**, so the tool and the data it checks cannot
  become separated.

The intent is that this repository is the primary channel and not the only one, with independent
durable archives mirroring it. Those mirrors are not yet established.

## Verifying

Verification is intended to require no Herita service, no Herita runtime, and no code from this
organisation that you are unwilling to read. A verifier reads the published export and checks the
hash chain from genesis; the trust root is the genesis checkpoint.

Two facts worth stating plainly, because they are what the design rests on:

- **Anchoring proves time, not truth.** A timestamp shows a checkpoint existed by a given moment. It
  does not show the history it commits to is honest.
- **Any two anchored checkpoints where neither extends the other are cryptographic proof of a fork.**
  That is evidence of fraud, not an ambiguity to be adjudicated. A checkpoint that does not extend
  the accepted one is rejected regardless of its sequence number.

An archive proves "as of", never "latest": locating a checkpoint proves the position existed, but
cannot prove no later checkpoint exists. Establishing currentness means checking the designated
channels for the latest accepted core.

## Privacy

Public payloads carry document hashes and opaque party commitments. They do not carry names,
amounts, invoice numbers, currencies or bank details.

## Contact

support@herita.eu
