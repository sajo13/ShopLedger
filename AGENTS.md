# Repository Guidelines

## Project Structure

- `server.js` starts Express, serves the browser UI, mounts the API under `/api`, and exposes `GET /orders/:id/invoice`.
- `routes/` handles HTTP requests for products, orders, customers, and reports. `lib/` holds pricing, GST, inventory, Khata, invoice, reporting, and persistence logic.
- `public/index.html`, `public/js/app.js`, and `public/css/style.css` are the browser entry point and assets. `config.js` holds shop and business settings. `data/db.json` is the tracked seed data and the file the running app updates. See [the architecture diagram](docs/architecture.svg) for the order flow.

## Local Development

- `npm ci` installs the dependencies pinned in `package-lock.json`.
- `npm start` runs `node server.js`. Open `http://localhost:3000`, or set `PORT` to use another port. The repo has no build step.
- `npm test` runs a placeholder that exits with an error. For a JavaScript syntax check, use `node --check lib/pricing.js` with the file you changed.

## Coding Style

Match the surrounding JavaScript. Use two-space indentation, single quotes, semicolons, and camelCase names such as `computeTotals`. The server uses CommonJS (`require` and `module.exports` or `exports`), and the browser uses plain JavaScript. Keep request and response handling in `routes/` and reuse business logic in `lib/`. The repo has no configured lint or formatting tool.

## Testing

There is no automated test suite, coverage target, or test naming convention. Smoke-test the flows you change with disposable data in a separate checkout, since orders and settlements write to `data/db.json`. For pricing changes, try a mixed-GST cart with and without a coupon and compare the cart preview, saved order, printable invoice, and GST reconciliation. For Khata or inventory changes, check the affected balances and stock before and after checkout or cancellation. Keep local sales and customer data out of commits.

## Commits and Pull Requests

Use a short, descriptive subject. Recent commits use prefixes such as `feat: add architecture diagram` and `chore: update package-lock.json`. In the PR, summarize what changed, link the issue if available, and list the checks you ran. Include screenshots for visible UI or invoice changes and expected totals for pricing changes.
