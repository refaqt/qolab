# Scoped royalty / Cred-weighted euro-par Q (viable path)

**Status: viable; proposed base for the large upside.** Not the live spec. [ADR 2026-09-14 (two bases, Proposed)](../../../docs/decisions/2026-09-14_two-bases-10x-off-effort.md) makes this path — or [cash shares](../cash-shares-residual/README.md) — the place where a 10×-shaped return on a contribution is an ordinary outcome, while [option 2](../option-2-contingent-fee/README.md) stays at or near 1× on documented effort. Nothing here is accepted until counsel and a DVB prefiling have seen it. Design input, not a ruling.

Source log: [2026-09-10 Cred-weighted euro-par Q](../../../docs/log/2026-09-10_cred-value-q-euro-par.md). Why it answers the 10× question: [2026-09-10 review §1.5](../../../docs/log/2026-09-10_arms-length-10x-and-repo-review.md).

**Prevention rules applied:** [no euro spot price on a growing pool](../../../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md) — this path **accepts** `1 Q = €1` and therefore **accepts priced consideration**; it does not try to defer tax; [no day-one lifetime multiple](../../../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md) — no hours cap is a remaining arm’s-length question, not a reason to call this labour-hours; [no labour-quota dividend dressing](../../../docs/mistakes/2026-09-04_cheap-share-euro-par.md); [no multiple on the effort base](../../../docs/mistakes/2026-09-14_10x-on-the-effort-base.md).

---

## Mechanism

1. **Contract up front:** *dienstenovereenkomst* or IP licence + Cred annex. The contributor opts in; compensation is a Cred-weighted share of a defined royalty pool, redeemable **with Refaqt**.
2. **Contribution** (a design, a tool, a file) goes onto the Refaqt repo. **No timesheet.** A value-based algorithm (SourceCred-style graph score, “Cred”) computes each contributor’s share. Cred is the governance of the split, not the tax box.
3. **Pool:** each period a royalty pool is formed from **the revenue of the products that embody the contributions in that graph** (the scoping rule, below), after the same solvency waterfall as `P_t`. The pool mints that many **Q** at **`1 Q = €1`**.
4. **Allocation:** Q are allocated by Cred share. Allocation is the taxable moment for this path (a hard par is ascertainable value).
5. **Cash-out:** the contributor BV **invoices** Refaqt (or Refaqt self-bills) — description: revenue share / success fee / licence — design X — Cred period T; VAT extra; Q cancelled on payment. Never a nominal €1 invoice for 15,000 Q.
6. Repeat each period. Upside is **more Q** when Cred is high and the pool is large, never Q appreciating.

## The scoping rule (what makes this the answer to the 10× question)

An **uncapped** Cred share of **all** Refaqt revenue is residual-claimant-shaped: a foundational node that keeps taking a slice of every future euro looks like equity, and the [2026-09-10 log](../../../docs/log/2026-09-10_cred-value-q-euro-par.md) already named that as the aggressive end. The fix is to **scope the royalty to the products that use the contribution**:

- The comparable is then a **royalty rate** for engineering / design IP (typically low single-digit % of net sales of the products concerned), not hours × rate. Nobody divides a royalty by the designer’s hours; a 10× lifetime return on a five-minute design is an ordinary outcome of an ordinary royalty. Arm’s length (art. 53, 10° WIB 92 for the excess, art. 49 for the conditions; art. 26 §1 is neutral for a taxed Belgian recipient) is tested against **that** comparable.
- Scope follows the product graph: a contribution shares in the products that embody it (including forks and dependencies that ship with them), not in unrelated turnover. The mapping product → contribution set is a governance object (the same graph that computes Cred), written into the annex.
- A policy rate cap on the pool (e.g. “at most x% of net sales of the products concerned”) replaces the hours ceiling as the brake. It is a royalty rate, not a multiple of effort.

Two bases, two tests: time-based work on option 2 (comparable: hours × band, target ~1×); designs and outputs on this path (comparable: royalty rate). Never both on one instrument, never a Cred share that is secretly `f(hours)`.

## What this path accepts and what it refuses

| Accepts | Refuses |
| --- | --- |
| VAT + professional income / VenB in the BV **at allocation** of Q (published par) | Grant-time deferral (that is option 2’s hypothesis, not this one) |
| That the money is a **fee / royalty / IP sale** — a supply to Refaqt with a direct link (WBTW arts. 22, 26; Tolsma) | “Not labour, so no VAT”; the Bitcoin-mining analogy (there is an identifiable customer) |
| Cred as allocation key; a GA dispute process for weights | A GA override that reads as a discretionary bonus |
| Issuer-only redemption; Q cancelled on payment | A peer market in Q at par (e-money-shaped; MiCA) |
| More Q when the pool is large | Q “rising 20×” — a par token cannot; a 20× needs a different instrument and brings art. 53, 10° / art. 26 fully back |

## How it sits beside the live spec

| | Option 2 (live) | This path |
| --- | --- | --- |
| Input | Hours | Value (Cred) |
| Split key | `p` weights | Cred share |
| Brake | Opened cap on documented effort | Royalty scope + rate cap |
| Tax posture | Defer to invoice (hypothesis) | Priced at allocation (accepted) |
| Where the large upside lives | Not here (target ~1×) | Here (royalty outcome) |
| Contract | *dienstenovereenkomst* + QOLAB annex | IP licence or *dienstenovereenkomst* + Cred annex |

Options recorded in the source log: **replace** option 2 for design contributions, sit **beside** it (designs here, time-based work there — the two-bases reading), or drop. The ADR takes the second.

## Open questions

- Counsel / DVB: characterise the Cred allocation as a contractual success fee or IP royalty; confirm not a dividend when the key is Cred (**(b)** as applied here).
- Time of supply: allocation of Q vs invoice, given the published par (**(c)** as applied here; art. 22bis WBTW backstop).
- **(s)** Scoped royalty: is a royalty scoped to the products embodying the contribution, Cred-allocated, a deductible fee at arm’s length without an hours comparable; what scoping and what rate cap are required versus an uncapped share of all `P_t`.
- Self-billing vs contributor-issued invoice; the natural person without a BV (see the [adoption constraint](../../README.md#adoption-constraint)).
- Cred algorithm governance: who may change weights, dispute process, what the product → contribution mapping looks like in the annex.
- Whether the Refaqt sales entity and the pool entity are the same legal person (a royalty across entities is a supply between them).
- **Rename.** The [supplier-network access token](../q-supplier-access/README.md) also uses the letter Q. Proposal: Q stays with this euro-par coupon (it is the one that behaves like a currency-denominated voucher); the access token takes another name before any spec draft.

## Next steps

- If pursued: draft the licence / Cred annex with a worked number (e.g. 15,000 Q from a €100,000 product-scoped pool, a year with an empty pool, a year with a large foundational Cred share) and take **(b)**, **(c)**, **(s)** to prefiling together with the option-2 box.
- Do not promise a 20× or an ROI on Q. Do not describe Q as “not labour so no VAT.” Do not merge the two Q sketches.
