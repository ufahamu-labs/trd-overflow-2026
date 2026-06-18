# Roadmap

TRD connects East Africa's high-yield productive-asset market, where demand for
capital is strong and underserved, to debt investors seeking sustainable
real-economy yield. This page is the high-level sequence we are building in. The
guiding principle is simple: understand the market and customer needs, test
assumptions with small MVPs, secure access to real operating data and prove it can
be independently verified, then establish trust before asking investors to deploy
capital.

Detailed sequencing and timing for each workstream live in the per-domain roadmaps;
this page is the shape of the whole. The [problem statement](./problem_statement.md)
defines the trust gap from the debt investor's perspective, while the
[business plan](./business_plan.md) explains the product and commercial strategy.

## Roadmap Summary

| Status | Phase | Workstream |
|---|---|---|
| Completed | [Phase 1](#phase-1--the-compound-engineering-foundation-done) | Compound-engineering foundation |
| Completed | [Phase 2](#phase-2--understanding-the-market-done) | Market research and customer needs |
| Completed | [Phase 3](#phase-3--research-the-backend-solution-stack-through-mvps-done-built-in-parallel-with-phase-2) | Backend trusted-data-pipeline research through MVPs |
| Completed | [Phase 4](#phase-4--the-interactive-facility-model-done) | Open-Ended Adaptive Debt Facility Model explainer |
| In progress | [Phase 5](#phase-5--the-guides-docs-and-legal-drafts-in-progress) | Audience guides, TRD Docs, and first-borrower legal drafts |
| In progress | [Phase 6](#phase-6--the-risk-monitor-in-progress) | User-facing Risk Monitor |
| Open | [Phase 7](#phase-7--the-trusted-data-pipeline-planned) | Production trusted-data pipeline |
| Open | [Phase 8](#phase-8--the-on-chain-facility-planned) | First-borrower term sheet and Sui Move facility |
| Open | [Phase 9](#phase-9--scale-planned) | Additional lenders, assets, and markets |

## Phase 1 — The compound engineering foundation *(done)*

Before building the product, we built the system that builds the product: a
compound-engineering stack of AI agents, shared skills, and tooling — including a
bench of specialised AI advisors spanning the domains the work needs (legal
engineers, deal counsel, legal scenario writers, startup advisors and strategists,
and domain engineers) — that lets a small team operate with the throughput of a much larger
one.

## Phase 2 — Understanding the market *(done)*

A deep knowledge base built from the top down: the market at a high level, then
actor categories (borrowers and originators, debt investors, RWA protocols, Web2
productive-asset platforms, data providers, legal and registry actors, and more),
then specific actors within each — and finally concrete case studies, post-mortems,
and competitor analyses, each examined from different points of view.

The aim was not just to map East Africa's high-yield productive-asset market, but
to develop a deep understanding of customer needs, determine where the product fits
in the wider ecosystem, and identify its primary and secondary customers. The
**initial primary customer is the crypto-native stablecoin allocator** seeking
sustainable real-economy yield but lacking a trusted way to underwrite and monitor
this market. The productive-asset lender is the secondary customer: it needs a
credible way to present its performance to capital outside its existing network.
Building trust between these customers is what TRD exists to do.

## Phase 3 — Research the backend solution stack through MVPs *(done, built in parallel with Phase 2)*

This phase researched the backend solution stack for a **trusted data pipeline**
through a series of small MVPs. The objective was to determine how sensitive Web2
operating data — from government registries, fleet platforms, and the lender's own
systems — could reach the Risk Monitor in a form an outside party can **trust,
audit, and replay**. The key question was not whether the data could be fetched,
but whether it could move through consent, attested processing, secure key
handling, and verifiable storage end to end.

We tested a range of products and patterns against that pipeline and decided what to
adopt, adapt, or discard:

- **Adopted.** AWS Nitro Enclaves for attested processing; **Nautilus** for on-chain
  enclave attestation; **Seal** for recovering signing and storage credentials inside
  the enclave; **Walrus** for verifiable storage of the aggregated data (with caching
  and history caveats); a Chrome **consent bridge** that hands off an authenticated
  session without the user sharing credentials; a VSOCK/TLS bridge so the air-gapped
  enclave can reach Sui, Walrus, and the sources; and a browser-side verification
  console (WASM SQLite) that lets anyone audit the anchored data.
- **Discarded or superseded.** Reclaim-style Move proof verification (a useful
  primitive, but too narrow for a full pipeline); Oyster CVM (proved the model, then
  superseded by the Nautilus/Seal path); in-browser DOM scraping (the wrong trust
  boundary — extraction belongs in the enclave); and the SuiSQL anchoring sidecar
  (works, but needs hardening or replacement against SDK drift).

These came together in a working end-to-end prototype: a real enclave performing
consented data ingestion, anchoring an auditable snapshot to Walrus, with a console
that verifies provenance from blob IDs, object IDs, attestation (PCRs), and
transaction history. The architecture and its core pieces are proven; what remains
is productionising them, which lives on the engineering roadmap.

## Phase 4 — The interactive facility model *(done)*

The first user-facing MVP was the
[**Open-Ended Adaptive Debt Facility Model**](https://therealdeal.app/docs/model)
explainer. It was designed to help the first borrower understand and discuss the
proposed facility's rates, yield, withdrawals, and stress behaviour. This establishes
borrower buy-in before the commercial parameters are fixed in a term sheet and
implemented in Sui smart contracts.

## Phase 5 — The guides, docs, and legal drafts *(in progress)*

The first-borrower legal package has been drafted and is under review by the
borrower. Its core documents are the **Senior Debt Term
Sheet**, **Master Facility Agreement**, and **KPI Covenant Registry (KCR)**.
Supporting drafts include the debt-investor diligence NDA, corporate and security
structure documents, General Security Deed, and Protocol Administration Agreement.

The next review step is to obtain feedback from selected potential debt investors.
The live transaction documents under negotiation, are shared only with relevant counterparties and reviewers.

The guides are the organizing layer for the facility. They list the
product surfaces and legal agreements relevant to each audience. 
Together, these materials define how the future on-chain
debt facility interfaces with the borrower, debt investors, operating data, and
the real-world legal structure (the security agent).

- **Borrower Guide:** the borrower pitch, interactive facility-model explainer,
  FAQ, implementation guidance, and proposed legal documents.
- **Debt Investor Guide:** the investor pitch, interactive facility-model
  explainer, FAQ, monitoring approach, covenants, security, enforceability, and
  asset-recovery information.
- **TRD Investor Guide:** the business plan, product strategy, roadmap, technical
  architecture, and legal and regulatory position.

TRD Docs provides the shared product explanations and interactive model referenced
by the guides.

## Phase 6 — The Risk Monitor *(in progress)*

Only after the facility model, guides, and initial legal structure were developed
did work move to the user-facing **Risk Monitor**. It is being built with the
borrower to convert operating and loan-book data into investor-readable risk
evidence.

The current Risk Monitor uses Web2 source data. Moving it onto the attested data
pipeline is the next phase.

## Phase 7 — The trusted data pipeline *(planned)*

Move the Risk Monitor from the Web2 source data onto live, attested Web3 data by
productionising the pipeline proven in Phase 3: the TEE ingestion service, the
verification stack, and the storage of aggregated data on Walrus — from prototype to
a maintained, replayable service.

## Phase 8 — The on-chain facility *(planned)*

Build the machinery that lets capital actually flow, then open the facility: the
**Move smart contracts** — deposits, drawdowns, repayments, the adaptive rate and
its bounds, the cash buffer, payout epochs, and control states.

No facility smart contracts have been written yet. Development begins only after
the commercial term sheet is agreed with the first borrower, so the contract
architecture and parameters implement an agreed facility rather than a speculative
deal design.

Once trust is established and the facility is in place, capital is admitted — first
in a controlled batch, then more broadly.

## Phase 9 — Scale *(planned)*

Beyond the first lender and the first asset class: additional originators,
additional productive-asset classes, and additional markets. Each is added only
at the pace trust is proven — never faster than the monitoring and the structure
can stand behind it.
