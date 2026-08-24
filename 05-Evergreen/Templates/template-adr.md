# ADR-XXXX: <Title>

## Status
Proposed | Accepted | Superseded

## Context

## Decision

## Consequences

---

## Example (fictional — developer perspective)

# ADR-0003: Move ingestion service from polling to persistent WebSocket

## Status
Accepted

## Context
GPS pings currently arrive via 15-minute polling, which is the main blocker
to shipping real-time truck availability. Dispatchers have said in every
design-partner call that stale location data is the #1 complaint.

## Decision
Replace the polling ingestion path with a persistent WebSocket connection
from the driver app, falling back to polling only when the socket can't
stay connected (e.g. poor rural coverage).

## Consequences
Sub-60-second location freshness in good coverage; added complexity in the
ingestion service (connection state, reconnect/backoff logic) and a new
failure mode (silently-stale data if a socket drops without reconnecting) —
mitigated with a staleness indicator in the dispatcher UI.
