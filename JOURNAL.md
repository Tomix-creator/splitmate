# SplitMate — Ship Log Journal

## 1. What I decided to build

I built **SplitMate**, a simple shared-expense splitter. The product answers one question: after several people have paid different amounts for a shared activity, who should pay whom so everyone ends up contributing their fair share?

## 2. Problem observed

Group outings, trips, events and shared purchases often involve several people paying at different times. The arithmetic is simple in isolation, but it becomes tedious as the number of people and expenses grows. The real friction is not recording a payment; it is turning all payments into an understandable final settlement.

## 3. Product hypothesis

If users can enter the people in a group and record each expense with its payer, the application can remove the manual calculation and immediately show a clear settlement plan.

## 4. MVP decision

I deliberately kept V1 narrow. The core loop is:

**Add people → record expenses → calculate fair share → settle balances.**

A successful MVP does not need accounts, payments, AI, receipt scanning, a database, or a complex dashboard. Those features could make the product larger without proving that the core calculation is useful.

## 5. What shipped

- Group naming
- Participant management
- Expense entry
- Payer selection
- Total-spend calculation
- Per-person fair-share calculation
- Automatic settlement calculation
- Expense deletion
- Group reset
- Browser persistence with localStorage
- Responsive mobile/desktop UI

## 6. Technical approach

I used vanilla HTML, CSS and JavaScript to keep the project lightweight and easy to inspect. The application state contains the group name, people and expenses. Every meaningful change is persisted to `localStorage`, so the MVP works without a backend.

Each person receives an ID rather than using their display name as a database key. Expenses reference the payer's ID. This avoids coupling relationships to editable text labels and is closer to how the data would be modeled in a larger application.

## 7. Settlement algorithm

The app first totals all expenses and divides that total by the number of people to get the fair share.

For each participant:

`balance = total paid by participant - fair share`

A positive balance means the participant should receive money. A negative balance means the participant owes money.

The algorithm separates creditors and debtors, then repeatedly transfers the smaller of the current debtor's debt and creditor's credit. Once either side reaches zero, it moves to the next person. This continues until the outstanding balances are settled.

This was the most interesting engineering part of the project because the UI is simple, but the useful product behavior depends on transforming several expense records into actionable instructions.

## 8. UX decisions

The interface focuses on three things: entering data quickly, seeing the current group totals, and understanding settlement instructions without explanation. The visual design uses generous spacing and a small number of panels rather than turning the MVP into a dashboard full of charts.

I also prevented removal of a participant who still owns expense records. That protects referential consistency rather than silently leaving broken payer references.

## 9. What I intentionally did not build

I excluded authentication, cloud databases, bank integrations, Paystack, unequal splits, currency conversion, notifications, receipt OCR, AI categorisation and advanced analytics.

The availability of tools or AI that could make those features faster to build is not a reason to skip the MVP stage. The first version exists to validate the core workflow before expanding scope.

## 10. Testing performed

I checked the empty state, adding multiple participants, duplicate participant prevention, multiple expenses from different payers, expense deletion, participant removal rules, reset behavior, persistence after refresh, and settlement calculations where one or several people need to receive money.

## 11. What I learned

A small product can still contain a meaningful engineering problem. The complexity of SplitMate is not the number of screens; it is maintaining clean state relationships and converting balances into useful settlement instructions.

I also reinforced the importance of defining the MVP before coding. Without a boundary, a shared-expense app can quickly become a payments platform, travel app, accounting system or social product.

## 12. Ship status

**V1 shipped.**

The MVP is usable locally in a browser and demonstrates the complete core loop. Future features should be driven by feedback rather than added simply because they are technically possible.
