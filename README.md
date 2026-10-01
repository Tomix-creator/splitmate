# SplitMate

SplitMate is a small, mobile-friendly shared-expense splitter built as a Ship Log MVP. It helps a group record who paid for shared expenses, calculate each person's fair share, and reduce the final balances into a simple set of payments.

## Problem

Shared spending becomes confusing quickly. Different people pay for food, transport, tickets, or supplies, and manually working out who owes whom is error-prone.

## MVP

- Create/name a group
- Add and remove people
- Record an expense, amount, and payer
- Calculate total spending and fair share
- Generate settlement instructions
- Delete expenses and reset the group
- Persist data in browser localStorage
- Responsive interface

## Intentionally excluded from V1

Authentication, cloud sync, unequal/custom splits, multiple currencies, bank transfers, Paystack, receipt scanning, notifications, recurring expenses, AI features, and advanced analytics.

## Tech

Vanilla HTML, CSS and JavaScript. No framework and no backend. Data is stored locally in the browser.

## Run locally

Open `index.html` directly in a modern browser, or serve the directory with any simple local web server.

## Settlement logic

For each person, SplitMate calculates:

`balance = amount paid - fair share`

Positive balances are creditors; negative balances are debtors. The app then matches debtors to creditors until all balances are approximately zero, producing a compact set of settlement payments.

## Files

- `index.html` — application structure
- `styles.css` — responsive interface
- `app.js` — state, persistence, calculations, settlement logic
- `README.md` — project documentation
- `JOURNAL.md` — Ship Log/build journal

## Possible V2

Unequal splits, expense editing, shareable groups, export, multiple currencies, and cloud accounts could be explored only after validating the core workflow.
