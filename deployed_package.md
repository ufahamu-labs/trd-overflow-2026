# Deployed Sui Package

## Context within the wider project

TRD deployed this package to **Sui Testnet** as part of **MVP 20 — the Nautilus
Enclave Trusted-Data Pipeline Prototype**. It is provided with this submission
because the Sui Overflow application requires a deployed on-chain package.

MVP 20 tested how Nautilus, Seal, Walrus, Sui Move, and AWS Nitro Enclaves could
support a future trusted-data pipeline. The prototype remains relevant, but its
full technical implementation is not a current priority.

TRD's work with Jiwambe, the first borrower, is sequenced as follows:

1. **Build the interactive facility model — completed.** Create an interactive
   model of the TRD Open-Ended Adaptive Debt Facility to make its mechanics,
   rates, liquidity, and stress behaviour understandable.
2. **Define the facility with Jiwambe — in progress.** Use the model to discuss
   the facility, build a shared understanding of how it should work, and fix its
   commercial parameters in a term sheet.
3. **Build the Risk Monitor — in progress.** Connect the investor-facing
   frontend directly to the available Web2 APIs and iterate on its metrics,
   KPIs, and presentation.
4. **Collect investor feedback.** Test whether the Risk Monitor gives debt
   investors enough evidence to understand and price the borrower's risk.

The trusted-data pipeline is not required for this product-validation work. It
can be implemented later, after the Risk Monitor and its underlying data
requirements have been validated.

See the [strategic roadmap](./strategic_roadmap.md) for TRD's complete
high-level roadmap.

## Table of contents

- [Package details](#package-details)
- [What the package does](#what-the-package-does)
- [What MVP 20 demonstrated](#what-mvp-20-demonstrated)
- [Prototype limitations](#prototype-limitations)
- [Future role in the wider project](#future-role-in-the-wider-project)

## Package details

| Field | Value |
|---|---|
| Network | Sui Testnet |
| Package | `nautilus` |
| Package ID | `0x48a6a39f7d2e600e94398a2775f6194e4aff51d977d96eedbd9b61187e42be04` |
| Module | `nautilus::enclave` |
| Explorer | [View the package on SuiScan](https://suiscan.xyz/testnet/object/0x48a6a39f7d2e600e94398a2775f6194e4aff51d977d96eedbd9b61187e42be04/contracts) |

## What the package does

MVP 20 asked whether TRD could prove on Sui that data was processed by an
approved program inside an attested AWS Nitro Enclave.

The `nautilus::enclave` module provides the on-chain part of that proof:

1. An `EnclaveConfig` stores the approved PCR0, PCR1, and PCR2 measurements.
2. An AWS Nitro attestation document is checked against those measurements.
3. A matching enclave is registered on Sui with its public key and
   configuration version.
4. Other Move logic can verify payloads signed by the registered enclave.
5. Updated measurements can invalidate an earlier enclave registration when the
   approved build changes.

This creates a Sui trust root for distinguishing output signed by the approved
enclave build from output produced by unknown or modified software.

## What MVP 20 demonstrated

The prototype combined:

- an AWS Nitro Enclave for isolated processing;
- Nautilus and the deployed Move package for enclave registration;
- Seal for releasing protected credentials after enclave verification;
- a Rust sign server;
- a Python worker generating simulated Web2 motorbike rider records;
- a Node.js and SQLite aggregation sidecar;
- a VSOCK and TLS bridge for controlled outbound access; and
- Walrus for publishing the resulting SQLite snapshot.

The experiment demonstrated:

- execution of a multi-service application inside a real Nitro Enclave;
- generation of hardware-signed attestation measurements;
- enclave registration and verification on Sui Testnet;
- Seal threshold-key recovery inside enclave memory;
- processing of simulated motorbike rider records; and
- upload of an aggregated SQLite snapshot to Walrus.

Walrus blob ID:
`TwFc6On96HWeoRaM9jemon5UvKfNi3VIA506yIn7j5Q`

## Prototype limitations

MVP 20 was a feasibility test, not a production data pipeline:

- the records were simulated rather than fetched from live Jiwambe, Bolt, NTSA,
  loan-management, or payment systems;
- the schema was a small motorbike rider registry rather than the Risk
  Monitor's full data model;
- deployment and enclave lifecycle operations were manual;
- SuiSQL required compatibility patches after Sui SDK changes; and
- a Walrus Testnet upgrade broke the additional SuiSQL database-linkage step.
  The native Walrus `Blob` object was created, but the separate SuiSQL registry
  update was bypassed.

The Nautilus package deployment, enclave registration, Seal recovery flow, and
Walrus upload were real. Production requirements such as source reconciliation,
availability, privacy controls, key rotation, and disaster recovery remain to be
designed.

Attestation also proves which code processed an input; it does not prove that an
external API supplied complete or accurate data. A production pipeline must
therefore reconcile independent sources, preserve provenance, detect missing
feeds, and validate normalization before publishing trusted aggregates.

## Future role in the wider project

The current Risk Monitor will use the available Web2 APIs directly. This allows
TRD and Jiwambe to iterate on the investor experience without making the
trusted-data pipeline a prerequisite. Product requirements and debt-investor
feedback—not the earlier prototype—should determine the final pipeline
architecture.

If adopted, the future pipeline would:

```text
Borrower and third-party APIs
        ↓
Validate, reconcile, and aggregate inside an attested TEE
        ↓
Publish aggregate snapshots and provenance to Walrus and Sui
        ↓
Build a tamper-evident history for the Risk Monitor
```

Detailed borrower and rider data would remain private while investors receive
the verified aggregates needed to evaluate portfolio performance and covenant
status.

The package is reusable technical research for a later implementation, not the
architecture currently driving the MVP.
