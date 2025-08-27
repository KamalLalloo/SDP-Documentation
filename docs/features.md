# Features

Footbook provides a set of core features designed to deliver real-time football updates and make it easy to follow matches live. The platform is built to support both **fans** who want quick updates and **organizers/operators** who need tools to manage matches.

---

#### Match Viewer

- Shows the **current score**, match clock, and possession.
- Displays **key events** such as goals, fouls, cards, and substitutions.
- Provides a clean view for **fans, commentators, and organizers**.

---

#### Event Feed

- A **timeline of events** that updates in real-time as the match progresses.
- Each event has a **timestamp** and short description (e.g., “Goal – Salah 55’”).
- Events can be animated or highlighted to make important actions stand out.

---

#### Match Setup

- Allows admins to **create new matches** before kickoff.
- Add details like teams, players, and scheduled start time.
- Supports **CSV uploads** so users can import personal or community matches.
- Ensures that the match has all required info before going live.

---

#### Live Input

- Operators can **manually add events** (goals, substitutions, cards, etc.) if external live feeds aren’t available.
- Includes options to **pause/resume the clock** or edit the timeline if needed.
- Useful for community matches or when official live data is unavailable.

---

#### User Reporting

- Fans and organizers can **report incorrect match information** such as wrong scores, player names, or missing events.
- Reports are stored for **review by operators/admins**, ensuring data accuracy.
- A general reporting feature is available for **bugs, feedback, or inappropriate content**.

---

## API Modules

Footbook provides APIs so data can be stored, updated, and displayed across the app:

- **Live Update API** — Receives and stores events from external sources.
- **Feed API** — Provides the current state of the match for the frontend.
- **Match Setup API** — CRUD (Create, Read, Update, Delete) for matches, teams, and venues.
- **Display API** — Serves structured data to the UI (scoreboard, overlays, etc.).

---

## UI Modules

The user interface has dedicated screens for each key function:

- **Live Scoreboard** — Displays current score, teams, and match status.
- **Event Timeline** — Chronological list of all major match events.
- **Match Setup Screen** — Create and configure matches, assign teams, set times.
- **Manual Input Panel** — Add events manually such as goals, fouls, and cards.
- **User Reporting Panel** — Allows fans to flag incorrect match data or send general feedback.

---

## Database Entities

The backend uses Supabase (Postgres) to store structured data:

- **Match Info** — Match ID, start time, teams, and current status.
- **Event Log** — List of timestamped events (goals, fouls, substitutions, etc.).
- **Display State** — Current score, clock, possession, and game phase.
- **Player & Team Data** — Rosters that can be synced or manually entered.
- **Uploaded Match Data** — Imported CSV data for custom or community games.

---

## Authentication

- Footbook uses **Google Authentication via Supabase**.
- Roles can be extended to give **admins/operators** special permissions (like match setup and event input) while **fans** can view matches.
