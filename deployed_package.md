# Deployed Sui Package

## Context within the wider project

TRD includes this **Sui Testnet** package because the Sui Overflow application
requests a deployed on-chain package. The package comes from TRD's broader
technical research into a trusted data pipeline using Nautilus, Seal, Walrus,
Sui Move, and AWS Nitro Enclaves.

This research remains relevant to the future production architecture, but
productionizing the trusted data pipeline is not the current product priority.
TRD is first validating the facility design, legal structure, Risk Monitor,
underlying metrics, and debt-investor requirements with its operating partner.

The reduced MVP shared for Sui Overflow uses this package. Its exact scope,
implementation, and instructions are documented in the
[MVP Demo — Sui Overflow Hackathon 2026 repository](https://github.com/ufahamu-labs/mvp_demo_sui_overflow_hackaton_2026).

See the [strategic roadmap](./strategic_roadmap.md) for the completed work,
current priorities, and sequence toward the production trusted-data pipeline
and on-chain debt facility.

## Package details

| Field | Value |
|---|---|
| Network | Sui Testnet |
| Package | `nautilus` |
| Package ID | `0x48a6a39f7d2e600e94398a2775f6194e4aff51d977d96eedbd9b61187e42be04` |
| Module | `nautilus::enclave` |
| Explorer | [View the package on SuiScan](https://suiscan.xyz/testnet/object/0x48a6a39f7d2e600e94398a2775f6194e4aff51d977d96eedbd9b61187e42be04/contracts) |
| Reduced hackathon MVP | [MVP Demo — Sui Overflow Hackathon 2026](https://github.com/ufahamu-labs/mvp_demo_sui_overflow_hackaton_2026) |

## Trusted-data-pipeline research

TRD built a sequence of small internal MVPs to research how sensitive Web2
operating data could become independently verifiable evidence for debt investors.
The goal was to design a trusted data pipeline connecting sources such as fleet
platforms, payment rails, loan-management systems, and government registries to
the Risk Monitor without exposing private borrower or customer data.

The research tested the pipeline as a set of separate trust problems:

1. obtaining borrower-authorized access to third-party data;
2. processing and reconciling that data in an attested environment;
3. protecting credentials and cryptographic keys;
4. publishing privacy-preserving aggregates to verifiable storage;
5. anchoring the approved software and its outputs on Sui; and
6. allowing an outside party to audit provenance and replay the verification.

These experiments informed the proposed combination of AWS Nitro Enclaves,
Nautilus, Seal, Walrus, and Sui Move. The complete internal MVP collection and
production repositories remain private.

## What the MVP sequence established

The internal MVPs established that:

- consented Web2 data can be processed inside an attested enclave;
- Sui can register the approved enclave measurements and public key;
- protected credentials can be released only inside the verified environment;
- processed aggregates can be published to Walrus;
- provenance can be carried from source ingestion through processing and storage;
  and
- an investor-facing verification layer can audit the resulting evidence.

The research also established important boundaries. Attestation proves which code
processed an input, but it does not prove that an external source supplied complete
or accurate data. A production system must therefore reconcile independent
sources, detect missing feeds, preserve provenance, validate normalization, rotate
keys, and provide operational recovery procedures.

## Future plans

The current Risk Monitor is being developed against available Web2 data first so
TRD and its operating partner can validate the metrics, customer experience, and
investor requirements. Those findings should determine the production pipeline,
rather than treating the research architecture as fixed.

If adopted, the trusted data pipeline would connect:

```text
Third-party operating and financial data
        ↓
Attested processing and reconciliation
        ↓
Privacy-preserving aggregates on Walrus
Attestation and verification state on Sui
        ↓
Investor-facing Risk Monitor
```
