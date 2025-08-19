# Tech Stack

### High-level architecture

- **Frontend**: React + TypeScript (hosted on Vercel), provides live scoreboard, event timeline, match setup screens, and input panels.
- **Backend**: Node.js APIs for match setup, live updates, and data feeds.
- **Database**: Supabase (Postgres) storing matches, teams, events, and user accounts.
- **Hosting**: Vercel (frontend) + Render (backend), access to website and allows for api calls.
- **Authentication**: Google Auth via Supabase — secure login for admins, operators, and fans.
- **Other**: GitHub Actions for CI/CD, Jest for testing.

### Rationale

- **Frontend, React + TypeScript**: Chosen for fast development and reactive UI, ideal for real-time score updates and visualizations.
- **Backend, Node.js**: Lightweight and scalable, with excellent support for REST APIs and WebSockets to push live match data.
- **Database, Supabase (Postgres)**: Reliable relational DB with strong support for structured sports data, provides an adequite 500MB of storage, and a simple to use UI for database creation.
- **Hosting, Vercel (frontend) + Render (backend)**: Modern cloud platforms with quick deployment, CI/CD integration, and good scalability for live events.
- **Other, GitHub Actions and Jest**: Ensures reliability of APIs and UI modules, with automated checks on every commit.
