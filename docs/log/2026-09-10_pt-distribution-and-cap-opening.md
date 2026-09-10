# 2026-09-10 — `P_t` distribution and cap opening (discussion)

**Role(s):** finance, business-dev

**Prevention rules applied:** [do not put a euro spot price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not treat remaining `p` as remaining euros](../mistakes/2026-09-04_cheap-share-euro-par.md); [do not keep paid-off `p` as seniority](../mistakes/2026-09-08_unburned-p-after-cap.md).

Companion DVB catalog: [token-system-design/dvb-questions.md](../../token-system-design/dvb-questions.md).

## What happened

Design discussion (2026-09-09 → 2026-09-10) of how to **split yearly `P_t`** and **open the invoice cap**, compared with the live / parked option-2 path. Iterated a contributor-proposed formula, dropped loan-shaped `F`/`O` amortization, worked numerical lots-vs-blend and `Y` vs `Y+1` cases, then a filing conclusion: **option 2, lots, 1× in the first unpaid year, path to 10× at ~10 unpaid years, freeze after that lot’s 1× is paid.** No new ADR; tax characterisation remains a DVB hypothesis. Wrote the DVB catalog **(a)–(p)**.

---

### Round 1 — first proposed formula (proportional `F` / `O`)

Intent: parent project (sub-project pool later “the same way”). Monthly log; yearly success-fee pot.

| Symbol | Proposed meaning |
| --- | --- |
| `c_i` | `100 × hours` |
| `p_i(m)` | Bonding-curve mint that month |
| `P_i` | Stock of `p`; `P_i(m) = P_i(m-1) + p_i(m)` |
| `f_i` | Hours × contributor rate |
| `F_i` | Running “principle” of the ceiling, **reduced** by payouts |
| `O_i` | Opening; `O += F × r`, `r = 0.08`, clip so `cap < k F` |
| `cap_i` | `F_i + O_i` |
| `P_t(n)` | Yearly pot |
| `a_i` | `min(cap, P_t × P_i / Σ P)` |
| `P_i*` | `P_i (1 − a_i / cap_i)`; `cap = 0 ⇒ P = 0` |
| Payout vs cap | Split `a` onto `F` and `O` in proportion to `F/(F+O)` and `O/(F+O)` |

**Compared with what was already accepted or binding**

| Piece | Status then | Match? |
| --- | --- | --- |
| Hours → `c = 100 × hours`, `f = hours × frozen band` | Working sketch 2026-09-09 | Yes |
| Global bonding curve `p = c0 · c^k` | Live mint | Yes if curve is **global** `c`, not personal |
| `a_i = min(cap, P_t P / Σ P)` | Option-2 sketch | Yes |
| `P* = P (1 − a/cap)`, `cap = 0 ⇒ P = 0` | **Accepted** burn ([ADR 2026-09-08](../decisions/2026-09-08_p-burn-remaining-cap.md)) | Yes if `cap = rem` |
| `P_t` solvency-checked; leftover → reserves; default-in | Parked vintage analysis, still stands | Not specified in round 1 |
| `f` immutable; `paid` separate; freeze after 1× paid | Working freeze 2026-09-09 | **No** — `F` was paid down |
| Lots; first cap 1×; open only while unpaid | Parked vintage / gold-rush rule | **No** — one blended `F`/`O` |
| Work in `Y` first sits in `P_{Y+1}` | Parked record date | **No** |
| Sub-project: entity holds root `p`, euros in subpool | **Accepted** [ADR 2026-09-09](../decisions/2026-09-09_project-as-contractor.md) | Round 1 treated people like parent `i` |

**Why proportional `F`/`O` was a problem.** Paying down remaining “principle” `F` and “opening” `O` in proportion is loan amortization. `O += r F` is interest on outstanding principal. That is DVB **(h)** (receivable / interest), and it drops freeze-after-1× of **original** effort. New hours inherit old `O` and can lift `k F`.

---

### Round 2 — discarded split; `Fr` remainder; principal-first

Typos read as: `Fr(m+1)` → `Fr(m-1)`; `a_i` only at month 12; `cap < k F` → `≤`.

| Symbol | Meaning |
| --- | --- |
| `F_i` | Cumulative documented effort (**not** paid down) |
| `Fr_i` | Unpaid remainder of `F`; new `f` adds; `a_i` subtracts at year-end; leftover `a` hits `O` |
| Opening | If `Fr > 0`: `O += Fr × r` with **`r = 0.08` per month**, linear in `O`. If `Fr = 0`: leftover `a` reduces `O` until 0 |
| `cap` | `Fr + O`, clipped `k = 10` typically |
| Eligibility | Work of the 12 months before year-end sits in **this** year’s `P_t`; `O(0) = 0` but opening **runs before first `P_t`** |
| Option 2 | Chosen. Leftover `P_t` → reserves. Default-in. Invoice same fiscal year. Uninvoiced `a_i` → reserves, nobody can claim it |
| Sub-project | Same **pool math**; `j` is a database entity holding `p`, not necessarily a legal company |

`F` immutable + `Fr` + freeze when `Fr = 0` is structurally close to the live remainder model **for one lot**. Remaining disagreements: **8%/month from month 1**, **`k = 10`**, **one blended `Fr`/`O`/`P`**, **principal-first** (all `Fr` then `O`) vs oldest-lot remainder first, **no `Y+1`**, opening **before** first `P_t`.

If `Fr` is constant, 12 months of `r` give `cap / F ≈ 1.96` at the first `P_t`. About **9.4 years** unpaid to hit 10×.

---

### Lots vs blend (why they are not the same calculation)

**Lot** = one accepted block of work (typically a contribution year), with its own `E`, paid, opened cap, freeze. **Oldest unpaid lot first** = this year’s `a_i` applies to the oldest lot’s **remaining cap** (`Fr` **and** that lot’s `O` together) until that lot is exhausted.

**Medium payout example.** Old lot `E = €5,000`, `O = €15,000`, rem = €20,000. New December hours `E = €5,000`, `O ≈ 0`. Blended `cap = €25,000`. Fat year filling the cap: both methods pay €25,000. **Medium `a = €22,000`:**

| | Principal-first (blend) | Oldest lot first |
| --- | --- | --- |
| Where €22,000 goes | All €10,000 `Fr` (old **and** new hours), then €12,000 of `O` | €20,000 to the old lot, €2,000 to the new lot |
| After | `Fr = 0`, `O = €3,000`, freeze | Old lot gone; new lot still has €3,000 **principal**, and **only B** still opens |

Blend pays **this week’s 1× before last year’s opening**. Lots pay **the old wait** first.

**Lid vs filled cap (`k = 10`, `r = 0.08`/month).** Old work already at 10× of itself (`E_A = €5,000`, `cap = €50,000`). Add €5,000 in December.

| | Blend | Lots |
| --- | ---: | ---: |
| Opened cap at `t = 0` | 55,000 | 55,000 |
| Lid | 100,000 | A frozen 50,000 + B max 50,000 = 100,000 |
| After 12 months still unpaid | **64,600** | **59,800** |
| Difference | | **€4,800** = `0.08 × 12 ×` old `Fr` |

€90,000 is the **eventual lid on `O`** if blended `Fr` stays €10,000 (`cap = 100,000`), not the 1-year opened cap. Neither method fills that lid in a year. The live difference is extra **opening on old principal after it has already reached 10× of itself**, because the blended lid is `10 × (old+new)`.

---

### `Y` vs `Y+1` and “they can only invoice a little”

**Vintage** = the year-`n` pool `P_t(n)` and the one split/invoice round (like a wine year). **First vintage of a lot** = first `P_t` that lot may share. Parked: work in `Y` → first vintage **`Y+1`**, cap **1×**. That 1× is **per lot**, not newcomers only: a veteran’s **new** hours still start at 1×; old lots keep their opened caps.

`E = €5,000`. Boom = `P_t` large enough to fill opened cap.

**A — work only December 2026 (boom 2026)**

| | Round-2 model | Parked |
| --- | ---: | ---: |
| Cap at Dec 2026 | 5,400 (1.08×) | €0 from `P_2026` |
| First invoice | 2026 | Vintage 2027 at 1× = 5,000 |

Last-period newcomers really can only invoice a little in the new model. Parked, they miss the boom vintage entirely.

**B — work all of 2026, boom Dec 2026 (`Fr` from January, upper bound)**

| | Round-2 model | Parked |
| --- | ---: | ---: |
| Cap at Dec 2026 | 9,800 (**1.96×**) | €0 from `P_2026` |
| 2027 if 2026 filled | freeze (`Fr = 0`) | First vintage **1×**, then freeze → lifetime **1×** |

Parked: full-year 2026 work **misses** the 2026 boom, then only 1× in 2027. New model: ~2× **in** the boom year.

**C — work 2025, `P_2025 = 0`, boom 2026**

| | Round-2 model | Parked |
| --- | ---: | ---: |
| Cap at boom | 14,600 (2.92×) (24 months of `r`) | 5,000 (**1×**), first eligible vintage 2026 |

Same real wait. Continuous monthly `r` has **no cliff**; parked **first money pays 1×, not a multiple**.

Roadmap control stops **fake** tasks. It does not stop **needed** hours being **timed** to a forecast (front-load January if December `P_t` is already expected). That is the remaining short-fat-year gold rush at ~2×, not at 10×.

---

### Tax tables (both models option 2 unless noted)

€10,000 profit before the fee; €5,000 invoiced; VAT 21%; CV recovers VAT.

**VenB timing (20% SME band on this slice)**

| Year | Invoice in 2026 (chosen) | Parked `Y+1` (work 2026, invoice 2027) |
| --- | ---: | ---: |
| 2026 fee deducted | 5,000 | 0 |
| 2026 VenB on this slice | 1,000 | 2,000 |
| 2027 deduction | already paid | 5,000 only if 2027 has profit |

**Contributor rates** do not change with `Y` vs `Y+1` (still option 2). **VAT time of supply** does if FPS treat it as ordinary 2026 hours: delay to 2027 does **not** move VAT.

Same-year work + invoice is **normal option 2**. The risk is **substance**: if every year the pool pays ~this year’s `Fr` (and ~2× for people in from January), it looks like an annual billing cycle, not a contingent success fee. A year with `P_t = 0` is what keeps contingency real. `Y+1` was never a way to pay a lower **rate**.

**Employment:** monthly internal hours do not by themselves create RSZ. Subordination does. Freelancers may invoice monthly.

**Arm’s length / shouting distance (art. 49 WIB 92):** fee should still look like pay for **that documented effort**. No statutory max `k`. Examples used `k = 3`. `k = 10` can be argued as a long-wait risk premium; FPS can disallow the excess as hidden profit distribution. Uncapped share of **all** future `P_t` is residual equity, not the same as a salesperson’s 10% of **their** subscriptions. Too-high cap → mix of option 1 and 2 (deduction denied, WHT, possible VAT still on the “fee”).

**Uninvoiced `a_i`:** leftover to reserves only works if the haircut follows **allocation**, not cash received. Otherwise a skip of a thin year preserves `P` (and, if `Fr` is untouched, **grows `O`**). Example: equal `P = 100`, `cap = €5,000`, year 1 `P_t = €2,000` (`a = €1,000` each); Alice invoices, Bob does not. If Bob’s `P` stays 100, year 2 `P_t = €50,000` gives Bob a larger share.

**Bound discretion vs statutory surplus:** too automatic (`P_t` **is** x% of profit) → profit right / debt. Too discretionary (“if we feel like it”) → cannot provision, VenB first. Pattern: waterfall in the regulation; board **shall** open when positive **unless** solvency forbids; then invoice.

---

### 8%/month, 10× in 10 years, ETFs

| Path | Cash year 1 | After 10 years (if the cap is eventually filled) |
| --- | ---: | ---: |
| Freelance €5,000, ETF 8%/year | 5,000 | ≈ 10,800 (**2.16× on cash they already had**) |
| Unpaid €5,000, 10× at year 10 | 0 for 10 years | 50,000 (≈ **26%/year compound** on unpaid effort) |
| Parked `k = 3` after long wait | 0 until paid | 15,000 |

ETF return is return on **money in pocket**. The QOLAB multiple is catch-up because they **had no money**. 10× after ~10 **fully unpaid** years is a **startup-equity** story. If they **are** paid 1× in year 2–3, they can invest that cash; they should not also need 10× on the same work. 10× is for people who were **not** paid.

8%/month from month 1 **is** that 10-year path **and** ~2× at 12 months. You cannot have (1) 10× at 10 years unpaid, (2) ~2× already at 12 months, and (3) short period near 1×.

**Opening paths (`cap / E`):**

| Unpaid years | 8%/month from month 1 | 1× for 1 year, then linear to 10× at year 10 | Convex `1 + 9 (t/10)^2` |
| ---: | ---: | ---: | ---: |
| 1 | 1.96 | **1.00** | 1.09 |
| 2 | 2.92 | 2.00 | 1.36 |
| 5 | 5.80 | 5.00 | 3.25 |
| 10 | 10 | 10 | 10 |

Gated linear: year 1 is 1×; year 10 is 10×; after year 1 the add is about **8.3% of `E` per month** — same speed as 8%/month, **not in year 1**. Convex is gentler at year 2–4.

---

### Round 3 — conclusion asked: lots + year-1 freeze + 10× vs dividend / investment

**Working conclusion (not an ADR, not a ruling).** Continue as **option 2** with **lots**, **1× for the first 12 unpaid months of each lot**, then opening toward **10× at ~10 unpaid years**, **freeze** when that lot’s `paid ≥ E` (remainder of already opened `O` still payable), default-in, leftover to reserves, same-year invoice, fractional `p` burn.

That package does **not** force dividend treatment. It **reduces** the investment reading versus 8%/month from month 1, a blended cap, or no cap. **`k = 10` still looks equity-shaped.** DVB can accept the mechanism and still trim `k`. Do not launch as if FPS had agreed; do not promise 10× or publish `r` as ROI.

**Do not continue with:** 8% per month from month 1; one blended `Fr`/`O` for all years of work; “this beats ETFs” language.

If even gated 10× at 10 **unpaid** years is not enough (need 10× in expected value even when they **were** paid in year 2), that is **shares**, not a higher fee cap — and not on the same instrument as the invoice.

Lots are the same formulas **per row**; easier to explain to an administration (one engagement, one ceiling). Blend was only more elegant as a single pair `(Fr, O)`.

---

## Decisions

Proposed (discussion; **not** a new ADR):

1. Keep accepted payout weight: `a_i = min(rem, P_t P_i / Σ P)`; `P ← P (1 − a/rem)`; `rem = 0 ⇒ P = 0`; haircut on allocation including forfeit.
2. Option 2: dienstenovereenkomst; invoice in the fiscal year of `P_t`; leftover of `P_t` to reserves; default-in.
3. Work in year `Y` **may** sit in `P_Y` (no parked `Y+1` as the live rule). First **multiple** is still gated: **1× for the first unpaid year of each lot**.
4. **Lots**, not one personal `Fr`/`O`. Oldest unpaid lot first (or an explicit junior 1× / senior opening split, stated per lot).
5. `k = 10` as the **lifetime lid**, reached only after ~10 **unpaid** years; freeze opening when that lot’s 1× is paid.
6. Discard proportional amortization of remaining `F` and `O`. Discard 8%/month opening from month 1 as the filing path.
7. Sub-project **pool math** may copy the same functions; legal invoicing party for a database `j` is still DVB **(o)**.
8. Catalog DVB **(a)–(p)** in [token-system-design/dvb-questions.md](../../token-system-design/dvb-questions.md).

Unchanged: no unit `v`; no euro par; membership off the reward; nested mint gate and project-as-contractor cash path still accepted for legal entities; option 1 vs 2 was **chosen as option 2** for this pass (still a DVB hypothesis).

## Open Questions

- Exact opening curve after month 12: gated linear to 10× at year 10 vs convex.
- Oldest-lot-first vs explicit “pay all `Fr` then `O`” **inside** lots.
- Whether sunset `T` sits on top (DVB **(g)**).
- DVB **(a)–(f)**, **(h)–(j)**, **(p)**; nested **(k)–(o)** if in scope.
- Counsel may trim `k` below 10.

## Next Steps

- Counsel + accountant; file DVB with draft contracts, waterfall, and worked numbers (including `P_t = 0` and a year that fills opened cap).
- After that, draft dienstenovereenkomst + QOLAB annex; do not promise 10× or a yield in the text.
- If the opening path is accepted as design (not only discussion), write an ADR. Until then this log is the record.
