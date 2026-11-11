# usage-billing-engine

Usage-metered billing for a platform of paid APIs, load-tested and fault-tested against the targets below.

## Problem

A platform exposes about 200 APIs, and each one has a fixed price in credits. Credits are whole numbers and always positive. Customers prepay into a wallet and top it up when it runs low. A call is charged only when it returns 2xx. A 4xx, a 5xx or an upstream timeout costs the customer nothing.

A customer with no credits left gets 403 instead of the API's response. Billing must not slow the APIs down: apart from a small allowance (see the targets), an API's response time should be the same with billing as without it.

A small overdraft is acceptable. A busy customer may go slightly below zero before calls start being refused, as long as the overdraft stays within the limit below and the next top-up covers it.

For every customer, at all times:

```
balance = sum(top-ups) - sum(price × successful calls)
```

with each call counted exactly once.

## Targets

| What | Target | Why |
|---|---|---|
| Throughput | 7,000 to 8,000 calls/s across 20 to 30 customers, with the busiest customer sending 30 to 40% of them | One customer's wallet has to keep up with thousands of calls a second |
| Added latency | Billing adds at most 2 ms at p99 to any API call | Customers should not feel billing |
| Balance freshness | A charged call shows in the balance within 1 s at p99 | Customers and the 403 rule both depend on an up-to-date balance |
| Overdraft | At most about one second of that customer's spend; the largest seen is reported for every run | The business tolerates a little unpaid usage, not an open-ended amount |
| Correctness | Zero double charges and zero missed charges | Checked against the invariant after runs that kill a component mid-work, restart the database, replay duplicate events and apply the same top-up twice |

The first goal is correct behaviour at low load. Scaling to the targets comes after that.

## Out of scope

- Resets and expiring credits.
- Price changes. A call is charged the price in force when it was made.
- Refunds and invoices. Finance handles those downstream, from the usage this system records.

## Docs

- `docs/roadmap.md`: build plan and progress
- `docs/architecture.md`: components, data flow, data model
- `docs/decisions.md`: each design choice, the alternative and the reason
- `docs/journal.md`: dated notes, and every measured number with how it was measured
- `docs/findings.md`: results and lessons per milestone
