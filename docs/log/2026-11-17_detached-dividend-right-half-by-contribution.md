# 2026-11-17 — Another organisation's scheme: equal shares, a separate dividend right, half the pool split by all-time contribution

**Role(s):** finance, business-dev

**Path:** cross-cutting (review of an outside scheme). The equal half belongs to [cash-subscribed shares](../../token-system-design/paths/cash-shares-residual/README.md). The contribution-weighted half fails for the same reason as the [cheap-share dead-end](../../token-system-design/dead-ends/cheap-share-route.md): the payout tracks labour.

**Status:** Reading of a scheme another organisation uses. Not adopted. No ADR. This is input for counsel and an accountant, not a ruling.

**Prevention rules applied:** [labour-quota shares dressed as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md): the same fault, one step more direct, because here the dividend key itself is labour and not only the share count. [Second instrument as a pair](../mistakes/2026-09-14_second-instrument-publishes-the-comparable.md): the equal half and the labour half sit on one instrument, so the labour fact leaks onto the whole payment.

## The scheme as described

- Everyone buys one share for the same fixed amount.
- The organisation keeps a ledger of all-time time contribution.
- The dividend right is separated from the share (a separate profit right).
- Each year's dividend pool is split in two:
  - **50% equally** among all shareholders.
  - **50% by all-time time contribution**.
- Their lawyer says the separation is possible. The lawyer also argues there is a case against taxing the right when it is received: the dividend is uncertain, so the right cannot be valued.

## Questions asked

1. What does this mean for tax: corporate tax (VenB), then 30% withholding (RV); and if the holder is a company, VenB again and then RV or the liquidation reserve on the way out?
2. How can double taxation be avoided in this system?
3. Would the tax authority reclassify the payment as a reward for work and tax it at once as professional income?

## Working answers

### 1. The two halves are different payments for tax purposes

| | Equal half | Contribution-weighted half |
| --- | --- | --- |
| Why the holder receives it | Holds a share bought for cash | Worked hours, read from a ledger |
| Natural box | Dividend (art. 18 WIB 92) | Professional income: art. 23 and art. 30–32 WIB 92 (anything received "because of or on the occasion of" professional activity); for a contractor or a contributor's BV, a fee for services with VAT |
| Risk of reclassification | Low | Real. Highest for employees and company directors, lower for genuine partners with real capital at risk |
| VVPRbis possible? | Possibly, if the shares are issued for cash in a small company, fully paid, and the waiting period is met | No. VVPRbis follows qualifying **shares**. A detached profit right is not one, and its key is not capital |

Tax law qualifies a payment by its **cause**. A share bought for a fixed amount that receives an equal slice is a textbook dividend. A slice computed from hours worked is caused by the work. That holds whatever label the statutes use and wherever the right sits.

### 2. Layers of tax if the dividend label holds

Per €100 of company profit before VenB. Standard rate 25%; small-company rate 20% on the first band shown in brackets. RV 30%; VVPRbis and liquidation reserve ≈18% from 1 July 2026 ([analysis §4](../../token-system-design/analysis/belgian-tax-and-company-law.md#4-option-1-vs-option-2--tax-burden)).

| Route | Steps | Net in the person's pocket | Combined levy |
| --- | --- | ---: | ---: |
| Natural person, ordinary dividend | VenB → RV 30% | €52.50 (€56.00) | 47.5% (44%) |
| Natural person, VVPRbis (equal half only, if it qualifies) | VenB → 18% | €61.50 (€65.60) | 38.5% (34.4%) |
| Contributor BV, **no** DBI, then 18% out | VenB → VenB in BV → 18% | €46.13 (€52.48) | ≈54% (≈48%) |
| Contributor BV, **no** DBI, then 30% out | VenB → VenB in BV → 30% | €39.38 (€44.80) | ≈61% (≈55%) |
| Contributor BV **with** DBI, then 18% out | VenB → (exempt) → 18% | €61.50 (€65.60) | 38.5% (34.4%) |
| Compare: deductible fee invoiced by contributor BV (option 2), then 18% out | VenB in BV → 18% | €61.50 (€65.60) | 38.5% (34.4%) |

RV withheld on a dividend paid to a BV can be credited against that BV's VenB. It is a cash-flow cost, not a fourth layer. The third layer is the BV's own VenB on the dividend it receives.

**DBI (art. 202–205 WIB 92) is the only tool that removes the middle layer.** It needs a holding of at least 10% of the capital **or** an acquisition value of at least €2.5 million, held in full ownership for at least a year, in a company that is normally taxed. One share bought for a fixed member price almost never meets either test, unless there are ten members or fewer. In that case the receiving BV pays VenB on the dividend again, and the BV route is **worse** than holding the share personally.

### 3. Ways to avoid double taxation, and what each costs

1. **Hold the share personally, not through a BV.** Two layers (VenB + RV), not three. The equal half may reach VVPRbis. The labour half stays at 30% at best.
2. **Make the labour half deductible.** Pay it as a contingent fee or bonus, not as a dividend. Then there is one layer at the receiver and none at the company. This is QOLAB's live [option 2](../../token-system-design/paths/option-2-contingent-fee/README.md). Through a contributor BV it lands at about 34–38%, which is cheaper than the dividend route **and** is the honest box. A natural person without a BV lands near 63% (the [adoption constraint](../../token-system-design/README.md#adoption-constraint)).
3. **For employees only: the statutory profit-sharing regimes** (Law of 22 May 2001 participation; the *winstpremie*). These are the routes the legislator built for "profit share for workers". They are collective and come with their own conditions. As a rough guide: about 7% tax plus 13.07% employee social contribution, and not deductible. Have the accountant confirm the current rates.
4. **DBI** only where the 10% / €2.5 million test is met. See above.

None of these lets the labour half keep the dividend label **and** avoid the second layer. That combination does not exist in Belgian law.

### 4. Would the administration reclassify?

**The equal half: unlikely.** It is the normal case of dividends on shares bought for cash.

**The contribution-weighted half: a real risk.** Grounds in descending strength:

- **Social security.** RSZ (employees) works with its own concept of pay: everything received "because of the employment" (art. 14 RSZ Law, art. 2 Wage Protection Law). RSZ is not bound by the tax label. A payout keyed to hours worked is the clearest case. For the self-employed, RSVZ contributions follow professional income. So a tax reclassification brings social contributions with it.
- **Cause of the payment** (art. 31–32 WIB 92 for employees and company directors; art. 27 for the self-employed). The quantum is computed from hours, and the ledger is updated every year with new work. That is a direct, yearly link between work and money: a bonus pool.
- **Contractors and contributor BVs.** If a BV holds the right and its owner does the work, the slice looks like consideration for the BV's services. That means VAT at 21% and fee income, not a dividend.
- **General anti-abuse rule (art. 344 §1 WIB 92).** Choosing a non-deductible dividend over pay is a "less-taxed route". The administration can unwind it if the main motive is avoiding personal income tax and social contributions. This is the same question as DVB item **(q)** in [dvb-questions.md](../../token-system-design/analysis/dvb-questions.md).

**Arguments on the other side** (why the outcome is not certain):

- Belgian practice widely accepts directors who are also shareholders taking dividends instead of salary. Art. 18 WIB 92 has a strong pull: income from shares and profit rights is a dividend.
- Since the WVV of 2019, statutes may distribute profit disproportionately to capital.
- *Werkende vennoot* case law: a partner who works to make shared capital produce a return can receive profit without it automatically counting as wage. That holds when there is real *affectio societatis* and capital at risk, and no subordination.

**What separates this scheme from the accepted cases:** in the accepted cases the dividend follows **capital**. Here half of it follows **hours**, and each holder's capital is the same fixed amount. Hours as the key is the sign that the work is the cause. QOLAB's rule says so for the same reason: "contribution is an eligibility gate, never a quantum" ([cash-shares path](../../token-system-design/paths/cash-shares-residual/README.md#mechanism)).

### 5. The lawyer's "no value at receipt" argument

It answers **when** tax is due. It does not answer **what kind of income** this is.

- With a right that cannot be valued, the administration does not tax at grant. It taxes **each payment** when it is made. That is the usual outcome for unvalued rights received for work.
- In this scheme there is no single moment of grant anyway. The labour weights change every year as the ledger grows, so the main exposure is at **payment**, not at receipt.
- If the payment is professional income, the result is personal income tax at progressive rates plus social contributions. The RV already withheld is credited against the tax. The company booked the payment as a dividend, so it took no deduction. It may still be able to claim one, depending on the year and the paperwork. There may also be tax increases.

So the argument is sound for the narrow question it addresses. It does not protect against reclassification at payout.

## Questions to put to their lawyer (or to ours, if we borrow the idea)

1. Which legal form does the separated dividend right take in their company type (share class, *winstbewijs*, contract), and which WVV article allows it?
2. Has a DVB ruling been obtained on the labour-weighted half? If so, what facts were in it?
3. How do they treat holders who are **employees** of the company (RSZ), and holders who **invoice** the company as well?
4. Do any holders hold through a BV? If so, does DBI apply, or do those holders pay VenB twice?
5. Is VVPRbis applied to the equal half? Is it clear it is not applied to the labour half?
6. Is the labour ledger "all-time" with no decay or cap? That makes the yearly link between new work and payout stronger every year.

## Takeaway for QOLAB

Nothing new for the path map. The scheme is the [cash-shares](../../token-system-design/paths/cash-shares-residual/README.md) "fixed statutory split" plus a labour key on the dividend, which is what that path and the [cheap-share dead-end](../../token-system-design/dead-ends/cheap-share-route.md) rule out. The equal half is worth keeping in mind as the shape of the governance/residual share. The labour half belongs in a deductible fee (option 2), where it is taxed once at the company and once at the receiver.
