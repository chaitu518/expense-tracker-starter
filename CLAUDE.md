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

This is a single-component React app (Vite + React 19). All state and logic lives in `src/App.jsx`:

- **State**: `transactions` array (the data store), form fields (`description`, `amount`, `type`, `category`), and filter state (`filterType`, `filterCategory`).
- **Known bug**: `amount` is stored as a string in state. The `reduce` calls for `totalIncome` and `totalExpenses` concatenate strings instead of summing numbers, producing incorrect summary values.
- **No persistence**: transactions are in-memory only; reloading the page resets to the hardcoded initial data.
- **Categories**: `["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]` — defined inline in the component.

Styling is split between `src/index.css` (global/reset) and `src/App.css` (component styles). CSS classes `income-amount` and `expense-amount` are shared between the summary cards and the transaction table rows.
