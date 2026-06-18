# Design Decisions

TRD is shaped by a handful of deliberate design choices. They are what make the
product different from the private-credit and RWA models that came before it,
and each one exists to close a specific failure mode rather than to add features.

This document explains those choices in plain terms — what we decided, why, and
what it means for the people who use or fund the protocol. It is a companion to
the business plan: the business plan tells you what TRD is; this tells you why it
is built the way it is.

---

## D1. The primary collateral is the receivables pool; the bikes are secondary

**What we decided.** The facility is secured first and foremost by the lender's
**pool of outstanding loan receivables** — the live loan book — and it is that
pool that is registered. The financed motorbikes are **secondary collateral**.
So there are two tiers:

- **Primary — the revolving pool of registered receivables.** This is a
  *revolving* pool: as borrowers repay and the lender originates new loans, the
  pool continuously replenishes itself, so the security refreshes rather than
  runs down. Its live value at any moment — the **borrowing base** — is what
  actually backs the facility.
- **Secondary — the assets themselves.** The bikes are there to *perfect* the
  security under the Master Facility Agreement: they give the claim a
  registrable, enforceable foothold, and they are a worst-case fallback only.

**Why.** The receivables are the thing that actually produces an investor's
return — a stream of repayments from productive borrowers — and because the pool
revolves, the protection stays current instead of decaying like a static asset.
There is also simply no point in collecting bikes from people who are using them
to earn a living: it destroys the very productivity the loan depends on, and a
repossessed bike's resale price has nothing to do with what an investor is owed.
Recovery therefore runs through the receivables; seizing assets is a last-resort,
worst-case option, not the plan. And recovery in that worst case is the *lender's*
expertise — repossession and collections are their craft, on the ground, not
ours.

**What it means for you.**

- *If you are the debt investor:* your security is a live, revolving value that
  refreshes with the loan book — not a depreciating pile of hardware. Because the
  borrowing base changes every day, it is monitored every day; that continuous
  view is the whole point of the Risk Monitor, and it is why your coverage and
  loan-to-value are measured against the receivables pool.
- *If you are the micro-asset lender (the borrower):* the goal is never to come
  and take your bikes. The structure protects investors by holding a claim over
  the revolving book your servicing produces, while you keep running origination,
  collections, and recovery. **Our job is to monitor your operation at a high
  level, not to replace you** — repossession and recovery stay yours, because
  that is your expertise.

**What keeps it honest.** Because the collateral *is* the loan book, the figure
behind it has to be trustworthy. That number is not taken on the lender's word:
it is cross-checked against independent signals — real-world asset activity from
Bolt, the NTSA vehicle registry, and the M-Pesa payment rail that carries the
borrowers' repayments — so the reported receivables can be triangulated against
reality rather than self-attested. Verifiable performance, not a report the
borrower writes about itself.

---

## D2. The trust experience comes first; the trusted data pipeline comes last

**What we decided.** We build TRD in the opposite order to most fintech. The
first thing we build is the **trust experience**: the Risk Monitor front end, made
genuinely understandable, together with clear explainers of how the security and
the covenants protect an investor. The **trusted data pipeline** behind it —
extracting the operating data and pushing the attested aggregate to the trusted data
layer — together with the legal incorporation of the security structures, is built
*after* that, sequenced in the roadmap.

In other words, we make the trust **legible and convincing** before we make it
**operational**. Define the metrics, covenants, and security logic that actually
matter to an investor; show them clearly; and only then build the trusted data
pipeline and stand up the legal entities that enforce them.

**Why.** Trust is not a back-end feature you bolt on at the end — it is the whole
product, so it should be designed first. Most fintech builds the pipeline first
and the reporting last, which means the product ends up shaped by what the
pipeline happens to produce. We invert that so the product is driven by the trust
outcomes investors actually need. It also lets us validate the hardest question
early and cheaply: *does this trust model convince people?* — before incurring the
real cost of building the pipelines and legally incorporating the structures
behind them. An investor must first understand and believe the model; the trusted
data pipeline and the security structure are what make it operational and enforceable.

**What it means for you.**

- *If you invest:* you can see, read, and judge the trust model up front — what is
  measured, what the covenants do, how the security works — instead of waiting for
  a finished system to take on faith. The front end is the pitch.
- *If you are the lender:* the metrics and covenants are defined and agreed in
  plain view before anyone wires up your systems, so you know exactly what will be
  monitored and how it protects both sides.

**What comes later.** The technical implementation (data pipelines and the
verification stack) and the legal build (incorporating the security agent and
perfecting the claims) follow the validated design. Their sequencing lives in the
roadmap — deliberately downstream of getting the trust experience right.

---

## D3. For the debt investor: a revolving pool, not a long-term lockup

There is a simple trade-off between locking your capital and yield, because the
borrower lives on a longer time scale — their loans repay over months, not on
demand. Your capital sits in a revolving pool, and the more flexibility you want,
the more yield you give up: accept a lower return and you can withdraw earlier,
funded by a cash buffer the pool holds in reserve.

And in a crisis no one jumps the queue. Withdrawals run on a schedule, not
first-come-first-served, so every investor is treated equally — instead of the
fastest getting out while the rest are trapped, the dynamic that turns a wobble into
a run.

---

## D4. For the borrower: an open-ended facility that grows with you

**What we decided.** The facility is **open-ended**. Instead of a fixed-size term
loan you must renegotiate each time, it **grows with you** as trust is proven: more
capital can be deployed as your performance earns it, and your **borrowing cost can
fall as your track record builds** — all inside the original contract, without
going back to the market for a new deal each round.

**Why.** Re-approaching the market for every increment of capital is slow, costly,
and uncertain — and it punishes exactly the lenders who are performing well. An
open-ended, performance-linked facility does the opposite: it rewards a proven book
automatically with more capital and cheaper capital, and it lets a good lender
scale without re-papering a deal every time. The facility adapts to you, rather
than freezing you at the size and price of the day you signed.

**What it means for you (the micro-asset lender, the borrower).** One facility that
scales with you instead of a string of one-off raises. As you prove performance,
more capital unlocks and your cost of capital drops — automatically, within the
contract you already signed. You spend your time lending, not constantly
fundraising.

> Together, D3 and D4 are the two sides of the **Open-Ended Adaptive Debt
> Facility**: *open-ended* — it grows with the borrower (D4); *adaptive* — the rate
> moves with proven performance and demand, within agreed bounds, and liquidity is
> a predictable pool rather than a lockup (D3).

---

## D5. Monitoring is the headline protection; enforcement is the backstop

**What we decided.** TRD leads with **continuous monitoring** of portfolio
performance as the primary protection for investors. Legal enforcement and recovery
are a real but **secondary backstop** — the protection you hope never to use, not the
one you lead with.

**Why.** For this asset class the first-order risk is not whether a claim can be
enforced in court; it is whether the underlying assets stay productive enough to keep
generating repayments, and whether deterioration becomes visible early enough to act.
The failure that actually sinks portfolios is deterioration discovered too late, not
an unenforceable claim. So the product is built to make performance continuously
visible and to surface problems early; enforcement exists for the worst case and is
deliberately not the headline. This pairs with D1, where seizing assets is the
last resort, not the plan.

**What it means for you.**

- *If you are the debt investor:* your first line of defence is seeing the loan book
  deteriorate in time to act — not a courtroom remedy after the loss.
- *If you are the micro-asset lender (the borrower):* the relationship is
  monitoring-led, not enforcement-led — we watch performance at a high level, and the
  legal machinery is the fallback, not the daily mode.
