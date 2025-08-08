# Sport Live Feeds — Features

This section lists the deliverable features with user value, key capabilities, and acceptance criteria for Sprint 1.

## Match Viewer

**User value:** Fans and commentators see the truth of the match at a glance.

**Key capabilities**

- Current score, teams, period, and server-authoritative game clock.
- Possession indicator and recent key events.
- Resilient to reconnects; reload shows accurate state.

**Acceptance criteria**

- Scorebug shows correct score/period and running/paused clock.
- After browser refresh, viewer state matches server within 1 second.
- Latency from operator action to viewer update ≤ 800 ms on local network.

---

## Event Feed (Timeline)

**User value:** Everyone can follow a chronological list of in-game events.

**Key capabilities**

- Live timeline with timestamps, period grouping, and event icons.
- Supports goals, substitutions, yellow/red cards, period start/stop.
- Filters by team and event type.

**Acceptance criteria**

- New events appear in order without manual refresh.
- Each event shows: game time, period, team, player (optional), description.
- Out-of-order or duplicate ingest does not produce duplicates in the UI.

---

## Match Setup

**User value:** Organizers can prepare matches before kickoff.

**Key capabilities**

- Create matches with teams, scheduled time, venue, and rules profile (soccer).
- Add rosters for optional player attribution.
- Status transitions: `pregame → live → halftime → live → full_time`.

**Acceptance criteria**

- POSTing a new match returns an ID and is visible in operator console.
- Only valid status transitions are allowed.
- Editing teams/rosters before `live` is permitted; after `live` is restricted.

---

## Live Input (Operator Console)

**User value:** Fast, reliable entry of events with undo/amend.

**Key capabilities**

- Start, pause, resume, and set clock; add stoppage time.
- Quick-actions: Goal, Yellow, Red, Substitution, Period start/stop.
- Undo/amend last event; free-text note field.

**Acceptance criteria**

- Keyboard shortcuts exist for all quick-actions.
- Every mutation writes an immutable Event Log record and updates Display State.
- Undo creates a compensating event; history remains intact.

---

## API Modules

**Live Update API (ingest)**

- `POST /matches/{id}/events` — accepts single or batch events with idempotency key.
- `POST /matches/{id}/clock` — start/stop/set with reason.

**Feed API (read)**

- `GET /matches/{id}` — current snapshot (Display State).
- `GET /matches/{id}/events?since={cursor}` — incremental fetch.
- `WS /ws/matches/{id}` — server-push of deltas.

**Match Setup API**

- `POST /matches` — create match.
- `PATCH /matches/{id}` — update status/meta.

**Display API**

- Optimized payloads for overlays/scorebugs.

**Acceptance criteria**

- OpenAPI document generated; example requests/responses included.
- 400/409 errors defined for validation and idempotency violations.

---

## UI Modules

- **Live Scoreboard**: compact scorebug with period and clock.
- **Event Timeline**: scrollable, grouped by period with filters.
- **Match Setup Screen**: form for teams, schedule, rules profile.
- **Manual Input Panel**: operator console with quick-actions and undo.

**Acceptance criteria**

- All screens usable on desktop; scoreboard responsive for small embeds.
- Error states and loading states visibly handled.

---

## Database Entities (Sprint 1 scope)

- **Match**: `id, home_team_id, away_team_id, scheduled_at, status, rules_profile`
- **EventLog**: `id, match_id, ts_game, ts_ingest, type, team_id, player_id, period, params(jsonb), seq, idempotency_key`
- **DisplayState** (derived): `score_home, score_away, period, clock_running, clock_time, possession`
- **Team** / **Player**: minimal fields for names and jersey numbers.

**Acceptance criteria**

- EventLog is append-only; DisplayState is recomputable from scratch.

---

## Non-functional requirements (Sprint 1)

- Average end-to-end update latency ≤ 800 ms; p95 ≤ 1.5 s.
- Uptime target during live match demo ≥ 99% (lab environment).
- Basic roles: Operator (write), Viewer (read), Admin (setup).

---

## Out of scope (for now)

- Multiple concurrent matches per operator session.
- Advanced sports (basketball, rugby) rule packs.
- Historical analytics and export beyond JSON dump per match.
