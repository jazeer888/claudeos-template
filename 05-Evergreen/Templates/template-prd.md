# PRD: <Product/Feature Name>

## Problem

## Goals / Non-goals

## Requirements

## Success metrics

## Open questions

---

## Example (fictional — developer perspective)

# PRD: Real-time GPS ingestion

## Problem
Dispatchers see truck location updated every 15 minutes, which is too stale
to trust for load assignment — the #1 complaint across all design partners.

## Goals / Non-goals
Goals: sub-60-second location freshness for trucks with normal connectivity.
Non-goals: guaranteeing real-time updates in zero-coverage areas — a clear
"stale" indicator is an acceptable fallback there, not a blocker to ship.

## Requirements
- Persistent WebSocket connection from driver app to ingestion service
- Automatic reconnect with backoff on drop
- Staleness indicator in dispatcher UI when last ping is >2 min old

## Success metrics
- Median location age drops from ~7.5 min (polling midpoint) to <60 sec
- Dispatcher-reported "stale location" complaints drop to near zero in the
  next design-partner check-in round

## Open questions
Does battery drain from a persistent connection become a driver complaint at
scale? Not yet tested beyond 5 design partners.
