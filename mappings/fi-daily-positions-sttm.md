# Source-to-Target Mapping: Daily Fixed Income Positions

**Target table:** `fixed_income.gold.daily_positions`
**Grain:** one row per portfolio, ISIN and business date
**Source system:** Portfolio accounting system (end-of-day extract)

| Target column | Source field | Transformation / rule | DQ expectation |
|---|---|---|---|
| portfolio_id | ACCT_PORTFOLIO_CD | Trim, uppercase | Not null → fail |
| isin | SEC_ISIN | Trim | Not null → fail; exists in security master → drop |
| position_date | POS_DT | Cast to DATE | Equals latest business day → warn |
| quantity | NOMINAL_QTY | Cast to DECIMAL(20,4) | Not null → fail |
| clean_price | PRICE_CLEAN | From official end-of-day price source | Between 0 and 200 → warn |
| accrued_interest | ACCR_INT | Cast to DECIMAL(20,2) | Not null → warn |
| market_value | (derived) | quantity × clean_price / 100 + accrued_interest | Reconciles to source within 0.01% → warn |
| client_account_ref | CLIENT_REF | No transformation | Classified confidential; masked |

## Open questions
- Confirm whether prices are quoted per 100 nominal (assumed above)
- Confirm treatment of positions with zero quantity
