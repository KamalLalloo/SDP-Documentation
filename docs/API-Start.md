The Matches API is publicly accessible and does not currently require authentication.  
All endpoints are available under the base URL:

`https://sdp-webserver.onrender.com/api/v1`

### Example Request

Create a new match:

```bash
curl -X POST https://sdp-webserver.onrender.com/api/v1/matches \
-H "Content-Type: application/json" \
-d '{
  "league_code": "local.u20",
  "season_year": 2025,
  "utc_kickoff": "2025-09-10T13:00:00Z",
  "status": "scheduled",
  "home_team_name": "Soweto Stars",
  "away_team_name": "Parktown United",
  "venue_name": "Zoo Lake",
  "venue_city": "Johannesburg"
}'
```
