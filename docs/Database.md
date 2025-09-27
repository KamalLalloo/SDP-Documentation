# Database Documentation

## 1. Schema

We designed a relational database using **Supabase**, which is built on PostgreSQL. Below is the database schema for our live sports feed web app:

![alt text](<Untitled (1).png>)

### Tables Overview

#### `users`

- Stores basic user information, including username and role.
- **Primary key**: `user_id`
- **Fields**:
  - `user_id` (varchar, PK)
  - `username` (varchar, required)
  - `role` (smallint, default 0)
  - `created_at` (timestamp, default now)

#### `teams`

- Contains metadata about each sports team including name, display name, abbreviations, and logos.
- **Primary key**: `id`
- **Fields**:
  - `id` (bigint, PK)
  - `name` (text, required)
  - `short_name`, `abbreviation`, `display_name`
  - `logo_url` (text, optional)
  - `created_at`, `updated_at` (timestamps)

#### `favourite_teams`

- Join table that links users to teams they've marked as favourites.
- **Composite primary key**: `(user_id, team_id)`
- **Fields**:
  - `user_id` (FK → `users.user_id`)
  - `team_id` (FK → `teams.id`)
  - `created_at` (timestamp, default now)

#### `matches`

- Stores match metadata: kickoff time, scores, status, and related teams/venue.
- Tracks live fields like minute, possession, and notes.
- **Primary key**: `id`
- **Fields**:
  - `id` (bigint, PK)
  - `league_code` (text)
  - `season_year`, `week_number` (integers)
  - `utc_kickoff` (timestamp, required)
  - `status` (text, default `scheduled`)
  - `status_detail` (text)
  - `minute`, `attendance` (integers)
  - `home_team_id`, `away_team_id` (FK → `teams.id`)
  - `home_score`, `away_score` (ints, default 0)
  - `home_possession`, `away_possession` (ints, default 50)
  - `venue_id` (FK → `venues.id`)
  - `notes_json` (jsonb, optional)
  - `created_by` (FK → `users.user_id`)
  - `created_at`, `updated_at` (timestamps)

#### `match_events`

- Stores in-game events like goals, fouls, substitutions, etc.
- Supports detailed data with optional metadata.
- **Primary key**: `id`
- **Fields**:
  - `id` (bigint, PK)
  - `match_id` (FK → `matches.id`)
  - `team_id` (FK → `teams.id`)
  - `player_name` (text)
  - `minute`, `added_time` (ints)
  - `event_type` (text, required)
  - `detail`, `outcome` (text)
  - `notes_json` (jsonb, optional)
  - `created_at`, `updated_at` (timestamps)

#### `match_reports`

- Stores user-submitted reports related to a match (e.g., referee performance).
- **Primary key**: `id`
- **Fields**:
  - `id` (bigint, PK, identity)
  - `match_id` (FK → `matches.id`)
  - `message` (text, required)
  - `created_at` (timestamp, default now)

#### `venues`

- Stores information about stadiums or match venues.
- **Primary key**: `id`
- **Fields**:
  - `id` (bigint, PK)
  - `name`, `city`, `country` (text)
  - `created_at`, `updated_at` (timestamps)

---

## 2. Deployment

We chose **Supabase** to host our database because it offers a robust and developer-friendly PostgreSQL environment that’s well-suited for real-time, relational applications like ours. Since our app relies heavily on structured data such as users, teams, matches, and events, a relational database was essential, and Supabase provides this with minimal setup and solid reliability.

- **Hosting Platform:** Supabase
- **Database Engine:** PostgreSQL
- **Backend Hosting:** [Render](https://render.com)

Our backend is deployed on **Render**, and it communicates securely with Supabase using environment variables to manage the database connection. This setup allows us to separate our application logic (hosted on Render) from our data layer (hosted on Supabase), making our architecture both modular and easy to scale.
