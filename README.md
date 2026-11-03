# Banking Transaction Analysis System
**Project 16 — Intermediate | Educational simulation only**

Stores synthetic customers, accounts and transactions in MySQL. Python validates deposits/withdrawals; Pandas and NumPy generate summaries; Matplotlib creates charts.

**Safety:** Do not use real banking data, credentials, or sensitive financial information. Balances are simulated (`deposits - withdrawals`). A review flag is not a fraud determination.

## Setup
1. Install MySQL 8+ and Python 3.10+.
2. In MySQL, create a database and dedicated local user:
```sql
CREATE DATABASE banking_analysis CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'banking_app'@'localhost' IDENTIFIED BY 'ChangeThisLocalPassword!';
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, ALTER, INDEX ON banking_analysis.* TO 'banking_app'@'localhost';
FLUSH PRIVILEGES;
```
3. Copy `.env.example` to `.env` and set the password to the one you chose.
4. Install dependencies: `python -m pip install -r requirements.txt`
5. Create tables and seed synthetic data:
   - `python main.py init`
   - `python main.py seed`
6. Try:
   - `python main.py accounts`
   - `python main.py history 1001`
   - `python main.py deposit 1001 500 "Sample deposit"`
   - `python main.py withdraw 1001 125 "Sample withdrawal"`
   - `python main.py reports`
   - `python main.py charts`
   - `python main.py flags`
   - `python main.py` for interactive menu

The demo seed creates synthetic records. Use `accounts` to check account IDs rather than assuming IDs if the database already contains data.

## Outputs
CSV files are saved in `reports/`; PNG charts are saved in `charts/`. The default review threshold is 10,000 and can be changed in `.env`. The rule is only an educational review example and can produce false positives or miss unusual activity.

## Tables
`customers(customer_id, display_name)`, `accounts(account_id, customer_id, account_type)`, and `transactions(transaction_id, account_id, transaction_date, transaction_type, amount, description)`.


## Web frontend

1. Edit `.env` and set `DB_NAME=banking_transcations` if that is the database you created in MySQL Workbench. Ensure `DB_USER` and `DB_PASSWORD` match your MySQL user.
2. Install dependencies: `python -m pip install -r requirements.txt`
3. Initialize tables and add synthetic sample data: `python main.py init` then `python main.py seed`
4. Start the local web app: `python app.py`
5. Open `http://127.0.0.1:5000` in your browser.

This is an educational simulation. Use synthetic data only. Balances are simulated.
