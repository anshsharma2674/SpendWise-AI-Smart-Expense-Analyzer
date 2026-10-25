# SpendWise AI — Smart Expense Analyzer

SpendWise AI is a static, browser-based personal finance dashboard for recording expenses and income, organizing transactions, setting category budgets, tracking savings goals, and reviewing explainable spending analytics. Data stays in the browser's local storage; there is no backend, bank connection, external AI service, analytics tracker, or API key.

> “AI” is a product name. The current insights use deterministic rules and robust statistical summaries, not a trained machine-learning model.

## Features

- Add, edit, search, filter, sort, and delete income and expense transactions.
- Import CSV with quoted-field parsing, row validation, duplicate checks, preview, and explicit confirmation. Export transactions and a selected-month summary.
- Month-based dashboard, income/expense and category charts, category summaries, and a paginated transaction list.
- Category budgets with transparent 80% approaching and over-100% exceeded thresholds.
- Savings goals with progress and optional estimated monthly contribution.
- Local spending patterns, recurring-looking description checks, a median/MAD possible-outlier screen, and an average-of-three-complete-months forecast when enough data exists.
- Light, dark, and system appearance; INR, USD, EUR, and GBP display formatting.
- Fictional sample dataset, budgets, goals, and a clear-data action.
- Responsive desktop sidebar and mobile navigation, keyboard-focused controls, reduced-motion support, and accessible status/progress labels.

## Screenshots

No screenshots are included because none have been captured from the running application. To add genuine screenshots, run the app locally, capture Overview in light and dark modes and a mobile view, place the images in a `screenshots/` directory, and link them here.

## Technology and project structure

- HTML5, CSS custom properties, and vanilla JavaScript (ES6+).
- Chart.js 4.4.7 from a pinned jsDelivr CDN URL. If it does not load, charts show a fallback and all transaction totals and textual breakdowns remain available.
- Browser `localStorage`, browser-side CSV parsing, and `Intl.NumberFormat`.

```text
index.html      Complete no-build application
README.md       Project and deployment guide
TESTING.md      Verification record and manual test checklist
LICENSE         MIT license with copyright placeholder
.gitignore      Local/editor artifact exclusions
```

## Run locally

Open `index.html` in a current browser. No installation or build step is required. Chart.js needs internet access to load from the pinned CDN; transaction management and the rest of the app do not require an API key. Browsers may impose different storage behavior for directly opened files; if persistence is unavailable, use a simple static local server or the deployed GitHub Pages site.

## GitHub Pages deployment

1. Create a GitHub repository named `SpendWise-AI`.
2. Upload or push the project files.
3. Keep `index.html` in the repository root.
4. Open repository **Settings**, then **Pages**.
5. Choose deployment from the appropriate branch and the root (`/`) directory.
6. Save the settings, wait for GitHub Pages to deploy, then open the published URL shown by GitHub.

The application uses no root-relative asset URLs, so it can run under a repository path. No live URL is claimed here.

## Transactions, import, and export

Use **Add transaction** to enter a date, description, positive amount, type, and category; payment method and notes are optional. Transactions can be edited and deleted from the Transactions view. Search matches description, category, and notes. Filters include type, category, and inclusive date range. The list is sorted by date or amount and paginated.

The CSV template uses:

```csv
date,description,amount,type,category
2026-10-01,Monthly Salary,25000,income,Salary
2026-10-02,"Grocery, weekly",850,expense,Groceries
```

Dates use `YYYY-MM-DD`; `type` must be `income` or `expense`; amounts must be positive. Required headers are `date,description,amount,type,category`; optional columns `payment_method` and `notes` are accepted. Import validates and previews rows, reports skipped rows, and requires a confirmation click. Likely duplicates already in the account or duplicated in the same file are skipped. Transaction CSV export and a selected-month report export are provided. Exported cells are quoted and formula-like values are prefixed defensively.

## Budgets and savings goals

Budgets apply per category to expense records in the selected month. “Approaching limit” starts at 80%; “Over budget” starts above 100%. Remaining values may be negative when overspent. Goals track entered saved and target amounts separately and do not alter income or expense totals. When a goal date is present, its monthly pace is a simple estimate using elapsed calendar days converted to average months.

## Analytics methods and limitations

- Income, expenses, net balance, and savings rate are derived from transactions. Savings rate is `(income - expenses) / income` only when income is positive.
- Month comparisons use the immediately preceding calendar month and are labeled as such. Missing prior records are called out rather than replaced with fabricated percentages.
- Category totals and spending suggestions use recorded expense amounts.
- A possible unusual expense is considered only with at least five earlier expense observations in its category. The screen flags amounts above `median + 3 × 1.4826 × MAD`; when MAD is zero it uses `max(2 × median, median + 1)`. This simple rule is only a review prompt, not fraud detection or a confirmed mistake. Dismissals are stored in the browser.
- Recurring-looking activity requires the same normalized description at least three times over at least three distinct months. It does not establish that a payment is a subscription.
- Forecasting averages up to the three latest months with expense records before the current month, and requires three such months. It is an estimate, not a prediction guarantee. It does not infer values for missing months.
- Currency selection changes formatting only. Values are not converted; keep records in one consistent currency.
- Demo records are fictional and run through the same calculations as other records.

## Appearance and privacy

The preference defaults to **System Default**, follows `prefers-color-scheme`, and updates when the operating-system setting changes. Light and dark are explicit choices. The preference persists in localStorage. Reduced-motion preferences are respected.

Transaction and preference data are stored in this browser only. There is no encryption, remote backup, account, or bank integration. Do not put card numbers, credentials, PINs, or sensitive information in descriptions or notes, and avoid shared devices. Use **Delete all app data** to remove SpendWise records and preferences from this browser. Clearing browser storage also removes them. Local storage can be unavailable or full; the app reports a save/read error, but export important records regularly.

## Known limitations and future work

This is a single-user local prototype; it does not sync across devices, authenticate users, convert currencies, reconcile accounts, or provide professional financial advice. The chart library depends on an external CDN. Potential future, opt-in work could add a trained text categorizer, improved anomaly methods, transaction-description embeddings, or a secure backend for advanced AI features. None of those features are present now.

## Contributing

Keep the no-backend privacy default, explain any new analytical rule, validate imported/user-controlled data, preserve keyboard access and all theme modes, and update `TESTING.md` with checks actually performed. Avoid committing real personal transactions or secrets.

## License

MIT; see [LICENSE](LICENSE). Replace the copyright placeholder before distribution if the project owner is known.
