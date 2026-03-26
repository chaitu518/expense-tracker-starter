# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install       # Install dependencies
npm run dev       # Start dev server at http://localhost:5173
npm run build     # Production build
npm run preview   # Preview production build
npm run lint      # Run ESLint
```

There is no test suite configured.

## Architecture

React app built with Vite + React 19. Components live in `src/`:

- **`App.jsx`** — root component. Owns `transactions` array (the data store). Passes `onAdd` callback to `TransactionForm` and `transactions` to `Summary` and `TransactionList`.
- **`TransactionForm.jsx`** — owns form state (`description`, `amount`, `type`, `category`). Calls `onAdd(transaction)` on submit, then resets fields.
- **`TransactionList.jsx`** — owns filter state (`filterType`, `filterCategory`). Renders the filtered transactions table.
- **`Summary.jsx`** — displays income/expense totals derived from `transactions`.

**Shared constant**: `CATEGORIES` (`["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]`) is duplicated in `TransactionForm` and `TransactionList` — not yet extracted to a shared module.

- **Known bug**: The `reduce` calls in `Summary` for `totalIncome` and `totalExpenses` may concatenate strings instead of summing numbers if `amount` is not coerced — verify inputs are parsed with `parseFloat`.
- **No persistence**: transactions are in-memory only; reloading the page resets to the hardcoded initial data in `App.jsx`.

Styling is split between `src/index.css` (global/reset) and `src/App.css` (component styles). CSS classes `income-amount` and `expense-amount` are shared between the summary cards and the transaction table rows.
