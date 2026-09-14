# 2026-09-14 — A second instrument publishing the comparable the first was designed not to have

## What happened

Investors were to be added beside contributors, with the investor cap mirroring the contributor cap and using **the same `k` and the same `r`**. Simple, symmetric, and easy to explain to everyone involved.

It would have destroyed the argument the contributor leg rests on.

[Option-2 §5.2](../../token-system-design/paths/option-2-contingent-fee/README.md) defends `r` as an opening factor rather than an interest rate, and the first point in that argument is the load-bearing one: *"There is no principal. The contributor supplied work, not money. No loan, no principal, no interest."* On the investor leg there **is** principal, and the accrual is simple interest on a declining balance with payments split between interest and principal. That is correct and even useful there, because it produces a real arm's-length comparable.

The problem runs in the other direction. An investor cannot be asked for money without being told the return terms, and an FSMA *informatienota* compels the disclosure. So the design was one step away from **publishing, in a document written for the administration to read, the same named parameter, applied to capital, as a rate of return** — and thereby proving on the record that `r` is a capital return rate on the contributor leg too.

This is the second instance of the same shape. [2026-09-11 §4.1](../log/2026-09-11_cheap-share-ab-classes-sunset.md) found that adding a €100 investor class beside €1 contributor shares with equal per-share dividends made the statutes state that one contributor hour buys the same claim as €10 of investor capital: *"FPS do not have to build a comparable — the company wrote one."* Two instances make it a rule.

## Why it went wrong

The repo had been checking each instrument against the tax administration **on its own**. Both checks passed. The exposure was created by the two instruments being read **together**, which is exactly how they will be read: they sit in the same company, fund from the same pool, and in this design are coupled by one split formula.

An instrument's defence often consists of a fact that is **absent** — no principal, no euro price per hour, no unit conversion rate. Absence is not a property of one document. A second instrument can supply the missing term from the outside, and it is then in the file for good, written by the company itself, in a document it was legally obliged to publish.

The near-miss also had a second consequence that made it visible: the accountant instruction became self-contradictory. [annex-terms clause 27](../../token-system-design/paths/option-2-contingent-fee/annex-terms.md) says the contributor ceiling must **never** be booked as a liability, while a bond principal **must** be. One shared parameter name cannot carry two opposite booking instructions.

## Prevention rule

**Before adding any second instrument, list the facts the first instrument's defence relies on being absent, and check whether the second instrument supplies any of them.** Do this against the pair, never against each document alone, and include documents the company will be *compelled* to publish — an offering document, an *informatienota*, a prospectus, statutes — because those cannot be quietly omitted later.

Where a shared parameter would supply such a fact:

- **Give the second instrument its own named parameters.** The same values at launch are fine; the same *name* is not. Here `r_I` and `k_I` are separate policy parameters from `r` and `k`, defaulted to the same numbers, never described as one parameter and **never stated in the same document**.
- Say which leg each parameter belongs to wherever it appears.
- Treat a compelled disclosure as a publication. "We will not put it in marketing material" is not a control when a regulator requires the figure in a subscription document.

Two supporting checks worth running on any pair of instruments:

- **Compute the implied conversion between the two bases before shipping** — euros of capital per contributor hour, effective rate per year, whatever the pair makes computable. If the number is embarrassing or is one the design promised not to state, the pair publishes it whether or not any document does.
- **Check that per-instrument instructions to the accountant stay coherent.** If two instruments cannot both be booked as the design requires while sharing a name, they are not the same object and must not share the name.
