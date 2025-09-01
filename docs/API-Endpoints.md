This section describes all available endpoints in the Matches API.
Each endpoint includes a description, parameters, request/response
examples, and possible error codes.

---

## 3.1 Matches

### POST /matches

**Description:**\
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

Example Response:

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

Possible Errors:

- 400 Bad Request -- Missing required fields
- 500 Internal Server Error -- Database error

---

### PATCH /matches/:id

**Description:**\
Update match fields such as scores, status, minute, attendance, or
venue. Supports partial updates.

**Request Body Example:**

```json
{
  "home_score": 2,
  "away_score": 1,
  "minute": 60
}
```

Possible Errors:

- 400 Bad Request -- Invalid update fields
- 404 Not Found -- Match not found

---

### POST /matches/:id/score

**Description:**\
Convenience endpoint to update only the scores.

**Request Body Example:**

```json
{
  "home_score": 3,
  "away_score": 2
}
```

---

### POST /matches/:id/finalize

**Description:**\
Finalize a match. Requires scores to be present. Locks scores and clears
match minute.

**Request Example:**

```bash
curl -X POST https://sdp-webserver.onrender.com/api/matches/1/finalize -H "Content-Type: application/json" -d '{}'
```

Possible Errors:

- 400 Bad Request -- Missing scores
- 404 Not Found -- Match not found

---

### POST /matches/:id/unfinalize

**Description:**\
Revert a finalized match back to editable state (e.g., status changed to
in_progress).

**Example Request:**

```bash
curl -X POST https://sdp-webserver.onrender.com/api/matches/1/unfinalize -H "Content-Type: application/json" -d '{}'
```

---

### GET /matches/:id

**Description:**\
Retrieve full match details, including team/venue names and match
events.

**Example Response:**

```json
{
  "id": 1,
  "league_code": "local.u20",
  "season_year": 2025,
  "status": "final",
  "home_team_name": "Soweto Stars",
  "away_team_name": "Parktown United",
  "venue_name": "Zoo Lake",
  "home_score": 3,
  "away_score": 2,
  "events": [
    {
      "event_id": 1,
      "event_type": "goal",
      "team_id": 1,
      "player_name": "Thabo M.",
      "minute": 12
    }
  ]
}
```

---

### GET /matches

**Description:**\
List matches with optional filters.

**Query Parameters:**

- league_code (optional)
- status (optional: scheduled, in_progress, final)
- date_from and date_to (optional, ISO 8601 format)

**Example Request:**

```bash
curl "https://sdp-webserver.onrender.com/api/matches?league_code=local.u20&status=final"
```

**Example Response:**

```json
[
  {
    "id": 1,
    "league_code": "local.u20",
    "season_year": 2025,
    "status": "final",
    "home_team_name": "Soweto Stars",
    "away_team_name": "Parktown United",
    "venue_name": "Zoo Lake",
    "home_score": 3,
    "away_score": 2
  }
]
```

---

## 3.2 Events

### POST /matches/:id/events

**Description:**\
Add a timeline event (goal, own goal, penalty, yellow, red, etc.) with
player, team, and minute.

**Request Body Example:**

```json
{
  "event_type": "goal",
  "team_id": 1,
  "player_name": "Thabo M.",
  "minute": 12
}
```

**Example Response:**

```json
{
  "event_id": 1,
  "event_type": "goal",
  "team_id": 1,
  "player_name": "Thabo M.",
  "minute": 12
}
```

Possible Errors:

- 400 Bad Request -- Invalid event data
- 404 Not Found -- Match not found

---

### DELETE /matches/:id/events/:eventId

**Description:**\
Delete a specific event from the match timeline.

**Example Request:**

```bash
curl -X DELETE https://sdp-webserver.onrender.com/api/matches/1/events/1
```

Possible Errors:

- 404 Not Found -- Event not found
- 400 Bad Request -- Invalid match or event ID
