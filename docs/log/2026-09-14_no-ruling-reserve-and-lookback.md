# 2026-09-14 — Launch without a DVB ruling: consequences, a tax reserve, and how far back FPS can go

**Role(s):** finance, business-dev

**Status:** Follow-up to [§1.1 of the 2026-09-10 review](2026-09-10_arms-length-10x-and-repo-review.md#11-dvb-will-very-probably-never-tell-you-10-is-not-arms-length). Asked what happens if we skip the ruling, treat option 2 as an ordinary commercial contract, and keep a side pot for tax if FPS later reclassify. No ADR. Does not accept, unpark, or revive anything. Design input for counsel, not a ruling.

**Prevention rules applied:** [do not put a euro spot price on a growing pool](../mistakes/2026-09-03_unit-price-on-growing-pool.md); [do not open a lifetime multiple on day one](../mistakes/2026-09-03_immediate-multiple-gold-rush.md); [do not dress labour-quota cheap shares as a dividend](../mistakes/2026-09-04_cheap-share-euro-par.md). Skipping the DVB does not relax those. Labels still lose to facts.

## What happened

The [review](2026-09-10_arms-length-10x-and-repo-review.md) already says you can launch at 10× with no ruling and carry the risk yourself, and that DVB will very probably confirm the **box** and leave the **number** as an arm’s-length condition. This session asked the operational question that follows: if we never get a ruling, what actually happens, is a cash buffer enough, and how many years can they reopen.

Headline: **a ruling is optional insurance, not a licence to operate.** A documented dienstenovereenkomst is the intended box and is how Belgian companies pay contractors every day. A side pot can absorb the **cheap** failure (the CV loses a deduction). It does not cap the **expensive** failures (hidden dividend, wage/RSZ, tax at mint). Those are driven by the **shape** of the deal, not by the absence of a ruling. Look-back is a rolling clock per tax year, not “everything since founding.”

Procedure cites below follow the wet of 18 December 2025 (B.S. 30 December 2025), which reversed the 2022 6/10-year layers retroactively from assessment year 2023.

---

## 1. Direct answers

| Question | Working answer |
| --- | --- |
| Must we have a ruling before implementing? | **No.** Most Belgian contractor spend never sees the DVB. You lose a decision that binds FPS for **at most five years**, and only while the facts you described stay true. You do not lose a legal right to contract. |
| Is this “just a commercial contract like any company”? | **Yes as the intended box** (option 2: invoice, independent supply, membership share not the payout key). **No as a complete defence** once payout is allocated by contribution points among members of a profit-distributing CV, the ceiling is `k × hours × frozen band`, or people look staff-like on a ledger. Ordinary companies pay ~1× and invoice in the year of the work. |
| Can we keep money aside for the tax we would owe if they reclassify? | **As treasury, yes. As a deductible provision for hypothetical VenB, no.** Size it to the failure you actually believe in. “The tax we were supposed to pay if they reclassify” is not one number until you pick **which** reclassification. |
| Furthest back they can make us pay? | **Three assessment years** of income tax and VAT in the ordinary, timely, good-faith case. **Four** if the return is late or “complex.” **Seven** for tax fraud with a prior written notice of precise indications. **RSZ:** three years from when the claim is due; **ten** after fraudulent or intentionally incomplete employer filings. Art. 358 WIB 92 can reopen a closed year for 12 or 24 months after certain later discoveries. |

---

## 2. What you lose by not filing

Nothing the administration orders in advance. There is no cap they impose if you stay away from the DVB. The [review §1.1–1.3](2026-09-10_arms-length-10x-and-repo-review.md) stands:

- Prefiling is informal and non-binding. A formal negative decision cannot be appealed and is a bad artefact after execution.
- A positive decision binds FPS for max five years, conditions and facts holding.
- The ruling you would actually get is likely: **characterisation confirmed, quantum left as “provided arm’s length.”** The KB of 17 January 2003 already carves tax rates and the calculation of tax out of the DVB’s remit.

So skipping the DVB mainly leaves the **expensive** questions open: mint vs invoice **(a)**, fee vs dividend **(b)**, VAT time of supply **(c)**, contractor vs employee **(d)**. The 10× number was never going to be locked anyway. That matches [dvb-questions.md](../../token-system-design/dvb-questions.md) “How to file”: the gate is **(a)–(d)**, not **(p)**.

A ruling is still worth taking to prefiling if you want those box risks closed. It is not a reason to delay launch waiting for a blessing of `k = 10`.

---

## 3. “It is just a commercial contract”

That is the intended option-2 story: dienstenovereenkomst + IP/CLA + QOLAB annex; genuine independence; invoice when the fee exists; membership share separate; no euro quote of `p`; `P_t` may be zero.

It holds when the facts match an ordinary independent supply. It stops looking like any company’s contractor file when you add the machinery the repo already treats as smoking guns:

- payout **allocated by contribution points** among members of a profit-distributing CV
- a ceiling written as `k × hours × frozen band` — you handed FPS the comparable ([review §1.5](2026-09-10_arms-length-10x-and-repo-review.md))
- a monthly hours ledger inside a CV that directs the work (wage facts if there is subordination — DVB **(d)**)
- a 10× that only appears after a long unpaid wait — defensible as expected value ≈ 1×, but only if you can **evidence** years with `P_t = 0` and lots that lapsed unpaid ([review §1.6](2026-09-10_arms-length-10x-and-repo-review.md))

**Size drives deductibility. Shape drives characterisation.** A high `k` on a clean fee costs the CV a deduction (art. 53, 10° WIB 92). It does not, by itself, turn the payment into a dividend or a wage. Dividend and wage come from *who* is paid *why* — membership as the key, points as the key, subordination.

---

## 4. Consequences if FPS later disagrees

Same worked lot as the review: `E = €5,000`, paid €50,000 (10×).

| What they do | Who pays | Does a cash reserve cover it? |
| --- | --- | --- |
| **Accept the fee** | CV deducts €50k; contributor taxed on €50k | Nothing extra |
| **Disallow the excess** (art. 53, 10°) — likeliest quantum fight | Cash **already gone**. VenB on the €35k add-back: **€7,000 / €8,750**. Contributor **unchanged** | **Yes — this is the reserve that makes sense** |
| **Hidden dividend** | No deduction on the **whole** €50k **and** 30% *roerende voorheffing* (CV is debtor; gross-up if not withheld). VAT deduction on the “fee” also exposed | Only if you reserved ~VenB + 30% WHT + interest on the full amount, for every **open** year |
| **Wage / RSZ** | Employer contributions + arrears; worker gets employee RSZ + PIT | Poorly. Genuinely worse, and it hits **both** sides |
| **Tax at mint** | PIT/VAT in the year `p`/`f` was logged, if they treat it as consideration then | Only for years still open when they assess |
| **Art. 344 §1** (two instruments, share count tracks work) | Unwind the split; labour-quota profit right | A reserve does not change the characterisation |

On top of the tax itself:

- **Belastingverhoging** 10–200% (art. 444 WIB 92). First good-faith offense can be waived (programmawet 18 July 2025). A 10%+ increase **blocks** offset of losses, DBI and the other deductions listed in **art. 206/3 §1 WIB 92** against that supplement. For a cooperative with carried-forward losses, “lose the deduction” becomes **cash tax** ([review §1.4](2026-09-10_arms-length-10x-and-repo-review.md)).
- **Nalatigheidsinteresten** from the original due date: **4%/year** on income tax in 2026 (art. 414 WIB 92); **8%/year** on VAT. Charged per started calendar month.
- Extra CIT and CIT interest are **not deductible**. VAT interest follows VAT (generally deductible). RSZ increases are not.

**Nobody has written who bears an art. 53, 10° disallowance** — the pool, or a clawback from the contributor. That is a contract term. If we launch without a ruling, it still belongs in the annex before anyone is promised a cap.

---

## 5. A side pot is rational — with three limits

1. **Treasury, not a tax shield.** Parking cash is fine. Booking a *voorziening* for a fight that has not started is accounting (CBN/CNC: rekening 161 / 6703). It is **not** a deductible professional cost for VenB. Corporate tax is not deductible; a provision for “maybe they reclassify us” is the same economic object.

2. **Size it to the failure you actually believe in.** If the shape is a clean fee, reserve **tax on the excess** (roughly 20–25% of amounts above a 1× comparable), plus a buffer for interest, for **open years only**. If characterisation is in play, the number is a different order of magnitude (full add-back + 30% WHT, or RSZ + PIT). You cannot reserve “the tax we would have paid if they reclassify” until you pick which reclassification.

3. **It does not make the position safer.** A documented, invoiced, VAT-paid contractor file is the defence. An internal memo that money was set aside “in case they reclassify” is at best neutral. Combined with ROI language or “this is how we avoid dividend tax,” it is worse.

At any moment the pot only needs to cover years that are **still open**, plus payments about to be made (those open a new year). A 10× invoice in year 10 is a **year-10** problem; the 2026 mint is a **2026** problem.

---

## 6. How far back they can go

They do not reach back to founding forever. Each tax year closes on its own clock.

For a calendar-year CV, assessment year = income year + 1. The ordinary income-tax period runs from **1 January of the assessment year**. Example: income year 2026 = AY 2027.

| Regime | How far back | Typical close for income year 2026 (AY 2027) |
| --- | --- | --- |
| **Ordinary**, timely, complete return | **3 years** | 31 Dec 2029 |
| Late or no return, or **“complex”** return (CbCR/local file, tax-haven form, WHT exemption, FTC, hybrid, CFC, reportable legal construction, some DAC information, …) | **4 years** | 31 Dec 2030 |
| **Fraud**, with prior written notice of **precise indications** | **7 years** | 31 Dec 2033 |
| **VAT** (art. 81bis WBTW) | 3 years ordinary; 4 if late/no periodic return; **7** for fraud | VAT chargeable in 2026: generally through 31 Dec 2029 |
| **RSZ** | **3 years** from when the claim is due (after the quarterly filing/payment deadline) | ~3 years after that quarter |
| RSZ after **fraudulent or intentionally incomplete** employer filings | **10 years** | Far tail; concealment, not a documented contractor position |
| **Art. 358 WIB 92** | Extra 12 or 24 months after certain later discoveries (e.g. information from abroad) | Can reopen a year that already looked closed |

Books must be kept **7 years** (the 2025 law put retention back to 7 from the 2022 10-year experiment).

A good-faith, fully declared option-2 file (invoices, VAT, contributor BVs taxed on the fee) is the **3-year** case. Taking a reasonably arguable position without a ruling is not fraud. Fraud needs intent to evade; the 7-year CIT/VAT clock also needs a precise prior notification. Hiding the point-allocation, not invoicing VAT that was clearly due, or internal papers that the structure exists to dodge a box, is how you leave that world.

So in 2035, with timely filings and no fraud, they can still touch roughly income years **2032–2034** (and 2035 as it unfolds). 2026 mint, if never assessed, is closed. A 10× invoice in 2036 is open until the end of 2039.

If VAT was really due when the work was done in 2026, that VAT year may already be closed by the time a fat pool appears. That does not save the **invoice year**. Under the working hypothesis in DVB **(c)**, VAT attaches to the invoice when `P_t` crystallises; that year has a fresh 3-year clock. Art. 22bis WBTW remains the backstop against “we invoice later” as a deferral by itself.

Interest still runs from the original due date, so a year assessed at the end of the 3-year window already carries ~3 years of interest.

---

## Decisions

None as an ADR. Nothing accepted, unparked, revived, or rejected.

Working conclusions (still for counsel):

- Launching without a ruling is a normal Belgian choice. The residual quantum risk is the one DVB was never going to bless.
- A side pot sized to **art. 53, 10° on open years** is a reasonable way to live with that cheap failure. It is not cover for reclassification.
- If the facts are a labour-quota among members, staff-like people on a ledger, or a published euro rate on `p`, the bill is a different tax, often on a different person, and a reserve of “the extra VenB” will be short.
- Write the disallowance allocation into the annex whether or not a ruling is filed.

## Open Questions

- Counsel: confirm the clocks on this fact pattern (especially RSZ if anyone is close to subordination, and whether any DAC6 / “complex return” flag would move CIT from 3 years to 4).
- Who bears an art. 53, 10° disallowance — pool or contributor? Still unwritten.
- Can the expected-value ≈ 1× argument for `k = 10` be evidenced at launch, before any year with `P_t = 0` has happened? Unchanged from the review.

## Next Steps

- Unchanged from the review: take **(a)–(d)** to prefiling if we want the expensive risks closed; do not wait for a blessing of `k = 10`; keep ordinary time-based work near **1×** and put 10× on a **scoped royalty** or on **cash shares that are not `f(p)`** if we want the multiple without an hours-based fight.
- If we launch without a ruling, still write the disallowance risk allocation into the QOLAB annex.
- Do not publish 10×, `r`, or any ROI language.

## Sources checked

Ruling procedure and what DVB will and will not confirm: [2026-09-10 review](2026-09-10_arms-length-10x-and-repo-review.md), [dvb-questions.md](../../token-system-design/dvb-questions.md). Assessment and investigation periods after the wet of 18 December 2025: [PwC Legal](https://www.pwclegal.be/en/news/investigation--assessment-and-retention-periods---back-to-how-it.html), [Tiberghien FAQ](https://www.tiberghien.com/nl/4497/faq-inkorting-van-verjarings-en-aanslagtermijnen-inkomstenbelasting-btw), [FOD Financiën fiscale nieuwigheden 2026](https://fin.belgium.be/sites/default/files/media/documents/press-kit-fiscale-nieuwigheden-2026.pdf), [PwC Tax Summaries](https://taxsummaries.pwc.com/belgium/corporate/tax-administration). VAT fraud term and retention (circulaire 2026/C/31): [RSM Belgium](https://www.rsm.global/belgium/nl/insights/update-over-de-bewaartermijnen-van-btw-documenten-en-verjaringstermijnen). RSZ prescription (art. 42 RSZ-wet; 3 / 10 years): [RSZ administrative instructions 2026/3](https://www.socialsecurity.be/employer/instructions/dmfa/nl/latest/instructions/socialsecuritycontributions/prescription.html). Art. 444 first good-faith waiver: programmawet 18 July 2025. Nalatigheidsinteresten 2026: art. 414 WIB 92; FOD rate 4% income tax, 8% VAT. Art. 358 WIB 92 extra window. Accounting of a tax provision: [CBN/CNC advies Belastingen](https://www.cbn-cnc.be/nl/adviezen/belastingen).
