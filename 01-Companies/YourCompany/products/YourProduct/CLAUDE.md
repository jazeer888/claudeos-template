# YourProduct — Context

Rename this folder to your actual product name. Inherits company context from
`01-Companies/YourCompany/CLAUDE.md` — don't repeat company-level facts here.

## What it is

[One or two sentences — the product, who it's for, the core value prop.]

## Architecture summary

[One paragraph — enough for Claude to reason about the system without
re-reading every file in `architecture/`. Update only when the architecture
actually changes; details belong in `architecture/`.]

## Competitive summary

[One or two sentences — current positioning vs. the market. Update only when
this changes; detail belongs in `research/`.]

## Roadmap phase

[Where the product is right now — e.g. "pre-launch, building MVP" or
"GA, scaling to enterprise."]

## Links

- `product/` — PRDs, requirements, roadmap
- `architecture/` — system design, ADRs, technical decisions
- `research/` — competitive analysis, market research
- `gtm/` — positioning, messaging, launch strategy
- `meetings/` — dated meeting notes
- `decisions/` — ADRs and decision logs
- `engineering/` — infrastructure notes, runbooks

---

## Example (fictional — founder perspective)

# Northwind Dispatch — Context

## What it is

Real-time truck availability and load-matching for freight brokers running
5-30 trucks — a lightweight alternative to enterprise TMS software.

## Architecture summary

Multi-tenant SaaS on AWS: driver mobile app pushes GPS pings to a
Go ingestion service, dispatcher-facing React app reads from a Postgres
read replica. GPS ping frequency is the current bottleneck (15 min polling,
targeting sub-60s via a persistent WebSocket connection).

## Competitive summary

Priced and scoped for the segment enterprise TMS vendors ignore (too small
to sell to); main competition is brokers just staying on spreadsheets, not
another SaaS product.

## Roadmap phase

Pre-launch — 5 design partners live, targeting public launch after real-time
GPS ingestion ships.
