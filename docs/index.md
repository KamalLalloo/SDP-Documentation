# Sport Live Feeds — Overview

## What is it?

A real-time sports broadcasting and viewer experience tool. It ingests in-game events, keeps an authoritative game clock, and serves live scoreboards, timelines, and overlays for fans, commentators, and organizers.

## Why it exists

- Live community streams and school leagues rarely have reliable score/clock graphics.
- Existing tools are expensive, closed, or sport-specific.
- Operators need a keyboard-first console that makes recording events fast and undoable.

## Who it’s for

- **Operators**: match officials or volunteers entering events and managing the clock.
- **Commentators/Productions**: need structured data and overlays for broadcast.
- **Fans**: want an accurate, low-latency scorebug and event timeline.
- **Organizers**: require archival logs and basic analytics.

## High-level architecture (brief)

- **Frontend**: Scoreboard, Timeline, Operator Console.
- **APIs**: Match Setup (CRUD), Live Update (ingest), Feed API (snapshots and cursors), Realtime Gateway (WS/SSE).
- **Backend services**: Projector derives `DisplayState` from immutable `EventLog`.
- **Storage**: Postgres (events, matches, teams), Redis cache (hot display payloads).

## Glossary

- **Event Log**: Append-only list of timestamped game events.
- **Display State**: Computed snapshot (score, clock, possession, phase).
- **Projector**: Process that reduces events → state.
- **Operator**: Person driving the match console.
