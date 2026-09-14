# 2026-09-14 — Wrong article for the excess test (art. 49 instead of art. 53, 10°)

## What happened

Across the design notes and logs, **art. 49 WIB 92** was cited about eighteen times as the “not excessive” test on the fee cap and on any multiple `k`. Art. 49 sets the **conditions of deductibility** (incurred in the period to obtain or retain taxable income, and justified). The **excess** test is **art. 53, 10° WIB 92** (*kosten in zover zij op onredelijke wijze de beroepsbehoeften overtreffen*). In the same pass, **art. 26 WIB 92** was said to bite “even if you do not deduct,” although art. 26 §1 carves out an advantage that is taken into account in the Belgian recipient's taxable income — so it is largely neutral for an invoicing contributor. Found by the [2026-09-10 review §3](../log/2026-09-10_arms-length-10x-and-repo-review.md).

## Why it went wrong

The first analysis used art. 49 as shorthand for “deductible and reasonable,” and every later note copied the citation forward without checking it once against a source. Because art. 49 (whole expense, burden on the taxpayer) is harsher than art. 53, 10° (excess only, burden on the administration, no review of opportuneness), the repo over-penalised the multiple and blurred two different failure modes (size → partial disallowance at the CV; shape → requalification) into one “recharacterisation” fear.

## Prevention rule

Cite **art. 53, 10° WIB 92** for the excess test and **art. 49** for the conditions of deductibility; treat art. 26 as neutral where the Belgian recipient is taxed on the amount. Before a legal citation is repeated across more than one note, check it once against a primary or reputable secondary source and record that source in the note (a “Sources checked” line, as the 2026-09-10 and 2026-09-11 logs do). When a citation is corrected, add a dated citation note at the top of the affected logs instead of rewriting history, and fix the design notes in place.

## Related

- [docs/log/2026-09-10_arms-length-10x-and-repo-review.md](../log/2026-09-10_arms-length-10x-and-repo-review.md) §3.1–3.2
- [token-system-design/analysis/belgian-tax-and-company-law.md](../../token-system-design/analysis/belgian-tax-and-company-law.md) §5 (size vs shape)
- [token-system-design/analysis/dvb-questions.md](../../token-system-design/analysis/dvb-questions.md) (“Which article does what”)
- [token-system-design/glossary.md](../../token-system-design/glossary.md) (Belgian references)
