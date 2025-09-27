# API Endpoints

This section describes all available endpoints in the Matches API.  
Each endpoint includes a description, parameters, request/response examples, and possible error codes.

---

## Endpoint Summary

| Method | Endpoint                           | Description                                |
| ------ | ---------------------------------- | ------------------------------------------ |
| GET    | `/api`                             | Health check, returns "Hello from the API" |
| GET    | `/status`                          | Server status JSON                         |
| GET    | `/names`                           | Get all usernames                          |
| GET    | `/checkID`                         | Check if a user ID exists                  |
| GET    | `/teams`                           | Get all teams                              |
| POST   | `/teams`                           | Create (or upsert) a team                  |
| GET    | `/favourite-teams/:userId`         | Get user’s favourite teams                 |
| POST   | `/favourite-teams`                 | Add favourite team for user                |
| DELETE | `/favourite-teams/:userId/:teamId` | Remove favourite team                      |
| POST   | `/addUser`                         | Add a new user                             |
| POST   | `/matches`                         | Create a match                             |
| PATCH  | `/matches/:id`                     | Partially update match                     |
| PUT    | `/matches/:id`                     | Replace/update match fully                 |
| POST   | `/matches/:id/score`               | Update only the scores                     |
| POST   | `/matches/:id/finalize`            | Finalize a match                           |
| POST   | `/matches/:id/unfinalize`          | Reopen a finalized match                   |
| PATCH  | `/matches/:id/possession`          | Update possession stats                    |
| DELETE | `/matches/:id`                     | Delete a scheduled match                   |
| GET    | `/matches/:id`                     | Get match with events                      |
| GET    | `/matches/:id/details`             | Get match with events + squads             |
| PATCH  | `/matches/:id/extend`              | Extend match duration                      |
| POST   | `/matches/:id/events`              | Add a match event                          |
| DELETE | `/matches/:id/events/:eventId`     | Delete a match event                       |
| GET    | `/matches`                         | List matches with filters                  |
| POST   | `/matches/:id/reports`             | Add a report to a match                    |
| GET    | `/matches/:id/reports`             | Get reports for a match                    |
| DELETE | `/matches/:id/reports/:reportId`   | Delete a report                            |
| GET    | `/watchalongs`                     | Fetch live watchalongs or clips            |

---

## 3.1 Matches

### POST /matches

Create a new match (scheduled or completed).

**Request Body (JSON):**

```json
{
  "league_code": "local.u20",
  "season_year": 2025,
  "utc_kickoff": "2025-09-10T13:00:00Z",
  "status": "scheduled",
  "home_team_name": "Soweto Stars",
  "away_team_name": "Parktown United",
  "venue_name": "Zoo Lake",
  "venue_city": "Johannesburg"
}
```

**Example Response:**

```json
{
  "id": 1,
  "league_code": "local.u20",
  "season_year": 2025,
  "utc_kickoff": "2025-09-10T13:00:00Z",
  "status": "scheduled",
  "home_team_name": "Soweto Stars",
  "away_team_name": "Parktown United",
  "venue_name": "Zoo Lake",
  "venue_city": "Johannesburg",
  "home_score": 0,
  "away_score": 0,
  "events": []
}
```

**Errors:**

- 400 Bad Request – Missing required fields
- 500 Internal Server Error – Database error

---

### PATCH /matches/:id

Update match fields (scores, status, minute, etc.). Supports partial updates.

**Request Example:**

```json
{ "home_score": 2, "away_score": 1, "minute": 60 }
```

**Errors:**

- 400 Bad Request – Invalid fields
- 404 Not Found – Match not found

---

### POST /matches/:id/score

Convenience endpoint to update only the scores.

**Request Example:**

```json
{ "home_score": 3, "away_score": 2 }
```

---

### POST /matches/:id/finalize

Finalize a match. Requires scores.

**Example:**

```bash
curl -X POST https://sdp-webserver.onrender.com/api/matches/1/finalize -H "Content-Type: application/json" -d '{}'
```

**Errors:**

- 400 Bad Request – Missing scores
- 404 Not Found – Match not found

---

### POST /matches/:id/unfinalize

Revert a finalized match back to editable state.

**Example:**

```bash
curl -X POST https://sdp-webserver.onrender.com/api/matches/1/unfinalize -H "Content-Type: application/json" -d '{}'
```

---

### PATCH /matches/:id/possession

Update possession stats. `home_possession + away_possession` must equal 100.

---

### DELETE /matches/:id

Delete a scheduled match.  
**Note:** Only `scheduled` matches can be deleted.

---

### GET /matches/:id

Retrieve full match details (teams, venue, events).

**Example Response:**

```json
{
  "id": 1,
  "league_code": "local.u20",
  "status": "final",
  "home_score": 3,
  "away_score": 2,
  "events": [{ "event_id": 1, "event_type": "goal", "minute": 12 }]
}
```

---

### GET /matches/:id/details

Retrieve a match with squads (`lineupTeam1`, `lineupTeam2`) and events.

---

### PATCH /matches/:id/extend

Extend match duration (e.g., 90 → 120 minutes).

---

### GET /matches

List matches with optional filters:

- `league_code`
- `status` (scheduled, in_progress, final)
- `from`, `to` (ISO 8601 date range)
- `type` (live, past, upcoming)

---

## 3.2 Events

### POST /matches/:id/events

Add a timeline event (goal, own goal, yellow, red, etc.).

**Request Example:**

```json
{ "event_type": "goal", "team_id": 1, "player_name": "Thabo M.", "minute": 12 }
```

---

### DELETE /matches/:id/events/:eventId

Delete a specific event. Adjusts score if necessary.

---

## 3.3 Reports

### POST /matches/:id/reports

Add a text report to a match.

### GET /matches/:id/reports

Get all reports for a match.

### DELETE /matches/:id/reports/:reportId

Delete a specific report.

---

## 3.4 Teams & Users

- **GET /teams** – List all teams
- **POST /teams** – Create or upsert a team
- **GET /names** – List usernames
- **GET /checkID** – Check if user ID exists
- **POST /addUser** – Add new user

**Favourites API:**

- **GET /favourite-teams/:userId** – Get favourites
- **POST /favourite-teams** – Add favourite team
- **DELETE /favourite-teams/:userId/:teamId** – Remove favourite

---

## 3.5 Watchalongs

### GET /watchalongs

Fetch YouTube live watchalongs or fan reaction clips.  
Supports fallback samples if no YouTube API key is set.

---
