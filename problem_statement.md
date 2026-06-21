# Problem Statement

A market with strong, underserved demand for capital sits on one side. A growing
base of investors looking for real-economy yield sits on the other. The missing
piece between them is not demand, and not capital. It is a trusted, independent way
to see what is actually happening inside the loan book over time.

This document defines that problem from the point of view of TRD's primary
audience: the **debt investor**.

Two roles are easily confused, so to be precise: the **debt investor** supplies
capital into the TRD debt facility, while the **micro-asset lender** (the
originator) borrows from that facility and in turn lends to the end consumers who
use the financed assets. Where this document says "the investor," it means the debt
investor.

---

## 1. The core problem

### 1.1 Capital and demand exist; independent verification does not

Productive-asset lenders in markets like Sub-Saharan Africa originate real loans
against income-generating assets, collect real repayments, and have real, unmet
demand for capital to grow. Investors — increasingly including onchain stablecoin
allocators — want durable yield from real economic activity.

What stops the capital from flowing is trust. A debt investor cannot get
comfortable allocating into a lender they cannot independently verify. When trust
depends on personal relationships, capital moves; when it depends on documents the
borrower produces about itself, it does not. The core barrier is a **manual
verification bottleneck**: there is no independent, timely, affordable way to
confirm that the assets exist, are productive, and keep performing after the money
is deployed.

### 1.2 The first-order risk is invisible deterioration, not courtroom recovery

For this asset class the primary risk is not whether a claim can be enforced in
court. It is whether the underlying assets stay productive enough to keep
generating repayments — and whether deterioration becomes visible early enough to
act. Legal enforcement and recovery matter, but they are fallback protections an
investor hopes never to use. The real failure is portfolio deterioration that is
discovered too late.

---

## 2. Who feels it — the debt investor (primary)

### 2.1 Wants sustainable, competitive real-economy yield

The first target investor is a stablecoin allocator seeking yield that is both
competitive and sustainable — more than the thin returns of overcollateralized
crypto lending, and not dependent on token incentives that may not last. This first
customer sits inside a much larger eventual market: a globally distributed investor
base that onchain rails make able to reach real-economy credit directly.

### 2.2 Cannot underwrite or monitor what cannot be independently verified

An investor in New York, Berlin, or Singapore has no relationship with a lender in
Nairobi. They know the questions they need answered; what they lack is a trusted
way to keep getting those answers over time without relying on the borrower's own
PDFs, spreadsheets, and narrative updates. That is not enough to support conviction.

### 2.3 The consequence

Facing risk they cannot price, investors do one of three things: stay out of the
asset class entirely, demand a punitive return for unverifiable risk, or
concentrate only in managers they personally know. All three keep good loan books
underfunded and yield locked behind opacity.

### 2.4 The same gap on the micro-asset lender's side (secondary)

The micro-asset lender — the originator that borrows from the facility and in turn
lends to end consumers — feels the mirror image: real assets, repayment activity,
and operating data, but no credible way to present that performance to capital that
does not already trust it. The result is a narrow funding base, expensive capital,
and slow growth. The pain is not symmetric — the debt investor is the party TRD must
ultimately convince — but it is the same trust gap from both ends.

---

## 3. Why today's information fails

### 3.1 Self-reported, low-frequency, weakly verified, manual

The current private-credit workflow was built for relationship lending, not for
outside investors who need ongoing visibility after capital is deployed. Its
failure modes are consistent: the borrower is the main source of truth even though
it is also selling the debt; reporting is quarterly when operations move daily;
asset existence, usage, and repayment flows are hard to inspect independently; and
monitoring is manual, fragmented, and expensive.

### 3.2 Geography-level discounting instead of real underwriting

When investors lack reliable asset-level data, they substitute broad country and
sector assumptions for actual underwriting — pricing a whole geography as risky
rather than pricing the specific, performing loan book in front of them.

---

## 4. Evidence this is a real failure mode

### 4.1 What the last generation of RWA credit got wrong

This is not theoretical. RWA lending systems that relied on borrower-reported
information and delayed monitoring repeatedly failed when real-world conditions
deteriorated. The clearest reference is the Goldfinch experience: diligence built
on static, self-reported documents and social consensus rather than independent,
high-frequency operational data. Covenant breaches and portfolio deterioration
surfaced only after the damage was severe — at the point where investors were
forced to think about recovery rather than performance. The same pattern recurs in
traditional private credit through fake invoices, ghost collateral, and delayed
discovery. The lesson is consistent: weak, periodic, self-reported monitoring is
the root cause, and real yield, perfected security, and honest disclosure of loss
are what was missing.

---

## 5. What a credible solution must therefore do

Close the verification gap at its root: turn independent, third-party operating data
into a live, investor-readable view of portfolio performance — continuous rather than
quarterly, and verifiable rather than self-reported — so an investor can underwrite
and monitor the specific loan book in front of them instead of discounting a whole
geography or staying out of the asset class.

---

## 6. The thesis in one sentence

**If productive-asset performance can be made independently visible, debt investors
can fund micro-asset lenders more directly — with fewer intermediaries, lower cost,
and greater confidence.**
