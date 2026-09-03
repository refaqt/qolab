# 2026-09-02 — Belgian tax analysis of the token sketch

**Role(s):** finance, business-dev

## What happened

Analysed the C / bonding-curve / R / U (1 U = 1 euro) sketch against Belgian VAT, income tax, cooperative law, and EU token regulation. Wrote the first analysis (later moved to [token-system-design/token-system.md](../../token-system-design/token-system.md)) and proposed [ADR 2026-09-02](../decisions/2026-09-02_tax-aware-contribution-credits.md). Noted that the U par claim contradicts the pro-rata pool formula.

## Decisions

Proposed (not accepted): drop U-tokens and peer sales; keep early-bird as a weight mint; cash out only on invoice in a solvency-checked round; cap as a multiple of documented effort; keep membership off the credit.

## Open Questions

- DVB ruling on “no taxable event at grant” for the final regulation text.
- Pool formula (profit vs revenue) and `k` for the personal cap.
- Whether Refaqt is or will be a CV erkend als sociale onderneming (6% advantage cap on shares).

## Next Steps

- Counsel + accountant review.
- Draft dienstenovereenkomst + QOLAB annex after that review.
