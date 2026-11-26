# Changelog

Home Assistant shows this file on the add-on's update screen. Newest first.

## 0.25.0

- New Investments page: what your investments are worth, how much of the change was money you put in and how much was market growth, and the return for this year, the last 12 months or since the start (money added during the period doesn't inflate the return).
- A chart of value against money put in, allocation by holding type, a table by account, and your largest holdings.

## 0.24.0

- New Balance sheet page: everything you own and owe on any date, grouped into cash, investments, loans and cards, with subtotals and net worth, compared with an earlier date (a year earlier by default). Its numbers match the Net worth page. Pensions are listed separately as a monthly benefit.

## 0.23.0

- New Goals page. Turn any savings fund into a goal with a target amount and date, and see how much is saved, the percent done, how much is needed each month versus what you budget, the projected finish date, and whether you're on track.
- Each goal has a chart of what's saved, the path to the target, and where your current rate leads. Reorder goals to set priorities.

## 0.22.0

- Debt page: a payoff chart showing the original schedule, your actual balance and your plan, with today marked.
- What-if: try an extra amount each month or one-time lump sums and see the new payoff date, months saved and interest saved. Save a plan to make it the page's default.
- Pay down or invest: set an expected return and see, side by side, what you'd have if you put the extra toward the mortgage versus investing it instead.
- New reminder: if a mortgage payment hasn't shown up 5 days after it's due, the Reminders page says so.

## 0.21.0

- New Debt page. Enter your mortgage's loan details once (from the closing disclosure) and see the balance, rate, payment, months left, payoff date and interest left, plus how far ahead of the original schedule your extra payments put you. Escrow is shown beside the payment but kept out of the payoff math.
- Full amortization table, from today or from the start of the loan, with a CSV download.
- The page warns when the saved rate or payment doesn't match the latest mortgage statement.

## 0.20.0

- New on the dashboard: Top variable expenses. Your biggest spending categories and payees for a month, compared with the month before and with your 12-month average. Recurring bills, transfers and card payments are left out.
- Audit: "Amount differs" now only pairs rows whose amounts are close (within $25 or 25%) and whose payee really matches, so unrelated rows that share a word like "Apple" or "Payment" are no longer paired.

## 0.19.0

- Audit: EveryDollar investment rows (HSA, 401k) and rows with no account can't be matched to a bank row, so they're now listed under a collapsed "Not checked" section instead of counting as items that need a look.
- Audit: the current month is marked "In progress", since the bank and EveryDollar are still filling it in. The page now opens on the oldest finished month with work left.

## 0.18.1

- Fixed: loading the Excel history again from a re-saved copy of the workbook now says it's already loaded, instead of failing with an error.

## 0.18.0

- Reminders can now be yearly. The first one: "Check whether Apple Card can sync automatically", due every July 1, with what to look at. Mark it done once checked.

## 0.17.0

- Documents page (Books): mortgage statement PDFs are kept on the Pi and read automatically. Each statement adds the mortgage balance to Net worth, and a Mortgage table shows principal, interest and escrow paid, extra principal and the escrow balance, with this year's totals. The first statement creates the mortgage account.
- The Mac uploader sends mortgage statement PDFs from Downloads too.
- Pensions: a new pension account type. A pension's amount is its estimated monthly benefit, so it is no longer added to Net worth; Net worth lists it separately ("$X/month from age N"). Set the starting age on Accounts. Plaid pension accounts switch to this type on their own.

## 0.16.0

- Accounts: a new Updated column shows when each account last got new data, either a Plaid sync or an import (from the Import page or the Mac), or "Never". When an account has both, hovering shows the other one.

## 0.15.0

- Fixed: some Fidelity 401(k) contributions were skipped because the database treated two different Plaid IDs as the same when they differed only in upper or lower case. Plaid IDs are now compared exactly, and the next Fidelity sync saves the missing ones.
- Connections: an "Add account" button at the end of each row that doesn't feed an account yet, instead of a choice in the list.
- Connections: "Syncing…" shows only on the connection that is syncing, and never on one whose last sync failed.

## 0.14.1

- Fixed: a Fidelity sync could fail with "Saving balances or investments failed" when one investment transaction clashed with a row already saved. That row is now skipped (and noted in the add-on log) and the rest of the sync saves.
- "New account from this" names the account after Plaid's description of it instead of a generic "Investment".

## 0.14.0

- Connections: "New account from this" in the Feeds list adds a site account for a bank or retirement account that doesn't have one yet (name, type and last 4 digits come from Plaid) and starts feeding it right away.
- Fixed: a sync could stay on "Syncing…" forever if Plaid never answered a request, and any change on Connections then failed. Each request to Plaid now gives up after 2 minutes, and the next sync tries again.

## 0.13.2

- Fixed: removing a bank connection, or choosing its accounts, could fail if a sync was running at that moment. It now waits for the sync to finish.

## 0.13.1

- Fixed: connecting a bank failed with "client_user_id should not contain sensitive information" when the signed-in username was an email address.
- Plaid keys pasted with a stray space or line break now work.
- The Mac uploader sends through the Mac's built-in curl, which accepts the home certificate.

## 0.13.0

- Statements upload themselves from the Mac: Apple Card, Apple Savings, EveryDollar, Chase and Fidelity exports saved to Downloads are sent to the site and moved to Downloads/Imported. Install it once with mac/install.sh (see mac/README.md).
- Clean files import on their own. A file that needs a look (skipped rows, unknown account) waits in "Waiting for review" on the Import page, with Import, Open in importer and Discard.
- Upload tokens on the People page (admins): the Mac's key, which can only upload files and can be revoked at any time.

## 0.12.1

- Fixed: after an update, a Finance tab that was already open could stop loading pages. It now reloads itself onto the new version.
- Release notes (this file) now show in Home Assistant.

## 0.12.0

- Plaid for Chase and Fidelity: connect each bank once on the new Connections page (Setup). New transactions, pending charges, balances and Fidelity holdings then arrive every 4 hours, through the same rules and transfer detection as file imports. Plaid starts the day after your last imported file, so nothing is counted twice.
- "Check Plaid connections" reminder, due at once when a bank needs you to sign in again. "Load Chase" and "Load Fidelity" clear themselves once Plaid covers those accounts. Download reminders renamed (Apple Card, Apple Savings, EveryDollar).
- Security: 5 wrong passwords lock a username for 15 minutes (admins can unlock it on People); the database backups taken before each update are encrypted.

## 0.11.0

- HTTPS: the site is served at https://homeassistant.local:8099 with its own home certificate. Trust it once per device (see the add-on README).

## 0.10.0

- The database password moves out of the Configuration tab into the add-on's own secrets file. The People page tells admins when to clear the field.

## 0.9.1

- Fixed: adding a person failed with a confusing error when the username had a space. Spaces around it are now trimmed and the rule is explained.

## 0.9.0

- New look with a sidebar instead of top tabs.
- Pages keep their place and keep working while you visit other pages.
- Everyone signs in with their own username and password; admins manage people on the new People page.
- Budget page: EveryDollar's plan against what was actually spent and received, from its BudgetItems export.

## 0.7.0

- Audit page: EveryDollar transactions matched against the bank and card files, month by month, with sign-off.
- Reminders page: monthly data loads that clear themselves when the data arrives, including money owed from savings to checking.

## 0.6.0

- Net worth page with a trend over time.
- Recurring page: subscriptions and bills found automatically, to confirm or dismiss.
- Fidelity positions files for investment balances and holdings.

## 0.5.0

- Dashboard: income against spending, top categories, trends and payees.

## 0.4.1

- Import several files at once, with progress; one Fidelity file loads all its accounts in one pass.

## 0.4.0

- Importers for Chase credit card, Apple Card, Apple Savings and Fidelity.

## 0.3.1

- EveryDollar category names; files with a blank account column.

## 0.3.0

- One-time import of the earlier Excel history.

## 0.2.1

- Edit accounts; categories matched to accounts by the last 4 digits.

## 0.2.0

- Categories, rules and transaction kinds (transfers and card payments left out of totals).

## 0.1.0

- Import pipeline: Chase checking and savings files, duplicate detection, import log with undo.

## 0.0.1

- First version: the add-on runs and connects to MariaDB.
