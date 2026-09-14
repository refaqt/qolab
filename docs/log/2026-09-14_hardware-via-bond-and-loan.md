# 2026-09-14 — Hardware for experiments: ordinary bond, company purchase, loan for use

**Role(s):** finance, business-dev, hardware

**Status:** Proposed — [ADR 2026-09-14](../decisions/2026-09-14_hardware-via-bond-and-loan.md). Design input for counsel, not a ruling and not an offer.

**Path:** [capped participating bond](../../token-system-design/paths/capped-participating-bond/README.md) (use of the investor leg); labour row unchanged — [option 2](../../token-system-design/paths/option-2-contingent-fee/README.md).

**Prevention rules applied:** [do not put a euro spot price on contribution credits](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not dress labour-quota cheap shares as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md) — nothing here is issued for work; [no multiple on the effort base](../mistakes/2026-09-14_10x-on-the-effort-base.md) — hardware does not enter `E`; [a second instrument must not publish the comparable the first is designed not to have](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md) — this is not a new instrument, but sizing a subscription from hours would publish a rate; [art. 53, 10° for the excess test](../mistakes/2026-09-14_wrong-article-for-excess-test.md) if deductibility of the equipment spend is later discussed.

## What happened

Asked how **hardware and equipment** for a contributor experiment are paid, without putting that cost on the labour row.

The sequence that was accepted as the working sketch:

1. A contributor wants or needs to run an experiment and to put money into hardware or equipment.
2. That person first **buys a bond**, like any other investor, on the [capped participating bond](../../token-system-design/paths/capped-participating-bond/README.md).
3. Refaqt then uses the money to **pay for the equipment** and **lends the equipment** to the contributor.

The bond is the existing investor instrument. The loan of the tool is a separate operational contract (a loan for use). There is no third token.

## Why the two naive answers fail

| Naive answer | Why not |
| --- | --- |
| Add the invoice to documented effort | `E` is hours times a frozen band, or a quoted effort. A machine's price next to hours is a euro rate. That is the comparable option 2 is designed not to have |
| Let the contributor buy and own the tool | The machine then sits outside the company. That fights the mission (shared access to manufacturing tools) and leaves the CV with no asset if the person leaves |

## Decisions

- Hardware for an accepted experiment is **company property**, funded as **capital**, not as labour. It does not enter `f`, `E`, `c`, or `p`, and it is not paid from `P^C_t`.
- **Same bond as any holder.** No hardware-bond class. No serial number in the offering document. The board may still buy a named tool after a subscription; that lives in the purchase file and the loan-for-use contract.
- **The contributor holds a bond, not the machine.** Exclusion on the labour side does not touch the bond. The company may recall the tool because it owns it.
- **Three documents stay apart:** contributor annex, bond offering, loan-for-use contract.
- Durable equipment is in scope. Consumable materials are not decided.

## Open Questions

- Benefit in kind (*voordeel van alle aard*) if the tool is used privately rather than for the experiment.
- VAT on the purchase and on a loan for use.
- Whether a modest hire is safer than a free loan.
- What happens if the tool is destroyed or consumed in the experiment.
- Recall, shared use, and where the tool may sit.
- Whether consumable materials are ordinary project cost or something else.

## Next Steps

- Counsel on the loan-for-use contract and the VAT / benefit-in-kind questions before any tool is bought this way.
- Do not offer a bond, and do not buy equipment against a promised subscription, until the investor leg is accepted.
