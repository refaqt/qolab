# Contract tokens — phantom, revenue-share, profit-share, warrants (open, not pursued)

**Status: open, not pursued.** Explored on 2026-09-10 as a way to pay contributors without a *bedrijfsrevisor* and without *inbreng in nijverheid*. The conclusion was that these are all **contracts** (available to a BV and a CV) and therefore all **fees**: they skip the revisor, they do not skip arm’s length, and they add nothing the live option-2 path does not already have. Kept on the record; no ADR. Design input, not a ruling.

Source: [2026-09-10 tokens not shares, to avoid the bedrijfsrevisor](../../../docs/log/2026-09-10_tokens-not-shares-avoid-revisor.md) (§1–§6; §7 became [structure A](../cash-shares-residual/README.md)). **Citation note:** where that log cites art. 49 for “not excessive” read art. 53, 10° WIB 92; art. 26 §1 does not add back an advantage taxed at the Belgian recipient ([review §3](../../../docs/log/2026-09-10_arms-length-10x-and-repo-review.md)).

**Prevention rules applied:** [no euro spot price](../../../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md); [no day-one multiple](../../../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md); [no *inbreng in nijverheid*](../../../docs/mistakes/2026-09-10_inbreng-in-nijverheid-plan-ahead.md).

---

## Instruments and what they are

| Instrument | Object | Legal form | Tax | Verdict |
| --- | --- | --- | --- | --- |
| **Revenue- / profit-share token** (contract) | Flow: this period’s pool | Contract; BV or CV | Fee (VAT 21% + professional income / VenB); deductible if art. 49 conditions hold; excess tested under art. 53, 10° | This **is** live option 2 with a different name |
| **Phantom shares / SAR** | Stock: company value | Contract; BV or CV | Grant ≈ invoice can be a cost; a later GA-set price with an issuer put is a discretionary bonus / related-party advantage, not a market gain | Not pursued; a CV has no market price |
| **NV *winstbewijzen*** | Statutory profit security | NV only (arts. 7:58–7:59); **not** a CV tool (art. 6:19); disputed in a BV | Usually dividends; taxed at grant on FMV if issued for work | Out of scope while the entity is a CV |
| **Warrants / options** | Right to buy shares | *Inschrijvingsrechten* BV/NV only; a CV cannot issue them; contractual option on existing shares possible | Optiewet lump sum for natural persons (60-day accept); contractor VAT on option FMV; cash exercise = *inbreng in geld* (no inbreng-revisor); netting with Refaqt = *inkoop van eigen aandelen* / fee | Only does equity work if a **third party** pays the exit; does not scale per contribution |

## Why not pursued

- There is no third tax box: a priced token for labour is a fee, not a dividend. Choosing not to deduct, paying VenB first and withholding 30% does not turn a `k × contribution` formula into a capital return.
- An effort ceiling still belongs on any labour-priced token unless a real third-party market prices the instrument.
- Grant-time taxation is accepted on this path, so its only advantage over option 2 (no revisor) is one option 2 already has.

## If ever revisited

- Confirm with counsel that QOLAB credits stay off the *effecten* registers and never convert into shares (art. 6:19, 6:39 WVV).
- DVB: grant-time VAT/PIT on a puttable phantom; fee vs disguised distribution when a member cashes above documented effort; Optiewet vs contractor VAT if warrants are used in a BV/NV vehicle.
- Do not add an issuer put at a GA-set share price. Do not net a warrant exercise against a buyback by Refaqt.
