# Vintage pools instead of a unit certificate price

Working design note on the idle-pool / wait-and-run problem that follows from `v = pool / certificates`. Companion to [token-system.md](token-system.md). This is **design input for counsel and an accountant**, not a ruling.

**Prevention rules applied:** none yet in `docs/mistakes/` at the start of this note (folder was empty). Token-engineering rules that apply: do not publish ROI or a euro price on contribution credits; do not recreate a statutory surplus right via a token; labels do not take compensation outside VAT or income tax.

---

## Direct answers

| Question | Working answer |
| --- | --- |
| Does `v = pool / (# certificates issued)` cause everyone to wait, then withdraw at once? | **Yes**, if redeeming burns certificates and leftover pool stays in the pot. Waiting is then a free option on pool growth. When `v` finally looks like a “decent ROI”, exercise is simultaneous. |
| Does that trap a large unused pool and tax profit twice? | **Yes, if the money sits as retained earnings.** Refaqt pays VenB (20/25%) on profit that was never deducted. Later the contributor’s BV pays VenB again on what it receives. Immediate (same-year) distribution as a **deductible success fee** taxes the amount once, at the BV. That only happens if the money actually leaves (or is a certain payable) in the year the profit is earned. A low `v` that nobody will take prevents that. |
| Does `v = pool / (capped number of certificates)` fix it? | **No.** It moves the price into the cap. The GA then either picks `C` arbitrarily, or picks `C` so that `v` hits a target ROI on contribution points — which **is** a euro price on the points, the grant-time tax problem. |
| How do we get money out every year without pricing points or setting an ROI? | Stop defining a unit price on a **stock**. Each year the GA/board sets a **budget** `P_t` (this vintage only). Split `P_t` across eligible weights with **default-in**. Do not burn weights for taking the vintage. Leftover (opt-out, no invoice, over cap) goes to **operating reserves**, not back into a certificate pool. Weights keep participating until a **fee ceiling** or a **sunset**. The implied €/certificate is a residue of a budget split, not a target, and is not published at mint. |

---

## 1. Why both formulas fail

They are two ways to write a **spot price per certificate** on a growing pot.

```
v_issued = P / N_issued          # price rises as the pool fills
v_capped = P / N_cap             # GA chooses N_cap ⇒ GA chooses v
```

Cash-out is then `euros = certificates_offered × v`, and offered certificates are **burned**.

### Wait-and-run (`v = P / N_issued`)

A holder compares:

- Withdraw now: burn the certificates, receive today’s small `v`.
- Wait: keep the certificates, `P` grows (new profits + leftover from people who also wait), `v` rises, then burn later.

There is no carrying cost and no lapse. The rational policy is to wait until `v` is “worth it” (a target ROI on the work). Everyone sees the same `v`, so they wait for the same threshold and then **all** offer. That is a run: a large pool must sit untouched until that day, and then it leaves at once.

That is the same economics as a DAO ragequit price `treasury / shares` with no ragequit penalty, not a wage or a success fee.

The leftover rule in [token-system.md](token-system.md) (“unoffered certificates leave their share in the pool”) **feeds** this option: leftover today is a higher `v` tomorrow.

### Double VenB is a timing-and-box problem

Compare **€10,000 of CV earnings** before the reward, paid to contributors who invoice through a BV (the case you described).

| Path | Refaqt VenB | BV VenB | Combined on this €10,000 |
| --- | --- | --- | --- |
| Same-year **deductible fee** (option 2, money actually allocated and invoiced) | €0 on this slice | 20/25% | **once**, at the BV |
| Money sits as **retained earnings**, later paid as a **dividend** (option 1) | 20/25% then | 20/25% again unless DBI applies (a tiny membership share usually does **not**) | **twice** |
| Money sits as retained earnings, later paid as a **fee** | 20/25% in the earning year; deduction only later, and only against later profit | 20/25% on the fee | **twice in cash terms** if the later deduction cannot fully offset; at best a **timing** leak (the pool that can be paid is the after-tax remainder) |

“If we could distribute immediately, this would not be the case” is true **only for option 2**, and only if distribution (or a certain payable) happens in the **same fiscal year** as the profit. Option 1 always pays VenB at Refaqt first; that is the dividend box, not a waiting bug.

`v = P / N` with leftover-in-pool **prevents** the same-year fee: nobody invoices at a low `v`, so the slice is never a cost of year T. The idle pool is not a treasury someone else can use either: if it is earmarked for certificates, Refaqt should not spend or invest it as free cash; if it is not earmarked, the certificates are an even purer option on future surplus.

A current-account (book the allocation as debt, keep the cash at Refaqt) would let Refaqt invest, but it crystallises a **euro receivable** for the BV — income without cash — and turns contributors into lenders. Do not use that as the default.

### Capped `N` is price-setting

`v = P / N_cap` with `N_cap > N_issued` means each issued certificate is worth more, and `(N_cap − N_issued) / N_cap` of the pool stays with the house.

Who chooses `N_cap`?

| How `N_cap` is chosen | What it is |
| --- | --- |
| GA picks a number | Arbitrary. Governance fights, fairness disputes, and still a published €/certificate once `P` is known. |
| Chosen so holders get a target ROI on contribution points | **Pricing the points.** `N_cap` is just `P / v*` with `v*` backed out from `k × points`. That is the grant-time mark-to-market [token-system.md](token-system.md) already rejected (`w = dc/dp` in euros). |
| Fixed max supply announced in advance | Still a price `P / N_cap` that **rises with the pool**, so wait-and-run remains if burn-on-withdraw remains. If `N_cap` is small, `v` is high from day one (ascertainable value). If `N_cap` is huge, `v` stays tiny and nobody withdraws. |

You cannot use the denominator as a dial for “fair ROI” without putting a euro value on contribution points. That coupling is the thing to refuse, not to tune.

---

## 2. The design move: vintages, not a stock price

Keep the mint. Drop the **redemption price**. Change the **time structure** of the pool.

```
work → contribution points c
     → mint certificates / weights  Δp = p(c_new) − p(c_old)
        with p = c0 · c^k          (early-bird lives HERE only)
each fiscal year t, after solvency:
     GA/board sets this vintage’s budget P_t
        P_t = min(policy % of profit or EBITDA,
                  optional revenue cap,
                  cash available after reserves / investment)
     eligible = default-in (opt-out before a deadline)
     gross_i = P_t × W_i / Σ W_eligible
     pay_i   = min(gross_i, remaining_ceiling_i)
     invoice in year t (VAT-exclusive) → pay
     leftover (opt-out, no invoice, over ceiling) → operating reserves
        NOT added to a future certificate pool
     W_i is NOT burned for taking the vintage
     retire W_i only when the ceiling is exhausted, sunset hits, or the person exits
```

No `v` in the rules. No “how many certificates per euro”. The invoice is a share of **this year’s budget**, not a sale of certificates at a spot price.

### Why waiting stops being rational

| Old stock model | Vintage model |
| --- | --- |
| Burn now vs burn later at a higher `v` | Taking this vintage does **not** spend the right to the next one |
| Leftover raises tomorrow’s `v` | Leftover goes to **reserves** (Refaqt can invest). Waiting does not fatten your pot |
| Opt-in: you can sit out until `v` is fat | **Default-in:** sitting out is an opt-out, and that slice is **forfeited** |
| Pool is a growing stock | `P_t` is a **flow**. Miss year t, that flow is gone |

Time value of money then says: take each vintage until the ceiling. That is the opposite of a run.

### Why this does not price contribution points

Two different GA jobs get confused:

| Job | Legitimate? | What it sets |
| --- | --- | --- |
| **Budget** `P_t` | Yes. Same as approving a bonus / contractor-success pool. Solvency, reserves, reinvestment. | How much cash **leaves the CV this year** |
| **Price** `v` or `N_cap` to hit an ROI on points | No. That is a euro quote on the mint. | What one point is “worth” |

Ex-post return still **scales with how well Refaqt is doing** (goal 4): good years have larger `P_t`, so the same weights invoice more, and hit the ceiling sooner. That is not the GA targeting `v* = ROI × points / certificates`. If Refaqt does poorly, vintages are small or skipped and the ceiling is never reached.

Do not publish `P_t / Σ W` as a certificate price. The contributor sees an **invoice amount**. If someone divides it by their weight, that is hindsight on a budget split, not a running FX rate at mint.

### Vacuuming without a euro rate `w`

The spreadsheet used `w` so a lone offerer could not empty the pool. Default-in does that job without a price: the denominator is (almost) **everyone**, so one person cannot vacuum. The personal ceiling is a second brake. You do not need leftover-in-pool or a bonding-curve FX rate for that behaviour.

### Ceiling vs “ROI pricing”

A **lifetime euro ceiling** `k × documented effort` (hours × frozen contractor band, or a task estimate) is a **fee cap** at payout. It is what makes option 2 look like a capped success fee rather than unlimited profit participation.

That is not the same as setting `v` so that people *realise* a target ROI:

- The ceiling is an **upper bound**. Actual pay can be less.
- It is not used to compute a unit price or to choose `N_cap`.
- It exists so Refaqt cannot be drained without bound, and so the fee stays in shouting distance of the work (arm’s length / art. 49 WIB 92).

If even a reference rate in the ceiling feels like “pricing points”, use a **sunset** instead or as well: weights minted in year `Y` participate in vintages `Y … Y+T` and then lapse. No euro in the formula. Lifetime euros are then bounded only by how large those `T` budgets were — weaker for option-2 characterisation, cleaner if the political constraint is “no rate on points”.

Unlimited lifetime share of every future `P_t` (no ceiling, no sunset, no burn) is an equity-like stream. Do not leave that open.

---

## 3. Worked numbers

Ten people, equal weights (1,000 each, 10,000 outstanding). Policy: half of profit into `P_t`, half reinvested at Refaqt. Profits before the reward: year 1 €20,000; year 2 €50,000; year 3 €200,000.

### Stock price `v = pool / outstanding`, leftover stays, burn on withdraw

| Year | New money into the pot | Pool if nobody withdrew | `v` | Typical behaviour |
| --- | --- | --- | --- | --- |
| 1 | €10,000 | €10,000 | €1.00 | Nobody burns (“ROI is a joke”) |
| 2 | €25,000 | €35,000 | €3.50 | Still wait |
| 3 | €100,000 | €135,000 | €13.50 | If this is finally “decent”, **everyone** burns; the pot empties at once |

Until year 3 the €135,000 is earmarked and idle. If it sat as retained earnings, Refaqt already paid VenB on the underlying profit. The BVs are taxed when they finally invoice. That is the double layer.

### Vintage split, default-in, no burn, leftover to reserves

| Year | `P_t` | Each invoice | Refaqt reinvests (the other half) | Trapped certificate pool |
| --- | --- | --- | --- | --- |
| 1 | €10,000 | €1,000 | €10,000 | €0 |
| 2 | €25,000 | €2,500 | €25,000 | €0 |
| 3 | €100,000 | €10,000 | €100,000 | €0 |

After three years each person has received **€13,500** — the same cash as splitting the accumulated €135,000 once — but (a) they received it as they went, (b) Refaqt invested **€135,000** of unallocated profit along the way instead of parking a certificate pot, (c) if these invoices are option-2 costs of each year, that €135,000 of fees reduced VenB in those years and is taxed once at the BVs.

If one person opts out in year 1, their €1,000 goes to **reserves**, not to year 2’s `P_t`. They cannot wait for a fatter `v`.

Implied `P_t / 10,000` was €1, €2.50, €10. Those numbers are not a mint-time price and are not a GA ROI target.

---

## 4. Option 1 vs option 2 under vintages

Vintages solve **idle capital** and **runs** for either tax box. They solve **double VenB** only if the vintage is a **same-year deductible cost**.

| | Option 2 (recommended wrapper for this flow) | Option 1 (genuine dividend on a share class) |
| --- | --- | --- |
| What `P_t` is | Contractual success-fee budget, solvency-checked | After-tax profit the GA distributes under WVV tests |
| Same-year invoices | Refaqt deducts; BV pays VenB once | Refaqt already paid VenB; then 30% WHT (or BV tax without DBI) |
| Default-in | Needed so the cost actually exists in year t | A declared dividend is attributed even if cash is later — different machine |
| Allocation key | Contribution weights (labour) | Must look like **capital / membership**, not points, or it recharacterises |
| Ceiling | Supports “fee for work” | A labour ceiling on a dividend is a smoking gun that it is not a dividend |

If certificates are minted from **contribution points**, option 1 remains the weak characterisation ([token-system.md](token-system.md) §3). Vintages do not fix that. They only stop you from having to choose between a trapped pool and a GA-set ROI price.

**Tightrope (option 2, for the accountant):** too discretionary → cannot provision, VenB first, waiting returns. Too automatic → looks like a profit right. Practical pattern: the **regulation** states the waterfall in advance; the board **shall** open a vintage when the waterfall is positive unless solvency forbids; then named persons have a payable; invoice in the same fiscal year. Bound discretion, not a statutory claim on surplus, not a share.

VAT: invoice in year t; pool specified **VAT-exclusive** (already in the 2026-09-02 ADR).

---

## 5. What to keep from the 2026-09-03 iteration

| Keep | Drop |
| --- | --- |
| Mint `p = c0 · c^k` as a **weight** function | `w = dc/dp` in euros, at mint or at payout |
| Non-transferable, off-chain, no peer market | `v = pool / N_issued` as the burn FX |
| GA/board sets the **size** of each pool | `v = pool / N_cap` or any ROI-calibrated cap on `N` |
| Members for **governance** (small cash share) | Leftover recycling into the certificate pot |
| Employees on euro payroll | Opt-in + burn-on-withdraw as the default cash-out |
| | Waiting-is-rewarded as a second early-bird |

Early-bird stays in **Δp**. A second early-bird in a rising `v` is the investment story.

---

## 6. Implementation defaults (until counsel)

1. One instrument: non-transferable **weights** (call them certificates internally if you want; they must not have a euro par or a public `v`).
2. **Vintage budget** `P_t`, not a stock pot. Policy `%` and reserves are GA/board; not an automatic 10% of turnover.
3. **Default-in**, short opt-out. No invoice by the stated date → that allocation **forfeits to reserves**.
4. **No burn** for taking a vintage. Retire on ceiling, sunset, or exit.
5. **Ceiling** (`k × documented effort`) and/or **sunset** (`T` vintages). Pick at least one.
6. Leftover and unallocated profit are **Refaqt’s to invest**. Earmarked `P_t` is paid in year t.
7. Option 2 wrapper: dienstenovereenkomst + QOLAB annex; invoice is the consideration. Do not mix a dividend story on the same instrument.
8. Still a **pre-legal spec**. DVB questions to add: (e) same-year deduction of a default-in vintage; (f) forfeiture of opt-out / uninvoiced slices; (g) ceiling vs sunset as the bound.

Until those sign-offs exist, do not promise holders a unit price, a target ROI, or a pot that “will be worth more if you wait”.
