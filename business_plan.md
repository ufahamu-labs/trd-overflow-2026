# Business Plan

The top-level strategy-and-execution narrative for TRD. It stays concise and
decision-oriented, and points to companion documents for depth: the
[problem statement](./problem_statement.md), the
[design decisions](./design_decisions.md), the
[roadmap](./strategic_roadmap.md), and the product pitches (published in the TRD
docs front end).

Audience: primarily the **TRD investor** (equity / protocol) and the **internal
team**, for whom this is the company's strategy and execution guide — and
secondarily the **debt investor**. It is a **public document**. (The debt
investor's primary, purpose-built surfaces remain the product pitches, the guides,
and the Risk Monitor in the TRD docs front end.)

---

## 1. Executive summary

TRD is **an onchain credit protocol — permissionless capital, curated credit,
publicly verifiable.** It is building the trust layer that lets onchain capital fund
productive-asset lenders more directly. The problem is not a lack of capital or borrower demand, but
the absence of trusted, ongoing visibility into portfolio performance for investors
outside a lender's personal network.

TRD addresses this with two innovations in one product: a **Risk Monitor** that
turns independent third-party operating data into a live, investor-readable view of
the loan book, and an **Open-Ended Adaptive Debt Facility** that lets capital fund
that book on terms built for both sides. The first proving ground is a Kenyan
electric-mobility lender financing income-generating motorbikes. The first MVP is
deliberately the trust layer, not the capital: prove the monitoring and the
protections convince investors before opening the facility.

The thesis: better visibility compresses the trust premium that keeps productive
private credit expensive and hard to scale.

---

## 2. Problem & opportunity

A market with strong, underserved demand for capital meets a growing base of
investors seeking real-economy yield; the missing piece is a trusted, independent
way to monitor performance over time. The full analysis lives in the
[problem statement](./problem_statement.md). The opportunity is to close that trust
gap, compress the intermediary stack, and open a larger market for directly
monitored productive-asset credit.

---

## 3. The product — two innovations in one

### 3.1 The Risk Monitor (the trust layer)

A live surface that turns independent third-party data — the borrowers' real-world
productivity, the lender's aggregated loan book, and registry data — into the same
risk metrics the lender runs internally, exposed to investors with no information
asymmetry.

### 3.2 The Open-Ended Adaptive Debt Facility

The instrument capital sits in: an open-ended facility that scales with verified
performance rather than a fixed, static loan, with an adaptive rate that prices risk
within agreed bounds.

---

## 4. How it works

### 4.1 The trusted data pipeline

Detailed operating data is extracted and aggregated inside a Trusted Execution
Environment on a daily cadence; the aggregate is published openly on Walrus, the
shared trust layer; the front end forms the KPIs from that public aggregate.
Third-party API credentials are held by Seal. Independent sources are cross-checked
(fleet activity, the lender's loan-management system, the vehicle registry, and the
M-Pesa payment rail that carries borrower repayments) so an asset cannot earn on
paper while missing in reality — and so reported repayments are confirmed by cash
actually reaching the lender rather than self-reported in the loan-management system.

### 4.2 The collateral: the revolving receivables pool

The facility is secured by the current value of the outstanding loan receivables —
a revolving pool that replenishes as borrowers repay and new loans are originated —
not by the physical assets. The assets only perfect the claim. See
[design decisions, D1](./design_decisions.md).

### 4.3 The security structure

A security agent incorporated where the assets operate holds a perfected,
registrable claim over the receivables, and steps in on the receivables on default.
The goal is never to seize physical collateral.

---

## 5. What makes it different — the design decisions

The full rationale is in [design_decisions.md](./design_decisions.md):

### 5.1 Trust before capital (order of operations)

The trust experience — the monitoring and the explainers — is built and proven
before committed capital is raised.

### 5.2 For the debt investor: a revolving pool, not a long-term lockup

A clean trade-off between locking capital and yield, with predictable, scheduled
liquidity and equal treatment under stress rather than first-come-first-served.

### 5.3 For the borrower: an open-ended facility that grows

A facility that scales as trust is proven — more capital, falling cost of capital —
all within the original contract, without returning to the market each round.

---

## 6. Lessons from prior RWA failures — and what we do differently

The Goldfinch experience is the clearest reference for what went wrong in
onchain real-world credit: capital ahead of monitoring, self-reported diligence,
weak security, yield propped up by token incentives, and loss discovered late. TRD
inverts each: monitoring before capital, independent and continuous verification,
security perfected over the receivables, real yield from asset productivity, and
honesty about what can fail. Full reference:
[Goldfinch post-mortem](../product/market_research/case_studies/rwa_protocols/goldfinch_post_mortem.md).

---

## 7. Market

### 7.1 Size and shape of the opportunity

TRD sits at the intersection of productive-asset lending in emerging markets,
wholesale private credit, and onchain capital seeking yield. The underlying
financing gap for small and growing businesses is measured in the trillions; the
wedge is the segment where performance can be monitored credibly and onchain
capital can move first.

### 7.2 Customers (personas)

Primary: the crypto-native stablecoin allocator. Secondary: institutional/DFI
credit, the originator/lender, the technologist, and — later, subject to
regulation — the retail investor. Full definitions in
[personas.md](./personas.md).

### 7.3 Competitive landscape

TRD spans several categories without sitting fully in any: originators (the lenders
themselves), the wholesale capital stack (debt funds, DFIs, marketplace lenders),
and onchain RWA protocols. Its distinct position is the monitoring-and-trust layer
that makes productive credit independently inspectable. The durable defensibility is
not the monitoring itself — which, by making a lender legible, is portable — but the
per-jurisdiction legal and security infrastructure, the attested data integrations,
and, at scale, becoming the cross-lender standard capital trusts. A comparison against
the closest categories (traditional banks, marketplace lending, smart-asset finance
platforms, first-wave on-chain RWA, and the traditional audit) is in
[product_differentiators.md](./product_differentiators.md).

---

## 8. Business model & protocol economics

TRD earns from the facility it enables rather than from selling data: a share of
the interest, commitment and administration fees on committed capital, and
event-based fees. It is not a revenue-share structure.

---

## 9. Go-to-market

### 9.1 The first facility and first lender

A collaboration with a Kenyan electric-mobility lender financing income-generating
motorbikes — chosen because the asset is productive and observable, the data is
accessible, the capital need is real, and the operator is a strong, collaborative
partner.

### 9.2 How capital is brought in

Monitoring-first: prove the trust layer and register investor demand, then admit
capital once the structure is in place — first in a controlled batch, then more
broadly.

---

## 10. Roadmap

The build follows one principle — understand the market and prove trust before
raising capital. High-level phases (compound-engineering foundation → market
understanding → backend trusted-data-pipeline research through MVPs → interactive
facility model → audience guides, TRD Docs, and legal drafts → Risk Monitor →
trusted data pipeline → on-chain facility → scale) are detailed in
[strategic_roadmap.md](./strategic_roadmap.md).

---

## 11. What we are proving next

TRD's positions are set out above: **monitoring** as the headline protection with
legal recovery as the backstop, a **neutral, fee-earning layer** alongside a separate
**security-agent** entity that holds the enforceable claim for the debt investors, and
a **moat** built on per-jurisdiction legal and security infrastructure, attested data
integrations, and — at scale — becoming the cross-lender standard that capital trusts.

The thesis that drives everything is the one we are out to demonstrate: that
independent, continuous verification delivers a **materially lower cost of capital**
than a lender's existing alternatives, and that the model scales cleanly beyond the
first lender and asset class. Proving it means deepening the verification stack,
expanding to additional lenders, productive-asset classes, and markets, and earning
the regulatory footing for each — always at the pace trust is established. Every step
compounds the same advantage: capital priced on real performance rather than opacity.
