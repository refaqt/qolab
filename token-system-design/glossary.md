# Glossary

Symbols and terms used across the design notes. Where two notes use the same letter for different objects, this page says so.

## Ledger and mint (option 2)

| Symbol | Meaning | Not |
| --- | --- | --- |
| hours | The one input per accepted item (role, task, project). Logged when the work is accepted. | Reconstructed years later |
| `c` | Contribution points, `c = hours × 100` for everyone. A weight scale that renames hours. | A wage; never calibrated to a market €/hour |
| `p` | Non-transferable weights minted on the global curve `p = c0 · c^k` (early work mints more `Δp` per `Δc`). Splits `P_t`. | A euro claim; remaining `p` is not remaining euros |
| `k` (mint) | Exponent of the mint curve (`≈ 0.737` in the 2026-09-03 sheet). | The fee-cap multiple below |
| `f`, `E` | Documented effort: hours × **frozen contractor band**, or a quoted effort in the annex. The invoice **ceiling** at cash-out. | An unissued invoice; “fees he would normally have invoiced”; the letter `f` is **not** fees paid |
| `e_i(n)`, `E_i(n)` | Documented effort accepted in year `n` (a flow), and its cumulative total. | A payment |
| `a_i(n)`, `A_i(n)` | Allocation in vintage `n` (= `alloc_i`, counted whether or not invoiced) and its cumulative total. | Cash only; a forfeited slice counts too |
| `U_i(n)` | **Unrecovered effort:** `max(0, E_i(n−1) − A_i(n))`. The part of the documented work that is still at risk. The base the opening multiplies. | A principal; a debt |
| `O_i(n)` | Accumulated opening: `min(O_i(n−1) + r · U_i(n), (k−1) · E_i(n))`. | Accrued interest |
| band | A rate-card line (junior / senior / specialist €/h, or a project rate) frozen at join / accept. | A live market rate |
| lot `L` | **Retired for option 2** since [ADR 2026-09-14 one-row cap](../docs/decisions/2026-09-14_simplified-cap-one-row.md). The cap is one row per contributor. The term survives only in the [parked vintage note](parked/vintage-pools.md). | The live option-2 cap |
| `p_j`, `c_j`, `f_j` | Local ledger of sub-project `j`. `p_j` splits **euros** in `j`’s subpool; `f_j` is the project entity’s ceiling at the project band. | A claim on parent `P_t` |
| `A_{t,j}`, `B_{t,j}` | Points admitted / mint budget the parent spends on project `j` per period. | A euro valuation of the project |

## Pool and payout (option 2)

| Symbol | Meaning |
| --- | --- |
| `P_t` | This year’s budget: `min(policy % of profit or EBITDA, optional revenue cap, cash after reserves)`. A **flow**, set under bound discretion. May be zero. |
| vintage | The year-`t` pool and its one split / invoice round. |
| `gross_i` | `P_t · p_i / Σ p`. |
| `rem_i` | Remaining **opened** cap before this vintage’s allocation: `max(0, cap_i − A_i)`. The one number a contributor needs. |
| `alloc_i` | `min(gross_i, max(0, rem_i))`. Assigned whether or not invoiced. Uninvoiced slices forfeit to operating reserves. |
| opened cap | `cap_i(n) = E_i(n) + O_i(n)`, one row per contributor. Work opens only after it has survived one full vintage unpaid; opening stops on its own when `U = 0`; `cap ≤ k · E` for life. |
| `k` (cap) | Lifetime multiple lid on the row, GA/board policy. Under the [two-bases ADR](../docs/decisions/2026-09-14_two-bases-10x-off-effort.md) the default for time-based work is at or near 1×. Not a return. Without it the ceiling is unbounded and `p` never retires. |
| `r` | Cap-opening parameter per unpaid year. It multiplies **unrecovered effort** `U`, never a balance: `O += r · U`, linear, not compound. Not interest, not a yield, never published as one — the argument is in the [spec §5.2](paths/option-2-contingent-fee/README.md). |
| burn | `p_i ← p_i · (rem_i − alloc_i) / rem_i`; `rem_i = 0 ⇒ p_i = 0`. Amortizes weight as the ceiling is consumed. |
| freeze | Opening stops because `U = 0`, not because a separate rule fired. Not “only 1× ever”; not forfeiture of opened headroom. |
| sunset `T` | Optional bound on **duration**: after `T` years the opening stops (`O` frozen) while `rem` stays invoiceable. Under one row there is no lot to lapse. The lid `k` bounds the amount. DVB **(g)**. |
| default-in | Everyone eligible is allocated; opting out forfeits the slice and still haircuts `p`. |

## Three objects that get confused

| Object | What it is | Used? |
| --- | --- | --- |
| **Unit FX** | A conversion rate in euros per token, the same for every outstanding token at a date (`w = dc/dp`, `v = pool / N`, 1 `p` = €1, `S − €`). | **Never.** It prices the mint (tax at grant). |
| **Effort ceiling** | `pay ≤` opened cap on documented effort. Independent of how many `p` the work minted. | Yes (option 2). Arm’s-length brake: art. 53, 10° WIB 92 for the excess, art. 49 for the conditions. |
| **Ex-post return** | Cash actually received ÷ effort, after the fact. | Always exists. Never a target, never published. |

## Other paths

| Term | Meaning |
| --- | --- |
| Cred | A value-based allocation key (SourceCred-style graph score), not hours. Governance of the split, not a tax box. |
| Q (euro-par) | `1 Q = €1` coupon minted from a pool, Cred-weighted, redeemed by invoice or self-billing. Accepts priced consideration. [scoped-royalty path](paths/scoped-royalty-cred-q/README.md). |
| access token | A **different** object sketched under the same letter Q: a ticket to place supplier orders, no par. [q-supplier-access](paths/q-supplier-access/README.md). Must be renamed before any spec draft. |
| scoped royalty | A royalty on the products that embody the contribution, not on all Refaqt revenue. The base on which a large multiple is an ordinary outcome. |
| structure A | Two instruments: option-2 fee for labour beside cash-subscribed shares (count not `f(p)`) for residual upside. DVB **(q)**. |
| option 1 | Dividend box: after-tax profit, GA distribution, 30% RV (18% VVPRbis if eligible), not deductible, no VAT. Needs a share whose count does not track work. |
| option 2 | Fee box: professional service / royalty, deductible for the CV, VAT 21%, PIT + social or BV VenB. The box for anything allocated by contribution. |
| `S` | Weight in the rejected 2026-09-07 sketch that burned at euro par. Dead-end. |
| `w`, `v` | Rejected euro rates: withdrawal rate `dc/dp` and payout-time `pool / N`. |

## Belgian references used most

| Reference | Role in the design |
| --- | --- |
| art. 49 WIB 92 | Conditions of deductibility (incurred to obtain or retain taxable income, justified). |
| art. 53, 10° WIB 92 | Excess test: costs that unreasonably exceed professional needs. Burden on the administration; partial rejection only. |
| art. 26 WIB 92 | Abnormal or benevolent advantage; §1 carve-out where the Belgian recipient is taxed on it — largely neutral here. |
| art. 206/3 §1 WIB 92 | No offset of losses, DBI, innovation deduction against a supplement carrying a tax increase ≥ 10%. |
| art. 344 §1 WIB 92 | General anti-abuse rule. DVB **(q)**. |
| art. 18 / 269 WIB 92 | Dividend definition; VVPRbis conditions. |
| arts. 22, 22bis, 26 WBTW | VAT taxable event, chargeability backstop, taxable amount. |
| art. 1:8, 6:8, 6:19, 6:39, 6:110, 6:121–6:122 WVV | Inbreng in nijverheid; CV reports; CV securities; issuance only for inbreng; *uittreding van rechtswege*. |
| Wet 3 juli 2005 | Volunteer law — a poor fit for a profit-distributing CV. |
| Arbeidsrelatiewet | Subordination test (contractor vs employee). |
