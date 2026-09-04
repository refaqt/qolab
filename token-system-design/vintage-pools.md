# Vintage pools instead of a unit certificate price

**Status: parked (complexity).** The idle-pool / no-unit-`v` analysis still stands. The lot / record-date / time-opened-cap packaging is too heavy to explain, so this is not the live spec. Do not replace it with cheap €1 shares — that route is a **dead-end** ([cheap-share-route.md](cheap-share-route.md), [ADR 2026-09-04](../docs/decisions/2026-09-04_cheap-share-route-dead-end.md)). Next pass is option 2 with less machinery.

Working design note on the idle-pool / wait-and-run problem that follows from `v = pool / certificates`, and on the gold rush that follows from a static `k×` ceiling. Companion to [token-system.md](token-system.md). This is **design input for counsel and an accountant**, not a ruling.

**Prevention rules applied:** [do not put a euro spot price on a growing pool](../docs/mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../docs/mistakes/2026-09-03_immediate-multiple-gold-rush.md). Token-engineering: do not publish ROI or a euro price on contribution credits; `r` and the lifetime multiple are a **fee cap**, not a yield; do not recreate a statutory surplus right via a token; labels do not take compensation outside VAT or income tax.

---

## Direct answers

| Question | Working answer |
| --- | --- |
| Does `v = pool / (# certificates issued)` cause everyone to wait, then withdraw at once? | **Yes**, if redeeming burns certificates and leftover pool stays in the pot. Waiting is then a free option on pool growth. When `v` finally looks like a “decent ROI”, exercise is simultaneous. |
| Does that trap a large unused pool and tax profit twice? | **Yes, if the money sits as retained earnings.** Refaqt pays VenB (20/25%) on profit that was never deducted. Later the contributor’s BV pays VenB again on what it receives. Immediate (same-year) distribution as a **deductible success fee** taxes the amount once, at the BV. That only happens if the money actually leaves (or is a certain payable) in the year the profit is earned. A low `v` that nobody will take prevents that. |
| Does `v = pool / (capped number of certificates)` fix it? | **No.** It moves the price into the cap. The GA then either picks `C` arbitrarily, or picks `C` so that `v` hits a target ROI on contribution points — which **is** a euro price on the points, the grant-time tax problem. |
| How do we get money out every year without pricing points or setting an ROI? | Stop defining a unit price on a **stock**. Each year the GA/board sets a **budget** `P_t` (this vintage only). Split `P_t` across eligible weights with **default-in**. Do not burn weights for taking the vintage. Leftover (opt-out, no invoice, over cap) goes to **operating reserves**, not back into a certificate pool. Weights keep participating until a **time-opened fee cap** is exhausted, a **sunset** hits, or the person exits. The implied €/certificate is a residue of a budget split, not a target, and is not published at mint. |
| Does a default lifetime multiple `k × effort` invite a gold rush when a fat year is forecasted? | **Yes**, if that `k×` is open from the first vintage. A short payback then still pays the long-risk multiple. **Open the extra multiple only while a contribution lot stays unpaid.** First eligible vintage: cap = 1× documented effort. Later vintages raise the cap only if principal is still unpaid, up to `k×`, then freeze once 1× is paid. Lots minted in year `Y` first sit in vintage `Y+1` (record date). |

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
     → mint lot L: weights Δp, documented effort E_L
        with p = c0 · c^k          (early-bird lives HERE only)
lots minted in fiscal year Y first sit in vintage Y+1   (record date)
each fiscal year t, after solvency:
     GA/board sets this vintage’s budget P_t
        P_t = min(policy % of profit or EBITDA,
                  optional revenue cap,
                  cash available after reserves / investment)
     for each eligible lot L:
        if first vintage for L:     cap_L = E_L
        else if paid_L < E_L:       cap_L = min(k × E_L, cap_L × (1+r))
        else:                       cap_L frozen
        remaining_L = cap_L − paid_L
     eligible = default-in among lots that have reached Y+1 (opt-out before a deadline)
     W_i = sum of weights of i’s eligible lots
     gross_i = P_t × W_i / Σ W_eligible
     pay_i   = min(gross_i, Σ remaining_L)
     allocate pay_i oldest unpaid lot first
     invoice in year t (VAT-exclusive) → pay
     leftover (opt-out, no invoice, over opened cap) → operating reserves
        NOT added to a future certificate pool
     W_i is NOT burned for taking the vintage
     retire a lot when its cap is exhausted, sunset hits, or the person exits
```

`k` in `k × E_L` is the lifetime **multiple cap** (GA/board policy). It is not the mint exponent in `p = c0 · c^k`. `r` is the per-unpaid-year opening factor, also policy, **not** a published return. Worked examples below use `k = 3`, `r = 0.20` — parameters, not a promise.

Do **not** book `cap_L` as a growing euro receivable. It is only a ceiling on a future contingent invoice. If `P_t` is zero, nothing is owed.

No `v` in the rules. No “how many certificates per euro”. The invoice is a share of **this year’s budget**, not a sale of certificates at a spot price.

### Why waiting stops being rational

| Old stock model | Vintage model |
| --- | --- |
| Burn now vs burn later at a higher `v` | Taking this vintage does **not** spend the right to the next one |
| Leftover raises tomorrow’s `v` | Leftover goes to **reserves** (Refaqt can invest). Waiting does not fatten your pot |
| Opt-in: you can sit out until `v` is fat | **Default-in:** sitting out is an opt-out, and that slice is **forfeited** |
| Pool is a growing stock | `P_t` is a **flow**. Miss year t, that flow is gone |

Time value of money then says: take each vintage up to the **opened** cap. That is the opposite of a run. Waiting does not fatten tomorrow’s pot; it only opens more cap if this lot is still unpaid.

### Why this does not price contribution points

Two different GA jobs get confused:

| Job | Legitimate? | What it sets |
| --- | --- | --- |
| **Budget** `P_t` | Yes. Same as approving a bonus / contractor-success pool. Solvency, reserves, reinvestment. | How much cash **leaves the CV this year** |
| **Price** `v` or `N_cap` to hit an ROI on points | No. That is a euro quote on the mint. | What one point is “worth” |

Ex-post return still **scales with how well Refaqt is doing** (goal 4): good years have larger `P_t`, so opened caps fill faster. They do **not** jump to `k×` on the first fat invoice. That is not the GA targeting `v* = ROI × points / certificates`. If Refaqt does poorly, vintages are small or skipped and the opened cap is never reached. The extra multiple is compensation for **unpaid waiting**, not a default windfall.

Do not publish `P_t / Σ W` as a certificate price. The contributor sees an **invoice amount**. If someone divides it by their weight, that is hindsight on a budget split, not a running FX rate at mint.

### Vacuuming without a euro rate `w`

The spreadsheet used `w` so a lone offerer could not empty the pool. Default-in does that job without a price: the denominator is (almost) **everyone**, so one person cannot vacuum. The opened cap is a second brake. You do not need leftover-in-pool or a bonding-curve FX rate for that behaviour.

### Time-opened cap vs a static `k×` vs “ROI pricing”

A **static** lifetime ceiling `k × documented effort`, open from the first vintage, is a fee cap — and a gold-rush magnet. Anyone who can forecast a large `P_t` contributes to grab that multiple in one short payback. The mint curve only changes **weight**; a late lot still mints `Δp` and races to the same `k×`.

**Replacement:** track **lots** (a mint event / contribution year), not one blended ceiling per person. Otherwise last week’s work inherits five years of “waited” cap.

For each lot `L` with documented effort `E_L` (hours × frozen contractor band, or a task estimate):

1. **Record date.** Lots minted in fiscal year `Y` first sit in vintage `Y+1`.
2. **Opened cap starts at 1×.** At first eligibility: `cap_L = E_L`.
3. **The extra multiple opens only while principal is unpaid.** At the start of each later vintage, if `paid_L < E_L`: `cap_L = min(k × E_L, cap_L × (1+r))`. If `paid_L ≥ E_L`, **freeze** `cap_L`. No trailing bonus after a short payback.
4. **Payout:** `pay_i = min(gross_i, Σ remaining_L)` with `remaining_L = cap_L − paid_L`, oldest unpaid lot first.

That is still not setting `v` so that people *realise* a target ROI:

- The opened cap is an **upper bound**. Actual pay can be less. If `P_t` is zero, nothing is owed.
- It is not used to compute a unit price or to choose `N_cap`.
- It exists so Refaqt cannot be drained without bound, so a short engagement cannot extract the long-risk multiple, and so the fee stays in shouting distance of the work (arm’s length / art. 49 WIB 92).
- Do not describe `r` as interest on a balance. Do not book a growing receivable.

Sunset `T` can stay as a **second** bound: lots lapse after `T` vintages. It does not replace the opened cap; a fat year inside `T` would still fill a static `k×`.

Unlimited lifetime share of every future `P_t` (no opened cap, no sunset, no burn) is an equity-like stream. Do not leave that open.

**Rejected as the default** (they do not tie the multiple to payback, or they reprice points):

| Alternative | Why not |
| --- | --- |
| Seniority waterfall (late lots get nothing from a pot earned before they joined) | Punishes people you want when a product takes off. New needed work should still be able to take **1×**. |
| Fixed annual drip (`pay ≤ 0.3×` per year) | Stretches a jackpot but still pays `k×` if several fat years are forecasted. |
| Coverage-based mint (fewer weights when forecasted `P` / unpaid caps is high) | Reprices points; same family as the rejected `N_cap` / ROI dial. |
| Age-opens-cap even after repayment | Still pays `k×` over following fat years after a one-year payback. |

Optional later hardening (only if junk-volume dilution shows up): split `P_t` into a junior slice (everyone, toward 1×) and a senior slice (lots still unpaid after year one). Not in this iteration.

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

Those three invoices (€1,000 + €2,500 + €10,000 = €13,500) assumed a static ceiling above that total. With a time-opened cap the third year cannot pay the long-risk multiple after a short payback. The next three stories use `k = 3`, `r = 0.20`, documented effort `E = €5,000` per person, half of profit into `P_t`.

### Sudden success (short payback)

Ten people, each one lot minted in year 0, first eligible in year 1. Year 1 profit before the reward is €200,000, so `P_t = €100,000`. Equal weights.

| | Static `k×` (old ceiling) | Time-opened cap |
| --- | --- | --- |
| Opened cap at year 1 | €15,000 | €5,000 (1×) |
| Gross each | €10,000 | €10,000 |
| Invoice each | €10,000 (2×) | €5,000 (1×) |
| Leftover of `P_t` → reserves | €0 | €50,000 |
| Cap afterwards | €5,000 still open | **frozen** at €5,000 |

No 3× jackpot. Surplus stays at Refaqt to invest. A later fat year pays these lots nothing more.

### Long unpaid wait, then success

Same ten lots, `E = €5,000`. Lean years, then a fat one. Cap opens only because principal is still unpaid.

| Vintage | `P_t` | Cap at start (each) | Invoice each | Paid to date | Unpaid principal? |
| --- | --- | --- | --- | --- | --- |
| 1 | €2,000 | €5,000 | €200 | €200 | yes |
| 2 | €5,000 | €6,000 | €500 | €700 | yes |
| 3 | €100,000 | €7,200 | €6,500 | €7,200 | no (freeze) |

Lifetime multiple is **1.44×**, not 3×: two unpaid openings at 20%, then the fat year fills the opened cap. Four vintages with `P_t = 0` then a fat year would open `€5,000 × 1.2^4 ≈ €10,368` (2.07×). About six unpaid openings after the first vintage reach the `k = 3` cap. That is the risk premium for waiting.

### Forecasted boom, gold rush

Ten veterans minted in year 0 (`E = €5,000`). Dana works in year 1 after the boom is visible (`E = €5,000`), so her lot first sits in vintage 2 (record date). Equal weights (1,000 each).

| Vintage | Who is eligible | `P_t` | Veteran invoice | Dana invoice |
| --- | --- | --- | --- | --- |
| 1 | 10 veterans | €10,000 | €1,000 (cap still €5,000) | not eligible |
| 2 | 10 veterans + Dana | €100,000 | €5,000 (cap opened to €6,000; remaining €5,000) | €5,000 (first vintage, cap €5,000) |

Dana’s sure bet is **1×**, then freeze — getting paid for needed work, not `k×`. Veterans who were still unpaid get the one opening they waited for (lifetime €6,000 = 1.2×), not a 3× grab. Leftover of vintage 2: `€100,000 − 10 × €5,000 − €5,000 = €45,000` → reserves.

Under a static `k×` with no record date, Dana would have shared vintage 1 or taken `min(gross, €15,000)` in the fat year.

---

## 4. Option 1 vs option 2 under vintages

Vintages solve **idle capital** and **runs** for either tax box. They solve **double VenB** only if the vintage is a **same-year deductible cost**.

| | Option 2 (recommended wrapper for this flow) | Option 1 (genuine dividend on a share class) |
| --- | --- | --- |
| What `P_t` is | Contractual success-fee budget, solvency-checked | After-tax profit the GA distributes under WVV tests |
| Same-year invoices | Refaqt deducts; BV pays VenB once | Refaqt already paid VenB; then 30% WHT (or BV tax without DBI) |
| Default-in | Needed so the cost actually exists in year t | A declared dividend is attributed even if cash is later — different machine |
| Allocation key | Contribution weights (labour) | Must look like **capital / membership**, not points, or it recharacterises |
| Opened fee cap | Supports “fee for work”; delay before `k×` is more arm’s-length than an immediate windfall | A labour ceiling on a dividend is a smoking gun that it is not a dividend |

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
| Time-opened cap on unpaid lots | Waiting-is-rewarded as a second early-bird |
| | Static `k × effort` open from the first vintage |

Early-bird stays in **Δp**. A second early-bird in a rising `v` is the investment story.

---

## 6. Implementation defaults (until counsel)

1. One instrument: non-transferable **weights** (call them certificates internally if you want; they must not have a euro par or a public `v`).
2. **Vintage budget** `P_t`, not a stock pot. Policy `%` and reserves are GA/board; not an automatic 10% of turnover.
3. **Default-in**, short opt-out. No invoice by the stated date → that allocation **forfeits to reserves**.
4. **No burn** for taking a vintage. Retire a lot when its opened cap is exhausted, sunset hits, or the person exits.
5. **Time-opened fee cap** per lot (1× at first eligibility; opens with `(1+r)` only while principal is unpaid, up to `k×`, then freeze). **Record date:** lots minted in year `Y` first sit in vintage `Y+1`. Sunset `T` may sit on top; it does not replace the opened cap.
6. Leftover and unallocated profit are **Refaqt’s to invest**. Earmarked `P_t` is paid in year t.
7. Option 2 wrapper: dienstenovereenkomst + QOLAB annex; invoice is the consideration. Do not mix a dividend story on the same instrument.
8. Still a **pre-legal spec**. DVB questions to add: (e) same-year deduction of a default-in vintage; (f) forfeiture of opt-out / uninvoiced slices; (g) opened cap vs sunset as the bound; (h) time-opened fee cap vs interest / receivable.

Until those sign-offs exist, do not promise holders a unit price, a target ROI, a pot that “will be worth more if you wait”, or a default `k×` on a short payback.
