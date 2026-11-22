# Financial Dataset v2.0 — Methodology

## Business scenario
Nexora Business Solutions Ltda. is a fictional mid-sized Brazilian company. All entities and transactions are synthetic and were generated for portfolio and educational purposes.

## Coverage
- Transaction period: 2021-01-01 to 2025-12-31
- Transactions: 5,000
- Currency: BRL
- Geography: Brazil's five macro-regions

## Files
- `data/raw/financial_transactions.csv`: transaction-level fact table.
- `data/raw/customers.csv`: synthetic customer dimension.
- `data/raw/suppliers.csv`: synthetic supplier dimension.
- `data/processed/monthly_financial_summary.csv`: monthly revenue, expenses and net result, excluding cancelled transactions.
- `data/metadata/data_dictionary.csv`: field definitions and table descriptions.

## Important modeling notes
1. `transaction_type` distinguishes Revenue and Expense.
2. `net_amount_brl = gross_amount_brl - discount_amount_brl + tax_amount_brl`.
3. `signed_amount_brl` is positive for revenue and negative for expenses.
4. `late_payment_flag` is the supervised-learning target. It is 1 for late outcomes and 0 for on-time or early payments. It is blank for cancelled, pending, or otherwise unobserved outcomes.
5. For a model predicting late payment at transaction creation time, do not use post-outcome fields such as `payment_date`, `payment_status`, or `days_late` as predictors.
6. `monthly_financial_summary.csv` is a derived analytical table. It can be recreated from the transaction fact table.
7. All records, customer IDs, supplier IDs, risk bands and amounts are synthetic. They do not describe real people or businesses.

## Limitations
- This is a synthetic teaching dataset, not an audited financial statement.
- Tax rates, payment behavior and business patterns are simplified assumptions.
- Statistical significance and model performance should be interpreted within the synthetic data-generating process.
- The 60 monthly observations are useful for demonstrating forecasting workflows, but model complexity must remain appropriate for the limited time-series length.

## Suggested analytical questions
- How do revenue, expenses and net result evolve over time?
- Which categories, regions and customer segments contribute most to revenue?
- Are payment delays associated with payment method, terms, amount or risk band?
- Do revenue levels differ across regions or customer segments?
- Can monthly revenue be forecast using time-series methods?
