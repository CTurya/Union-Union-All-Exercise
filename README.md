# NexBank · UNION & UNION ALL Exercise
**BrightLearn · AI & Data Skills**
SQL Environment used : SQLOnline.com
---

## What This Exercise Is About

This exercise teaches you how to combine data from two tables using SQL's `UNION` and `UNION ALL` operators. You work through 10 questions + 3 bonus questions using tables from a fictional African retail bank called **NexBank**.

---

## The Core Difference

| | UNION | UNION ALL |
|---|---|---|
| What it does | Combines both tables | Combines both tables |
| Duplicates | Removed automatically | Kept — every row appears |
| Speed | Slightly slower | Faster |
| Use when | You want a unique list | You want a full history / audit log |

**The one question to ask yourself every time:**
> *Do I want only unique records, or do I want every single row?*

---

## The Three Rules (Break Any of These and Your Query Fails)

1. Both SELECT statements must return the **same number of columns**
2. Matching columns must have **compatible data types**
3. **Column names come from the first SELECT** — alias there if needed

---

## Syntax

```sql
-- UNION: removes duplicates
SELECT column1, column2 FROM table_A
UNION
SELECT column1, column2 FROM table_B;

-- UNION ALL: keeps every row
SELECT column1, column2 FROM table_A
UNION ALL
SELECT column1, column2 FROM table_B;
```

---

## Questions Overview

### Questions 01–05 · UNION
Each pair of tables has overlapping rows. Return one unique combined list.

| Q | Tables | Key Concept |
|---|---|---|
| 01 | branch_sandton_accounts + branch_rosebank_accounts | Duplicate account holders across branches |
| 02 | savings_products + current_products | Product appearing in both lists (SV03) |
| 03 | retail_banking_staff + corporate_banking_staff | Staff assigned to both divisions |
| 04 | mobile_branch_cities + digital_branch_cities | Cities served by both channels |
| 05 | push_notification_targets + inapp_banner_targets | Customers targeted by both campaigns |

### Questions 06–10 · UNION ALL
Every row from both tables must appear — including duplicates.

| Q | Tables | Key Concept |
|---|---|---|
| 06 | atm01_transactions + atm02_transactions | Full fraud log — sync duplicates must stay |
| 07 | gauteng_loan_applications + western_cape_loan_applications | Both regions may have captured same application |
| 08 | email_complaints + app_complaints | Total complaint volume — no rows dropped |
| 09 | april_payments + may_payments | Half-year reconciliation — row count matters |
| 10 | debit_entries + credit_entries | General ledger — every entry for the audit |

---

## Bonus Questions (Written — No SQL Required)

**Bonus 01:** Unique high-risk customer watch list across January and February
→ **UNION** — you want each customer to appear once only

**Bonus 02:** Count every Q1 transaction, even if recorded in two systems
→ **UNION ALL** — dropping duplicates would give an incorrect count

**Bonus 03:** Why does this query fail?
```sql
SELECT account_id, account_holder FROM branch_sandton_accounts
UNION
SELECT account_id, account_holder, city FROM branch_rosebank_accounts;
```
→ Column count mismatch (2 vs 3). Fix by adding `city` to the first SELECT:
```sql
SELECT account_id, account_holder, 'Sandton' AS city FROM branch_sandton_accounts
UNION
SELECT account_id, account_holder, city FROM branch_rosebank_accounts;
```

---

## How to Run the Queries

### Step 1 — Open a free SQL environment
Go to [sqliteonline.com](https://sqliteonline.com) — no account or install needed.
Make sure **SQLite** is selected in the top left.

### Step 2 — Run the setup script
Open `nexbank_setup.sql`, select all, paste it into the editor, and click **Run**.
This creates and populates all 20 tables.

### Step 3 — Verify the setup worked
```sql
SELECT * FROM branch_sandton_accounts;
```
You should see 4 rows. If yes, you're ready.

### Step 4 — Run your queries
Clear the editor, paste one query at a time, and click **Run**.

### Troubleshooting
| Error | Fix |
|---|---|
| `table already exists` | The setup script has `DROP TABLE IF EXISTS` — re-run it |
| `no such table` | The setup script didn't run yet — paste and run it first |
| `SELECTs to the left and right of UNION do not have the same number of result columns` | Column count mismatch — check both SELECT statements |

---

## Files Included

| File | Description |
|---|---|
| `nexbank_setup.sql` | Creates and populates all 20 tables — run this first |
| `README.md` | This file |

---

## Key Takeaway

`UNION` and `UNION ALL` do the same thing — they combine rows from two queries.
The only difference is what they do with duplicates.
**UNION removes them. UNION ALL keeps them.**

---

*BrightLearn · AI & Data Skills*
