# MarketLens AI: Sample Web App Overview

**Status:** Proposed sample specification; not implemented or validated  
**Owner:** Product team  
**Last updated:** 2026-10-06

MarketLens AI is a web app that uses machine learning to estimate future stock returns. Users choose a supported stock, inspect historical prices, and view a forecast with an uncertainty range and its historical evaluation results.

This folder demonstrates how to fill in the six web app planning documents. It contains documentation, not a running application, trained model, or measured prediction results. Technology choices, budgets, timelines, and targets are proposals for this example.

## Documents

| Document | What it defines for this app |
| --- | --- |
| [1. Product Requirement Document](product-requirements.md) | Stock search, charts, forecasts, watchlists, evaluation, and administration. |
| [2. Technical Requirements Document](technical-requirements.md) | React UI, Python API and ML pipeline, PostgreSQL, authentication, and deployment. |
| [3. App Flow](app-flow.md) | Sign-in, stock selection, forecast viewing, watchlist actions, and admin jobs. |
| [4. Design Brief](design-brief.md) | Navy and teal branding, fonts, chart styles, components, and responsive layouts. |
| [5. Background Schema](background-schema.md) | Users, market datasets, models, forecasts, evaluation, permissions, and storage. |
| [6. Implementation Plan](implementation-plan.md) | Ordered tasks from data preparation through model validation and release. |

## Example scope

- **Audience:** Students, researchers, and analysts studying stock-price forecasting.
- **Starting universe:** AAPL, MSFT, AMZN, GOOGL, and NVDA, identified by symbol and exchange. This is an illustrative coverage list.
- **Frequency:** End-of-day data; forecasts refresh after a completed exchange session is ingested and validated.
- **Horizons:** One or five future trading sessions, not calendar days.
- **AI approach:** Gradient-boosting regressors estimate log returns and quantiles separately for each stock and horizon.
- **Core output:** Median projected adjusted price, estimated return, nominal 80% prediction interval, cutoff date, target date, and model version.
- **Evaluation:** Chronological historical evaluation against a no-change baseline, with error and interval-coverage measurements.
- **Product boundary:** Research forecasts and watchlists; brokerage integration and order execution are outside the MVP.

## Main user journey

1. Sign in and open the dashboard.
2. Search for a supported stock and open its detail page.
3. Review historical prices and the dataset's latest completed session.
4. Select a one- or five-session horizon and click **View forecast**.
5. Inspect the forecast, uncertainty interval, and model evaluation.
6. Add the stock to a personal watchlist for future visits.

Forecasts describe model estimates. The interface must distinguish historical observations from predictions, label demonstration data, and report historical performance without promising future accuracy.

## Traceability

Features use `F-01` through `F-07`, pages use `P-01` through `P-07`, data entities use `E-01` through `E-10`, and implementation tasks use `T-01` through `T-12`. These IDs connect behavior, routes, data, and build tasks across the documents.

## Decisions required before implementation

| Decision | Example approach | Owner |
| --- | --- | --- |
| Market-data access and display rights | Start development with clearly labeled synthetic CSV fixtures; select a licensed provider before live-data release. | Product lead |
| Authentication service | Use an OpenID Connect provider supporting server-side sessions. Select the actual provider during setup. | Backend lead |
| Production hosting | One Linux application host plus private database and artifact storage for the initial pilot. Size and procure it after measurement. | Operations lead |
| Forecast release gate | Adopt the evaluation thresholds in the technical requirements before running the final holdout evaluation. | ML lead |

The specification is complete as an example. Provider selection, credentials, dependency versions, deployment capacity, and empirical model results remain implementation work.
