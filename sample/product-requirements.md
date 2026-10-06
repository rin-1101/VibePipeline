# 1. Product Requirement Document: MarketLens AI

**Status:** Proposed sample specification  
**Owner:** Product lead  
**Last updated:** 2026-10-06

## Problem and purpose

People learning about stock forecasting need a single place to compare historical prices, model predictions, uncertainty, and evaluation results. MarketLens AI makes those elements visible together so users can examine how a forecasting model behaves.

## Target users and roles

| User | Need | Role |
| --- | --- | --- |
| Student or researcher | Inspect forecasts and understand their limitations. | Analyst |
| Market analyst | Compare selected stocks and revisit saved symbols. | Analyst |
| System operator | Monitor data imports, training, and model availability. | Administrator |

Administrators also have analyst capabilities. The ingestion and training service has a separate worker identity.

## Goals and success measures

These are acceptance targets, not observed results.

| Goal | Measure | Proposed target |
| --- | --- | --- |
| Make forecasts easy to inspect | Moderated usability exercise | At least 4 of 5 pilot users find a stock forecast and its cutoff date within two minutes. |
| Make results traceable | Forecast response checks | Every displayed forecast references a dataset and model version. |
| Support responsive browsing | Load test with 20 concurrent users | Cached forecast API responses have p95 latency below two seconds. |
| Present evaluation honestly | Release review | Every enabled stock/horizon has held-out results, baseline comparison, and measured interval coverage. |

## Scope

The MVP supports the five stocks and two horizons in [Overview](overview.md), daily historical charts, account access, personal watchlists, evaluation pages, and operational jobs.

Intraday predictions, other markets, news sentiment, portfolio optimization, price alerts, automatic trading, and user-uploaded model files are deferred. User CSV uploads are excluded; only operators can import data through the controlled pipeline.

## Features and acceptance criteria

| ID | Feature | Priority | Pages | Acceptance criteria |
| --- | --- | --- | --- | --- |
| F-01 | Account access | Must | P-01, all protected pages | A valid identity creates an analyst session; unauthenticated requests cannot access protected data; sign-out invalidates the session; only approved admins access P-07. |
| F-02 | Stock search | Must | P-02, P-03 | Case-insensitive symbol or company-name search returns only supported instruments; selecting a result opens its detail page; no matches shows an empty state. |
| F-03 | Historical charts | Must | P-03 | The user can switch between 3-month, 1-year, and all-available views; charts identify adjusted prices, source, currency, and last completed session; demo datasets have a visible label. |
| F-04 | AI forecasts | Must | P-03, P-04 | Selecting horizon 1 or 5 and viewing a forecast shows the median estimate, return, ordered interval endpoints, dates, freshness, and model version; missing or invalid results display an unavailable state. |
| F-05 | Personal watchlist | Should | P-03, P-04, P-05 | A user can add and remove supported stocks; duplicate adds are idempotent; the list persists across sessions; another user's list cannot be read or modified. |
| F-06 | Model evaluation | Must | P-04, P-06 | Users see held-out return error, no-change baseline error, interval coverage, interval width, sample count, and test dates for the selected model; values are labeled historical. |
| F-07 | Data and model administration | Must | P-07 | An admin can queue import or training, inspect job outcomes, and promote only an eligible model; analysts receive access denied for these operations; actions are audited. |

## Forecast business rules

1. Predictions use validated end-of-day datasets. No partial current-session bars are used.
2. Target dates advance by exchange trading sessions using an exchange calendar, including holidays and early-close schedules.
3. Prices are adjusted for corporate actions according to a recorded adjustment policy. The UI identifies that price basis.
4. A one-session estimate means the next session after the cutoff, even when the forecast is stale. A stale forecast is never relabeled as a new forecast.
5. Forecasts are stale when the dataset cutoff trails the latest session whose configured provider publication deadline has passed. Weekends alone do not make data stale.
6. Only models passing the predeclared release gates can serve live-data forecasts. When no model qualifies, display evaluation results and an unavailable forecast state.
7. A nominal 80% prediction interval is an estimated range, not a guarantee or an “80% accurate” claim. Show its measured held-out coverage.
8. Missing bars, invalid prices, unsupported symbols, and insufficient training history must produce explicit outcomes; do not silently invent data.

## Dependencies and open decisions

| Item | Impact | Owner | Resolution |
| --- | --- | --- | --- |
| Licensed daily historical data and display rights | Blocks a live-data pilot. | Product lead | Select provider before T-03 live ingestion. |
| Identity provider | Blocks integrated account access. | Backend lead | Select during T-01. |
| Historical revisions and adjustment policy | Affects reproducible evaluation. | ML lead | Record limitations and snapshot policy in T-03. |
| Model quality | May leave some stock/horizon pairs unavailable. | ML lead | Evaluate before promotion; reduce coverage if needed. |

## Release acceptance

All seven features meet the criteria above, all enabled forecasts have eligible models, and data freshness, uncertainty, and provenance are visible. Mocked or synthetic demonstrations must be labeled and must not be described as a validated live forecasting product.
