# Shared memory for every Hobasa agent

## Decisions

D-2026-031: aging buckets use calendar days after due date. D-2026-044: monetary amounts use Decimal, never float. D-2026-050: paid invoices are excluded from aging.

## Approved lessons

L-007: test the boundary day (exactly 30 days) explicitly for any day-count rule. L-011: keep Decimal arithmetic; never convert amounts to float.

## Conventions

- Monetary amounts are Decimal, never float.
- Commit messages start with the story ID.
- Every output cites the GitHub file it came from.
- Drafts never reach other agents; only approved outputs are pushed.
